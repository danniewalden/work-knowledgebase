---
source_url: https://www.linkedin.com/in/ricofritzsche/recent-activity/all/
title: "Event Sourcing does not require aggregates — and CCC vs DCB"
author: Rico Fritzsche
publication: LinkedIn (Rico Fritzsche)
published: 2026-06-19
retrieved: 2026-06-21
type: note
---

(Verbatim LinkedIn post text; captured via live logged-in Chrome. "→ Link to my
full article in first comment" — a fuller Medium/blog article is linked from the
post's first comment; not captured here.)

Event Sourcing is a straightforward concept that does not rely on the tactical design patterns of Domain-Driven Design (DDD). The persisted event history serves as the source of truth, influencing the acceptance of new events based on this history.

This definition does not involve aggregates, aggregate roots, or per-aggregate event streams. Within the DDD community, a specific implementation was often confused with the definition: rebuilding an aggregate from its stream, invoking a method, and appending events using the expected stream version. While this is a coherent implementation, Event Sourcing does not necessitate this boundary. The context can follow the decision rather than being constrained by a predefined object structure.

The reality is that Event Sourcing does not require aggregates.

Additionally, it's important to clarify the concepts of Command Context Consistency (CCC) and Dynamic Consistency Boundary (DCB). Both concepts operate on the same principle: a command defines a relevant event context, and the append is rejected if that context changes before the events are recorded.

Command Context Consistency defines the consistency principle without prescribing how the relevant event context is represented or queried. Tags, indexes, or other access structures may be introduced as implementation optimizations. In contrast, DCB establishes a specific event store contract where event types and tags form the query contract, while the event data remains opaque to the store. Thus, tags determine the discoverability of the event at the time it is written.

CCC ensures consistency against the event context needed for the decision conceptually while DCB specifies a specific tag-based event store contract to apply the same principle. Both CCC and DCB address consistency in an event-sourced system. Neither is a synonym for Event Sourcing. Event Sourcing remains the underlying persistence concept.
