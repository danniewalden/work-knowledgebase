---
title: Event Versioning & Upcasting (Schema Migration)
type: concept
created: 2026-06-17
updated: 2026-09-04
sources: [event-modeling-event-sourcing-podcast, atomicobject-cqrs-event-sourcing-production-walkthrough, dilger-done-is-done-open-closed-new-slice, dudycz-strictland-contract-testing, dudycz-fixing-bugs-in-event-sourcing]
tags: [event-sourcing, schema-migration, versioning, pattern]
---

# Event Versioning & Upcasting (Schema Migration)

In an [[event-sourcing|event-sourced]] system the event log is **immutable**, so when an event's shape
needs to change you can't migrate rows in place — you have to deal with *old* events forever. The two
classic answers:

- **Upcasting** — at read/replay time, transform an old event version into the current shape on the fly
  (a function `vN → vN+1`). Keeps the rest of the code seeing only the latest schema.
- **Versioned events** — keep multiple event types/versions explicitly and let handlers/projections
  decide what to do with each.

This is *the* recurring "hard part" of event sourcing, and the podcast treats it as such: **Ep 5 "A
Case Against Upcasters"** argues against upcasters (credited to [[yordis-prieto]]) in favour of keeping
things simple and not reusing models across workflows; **Ep 37 "Version 2 of Everything: The Looming
Schema Migration Nightmare"** frames version-2-of-everything as the looming cost; and **Ep 46** returns
to event versioning, upcasting, and "navigating event types and versioning decisions"
([[event-modeling-event-sourcing-podcast]]).

## The two camps

The KB's production reference takes the **opposite** stance to the podcast's Ep-5 line:
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object]] recommends
**upcasters / event-versioning from day one** as standard discipline. So there's a genuine open
disagreement worth holding: *avoid upcasters, keep events stable and simple* (Dymitruk/Prieto, Ep 5)
vs. *expect schema change and build upcasting in early* (Atomic Object). Both agree the immutable log
makes naïve in-place migration impossible; they differ on whether to absorb change via transformation
or via discipline that minimizes it.

There's also a **design-time move that sidesteps the question**: [[martin-dilger]]'s "Done is Done"
([[dilger-done-is-done-open-closed-new-slice]]) prefers building a genuinely-distinct concept as a **new
[[vertical-slice-architecture|slice]]** rather than modifying an existing flow — precisely *because*
changing a live event-sourced flow risks migrations/upcasters and full retesting. I.e. the
[[open-closed-principle]] is partly a strategy for *avoiding* schema-migration pain, not just a coupling
preference.

## Tooling — catch breaking changes at build time ([[oskar-dudycz|Dudycz]], 2026-06-15)

[[dudycz-strictland-contract-testing|Strictland]] is a small JVM library that turns "did this event's
shape change?" into an ordinary unit test: it **serializes a message and commits the output as a snapshot
file**, so a **snapshot check** fails (in a normal PR diff) when the shape drifts, and a **compatibility
check** (`thenBackwardCompatible()` / `thenForwardCompatible()`) confirms old and new versions can still
read each other's data. No broker or schema registry. It doesn't *resolve* the upcasting-vs-versioning
debate above — it's the **detection** layer that makes either discipline enforceable in CI, in the same
fast feedback loop as the code. (.NET / TypeScript ports planned.)

## Not the same problem: an event whose *value* is wrong

Versioning and upcasting are about an event's **shape** changing. A separate and more common Tuesday
morning problem is an event whose shape is fine and whose **value** is wrong — a bad deploy wrote a
miscalculated number. [[dudycz-fixing-bugs-in-event-sourcing]] treats that case, and the answer is not an
upcaster: **append a corrective event** (the accountant's correcting entry — `previousTotal`,
`correctedTotal`, `reason`), rebuild the read models, fix the bug, and **never edit in place** ("having
precise history, bugs included, is a valid scenario"). If a clean stream is genuinely needed later, copy
and transform into a **new** stream and keep the original.

Two techniques from it belong on this page:

- **`buildSha` in event metadata** — record the commit the service was running when it appended. Then the
  blast radius of a bad deploy is a query (`WHERE metadata->>'buildSha' = '…'`) rather than a guessed
  `WHERE` clause over timestamps, which is exactly the failure that makes state-based corrective
  migrations compound. `correlationId`/`causationId` do the same job for diagnosis.
- **Model the correction as a capability** — a permissioned `CorrectReservationPrice` command with a
  mandatory reason, so bulk fixes and front-desk fixes emit the same events. The same "add a slice rather
  than change the past" instinct as [[dilger-done-is-done-open-closed-new-slice|"Done is Done"]], applied
  to operations — and it composes with
  [[fritzsche-how-event-sourcing-grows-with-the-business|additive evolution]]: a correction is just
  another event type.

*Caveat: an invented hotel-pricing scenario throughout; `buildSha` is advice, not a reported practice.*

## Related

[[event-sourcing]] · [[event-modeling]] · [[dynamic-consistency-boundaries]] · [[cqrs]] · [[yordis-prieto]] · [[open-closed-principle]] · [[oskar-dudycz]] · [[decision-trace]]

_Sources: [[event-modeling-event-sourcing-podcast]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]] · [[dilger-done-is-done-open-closed-new-slice]] · [[dudycz-strictland-contract-testing]] · [[dudycz-fixing-bugs-in-event-sourcing]]._
