---
title: Entity-Centric Thinking (and why it survives good architecture)
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-why-the-entity-model-is-an-illusion, fritzsche-the-entity-is-a-projection-not-a-row, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-vsa-does-not-fix-entity-centered-thinking, fritzsche-event-sourcing-is-not-an-audit-feature, fritzsche-thinking-in-events, dudycz-vertical-slices-ownership-and-external-dependencies, dudycz-fixing-bugs-in-event-sourcing]
tags: [entity-centric-thinking, business-capabilities, event-sourcing, vertical-slice-architecture, ddd, substrate, focus]
---

# Entity-Centric Thinking (and why it survives good architecture)

The habit of organising a system around **the things that change** (nouns, rows, entity lifecycles)
rather than around **what happens in the business** (operations, decisions, facts). Named as a single
problem by **[[rico-fritzsche]]** across four captures in Aug 2026, whose claim is that this habit —
not layering, not the wrong framework — is the root defect that other architectural moves fail to fix.

## The claim, in four steps

1. **The entity is an illusion.** "The database contains one row for each vehicle. The row resembles the
   vehicle itself, and is actually only the result of the last write. It holds the values that survived
   the last update and says nothing about how they got there"
   ([[fritzsche-why-the-entity-model-is-an-illusion]]). The tell: "almost every system has audit tables,
   history tables, status columns, timestamps and change logs" — workarounds for what the row destroys.
2. **The entity is a projection, not a row.** A physical vehicle exists; in the software there is only a
   **reference** (an ID, or an immutable natural attribute like a VIN) against which facts are recorded.
   "Every form that someone needs is derived from these events"
   ([[fritzsche-the-entity-is-a-projection-not-a-row]]). Perspectives are plural by design — purchasing
   and the repair shop want different views of the "same" thing.
3. **Mutation costs two things.** Load-mutate-write "(1) destroys the information about what happened,
   (2) turns every concurrent request into a conflict we have to defend against" — which is why this page
   connects to [[command-context-consistency]] and [[dynamic-consistency-boundaries]] and not only to
   modelling.
4. **The replacement unit is the capability.** `AcquireVehicle`, `ReceiveVehicle` are "autonomous,
   self-contained, and coherent… they share only the Application State" — an event store and the event
   definitions — "however, they know nothing about each other." See
   [[autonomous-domain-capabilities]] and [[business-capabilities]].

## Why good architecture doesn't fix it

The sharpest consequence, and the reason this page exists rather than a paragraph on another one:
**[[vertical-slice-architecture|VSA]] improves locality *after* a team chooses a request boundary; it
does not discover that boundary** ([[fritzsche-vsa-does-not-fix-entity-centered-thinking]]). Noun
folders with `Create/Get/Update/Delete` beneath them are vertically organised *and* entity-centred:
"Starting with the record that changes makes the entity lifecycle the use-case boundary. **That is an
ownership problem.**" The same charge lands on Clean Architecture: "Horizontal layers and vertical slices
arrange code differently. Both preserve the same ownership problem when entity lifecycles determine the
use cases."

His three-question design test (a heuristic, **not a study**): list the business changes a generic update
accepts; count how many slices depend on the shared entity model; change one business rule and observe
what else must move. Note that the last two are coupling measurements by inspection — the quantity
[[balanced-coupling]] formalises.

An event store does not fix it either: "If the stored events are named `ReservationUpdated`,
`GuestUpdated`, or `PropertyChanged`, the system may technically use Event Sourcing while still
preserving a CRUD-shaped understanding of the domain. **Storing vague events only preserves the vagueness
permanently**" ([[fritzsche-thinking-in-events]]). The messaging twin of the same failure is
[[oskar-dudycz|Dudycz's]] **"Poor Man's replication through the queue"** — publishing
`SthSthCreated/Updated/Deleted` as if they were events
([[dudycz-backend-for-frontends-for-event-driven-apis]], and see [[internal-vs-external-events]]).

## What it costs when it breaks

[[dudycz-fixing-bugs-in-event-sourcing]] is the operational bill for step 1. After a bad deploy, the row
holds a total with no record of the inputs that produced it, so the corrective migration must recompute
against *today's* configuration — repricing rows that were never wrong, and destroying the evidence
needed to check the fix, so "the input to migration three is the output of migration two." **A bug and a
deliberate human correction look identical: a number in a column. There's nothing to branch on.**
(Illustrative scenario, not measured data.)

## The counter-position, held on purpose

**The entity is not universally rejected, and this KB does not pick a side.** [[oskar-dudycz]], in the
same week, keeps it as a deliberate rule: **"Business logic goes per entity or aggregate.** The rules
about what states an order can be in and which transitions are legal belong to the order. One place, and
every slice that decides about an order goes through it. **Slices don't each get a private notion of what
an order is**" ([[dudycz-vertical-slices-ownership-and-external-dependencies]]). He agrees entirely on
the *naming* half — CRUD verbs give you nothing to slice along, name the business operation, and he cites
[[greg-young]]'s Task-Based UI for it — and disagrees on where rules live. **Fritzsche argues from
information loss; Dudycz from cohesion. Both are 2026-08 practitioner primaries, neither cites the other,
and neither is measured.** The KB carries the disagreement rather than picking a winner or splitting the
difference.

Note also that Dudycz's rule puts him alongside the **conventional "keep the aggregate small"** line
already recorded on [[dynamic-consistency-boundaries]] (Atomic Object's production walkthrough), so this
is not a lone dissent — it is the mainstream position, restated in slice vocabulary.

Related: [[sara-pellegrini]]'s "Kill Aggregate" line removes the aggregate as a *consistency* unit
([[dynamic-consistency-boundaries]]); Fritzsche removes the entity as a *modelling* unit. Both can hold;
neither implies the other.

## Evidence standing

**Weak, and uniformly so.** Every claim on this page is practitioner argument — position papers, LinkedIn
posts, and one worked vehicle-rental example authored by the person making the claim. No measurement, no
case study, no failed-adoption report, and the fuller article behind the VSA argument is **uncaptured**
(linked in a LinkedIn first comment, unresolved at capture). Read it as a well-articulated hypothesis
with a named counter-position, not a settled finding.

## Related

[[event-sourcing]] · [[event-modeling]] · [[business-capabilities]] ·
[[autonomous-domain-capabilities]] · [[command-context-consistency]] ·
[[vertical-slice-architecture]] · [[slice]] · [[cqrs]] · [[domain-driven-design]] ·
[[dynamic-consistency-boundaries]] · [[internal-vs-external-events]] · [[balanced-coupling]] ·
[[locality-of-reference]] · [[event-modeling-anti-patterns]]

_Sources: [[fritzsche-why-the-entity-model-is-an-illusion]] · [[fritzsche-the-entity-is-a-projection-not-a-row]] · [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-thinking-in-events]] · [[fritzsche-event-sourcing-is-not-an-audit-feature]] · [[dudycz-vertical-slices-ownership-and-external-dependencies]] · [[dudycz-fixing-bugs-in-event-sourcing]]._
