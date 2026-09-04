---
title: Sara Pellegrini
type: entity
created: 2026-06-14
updated: 2026-09-04
sources: [pellegrini-dynamic-consistency-boundary, pellegrini-dcb-tag-dilemma]
tags: [person, event-sourcing, dcb, ddd, substrate]
---

# Sara Pellegrini

Italian (Parma) software architect specializing in distributed architectures; originator of the
[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] concept. Author of the **"Kill
Aggregate"** series (Event Thinking blog, Apr 2023) arguing the DDD **aggregate** is the weakest,
most-misunderstood element of the method, and of the post that *named* DCB
([[pellegrini-dynamic-consistency-boundary]], May 2023). She later presented DCB together with **Milan
Savić** (AxonIQ). The idea has since been adopted by major event-sourcing frameworks (Axon Framework 5,
Marten 9.0) and is also associated with [[adam-dymitruk]].

In the KB she anchors the [[dynamic-consistency-boundaries]] concept on the [[event-sourcing]] /
[[event-modeling]] substrate (focus area as broadened 2026-06-14).

## Still publishing on DCB — the tag argument (2026-03)

[[pellegrini-dcb-tag-dilemma]] (Event Thinking, 2026-03-05) is her first substantial capture in the KB
since the naming post, and it supplies the mechanism the [[dynamic-consistency-boundaries]] page was
missing. **Type and tag are orthogonal dimensions of one fact:** the type is "the nature of the fact
itself: what happened"; a tag is **"the identifier of a historic route in the domain,"** semantically
tied to the *business rules* rather than to storage. Hence the payoff over the aggregate, in her words:
"the limitation was that **an aggregate is only one historic route**. In reality, a single decision may
advance more than one… The tags of DCB make it possible for the consistency boundaries to involve more
than one historical route." Involving types in the selection "avoids unnecessary collisions between
things that are actually irrelevant." Tags can mark actor, target, or **context** (the previous username
released by a `UsernameChanged` event, if username availability is a constraint elsewhere).

**Note where this puts her against the KB's other DCB voices.** She treats a tag as a **domain-level**
construct; [[martin-dilger]] treats tags as "indices, not domain concepts" added late in modelling; and
[[rico-fritzsche]] demotes them to an optional implementation optimization of a store-agnostic principle.
Three statuses for one construct — see the comparison table on [[dynamic-consistency-boundaries]].

**Markers:** **NOT INDEPENDENT** as corroboration that tags are the right mechanism (she originated the
concept — authoritative on intent), and the piece **contains no measurements, benchmarks or outcome
claims** at all. Also an **out-of-window backfill** (2026-03), not a new development.

_Source pages: [[pellegrini-dynamic-consistency-boundary]] · [[pellegrini-dcb-tag-dilemma]]._
