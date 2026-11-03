# AGENTS.md: instructions for AI agents working on Petsify

Read this before making any change. It is the shared source of truth for every agent (Claude, Codex, Lovable) and for me.

## What lives where

The workspace is a coordination hub, not a code repo. Code lives in nested projects:

| Project | Role |
|---|---|
| `petsify-fresh-look` | **Production web frontend** for petsify.pl. Built and edited with Lovable, TanStack Start, connected to GitHub. Default place for web work. |
| `petsify-web` | Legacy frontend plus the backend definitions (entities and functions). Use it for backend work, not new UI. |
| `petsify-mobile` | Expo / React Native app for iOS and Android. |

All three talk to **one backend**. There is a single source of truth for data, so a change made from any surface is visible on all of them.

**Decision (2026-08-09):** production web moved to the Lovable frontend. Don't revert to older assumptions based on old notes or screenshots.

## Git rules

- Never `git add .`, `git reset --hard` or force-push. Never delete files without explicit approval.
- Stage and commit only the files you changed. The worktree is often dirty with other work.
- Lovable can push to `main` independently of your session. Always `git fetch` and `git pull --rebase` before pushing.
- After pushing, the frontend still needs a manual **Publish** click from me. Always say when something is waiting on it.

## Verification loop for frontend changes

1. TypeScript: `npx tsc --noEmit`
2. Lint the files you touched.
3. Production build.
4. Run it locally and smoke-test the real page, at desktop and ~390 px mobile width.

Known pre-existing issues are listed in the repo notes. Don't "fix" them unless asked, and don't hide new errors behind them.

## Product rules that agents must not break

- **No blanket trust claims.** Never write "verified", "checked", "certified" or "safe" as a general claim. There is no formal verification process yet. Say exactly what was checked, or say nothing. (See [decision 0002](decisions/0002-no-blanket-verification-claims.md).)
- **Badge semantics.** Verified organizations show "Partner Petsify", a manually granted badge. Everyone else shows a neutral "Not verified". Never "verification in progress", which implies a check that isn't happening.
- **Public visibility.** Show organizations unless they are rejected or suspended. Don't filter the catalog to verified-only by default; that would empty it.
- **Payments.** Petsify does not process payments for animals. Contact and payment happen directly between the parties. Don't imply otherwise.
- **Tone.** No "good guys vs bad guys" framing of the market. Use "organization" (or shelter / foundation / breeder) in UI, never bureaucratic legal terms.
- **CTAs.** The universal header action is "Add a listing". Business features stay secondary, shown only to users who already have business status.

## Domain rules that are easy to get wrong

- Alert matching treats the literal string `"any"` as a wildcard. Matching code must check `!== 'any'` explicitly.
- Traits match on at least one overlap, not an exact match.
- Price filter: `0` means adoption only; the top cap means "no limit" and is omitted from the payload, not sent as a number.
- Dogs and cats use separate size fields. Don't merge them.
- Breed and city pickers follow one pattern: a searchable combobox, popular items when empty, full list on search, plus "use what I typed". Reuse it; don't invent a new picker.

## Final report format

End every task with a short report:

- what changed,
- what was confirmed by a test,
- what could not be verified,
- whether a push, Publish, deploy or test on a physical device is still needed,
- one concrete next step.

## If something breaks

Stop the deploy and keep the evidence. Revert a published change with a new commit; never rewrite history that Lovable already has. If production data is at risk, escalate to me before any bulk operation.

## Ask before you act

Payments, account deletion, emails to real users, and anything else irreversible or external: show the plan and wait for my explicit yes right before the action.

## Open items

- The interactive app demo on the homepage is deferred until the mobile app is live in the stores. Don't build it until asked.
- One folder in the workspace has an unclear purpose. Ask before using it.
