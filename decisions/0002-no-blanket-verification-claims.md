# 0002: No blanket "verified" claims; visibility doesn't depend on verification

Status: accepted

## Context

Trust is the core problem of this market: buyers can't tell a responsible breeder from a puppy mill. The easy move is to put "verified" badges everywhere. But we don't run a formal verification or certification process yet.

## Decision

- We never make general claims like "verified", "checked", "certified" or "safe". If something was checked, we say exactly what (for example "Checked: identity, documents"). If nothing was checked, we show nothing.
- "Partner Petsify" is a manually granted cooperation badge, not a synonym for verification. Everyone else shows a neutral "Not verified", never "verification in progress".
- Organizations stay publicly visible unless they are rejected or suspended. "Verified only" is a filter users can turn on, not the default.

## Why

- A trust claim we can't back up would destroy exactly the trust we sell.
- A verified-only catalog would be close to empty today.
- "In progress" labels imply an active check that isn't happening.

## Consequences

- Copy reviews (human and agent) check every trust word. This rule is in [`AGENTS.md`](../AGENTS.md) because agents kept reintroducing it.
- When a real verification process exists, this record gets replaced, not quietly ignored.
