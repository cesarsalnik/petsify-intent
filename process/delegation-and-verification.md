# Delegation and verification

How work gets done on Petsify, and how I check that what comes back is right.

## Who does what

| Who | What they own |
|---|---|
| **Me** | Product decisions, priorities, intent docs, review of everything, every irreversible action. |
| **AI coding agents** (Claude and Codex, often in parallel) | Code changes across web, mobile and backend, audits, plans, migrations of data between tools. |
| **Lovable** | The production web frontend. It can also push to `main` on its own, which is why agents always rebase before pushing. |
| **Fibery** | The team knowledge base: documents, meetings, decisions, roadmap. An agent migrated the whole workspace there from Notion. |
| **External SEO specialist** | SEO strategy and audits. |
| **Partner (copywriter and marketer)** | Brand, copy, go-to-market and lead generation. |

People get the areas where judgement, relationships or accountability matter. Agents get execution that can be checked.

## How I delegate to an agent

1. **Point it at the intent.** Every session starts with [`AGENTS.md`](../AGENTS.md) and the relevant repo notes. If an agent gets something wrong twice, the fix goes into `AGENTS.md`, not just into the chat.
2. **Say what "done" looks like.** Which files, which checks, what the result should look like on screen.
3. **Name the limits.** What it must not touch, and which steps need my approval.
4. **For anything big, ask for a plan first.** The [backend migration plan](../plans/backend-migration.md) is an example: an audit and a phased plan, with open decisions listed, before any code changed.

## How I check what comes back

**Reports in four buckets.** Every agent report separates:

- **Verified:** checked with evidence (a passing build, a query result, a screenshot of the real page).
- **Deployed:** live, with proof.
- **Waiting for publish:** pushed, but needs my manual Publish click.
- **Unverified:** written, but not checked.

"Done" without evidence counts as unverified.

**Automated checks for code.** TypeScript, lint and a production build after every frontend change, then a smoke test of the real page on desktop and mobile width.

**Checks against the product rules.** I review copy for trust words that we can't back up ([decision 0002](../decisions/0002-no-blanket-verification-claims.md)) and invented numbers. Agents are told not to invent facts, prices, reviews or results.

**Human gates.** Payments, account deletion, emails to real users and other external or irreversible actions: the agent shows the plan and waits for my explicit yes right before acting. Test accounts and test data are always labelled as QA. Secrets never go into code, commits or reports. Backend deploys cover only the functions or entities named in the task, never "everything, just in case".

## Worked examples

**Agent work, checked by me.** See [case-notion-to-fibery.md](case-notion-to-fibery.md): the first result looked finished but kept links to Notion, I rejected it, and a final scan proved no Notion dependency was left.

**Delegating to a person: a full copy review.** In late September I asked my partner, a copywriter and marketer, to review all of the site's copy from an export. The result was a sheet with 71 topics that needed my decision and 1,508 line-level fixes. I separated the two: language and consistency fixes could go straight in, while anything touching promises or legal matters needed a decision first. I then implemented the approved part with an AI agent, live on 2026-10-11:

- one commit across 54 files: the 14 topics I approved, the uncontroversial bulk changes, and about 1,200 small fixes (mostly in breed descriptions),
- 74 changes in 6 blog guides stored in the database, applied with a rollback script ready,
- the writing rules that came out of the review were saved to our knowledge base, so future copy follows them.
