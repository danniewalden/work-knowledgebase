---
title: Process Managers vs. To-Do List Projections
type: concept
created: 2026-07-29
updated: 2026-07-29
sources: [adaptech-workflow-not-inside-giant-process-manager, event-modeling-event-sourcing-podcast]
tags: [event-modeling, event-sourcing, cqrs, process-manager, saga, automation-pattern, focus-substrate]
---

# Process Managers vs. To-Do List Projections

A design choice for **long-running business processes**: coordinate them with one large **saga /
process manager** (all steps, retries, and compensations inside a single coordinator), or model
progress as **visible information** — a **projected to-do list** that many small, focused
**processors** act on. The [[event-modeling]] answer is the latter, and it is the concrete
realization of the method's **Automation pattern** ("a processor works a todo list").

## The saga / process-manager anti-pattern

A workflow that begins as a simple sequence grows, under real operating conditions (timeouts,
late confirmations, retries, mid-process restarts), into one coordinator holding every branch. The
failure is not code complexity but **loss of visibility**: the current state of the business process
can only be read by understanding the coordinator's internal logic. Support, operations, developers,
and leaders can't answer "what finished / what's still missing / did it fail or arrive late / can it
resume safely / would a retry double-act?" — so the workflow exists but the business cannot inspect
it, which is itself delivery risk ([[adaptech-workflow-not-inside-giant-process-manager]]).

## The to-do-list projection alternative

Two moves ([[adaptech-workflow-not-inside-giant-process-manager]]):

1. **Represent progress as a projection.** Per active process, a read model records what is known,
   done, unfinished, and whether there's enough information to continue (e.g. a stock purchase:
   price received?, price timestamp, order submitted?, submission result, retry allowed?). It **does
   not replace the event log** — events stay the record of what happened; the projection is a
   [[cqrs]] view that **people and automated processors both read**.
2. **Give each processor one responsibility.** Several single-purpose processors observe the same
   to-do list — one fetches the price, one submits once a price exists, one retries or verifies an
   uncertain result — each reacting only to its fields. Focused, testable, replaceable; the
   projection (not a coordinator) says which step is ready.

## Why it holds up

- **External calls are business states.** not-sent / awaiting / arrived-too-late /
  done-but-unconfirmed are distinct, business-meaningful states needing timestamps (staleness) and
  stable identifiers (idempotency — don't charge twice). As events + statuses they're observable and
  improvable; buried in a procedure they're not.
- **Recovery is visible before failure.** an event history + to-do list are durable evidence, so a
  processor can **verify rather than repeat** a possibly-completed action after a restart — recovery
  as normal design, not special cases added post-incident. This is what makes legacy modernization of
  such workflows safer.
- **Visibility beyond architecture.** the same projection powers dashboards, support ("why did this
  stop?"), and SLA measurement; business-language statuses (`PaymentAcceptedAwaitingShipment`) beat
  "instance at step 7."

## Relationships

- The **Automation pattern** in [[event-modeling]] is exactly this (processor + todo list); Event
  Modeling exposes the structure *before* implementation — a timeline of commands/events/projections/
  automations instead of one "Saga" box.
- Sits on the [[event-sourcing]] substrate (events as the durable evidence recovery reads) and uses a
  [[cqrs]] projection as the coordination surface.
- One-processor-one-responsibility rhymes with [[vertical-slice-architecture]] (a processor as a
  focused slice) and with [[autonomous-domain-capabilities]] (Reactors — a capability owning its own
  processing, building context from recorded events, [[rico-fritzsche]]).
- Business-language statuses tie to [[domain-driven-design]] / [[business-capabilities]].
- Recurring theme on the [[event-modeling-event-sourcing-podcast]] ("sagas → to-do lists"); this is
  its first dedicated primary.

_Source pages: [[adaptech-workflow-not-inside-giant-process-manager]] · [[event-modeling-event-sourcing-podcast]]._
