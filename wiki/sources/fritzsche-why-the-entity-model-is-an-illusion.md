---
title: "Source: Fritzsche — Why the Entity Model Is an Illusion"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-why-the-entity-model-is-an-illusion]
raw_file: [raw/articles/fritzsche-why-the-entity-model-is-an-illusion.md]
tags: [event-sourcing, business-capabilities, ddd, entity-centric-thinking, substrate, focus]
---

# Source: Fritzsche — Why the Entity Model Is an Illusion

Article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-08-26), subtitled *"What Remains When You Model
What Happens."* Raw capture: `raw/articles/fritzsche-why-the-entity-model-is-an-illusion.md`.

This is the **root article of a four-capture arc** in this batch — the others being
[[fritzsche-how-event-sourcing-grows-with-the-business]] (the sequel, which continues its worked
example), [[fritzsche-the-entity-is-a-projection-not-a-row]] (the LinkedIn companion to *this* article —
**this page is the fuller primary**), and [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] (the
architectural corollary). Its argument names the problem the other three attack from different sides.

**Register:** practitioner position paper. "I come from this world and know the struggles it causes",
"I know from experience", "I've seen this happen too often" — **IMPRESSION NOT MEASUREMENT**
throughout; the vehicle-rental example is illustration, not evidence. (The often-quoted "Three decades of
experience have shown this" is NOT in this article - it is in the sequel,
[[fritzsche-how-event-sourcing-grows-with-the-business]].)

## Summary

The thesis is that **the entity is an illusion**: "The database contains one row for each vehicle. The
row resembles the vehicle itself, and is actually only the result of the last write. It holds the values
that survived the last update and says nothing about how they got there." The tell is that "almost every
system has audit tables, history tables, status columns, timestamps and change logs" — those are
**workarounds to keep the information the row destroys**.

His diagnosis is that the industry is "conditioned to think in terms of central data models," under "the
fallacy that we must model objects that represent the real world, endow them with properties and
behavior, and make them capable of changing on their own." Pre-defined entities make systems "rigid and
inflexible" and force development to proceed on assumptions: "the longer the process takes, the more the
product deviates from reality."

The replacement is to ask **what actually happens**. Registering a vehicle is not `CreateVehicle`
("that merely describes a database operation… the car rental company doesn't actually 'create' a
vehicle") but a sequence of domain events:
`VehicleAcquired → VehicleReceived → VehicleInfleeted → VehicleReleasedForRental`, each enriching the
system with new information. The "Vehicle" is then - "From my current perspective", his own hedge, which
must travel with the claim - **not an entity in the software** but "something that can appear in
different forms as a **projection**" - a "Received Vehicles" view exists because someone asked for it,
not because the model requires it.

## Key points

- **What mutation costs, stated as two losses:** retrieving an entity, mutating it in memory and writing
  it back "(1) destroys the information about what happened, (2) turns every concurrent request into a
  conflict we have to defend against." The second point ties the entity critique to the consistency
  thread ([[command-context-consistency]], [[dynamic-consistency-boundaries]]).
- **Identity without entity-hood.** "The existence of a unique identifier does not automatically
  constitute an entity in the sense of a specific data object. The vehicle itself is an entity because it
  **physically exists**. In our domain, it is a **reference**." The reference may be artificial (an ID)
  or "an immutable, unique, natural attribute" — for a vehicle, the VIN. From the events attached to that
  reference "one can deduce the state that possibly describes the physical entity at a specific point in
  time."
- **Capabilities, not objects, are the unit.** "A domain capability is something like 'AcquireVehicle' or
  'ReceiveVehicle.' They are independent of one another… autonomous, self-contained, and coherent. **They
  share only the Application State** — in this implementation, an Event Store and the event definitions.
  However, they know nothing about each other."
- **Perspectives are plural by design.** "Within a domain, there are different interests, which is why
  perspectives on a 'thing' vary and there isn't just one 'right' way… it's simply a different matter
  from the perspective of purchasing versus that of the repair shop. Every form that someone needs is
  derived from these events."
- **The "two worlds" observation** — business people value their real data and workflows; developers want
  patterns, new technology and beautiful code ("if the system follows SOLID and the Hexagonal
  Architecture, then it must be good") — and "when two worlds collide… exchanging Jira tickets for months
  on end, the disconnect can only grow." His practical corollary: **test data hides bugs**; "the bugs
  weren't noticed until the system went into production and was handling real data."
- **The modeling anti-pattern he names in passing:** when you talk to IT first, they "already think they
  know that this needs to be stored in the 'Vehicle' table" — "that's counterproductive because it
  immediately takes you into the 'how' phase."
- **Immutability as the conclusion, not the premise:** "data structuring remains important — but in a
  different way. Data is immutable and can only be superseded by a new version."

## Connections / contrast

- **Names a concept the KB has been circling without a page.** [[autonomous-domain-capabilities]],
  [[command-context-consistency]] and [[vertical-slice-architecture]] all describe symptoms of
  entity-centred design (a capability with no home; a guard wider than the context; a slice that is a
  local entry point into shared structure). This article states the **root claim** — that the entity
  itself is the error — and the batch deltas propose it as its own concept page, since four captures here
  argue one connected thesis.
- **Continuous with his own corpus, and one step further.**
  [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] held *state / event / fact / record*
  apart and concluded that ES is a storage decision. This article asks the prior question: **what is the
  thing being stored?** — and answers that the entity was never the thing.
  [[rico-fritzsche-rpu-reactor-vocabulary]] retired "Feature Slice" for RPU; here the capability is
  primitive and the object model is derivative. **Not from this article:** the "recorded state + the
  capabilities that know how to work with it" formulation of the domain does not appear in this capture -
  it is his wording in [[rico-fritzsche-autonomous-domain-capabilities-ccc]] and must be cited there.
- **Converges with Dudycz from the opposite direction.**
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] keeps a place for the entity —
  "**business logic goes per entity or aggregate**… slices don't each get a private notion of what an
  order is" — while Fritzsche denies the entity has any place in the software at all. That is a **real
  disagreement between two substrate primaries in the same batch**, not a difference of emphasis, and the
  KB should carry it as such. (Dudycz reaches his position from cohesion, Fritzsche from information
  loss.)
- **The DDD-internal target.** The critique lands on the **aggregate-as-object** reading of DDD, the same
  target as [[sara-pellegrini]]'s "Kill Aggregate" line and
  [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]. Note the difference in *level*:
  Pellegrini removes the aggregate as a *consistency* unit; Fritzsche removes the entity as a *modeling*
  unit. Both can hold; neither implies the other.
- **The agent relevance is implicit, not argued here.** The projection-per-interest position is what makes
  [[agent-readable-model-artifacts|model-derived views]] and per-capability context cheap; but this
  article makes no agent claim. For that, see
  [[fritzsche-functional-core-imperative-shell-agentic-coding]].
- Adjacent: [[event-sourcing]] · [[event-modeling]] · [[cqrs]] · [[business-capabilities]] ·
  [[domain-driven-design]] · [[locality-of-reference]].

## Limits

- **A position paper with one illustrative example** (vehicle rental) and no counter-case. No measurement,
  no before/after, no failed adoption discussed.
- **The example is small and greenfield.** The claim that pre-defined entities are unnecessary is argued
  on a four-event registration flow; nothing here addresses a large existing entity-centred system, a
  reporting estate built on normalized tables, or the migration cost.
- **Does not engage the strongest counter-arguments**: normalization's role in preventing update
  anomalies (he addresses this only in the sequel, via Pat Helland), query performance without a
  pre-shaped model, or the operational cost of many projections.
- **"They share only the Application State"** is asserted as achievable rather than demonstrated; the
  question of who owns a rule that spans capabilities he answers elsewhere
  ([[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]]), not here.
- Blog primary; ricofritzsche.me is client-rendered, so headless watches miss it (the KB's standing
  visibility note on this author).

_Source: `raw/articles/fritzsche-why-the-entity-model-is-an-illusion.md`._
