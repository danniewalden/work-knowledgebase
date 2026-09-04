---
title: "Source: Fritzsche — How Event Sourcing Grows With the Business"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-how-event-sourcing-grows-with-the-business]
raw_file: [raw/articles/fritzsche-how-event-sourcing-grows-with-the-business.md]
tags: [event-sourcing, business-capabilities, open-closed-principle, schema-migration, substrate, focus]
---

# Source: Fritzsche — How Event Sourcing Grows With the Business

Article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-08-30), subtitled *"Immutable Data, Domain
Capabilities, and an Additive Schema."* Raw capture:
`raw/articles/fritzsche-how-event-sourcing-grows-with-the-business.md`. The **direct sequel** to
[[fritzsche-why-the-entity-model-is-an-illusion]], which it cites and whose vehicle-rental example it
continues.

**Register:** practitioner argument with code. The C# fold and rule snippets are illustrative; the
"count what has to change" exercise is a **walkthrough of his own example**, not a measured study —
**IMPRESSION NOT MEASUREMENT** for every efficiency claim.

## Summary

The article's device is to **insert a new process step into a running system and count what breaks**. The
original flow was `Acquire → Receive → Infleet → Release`; the business later needs
`Acquire → Receive → **Inspect** → Infleet → Release`. In an entity-centred design that is a change to a
shared, global, mutable structure ("developers have long since done away with global variables, but the
database is one giant global variable" — Kleppmann, 2014). In an event-sourced design the event-type set
**only grows**: adding `VehicleInspected` means a new event type, a new function, and a change to
existing functions *only where the new information is relevant to their context*.

The mechanism is the **fold**. Each domain capability owns its **command context** and derives its own
state by querying the relevant events and reducing them (Greg Young, 2012: *"Current State is a Left Fold
of previous behaviours"*). `InfleetVehicle` needs to know only whether the vehicle was received and
whether it is already infleeted; `ReleaseVehicleForRental` folds a different subset. "There is no shared
vehicle object that both would need to share." So `AcquireVehicle` and `ReceiveVehicle` are untouched by
the new step, `InfleetVehicle` gains two lines (one fold case, one rule), and **no data migration is
required** — "vehicles already in the fleet simply do not have a `VehicleInspected` event," and the fold
must account for the absence where it matters.

## Key points

- **The schema is the answer to a question you cannot answer at the start.** "Tables that were originally
  intended to store only data records often end up with additional status, audit, and date columns over
  time. This is the typical outcome when modeling begins with an entity-centric approach and it is
  gradually realized that the business has a process."
- **The process is invisible in the schema.** Adding date columns is technically trivial — "but the
  process isn't visible. No one can tell from the schema in what order the date columns are filled or
  which ones are allowed to remain empty. That's specified in the code, scattered across all the places
  where the table is written."
- **Why normalization forces early completeness** (his one cited mechanism, from **Pat Helland**,
  *Immutability Changes Everything*, CIDR 2015): "Normalization exists to prevent update anomalies. A
  schema designed to handle updates must therefore be complete before the first record is written. This
  is not necessary for immutable data."
- **Names come in pairs.** Capability `InfleetVehicle` produces event `VehicleInfleeted`;
  `InspectVehicle` produces `VehicleInspected`. "Every action that leads to an event is a domain
  capability."
- **State is transient and context-scoped:** "The state exists for as long as the command is being
  processed: it is created, the rules are applied to it, and the result is one or more new events."
  **"Events that the rules do not read are not taken into account."**
- **The asymmetry he identifies as the reason it works:** "The autonomy of the functions and the
  immutability of the events are two sides of the same coin: **events are additive, since no reader needs
  to know the big picture. Functions, on the other hand, remain small because they derive their specific
  perspective precisely from the events.**"
- **Where cost does land — and he says so.** "A projection for displaying the inspection… is new code
  with its own rebuild"; for a status column, by contrast, "you must specify which of the new values
  should be assigned to the individual old rows." So the additive claim is about the **write model and
  stored data**, not about projections being free.
- **The audit-feature rejection, in article form:** "In my experience, the use of event sourcing is often
  justified on the grounds that it provides a complete history… I consider this to be fundamentally
  wrong… the fact that the history is preserved is a **consequence** of that very property, but it is not
  the reason for it. Anyone who views event sourcing as an audit function has misunderstood its purpose."
  The real motivation is "domain capabilities that are independent of one another and not tied to a
  central, shared data structure." This paragraph is the article the LinkedIn note
  [[fritzsche-event-sourcing-is-not-an-audit-feature]] compresses — **this page is the fuller primary.**
- **Also cites** Rich Hickey, *The Value of Values* (2012) on accumulative records, and
  [[adam-dymitruk]]'s 2019 [[event-modeling]] as the method for arriving at the events.
- **RPU note:** he mentions that a domain capability "is implemented as a **Request Processing Unit
  (RPU)**" but deliberately stays with *capability* in this article — the vocabulary from
  [[rico-fritzsche-rpu-reactor-vocabulary]], held at arm's length here.

## Connections / contrast

- **The clearest mechanism the KB has for the "additive change" claim.** [[open-closed-principle]] and
  [[dilger-done-is-done-open-closed-new-slice]] argue new behaviour should *add* code; this article shows
  **why the event log makes that structurally true** (no reader needs the big picture) and delimits it
  (projections still need building, folds still need the absent-event case). It is the counterpart, from
  the write side, to [[event-versioning-and-upcasting]]: **adding an event type is not a schema
  migration, which is different from changing an existing event's shape** — the case that page covers.
- **Fills in [[command-context-consistency]] with a concrete fold.** CCC has been stated as a principle
  and a guard; this gives the reduce-to-context step as code, and states the discipline that makes it
  safe ("events that the rules do not read are not taken into account").
- **Directly relevant to [[dudycz-fixing-bugs-in-event-sourcing]] in the same batch.** Fritzsche's
  argument is that the entity-centred *schema* accretes columns under process discovery; Dudycz's is that
  the entity-centred *row* destroys the evidence you need after a bad deploy. Same target (the last-write
  row), different failure mode (evolution vs. incident recovery) — the two make an unusually complete
  case together.
- **An internal tension in his own corpus, worth flagging.** In
  [[fritzsche-thinking-in-events]] (2026-07-03) he writes that "Event Sourcing becomes especially
  compelling when the team needs **strong auditability**, the ability to reconstruct past states, or
  independent read models"; here (and in the LinkedIn note) he says justifying ES on history/audit grounds
  is "fundamentally wrong." These are reconcilable — *auditability is a legitimate benefit but the wrong
  motivation* — but he does not reconcile them explicitly, and a page citing either should not present
  it as his settled single view.
- **Against the vendor framing.** [[axoniq-government-ai-explainability-requirements]] sells event
  sourcing precisely *as* an audit and explainability capability. Fritzsche's "history is a consequence,
  not a cause" is the standing objection to that pitch.
- Adjacent: [[event-sourcing]] · [[autonomous-domain-capabilities]] · [[business-capabilities]] ·
  [[cqrs]] · [[event-modeling]] · [[greg-young]] · [[vertical-slice-architecture]].

## Limits

- **One worked example, authored by the person making the claim.** "That shows how systems in the real
  world emerge and grow, and it lets you count what has to change and what does not" — the count is over
  *his* example, chosen to make the point. No comparative measurement against a real migration.
- **The favourable case is chosen.** The new step lands *between* existing steps and only one existing
  capability needs the new fact. He does not test the awkward cases: a new fact that every capability
  must read, a rule that must be applied retroactively to already-infleeted vehicles, or a change to an
  existing event's *shape* (which is [[event-versioning-and-upcasting|the actual hard problem]] and is
  outside this article's scope).
- **Projections and read-model cost are acknowledged but not quantified**; nor are replay times, storage
  growth, or the operational burden of many folds (see
  [[dudycz-archiving-events-stream-lifetime-slicing]] for the storage-growth answer from another author).
- **The cited authorities are secondary** (Helland, Kleppmann, Hickey, Young, Dymitruk) — none captured in
  the KB as primaries, and quoted here in Fritzsche's framing.
- Blog primary; client-rendered site (headless watches miss it).

_Source: `raw/articles/fritzsche-how-event-sourcing-grows-with-the-business.md`._
