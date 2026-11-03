# 0003: Sign-up must not block the first contact

Status: accepted
Date: 2026-08-06

## Context

A person who finds a pet wants to ask about it now. A forced registration at that moment is where many marketplaces lose people.

## Decision

Users can contact a shelter or breeder without creating an account. We offer an account only after the contact succeeds.

## Why

- The first contact is the moment of highest intent. Any wall there costs real inquiries, and good inquiries are what we expect breeders to pay for ([0001](0001-breeder-first.md)).
- An account makes sense to the user once they've seen the value: following up, saving favourites, getting alerts.

## Consequences

- We need protection against spam inquiries without accounts, so contact forms are rate-limited.
- Fewer registered users early on. We accept that in exchange for more first contacts.
- The bet behind it is tracked as a hypothesis, still to test: contact without login increases inquiries without lowering their quality ([hypotheses](../product/hypotheses.md)).
