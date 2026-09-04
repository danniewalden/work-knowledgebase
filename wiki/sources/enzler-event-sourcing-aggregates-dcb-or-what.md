---
title: "Enzler — Event Sourcing: Aggregates, Dynamic Consistency Boundaries, or what?"
type: source
created: 2026-07-02
updated: 2026-07-02
sources: [enzler-event-sourcing-aggregates-dcb-or-what]
raw_file: [raw/articles/enzler-event-sourcing-aggregates-dcb-or-what.md]
tags: [event-sourcing, dcb, ddd, cqrs, consistency, substrate]
---

# Enzler — Event Sourcing: Aggregates, Dynamic Consistency Boundaries, or what?

Blog post by **[[urs-enzler]]** (planetgeek.ch), 2026-06-23 — **part eleven** of his running
event-sourcing series. Captured verbatim at
`raw/articles/enzler-event-sourcing-aggregates-dcb-or-what.md`. A pragmatic **"third way"** in the
[[dynamic-consistency-boundaries|aggregate-vs-DCB]] debate: rather than pick a consistency *mechanism*,
**design the concurrency away.**

## What it says

Enzler frames the piece as *reasoning*, not a prescription. His starting principle: **start from the
real problems at hand, not from best practices applied widely** — "solve problems when they arise, not
earlier, and surely we don't 'solve' problems we don't have." The problem in scope is consistency:
never show *wrong* data (stale is usually fine). His canonical example is the classic DCB one — a
student registering for a course must not overbook the course or exceed their own course limit,
regardless of which side you query.

He lays out the two known solutions and why he uses neither by default:

- **[[domain-driven-design|DDD]] Aggregates** — everything that must change together atomically goes in
  one aggregate; changes go through methods that re-establish invariants. His critique: in more
  complicated systems this "can quickly lead to overly large aggregates," because *everything* needing
  consistency must live in a single aggregate.
- **[[dynamic-consistency-boundaries|DCBs]]** — he defers to dcb.events for the mechanism (even borrows
  its example "to lower your cognitive load") and grants they're "powerful, but quite complicated. So,
  if possible, I prefer simpler solutions."

**Why his team never cared.** They never debated aggregates or DCBs (the term didn't exist when they
started). Looking back, they *do* solve consistency — differently:

1. **Reframe "concurrent changes of *what*?"** For most data there are no concurrent changes (one
   employee enters their own data; HR/team-lead corrects monthly). Two conflicting commands would have
   to land within milliseconds. And "same data" rarely means *conflict*: two edits to a name (idempotent)
   or a name-and-address edit (independent) are fine — a real problem only exists when an **invariant**
   would be violated.
2. **"Small data" + task-based UI.** Project small things (small event streams), and expose **one
   command per task** carrying only that task's data — **no unit-of-work**, so there's no
   load-big-entity → mutate → conflict-on-save cycle. Collisions become even less likely.
3. **Replace a concurrent design with a non-concurrent one.** For the course example: students submit a
   **draft registration (intent)**; after the draft phase a **single-threaded algorithm** processes all
   drafts — which *also* lets you prioritise (e.g. final-year students) and pick among schedules. The
   concurrency is *eliminated*, and the overall solution is better. "All rules still need to be checked,
   but we are sure that there are no race conditions." Not always possible — but when it works, "much
   simpler than ever-growing aggregates or dealing with dynamic consistency boundaries."
4. **Serialise only where truly needed — with infrastructure, not a domain construct.** For validating a
   changed workday (dependent calculations + rules like breaks/max-hours), he doesn't validate in the
   request; he puts a message on **Azure Service Bus** and uses **sessions** (session-ID =
   tenant-ID + employee-ID + workday date) so the bus guarantees at most one message per session —
   serialising validation *within* the consistency boundary of an employee's workday. The bus also buys
   **scheduled future messages** (a 5-minute grace period so violations don't flash while the user is
   still typing), **dead-letter** debugging/reschedule, and **queue suspension** under heavy load.

His closing point is holistic design: solve the architectural problems *together* to get the simplest
overall solution, rather than optimising one in isolation.

## Why it matters here

The KB's DCB debate has so far been **DCB-vs-small-aggregate** ([[pellegrini-dynamic-consistency-boundary]]
and [[dilger-dcb-is-what-event-sourcing-should-have-been|Dilger]]'s "kill the aggregate" line vs
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object]]'s "keep the aggregate small").
Enzler adds a **third axis**: the cheapest consistency boundary is often **no concurrency at all**. It's
a concrete, production-grounded statement of the pragmatic "you might not need it" position, and it
independently rhymes with two things already in the wiki — **task-based UI / command-per-task** (a
[[cqrs]] intent-modeling instinct also seen in [[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic
Object]] and [[event-modeling]]'s command blocks) and **serialised writes** (his Service-Bus-sessions
answer is the message-infrastructure analogue of [[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche's]]
metadata-row-lock "serialised write order" argument — same insight, different layer). It also brings a
**new independent practitioner voice** into a debate the KB had mostly sourced from EM-adjacent authors.

## Caveats

Personal blog (secondary, one team's context: an HR/time-tracking product where concurrency is genuinely
rare — he says so). Enzler himself flags that the non-concurrent redesign "is always possible? Probably
not." The LLM aside ("wrong data is clearly bad. Why do I think of LLMs now?") is a throwaway — **no
agents angle is developed**; this is a substrate piece, not [[event-modeled-agent-design|EM×agents]].

_Source: [[enzler-event-sourcing-aggregates-dcb-or-what]] (raw: `raw/articles/enzler-event-sourcing-aggregates-dcb-or-what.md`)._
