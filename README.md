# Petsify: product intent docs

**A curated snapshot of the working documentation behind Petsify**, translated from Polish and cleaned of internal IDs, file paths and partner names. It is not the original git history: the originals live in a local workspace folder and in our knowledge base. Each document keeps the date it was written.

**Petsify** is a Polish platform for adopting and buying pets, with tools for breeders. I build it solo: product, UX/UI, AI and automation. Most of the execution is done by AI coding agents, with a few people on specific areas. These docs are how I keep all of them pointed in the same direction.

Working mission: *"We help you find a pet responsibly and take care of it for its whole life, in one place."*

## Suggested reading path (about 10 minutes)

1. [`product/brief.md`](product/brief.md): the problem, who we build for, MVP scope, metrics and riskiest assumptions.
2. Two decisions: [0001 Breeders first](decisions/0001-breeder-first.md) and [0003 Contact before sign-up](decisions/0003-contact-before-signup.md).
3. [`process/case-notion-to-fibery.md`](process/case-notion-to-fibery.md): one real task delegated to an AI agent, what came back wrong, and how I verified the fix.

Then, if you want more:

| File | What it answers |
|---|---|
| [`AGENTS.md`](AGENTS.md) | What every AI agent reads before touching the code: where things live, what not to break, product and copy rules. |
| [`product/hypotheses.md`](product/hypotheses.md) | The bets we're making, with their test status. None confirmed yet. |
| [`decisions/`](decisions/) | Example decision records: what we decided, when, why, and what it costs. |
| [`process/delegation-and-verification.md`](process/delegation-and-verification.md) | Who does what, and the general rules for checking agent output. |
| [`plans/backend-migration.md`](plans/backend-migration.md) | A technical plan written before any code changed, with a note on what was executed. |

## Status as of 2026-11-03

What's in place:

- petsify.pl is live, with automatic listing import set up for three shelters.
- Production web runs on the backend moved from Base44 to Supabase (cutover merged on 2026-09-17/18, see the [plan](plans/backend-migration.md)).
- The team knowledge base moved from Notion to Fibery (October 2026, see the [case](process/case-notion-to-fibery.md)).

What we don't know yet:

- Whether breeders will pay for saved time (brief, assumption 1). This hypothesis is in test: in October I spent a two-day dog show in Wrocław talking to breeders, with QR business cards I made for it, and collected breeder leads. There are no paying breeders yet.
- Whether adoption listings next to breeder listings put breeders off (brief, assumption 3).

## Principles behind the structure

- **Intent lives next to the work, in plain markdown.** Agents read it at the start of every session, so it has to be short, current and unambiguous.
- **Decisions are written down with their reasons.** When an agent (or I) want to undo something, the record says why it was done.
- **Every plan ends with open decisions.** A plan that hides what's still undecided gets built wrong.
- **"Done" needs evidence.** Reports separate what was verified from what was only written.

## How these docs were made

Written and translated with AI assistance (Claude), from my own working documents and decisions, then reviewed by me.
