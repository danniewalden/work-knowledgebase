---
title: Oskar Dudycz
type: entity
created: 2026-06-29
updated: 2026-09-04
sources: [dudycz-strictland-contract-testing, dudycz-fork-can-you-own-it, dudycz-vertical-slices-ownership-and-external-dependencies, dudycz-fixing-bugs-in-event-sourcing, dudycz-backend-for-frontends-for-event-driven-apis, dudycz-archiving-events-stream-lifetime-slicing, dudycz-checklist-first-event-sourcing-feature]
tags: [person, event-sourcing, cqrs, vertical-slice-architecture, focus-substrate]
---

# Oskar Dudycz

Event-sourcing practitioner and educator; creator of **Emmett** (a Node.js/TypeScript event-sourcing
toolkit), co-maintainer of **Marten** (see [[critter-stack]]), and a prolific blogger at
**event-driven.io** (CC BY-SA 4.0). A core **design-substrate** voice (Thread 6) on event sourcing,
CQRS, and [[vertical-slice-architecture|vertical slices]] — pragmatic and anti-hype.
Watch-listed in `watch-config.json`. **As of the 2026-09-04 batch he is the KB's most substantial
substrate practitioner**, with five captures spanning vertical slices, incident recovery, message design,
stream lifetime and adoption — superseding the earlier note that his VSA material was an out-of-window
gap ("Vertical Slices, CQRS, Semantic Diffusion", Aug-2025, remains uncaptured but is no longer the best
available source).

In the KB he is the author of:
- **[[dudycz-strictland-contract-testing|Strictland]]** (2026-06-15) — a small JVM contract-testing
  library that snapshots a message's serialized shape and checks backward/forward compatibility,
  committed as a file and reviewed in a normal PR diff; on the [[event-versioning-and-upcasting]] thread.
- **[[dudycz-fork-can-you-own-it|You can fork a package, but can you own it?]]** (2026-06-08) — mostly
  off-thread dependency-posture commentary, kept for its "LLM as a fork" point: LLMs change the cost of
  *producing* code, not *owning* it ([[agentic-coding]] ownership caveat).

## Position — cohesion over independence, and the slice as a function (2026-08/09)

- **[[dudycz-vertical-slices-ownership-and-external-dependencies]]** (2026-08-10) — his substantive VSA
  primary. Fixes the vocabulary (**slice** = one piece of functionality, "more a function than an
  entity"; **module** = grouping of slices by "what changes together"; **bounded context** = a linguistic
  barrier, so a frontend and a backend are "two deployment targets"), then answers the question the
  pattern usually dodges: **"From inside a slice, there's one category of thing: external."** A slice
  declares **narrow function types in its own vocabulary**, satisfied structurally, composed by hand in
  one file near the entry point — no container. Module `api.ts` (what it *offers*) and consumer-declared
  need (what it *asks for*) are two directions across one boundary and you want both. Cycles dissolve
  because neither module imports the other. Persistence: **logic per entity/aggregate, read models per
  query, schemas per module.** And the stance that distinguishes him: "**independence isn't a value in
  itself**… hidden dependencies are still there, only harder to find. What I'm optimising for is
  **cohesion**."
- **[[dudycz-fixing-bugs-in-event-sourcing]]** (2026-07-27) — the KB's answer to "you can't fix bad data
  in an immutable log." Runs one pricing incident twice; introduces **`buildSha` in event metadata** for
  exact blast radius; **fix forward with a corrective event**, never rewrite; and the argument that
  actually settles it — a blind bulk recalculation is arithmetically correct and **undoes a human's
  deliberate goodwill correction**, because "in the mutable model, a bug and a deliberate correction look
  identical: a number in a column." Then: **make correction a feature** (a permissioned command with a
  mandatory reason), so "nobody connects to the production database at 23:00." *All figures are an
  invented scenario.*
- **[[dudycz-backend-for-frontends-for-event-driven-apis]]** (2026-08-29) — **"Poor Man's replication
  through the queue"**: `SthSthCreated/Updated/Deleted` published as if they were events. Splits
  **internal vs external** events and insists messages are also **commands** (directed, rejectable) and
  **state** (Hohpe). Anchors the [[internal-vs-external-events]] page.
- **[[dudycz-archiving-events-stream-lifetime-slicing]]** — **slice streams per lifetime**, keep the last
  summary event, archive the rest; archiving strategy need not be uniform. (Date is a repost date at
  best.)
- **[[dudycz-checklist-first-event-sourcing-feature]]** (2026-09-01) — 14 questions for picking a first
  event-sourced feature, selecting for decision-shape, ownership, and **reversibility** ("off the critical
  path", "wrong for a day", "small enough to do slightly rogue"). He disclaims it himself ("that's why I
  don't like checklists!") and the fuller article is uncaptured.

**Register and interests.** Experience reports from client work, no measurement anywhere; he sells
consulting/training on these patterns (the VSA article closes with the offer). His agent claims are
appended to design arguments and framed as such — "an old argument that happens to have got more
valuable." The three LinkedIn captures came via **live logged-in Chrome**, dates day-accurate only.

**Where he disagrees with [[rico-fritzsche]]** (same fortnight): both reject CRUD-shaped operation names
and cite intent-carrying commands ([[greg-young]]'s Task-Based UI), but Dudycz **keeps the entity as the
home of business rules** where Fritzsche calls it an illusion. See [[entity-centric-thinking]].

_Source pages: [[dudycz-strictland-contract-testing]] · [[dudycz-fork-can-you-own-it]] ·
[[dudycz-vertical-slices-ownership-and-external-dependencies]] ·
[[dudycz-fixing-bugs-in-event-sourcing]] · [[dudycz-backend-for-frontends-for-event-driven-apis]] ·
[[dudycz-archiving-events-stream-lifetime-slicing]] ·
[[dudycz-checklist-first-event-sourcing-feature]]._
