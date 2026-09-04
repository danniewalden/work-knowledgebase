---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "Event Sourcing does not require aggregates; CCC vs DCB clarified"
author: Rico Fritzsche
publication: LinkedIn (post)
published: 2026-06-22
retrieved: 2026-06-29
type: note
---

(Verbatim capture of a Rico Fritzsche LinkedIn post, ~1w old when retrieved on
2026-06-29, pulled via logged-in Chrome. Full article linked in his first
comment / mirrored on his X @codewithrico Jun-22 ("Simply Event Sourcing:
Aggregates Were Never Required") — NOT captured here. NOTE: this is a tighter
restatement of the same thesis already captured in
[[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]] (from his ~Jun-19
post); kept for the sharpened CCC-vs-DCB wording. See also
[[dynamic-consistency-boundaries]] and [[fritzsche-ccc-atomic-append-vs-serialized-write-order]].)

Event Sourcing is a straightforward concept that does not rely on the tactical design patterns of Domain-Driven Design (DDD). The persisted event history serves as the source of truth, influencing the acceptance of new events based on this history.

This definition does not involve aggregates, aggregate roots, or per-aggregate event streams. Within the DDD community, a specific implementation was often confused with the definition: rebuilding an aggregate from its stream, invoking a method, and appending events using the expected stream version. While this is a coherent implementation, Event Sourcing does not necessitate this boundary. The context can follow the decision rather than being constrained by a predefined object structure.

The reality is that Event Sourcing does not require aggregates.

Additionally, it's important to clarify the concepts of Command Context Consistency (CCC) and Dynamic Consistency Boundary (DCB). Both concepts operate on the same principle: a command defines a relevant event context, and the append is rejected if that context changes before the events are recorded.

Command Context Consistency defines the consistency principle without prescribing how the relevant event context is represented or queried. Tags, indexes, or other access structures may be introduced as implementation optimizations. In contrast, DCB establishes a specific event store contract where event types and tags form the query contract, while the event data remains opaque to the store. Thus, tags determine the discoverability of the event at the time it is written.

CCC ensures consistency against the event context needed for the decision conceptually while DCB specifies a specific tag-based event store contract to apply the same principle. Both CCC and DCB address consistency in an event-sourced system. Neither is a synonym for Event Sourcing. Event Sourcing remains the underlying persistence concept.

→ Link to my full article in first comment
