---
title: CQRS (Command Query Responsibility Segregation)
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [eventmodeling-what-is-event-modeling, akka-event-sourcing-backbone-agentic-ai, atomicobject-cqrs-event-sourcing-production-walkthrough, enzler-event-sourcing-aggregates-dcb-or-what, dudycz-vertical-slices-ownership-and-external-dependencies]
tags: [cqrs, pattern, event-sourcing, architecture]
---

# CQRS (Command Query Responsibility Segregation)

An architectural pattern that **separates the write model (commands) from the read model
(queries/views)** instead of using one model for both. Closely associated with
[[greg-young]] and frequently paired with [[event-sourcing]] (the "CQRS/ES" lineage).

## Relevance to this KB

- [[event-modeling]]'s two core building blocks — **commands** (write/intent) and **views /
  read models** (read) — are CQRS made visual on the blueprint. Dymitruk built event
  modeling partly on Greg Young's CQRS/ES long-running process specifications.
- The read/write separation is also why [[kevin-hoffman]] calls agentic systems a "perfect
  match" for event sourcing — their distributed architecture already separates these models
  ([[akka-event-sourcing-backbone-agentic-ai]]).

## Related

[[event-sourcing]] · [[event-modeling]] · [[vertical-slice-architecture]] (organizing by feature
slice "gives CQRS out of the gate" — [[jimmy-bogard]]) · [[dynamic-consistency-boundaries]] ·
[[greg-young]] · [[domain-driven-design]]

**Production reference (2026-06-17):**
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object's walkthrough]] shows the
read/write split in a real codebase: a command bus + aggregate state-machine on the write side, and a
"mercifully boring" relational read model maintained by projections — and argues the asymmetry is a
feature (a write-side command bus earns its keep; a read-side query bus often doesn't).

**Task-based UI (2026-06-23):** [[urs-enzler]]
([[enzler-event-sourcing-aggregates-dcb-or-what]]) uses a **command per task** carrying only that
task's data (no unit-of-work) as a *consistency* tactic — small, intent-shaped writes make conflicting
commands unlikely, so the [[dynamic-consistency-boundaries|aggregate/DCB]] question rarely binds. The
same command-as-intent instinct as [[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic
Object]] and [[event-modeling]]'s command blocks, applied to sidestep concurrency.

**Read models per query, and why naming the command is the whole game (Dudycz, 2026-08).**
[[dudycz-vertical-slices-ownership-and-external-dependencies]] states the read-side rule in one line —
"**Read models go per query.** This is where a table per feature is right… Build a table that answers
that. The settlement report needs something else and gets its own. **Resist making a single query serve
five screens by expanding columns**" — while keeping write-side logic per entity/aggregate and schemas per
module. On the write side he grounds command-as-intent in [[greg-young]]'s **Task-Based UI**: when the
client posts data-centric structures, "the domain has no verbs, and the user's intent is lost on the way
in." The consequence: "If every operation is 'update the order', you have one feature and nothing to
divide. Once you have `VerifyOrder`, `ConfirmOrder`, `RejectOrder`, you have folders." **And it applies
without event sourcing: "the name is the value, and the underlying implementation can be a single
`UPDATE`."** A status column "records that the order is verified. It doesn't record that anybody verified
it."

Two more, from the same source: **return the available actions with the data** rather than letting the
frontend re-derive them from status fields ("the part of HATEOAS I find useful, without the rest of the
ceremony"); and a **backend-for-frontend is a legitimate slice** — "it's named after a screen because
that's honestly what it is" — since "one screen is routinely composed of data gathered from several
modules." *Experience report, no measurement.*

*(His write-side rule — logic per entity or aggregate — is the live disagreement with
[[rico-fritzsche]]; see [[entity-centric-thinking]].)*

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]] · [[enzler-event-sourcing-aggregates-dcb-or-what]] · [[dudycz-vertical-slices-ownership-and-external-dependencies]]._
