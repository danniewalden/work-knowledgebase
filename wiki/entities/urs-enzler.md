---
title: Urs Enzler
type: entity
created: 2026-07-02
updated: 2026-07-02
sources: [enzler-event-sourcing-aggregates-dcb-or-what]
tags: [event-sourcing, dcb, ddd, cqrs, substrate, practitioner]
---

# Urs Enzler

Software architect and blogger at **planetgeek.ch**, writing a long-running, hands-on
**[[event-sourcing]]** series (the captured piece is *part eleven*). A **pragmatist** voice on the
[[event-sourcing]] / [[cqrs]] / [[dynamic-consistency-boundaries|DCB]] substrate: design from the
concrete problems at hand rather than applying best practices broadly — "solve problems when they
arise, not earlier."

## Position captured here

In [[enzler-event-sourcing-aggregates-dcb-or-what]] (2026-06-23) he offers a **third way** in the
aggregate-vs-DCB debate: instead of choosing a consistency *mechanism*, **eliminate the concurrency**
that creates the consistency problem —

- **"Small data" + task-based UI** (a command per task, no unit-of-work) so conflicting commands are
  vanishingly unlikely;
- **replace a concurrent design with a non-concurrent one** (draft-intent + a single-threaded batch
  algorithm — which also enables prioritisation);
- **serialise only where needed via infrastructure** — Azure Service Bus **sessions** keyed on
  tenant+employee+workday, plus scheduled grace-period messages, dead-lettering, and queue suspension.

He treats **DCBs** as "powerful, but quite complicated" and **DDD aggregates** as prone to growing
"overly large," preferring the simplest overall design. His example domain is an HR / time-tracking
product where genuine concurrency is rare (a caveat he states himself).

## Related

[[dynamic-consistency-boundaries]] · [[event-sourcing]] · [[cqrs]] · [[domain-driven-design]] ·
[[sara-pellegrini]] (he cites a discussion with her on DCBs) · [[rico-fritzsche]] (parallel
"serialised write order" argument) · [[event-modeling]]

## Caveats / to capture next

Biographical detail is thin — the entity is grounded on a single captured post. Earlier parts of his
event-sourcing series (parts 1–10, incl. the "operation runner," "small data," and earlier consistency
posts he references) are candidates to capture if the substrate thread deepens.

_Source: [[enzler-event-sourcing-aggregates-dcb-or-what]]._
