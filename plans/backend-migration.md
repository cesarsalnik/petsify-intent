# Plan: moving the backend from Base44 to Supabase

*Written 2026-09-04 as an audit and plan, before any code changed. Shortened for this repo. It shows how I scope a risky technical change.*

> **What happened next:** the cutover for the production web frontend was built on a canary branch and merged on 2026-09-17/18, with production defaulting to Supabase through backend flags. The old backend code is still in the repo. This note covers what the git history shows; it is not a full report on every phase below.

## Starting decisions

- **Strategy:** gradual and parallel. Supabase grows next to the current backend, switched over entity by entity, with no downtime window.
- **This document:** audit + plan only. No code changes.

## 1. Inventory

The current backend is the single source of truth for three frontends.

| Layer | Size |
|---|---|
| Entities | 33 |
| Backend functions | 55, about 6,900 lines |
| Legacy web files calling the backend | 72 |
| Mobile files calling the backend | 28 |
| Production web | a narrow layer of ~8–10 files; the rest goes through hooks |

Finding that shaped the plan: **50 of 55 functions run with service-role access**, so the real security logic already lives in trusted backend code, not only in row-level rules. That architecture moves to Postgres + Edge Functions with the least change in how we think about it.

## 2. Security patterns that must survive 1:1

A security audit in August closed gaps the migration must not reopen.

1. **Field-level write locks.** Some fields (user role, verification status, subscription plan) are writable only by admins, even though the owner can edit the rest of the row. Postgres row-level security works on rows, not columns. Options:
   - (a) column-level `REVOKE/GRANT` per role: clean but brittle when the schema changes;
   - (b) a `BEFORE UPDATE` trigger rejecting changes to protected columns: flexible, testable;
   - (c) **recommended:** keep the current pattern. Protected fields are written only by trusted Edge Functions, policies give normal users no update on them, and a trigger acts as a safety net.
2. **Idempotency ledgers for payments.** Records keyed by the Stripe event / invoice / payment ID with a `processing → applied / failed` state, so a Stripe retry can never grant benefits twice. Postgres does this better, with real unique constraints and transactions.

## 3. Service by service

- **Database:** 33 entities → 33 tables. Add real foreign keys, which the current platform doesn't have.
- **Auth: a real improvement, not just a move.** Today branded email codes need a custom layer (an entity, two functions, a rate limiter) because the platform's own emails can't be branded. Supabase supports custom email templates natively, so that whole layer can be deleted.
- **Storage:** small surface. A public bucket for listing photos, a private bucket with signed URLs for identity and business documents.
- **Functions:** Edge Functions also run on Deno, so business logic mostly carries over. The real cost is rewriting ~55 data-access adapters. Grouped by risk:
  - *Low:* ~25 CRUD and validation functions.
  - *Medium:* self-contained domain logic, such as alert matching (watch the `"any"` wildcard).
  - *High:* money and idempotency: the Stripe webhook, promotions, checkouts, cancellations. These need the most careful parallel testing.
  - *Email:* no Supabase equivalent; needs a real provider. The only part that is pure added cost.
  - *Scheduled jobs:* move to `pg_cron` or the native scheduler.

## 4. Phases

Rule: nothing gets switched off until the new path is verified on production data.

| Phase | Scope | Why this order |
|---|---|---|
| 0 | Schema for all 33 tables + policies + foreign keys, no traffic | zero production risk |
| 1 | Auth | biggest win (removes the custom code layer), testable in parallel |
| 2 | Simple, read-heavy entities (blog, price catalog, reviews) | low stakes, good for testing dual-read |
| 3 | Core transactional entities (animals, alerts, favourites, messages, inquiries) | needs alert matching and moderation ported |
| 4 | Money (subscriptions, payments, promotions, webhook ledger, verification) | most expensive to get wrong, so last; both webhooks listen in parallel for a while |
| 5 | Storage, email provider, cleanup | remove the custom auth layer |

Every phase ends the same way: new path behind a feature flag → dual-write / dual-read on production for a set period → check they match → switch reads → retire the old path.

## 5. Open decisions for the founder

1. **Scope:** whole stack or database only at first? The plan assumes the whole stack, because a split (auth on the old platform, data on the new) means maintaining an identity mapping between two systems for the whole time.
2. **Email provider:** Resend, Postmark, SES or other. Affects when Phase 5 can finish.
3. **Legacy frontend:** migrate it in parallel or freeze it and migrate last?
4. **Data:** do we need real-time sync during each phase, or are periodic batch imports during testing enough, with one cutover at the end of each phase?
