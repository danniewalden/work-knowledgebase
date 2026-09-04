---
title: "Fritzsche — An atomic append isn't enough; CCC needs a protected write order"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [fritzsche-ccc-atomic-append-serialized-write-order]
raw_file: [raw/notes/fritzsche-ccc-atomic-append-vs-serialized-write-order.md]
tags: [event-sourcing, dcb, consistency, postgresql, business-capabilities, focus]
---

# Fritzsche — An atomic append isn't enough; CCC needs a protected write order

LinkedIn post by **[[rico-fritzsche]]** (~2026-06-23; captured 2026-06-29 via logged-in Chrome).
Source file: `raw/notes/fritzsche-ccc-atomic-append-vs-serialized-write-order.md`. A fuller article is
linked in the post's first comment (not captured). Tagged `#EventSourcing #SoftwareArchitecture
#PostgreSQL #SystemDesign`. The **implementation layer** beneath
[[autonomous-domain-capabilities|Command Context Consistency]] and [[dynamic-consistency-boundaries|DCB]].

## What it says

The headline claim: **an atomic conditional append can still let two incompatible decisions through.**
The concrete scenario, in PostgreSQL:

- Two commands evaluate the **same Event Query** almost simultaneously, observe the same command context
  and **context version**, reach identical decisions, and call the conditional append with the same
  expected version.
- A PostgreSQL **CTE** that combines the Event-Query check with the insert makes each append *atomic* —
  but under **READ COMMITTED** it establishes **no order** between the two concurrent executions. Both
  statements evaluate against the same committed history before either commits, so **both checks pass and
  both events are recorded.**
- Therefore: to achieve **Command Context Consistency**, atomic statements are not enough — a **protected
  write order (serialization)** is essential. Only once writes are ordered can the store re-evaluate the
  same Event Query, compare the current context version against the expected one, and decide to record or
  reject.
- A straightforward implementation: **lock a single metadata row** at the start of each append
  transaction. This **serializes the physical writes globally** while the **conflict decision stays
  local** to the command context. Example: registrations for *alice* and *bob* both succeed after
  waiting, but two concurrent *alice* registrations cannot.
- The takeaway is a **contract**, not a lock: "the lock itself is merely an implementation detail; the
  critical aspect is the contract the event store provides. **Atomicity safeguards one append;
  serialization prevents two decisions made from the same observed command context from being
  accepted.**"

## Why it matters here

The KB's [[dynamic-consistency-boundaries]] / [[autonomous-domain-capabilities]] pages describe DCB/CCC
as an *optimistic lock* ("append iff the relevant input stream is unchanged") but never pinned down what
that requires from the store under real concurrency. This is the missing **implementation contract**:
optimistic-version checking alone is insufficient under READ COMMITTED; you need a serialized write order
(e.g. a metadata-row lock) so the re-evaluation is meaningful. It's the operational counterpart to his
conceptual CCC-vs-DCB mapping ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]) — and useful
context for the [[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object]] walkthrough's
"advisory-lock serialization" note, which it now explains.

## Caveats

LinkedIn post; the worked code/article (first comment) is uncaptured. PostgreSQL-specific; the
"metadata-row lock" is one implementation. Fritzsche's own CCC vocabulary, no independent adoption.

## Touches

[[rico-fritzsche]] · [[dynamic-consistency-boundaries]] · [[autonomous-domain-capabilities]] ·
[[event-sourcing]] · [[cqrs]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]]

_Source: `raw/notes/fritzsche-ccc-atomic-append-vs-serialized-write-order.md`._
