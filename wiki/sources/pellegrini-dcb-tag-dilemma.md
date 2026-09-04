---
title: "Source: Pellegrini — The DCB Tag Dilemma"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [pellegrini-dcb-tag-dilemma]
raw_file: [raw/articles/pellegrini-dcb-tag-dilemma.md]
tags: [event-sourcing, dcb, ddd, consistency, substrate, focus]
---

# Source: Pellegrini — The DCB Tag Dilemma

Article by **[[sara-pellegrini]]** (Event Thinking blog, 2026-03-05), the first substantial new capture
of her in the KB since her 2023 naming post. Raw capture:
`raw/articles/pellegrini-dcb-tag-dilemma.md` — an **out-of-window backfill** (2026-03, filed on the
2026-09-04 sweep; a recency-bounded watch cannot reach it), transcribed verbatim from WebFetch with the
single lead image noted inline.

**Interested-party marker that travels with every claim below.** Pellegrini **originated** the
[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] ([[pellegrini-dynamic-consistency-boundary]],
2023). This piece is therefore the concept's own author defining her own terms — **authoritative on
intent, and NOT INDEPENDENT** as corroboration that tags are the *right* mechanism. It is conceptual
definition from start to finish: **it contains no measurements, benchmarks, or claims of outcome.**

## Summary

DCB filters the events relevant to a decision on two attributes, and Pellegrini's argument is that those
two attributes are **orthogonal dimensions of the same fact**, not two flavours of the same key. The
**event type** says *what kind of thing happened*; a **tag** says *which domain elements were involved* —
formally, "the identifier of a **historic route** in the domain." Used together they let you select
precisely the events a particular decision must consider.

The mechanism that matters for the KB's aggregate debate is stated in one paragraph: the aggregate carried
the same *meaning* of consistency boundary, but **"an aggregate is only one historic route,"** while in
reality a single decision may advance more than one. Because tags are orthogonal to type, a DCB selection
can involve **several historic routes at once** — and bringing types into the selection **avoids
unnecessary collisions between things that are actually irrelevant**. That is the precise sense in which
DCB is more than a renamed aggregate.

## Key points

- **Type = the nature of the fact.** `StudentSubscribedToCourse` conveys the kind of occurrence and
  nothing about who was involved. Type is also **semantically tied to the business logic**, because
  events of one type are generally handled by the same logic.
- **Tag = who/what was involved**, and it is **semantically tied to the business rules** — the rules
  "guide the domain's historic routes in the right direction, with consistency boundaries preventing them
  from going astray."
- **A tag captures a shared property across a set of facts**: all events sharing a tag involve the same
  domain element, which "might be a concrete entity, or something more abstract."
- **Tag candidates are not just the actor.** In student enrollment, both the *student ID* (the actor) and
  the *course* (the target) are tags. **Context can also be tagged**: on `UsernameChanged`, the
  **previously released username** should be a tag *if* the taken/available state of a username matters
  when validating another user's claim on it. So the tag set is a **domain-constraint decision**, not a
  schema decision.
- **The one-sentence form (her own compression, "with some loss of completeness"):** "An event's type
  tells you what kind of thing happened; the tags tell you which historic routes were advanced by the
  event."
- **The closing heuristic** is deliberately loose: "add a tag whenever you believe it will be a useful
  grouping key for protecting the consistency of your business model." She points readers to
  `dcb.events/topics/tags` for depth.

## Connections / contrast

- **This is the mechanism under "kill the aggregate."** [[dynamic-consistency-boundaries]] has so far
  carried DCB's *consistency rule* (dynamic query + conditional append, from
  [[pellegrini-dynamic-consistency-boundary]]) without the account of *why the selection can be wider
  than an aggregate*. Type-vs-tag orthogonality is that account: one boundary, several historic routes.
- **A live disagreement about what a tag IS.** [[martin-dilger]] treats tags as **"indices, not domain
  concepts"** — absent from Discovery models, added during Detailed Modeling before handing a slice to an
  agent ([[dilger-how-does-dcb-affect-event-modeling]]). Pellegrini treats a tag as a **domain-level
  identifier semantically tied to the business rules**, chosen from domain constraints. Both may be
  workable practice (an index whose keys happen to be domain identifiers), but they are **not the same
  claim about where tags belong in the modeling process**, and the KB should hold both rather than
  merging them. A third position exists: [[rico-fritzsche]]'s [[command-context-consistency|CCC]] calls
  tags an **optional implementation optimization** of a representation-agnostic principle
  ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]) — which is a *weaker* status than either.
- **Complements, does not replace, the concurrency work.** Pellegrini's piece is about *selection*;
  [[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche's serialized-write-order argument]] is
  about what the store must additionally guarantee at append time. Nothing here addresses that layer.
- **Implementation landscape.** The tag contract is what implementations expose: Axon Framework 5 and
  Marten 9.0 (per [[dynamic-consistency-boundaries]]), and now the brand-new Rust/Postgres
  [[klijs-skilj-rust-dcb-library|skilj]] (v0.0.1, nothing evaluated).
- Adjacent: [[event-sourcing]] · [[cqrs]] · [[domain-driven-design]] · [[event-modeling]] ·
  [[enzler-event-sourcing-aggregates-dcb-or-what|Enzler's "design the concurrency away"]] third way.

## Limits

- **No evidence of any kind.** No measurements, benchmarks, case study, or before/after — a definitional
  essay. Nothing here can be cited as showing DCB tags *work better*; only as showing what their author
  means by them.
- **NOT INDEPENDENT** on the question of whether tags are the right mechanism (see marker above).
- **"Historic route" is introduced without formal definition** and does most of the argumentative work.
  It is not a term used elsewhere in the KB's DCB material.
- The **tagging heuristic is explicitly subjective** ("whenever you believe it will be a useful grouping
  key"), so it gives no rule for deciding a contested case — exactly the "dilemma" of the title is left
  to the modeller's judgement.
- Out-of-window (2026-03), surfaced only by backfill; not a new development.

_Source: `raw/articles/pellegrini-dcb-tag-dilemma.md`._
