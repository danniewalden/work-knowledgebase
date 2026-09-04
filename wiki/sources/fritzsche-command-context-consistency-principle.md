---
title: "Fritzsche — The Command Context Consistency Principle"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-command-context-consistency-principle]
raw_file: [raw/articles/fritzsche-command-context-consistency-principle.md]
tags: [command-context-consistency, dynamic-consistency-boundaries, event-sourcing, aggregates, autonomous-domain-capabilities, focus, substrate]
---

# Fritzsche — The Command Context Consistency Principle

Blog article by **[[rico-fritzsche]]** (ricofritzsche.me, 2026-07-26). The **definitive canonical
[[command-context-consistency|CCC]] primary** the KB had been citing only through fragments
([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]],
[[fritzsche-ccc-atomic-append-serialized-write-order]]). Raw:
`raw/articles/fritzsche-command-context-consistency-principle.md`.

## The principle

**"Record the outcome of a command only while the facts the decision is based on still hold."** That one
sentence mentions no store — it fixes what must be true at commit and says nothing about how to check it.
The aggregate is the wrong unit for consistency: the boundary belongs to **the facts a command's
decision reads**, and that set changes from one command to the next.

## The argument

- **The aggregate is a *static* consistency boundary.** DDD (Evans → Vernon's "one aggregate per
  transaction") fixes one boundary per aggregate, enforced whole: a relational version column, or one
  event stream's expected sequence number. A command reading 3 facts and one reading 15 are validated
  against the *same* version. So one boundary is **too large** (two commands editing different parts of a
  reservation falsely conflict) *and* **too small** (the "one booking per listing-night" invariant lives
  across reservations, outside any single aggregate).
- **The command shapes its context.** A command expresses an intention; the app reads the relevant
  **facts** (a fact = a true statement about state/causality bound to its moment). The intent selects
  which facts matter; the context is read **once** as an immutable snapshot; `decide` uses only the
  command + snapshot → same command over same facts = same outcome. A decision is valid **only for the
  facts it was made from**; if a commit supersedes one before the write, the outcome must not be recorded.
  Fixed shape: **read → decide → record**, where record carries the condition.
- **Store-agnostic enforcement.** Ralf Westphal coined the name; Fritzsche set out the same rule in
  *Aggregateless Event Sourcing*; [[sara-pellegrini|Pellegrini's]] [[dynamic-consistency-boundaries|DCB]]
  is "an optimistic lock specific for event-sourcing." All three speak event-store language — **the
  principle doesn't.** An event store checks with a **conditional append over a query**; a relational DB
  with **locks + constraints**. Only the mechanism differs.
- **Guard the whole context, never less.** The logical context (facts `decide` read that a commit can
  supersede) must equal the physical guard (row/version/predicate/unique-constraint/tag-set/stream
  position). A **narrower** guard lets a fact change unseen → wrong commit; a **wider** guard (an
  aggregate version) is correct but resurrects false conflict/contention. Only *mutable facts whose
  continued validity matters* belong in the guard — a captured timestamp, a generated id, or a Provider's
  result is an input, not something to hold still.
- **Worked mechanics.** Relational: `UPDATE … WHERE guest_count=$3 AND status=$4` (the WHERE *is* the
  guard under READ COMMITTED); `INSERT` + `UNIQUE(listing_id, night)` guards the *absence* of a row;
  `FOR SHARE` (in a fixed lock order) holds read-only rows. Event store: a **context query** returns the
  context + its version (highest matching sequence no.), then `AppendIf(newEvents, query, expectedVersion)`
  — a non-matching committed event doesn't move the version, so unrelated commands commit side by side.
- **A failed guard is a business situation, not a technical error.** Zero rows / failed append / unique
  violation / serialization failure → the capability's **RPU** rolls back, reloads context, re-runs
  `decide` (may now accept or reject), or maps the conflict to a domain outcome (a claimed night →
  `ListingUnavailable`).

## Why it matters here

- Gives [[command-context-consistency]] its own canonical page and the DCB debate its cleanest
  resolution: **CCC is the representation-agnostic principle; DCB is its tag-based event-store form; the
  aggregate is the "Static Consistency Boundary."** Ties [[dynamic-consistency-boundaries]],
  [[event-sourcing]], [[autonomous-domain-capabilities]] (the RPU carries the context into the commit
  condition), and [[given-when-then]] (the GWT GIVEN ≈ the context/read-set, cf.
  [[dilger-how-does-dcb-affect-event-modeling]]).
- Caveat: single-author practitioner primary; converges with Westphal + Pellegrini but no external
  benchmark.

## Links

Entities: [[rico-fritzsche]], [[ralf-westphal]], [[sara-pellegrini]]. Concepts:
[[command-context-consistency]], [[dynamic-consistency-boundaries]], [[event-sourcing]],
[[autonomous-domain-capabilities]], [[vertical-slice-architecture]], [[given-when-then]].
Related sources: [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]],
[[fritzsche-ccc-atomic-append-serialized-write-order]], [[pellegrini-dynamic-consistency-boundary]],
[[dilger-dcb-is-what-event-sourcing-should-have-been]].

_Raw source: `raw/articles/fritzsche-command-context-consistency-principle.md`._
