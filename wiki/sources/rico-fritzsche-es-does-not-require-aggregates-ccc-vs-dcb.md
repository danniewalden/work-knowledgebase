---
title: "Rico Fritzsche — Event Sourcing does not require aggregates (CCC vs DCB)"
type: source
created: 2026-06-21
updated: 2026-06-29
sources: [rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]
raw_file: [raw/notes/rico-fritzsche-event-sourcing-does-not-require-aggregates-ccc-vs-dcb.md, raw/notes/fritzsche-es-does-not-require-aggregates-ccc-vs-dcb-restatement.md]
tags: [event-sourcing, dcb, ddd, consistency, business-capabilities, focus]
---

# Rico Fritzsche — Event Sourcing does not require aggregates (CCC vs DCB)

LinkedIn post by **[[rico-fritzsche]]** (~2026-06-19; captured 2026-06-21 via logged-in Chrome).
Source file: `raw/notes/rico-fritzsche-event-sourcing-does-not-require-aggregates-ccc-vs-dcb.md`.
A fuller article is linked from the post's first comment (not captured). On the
[[event-sourcing]]/[[dynamic-consistency-boundaries|DCB]] substrate.

## What it says

Two claims, tightly argued:

1. **Event Sourcing does not require aggregates.** ES is defined by the persisted event history as the
   source of truth, with new events accepted on the basis of that history — *not* by DDD's tactical
   patterns. The familiar "rebuild an aggregate from its stream, call a method, append with the expected
   stream version" is **one coherent implementation, not the definition**; the DDD community often
   conflated the two. ES does not need the aggregate boundary — "the context can follow the decision
   rather than being constrained by a predefined object structure."

2. **CCC and DCB are the same principle at different layers — and neither is a synonym for ES.** Both
   [[autonomous-domain-capabilities|Command Context Consistency (CCC)]] and
   [[dynamic-consistency-boundaries|Dynamic Consistency Boundary (DCB)]] work the same way: a command
   defines a relevant event context, and the append is **rejected if that context changes** before the
   events are recorded. The difference is layer:
   - **CCC** defines the consistency *principle* without prescribing how the relevant context is
     represented or queried (tags/indexes are optional implementation optimizations).
   - **DCB** is a specific *event-store contract*: event types and tags form the query contract while the
     event payload stays opaque to the store, so **tags determine an event's discoverability at write
     time.**

   CCC is the conceptual guarantee; DCB is one tag-based store contract that applies it. Event Sourcing
   remains the underlying persistence concept beneath both.

## Why it matters here

This is the cleanest articulation yet of how Fritzsche's CCC relates to Pellegrini's DCB — a question the
KB had left open on both [[dynamic-consistency-boundaries]] ("how (if at all) does CCC differ
operationally from DCB") and [[autonomous-domain-capabilities]]. His answer: **same rejection principle,
different abstraction level** — CCC is representation-agnostic, DCB pins it to a tags-as-query-contract
store. It also restates the "kill the aggregate" line ([[sara-pellegrini]], and [[martin-dilger]]'s "DCB
is event sourcing done right") from the capability-ownership side: the aggregate is an implementation
choice, not part of the ES definition.

## Restated (2026-06-22)

A week later Fritzsche posted the same two claims in tighter, near-canonical wording
(`raw/notes/fritzsche-es-does-not-require-aggregates-ccc-vs-dcb-restatement.md`, captured 2026-06-29;
mirrored on his X **@codewithrico** as "Simply Event Sourcing: Aggregates Were Never Required"). New
phrasing worth keeping: the aggregate-rebuild recipe is "a coherent implementation, **not the
definition**"; "the context can **follow the decision** rather than being constrained by a predefined
object structure"; and the crisp closer — **"Both CCC and DCB address consistency in an event-sourced
system. Neither is a synonym for Event Sourcing. Event Sourcing remains the underlying persistence
concept."** No new argument, sharper formulation; folded in here rather than given its own page. See the
companion implementation-layer post [[fritzsche-ccc-atomic-append-serialized-write-order]] for *how* CCC
is enforced under concurrency.

## Caveats

LinkedIn post; the worked detail sits in an uncaptured linked article. CCC/RPU remains Fritzsche's own
coinage with no independent adoption — the CCC-vs-DCB mapping is *his* framing of the relationship, not a
neutral consensus (DCB proponents might not accept "CCC is the more general principle").

## Touches

[[rico-fritzsche]] · [[event-sourcing]] · [[dynamic-consistency-boundaries]] ·
[[autonomous-domain-capabilities]] · [[business-capabilities]] · [[domain-driven-design]] ·
[[sara-pellegrini]]

_Source: `raw/notes/rico-fritzsche-event-sourcing-does-not-require-aggregates-ccc-vs-dcb.md`._
