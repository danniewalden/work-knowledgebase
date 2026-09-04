---
title: Command Context Consistency
type: concept
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-command-context-consistency-principle, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, fritzsche-why-your-software-cannot-explain-business-decisions, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, fritzsche-ccc-atomic-append-serialized-write-order]
tags: [command-context-consistency, dynamic-consistency-boundaries, event-sourcing, aggregates, autonomous-domain-capabilities, substrate, focus]
---

# Command Context Consistency

**CCC:** *record the outcome of a command only while the facts the decision is based on still hold.* A
store-agnostic consistency principle that replaces the fixed aggregate with a boundary **the command
draws for itself** — the set of facts its `decide` step read. Named by **[[ralf-westphal]]**, developed
independently by **[[rico-fritzsche]]** (out of *Aggregateless Event Sourcing*), and the same rule
[[sara-pellegrini|Pellegrini]] expresses for event stores as the
[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]]. Canonical primary:
[[fritzsche-command-context-consistency-principle]].

## The principle

A command expresses an intention; the application reads the **relevant facts** (a *fact* = a true
statement about state/causality bound to its moment) as an immutable **context snapshot**, read **once**.
`decide` uses only the command + snapshot, so the same command over the same facts yields the same
outcome. A decision is valid **only for the facts it was made from**: if another commit supersedes one
before the write, the outcome must **not** be recorded. Fixed shape: **read → decide → record**, where
`record` carries the condition.

## Why the aggregate is the wrong unit

The aggregate is a **Static Consistency Boundary** — fixed once, enforced whole (a relational version
column, or one event stream's expected sequence). It is simultaneously:

- **too large** — two commands editing different parts of one reservation (guest count vs. check-in date)
  falsely conflict on the shared version; and
- **too small** — the "one active reservation per listing-night" invariant lives *across* reservations,
  outside any single aggregate.

CCC guards exactly the facts each command reads, so unrelated commands commit side by side and only real
conflicts (two bookings of the same night) are refused.

## Store-agnostic enforcement — the logical/physical match

The principle names no store. Enforcement matches a **logical context** (facts `decide` read that a
commit can supersede) to a **physical guard**, which must **cover the context and never less**:

- **Relational** — a conditional `UPDATE … WHERE <facts unchanged>`, `FOR SHARE` on read-only rows (fixed
  lock order), and a `UNIQUE` constraint to guard the *absence* of a row.
- **Event store** — a **context query** returns the context + its version; a **conditional append**
  (`AppendIf(events, query, expectedVersion)`) commits only while the version is unchanged. The
  [[dynamic-consistency-boundaries|DCB]] is this guard in **tag-based** form.

A guard **narrower** than the context lets a fact change unseen (wrong commit); **wider** (an aggregate
version) is correct but resurrects false conflict. Only *mutable facts whose continued validity matters*
belong in the guard — a captured timestamp, a generated id, or a Provider's result is an input, not
something to hold still ([[fritzsche-ccc-atomic-append-serialized-write-order|and the append must be
serialized]], not merely atomic).

## Where it sits in the KB

- **CCC vs DCB vs aggregate:** CCC is the **representation-agnostic principle**; DCB is its **tag-based
  event-store contract**; the aggregate is the **static** boundary CCC retires
  ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]],
  [[dilger-dcb-is-what-event-sourcing-should-have-been]]). Event Sourcing is *one* enforcement option,
  not a requirement.
- **Capabilities:** the owning capability's **RPU** carries the context into the commit condition and
  maps a guard conflict to a **business outcome** (a claimed night → `ListingUnavailable`), not a
  technical error ([[autonomous-domain-capabilities]], [[business-capabilities]]).
- **Event Modeling seam:** the read-set a handler needs ≈ the [[given-when-then|GWT]] **GIVEN**, from
  which a build kit can generate the criteria query + tests ([[dilger-how-does-dcb-affect-event-modeling]]).
- **Explainability:** the visible command→context→decide→outcome path is what lets software *explain* a
  decision ([[fritzsche-why-your-software-cannot-explain-business-decisions]], [[agent-explainability]]).
- **Shared rules:** invariants are enforced *at commit*, not by a shared helper
  ([[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]]).

Caveat: heavily practitioner-authored (Fritzsche/Westphal/Pellegrini); strong internal convergence, no
external benchmark.

_Source pages: [[fritzsche-command-context-consistency-principle]] · [[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] · [[fritzsche-ccc-atomic-append-serialized-write-order]] · [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] · [[fritzsche-why-your-software-cannot-explain-business-decisions]]._
