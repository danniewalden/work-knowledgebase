---
source_url: https://sara.event-thinking.io/2023/05/dynamic-consistency-boundary.html
title: "A name for an idea: Dynamic Consistency Boundary"
author: Sara Pellegrini
publication: Event Thinking (blog)
published: 2023-05-15
retrieved: 2026-06-14
type: article
---

# A name for an idea: Dynamic Consistency Boundary

*Foundational/seed capture (origin of the DCB concept) — filed 2026-06-14 to ground the new
`dynamic-consistency-boundaries` wiki concept after Dannie broadened the focus. Not a "new this week"
watch item.*

Sometimes the best way to promote your idea is to give it a proper name. That's what some weeks ago,
@nicolaibaaring suggested I do. [Nicolai Baaring, Apr 8 2023: "Interesting concept. I feel this concept
should have a name of its own to make it easier to communicate and define. Do you have anything in
mind?"] After some time needed to find the best name for the concept, here we are, finally, talking
about **Dynamic Consistency Boundary!** - thank @RobertBaelde, for your suggestion - [Robert Baelde,
Apr 9 2023: "Maybe something in the direction of multi-stream event sourcing? Or dynamic consistency
boundaries? Also get a sense of event sourced transaction script with this concept…"]

I want to use this blog post to summarize, in easy terms, what *Dynamic Consistency Boundary* means,
in its most generic form.

*Dynamic Consistency Boundary* represents a form of **optimistic lock** specific for event sourcing
based systems.

The idea behind it is pretty simple.

While using event sourcing, any decision could be represented by a function that receives as input an
ordered stream of events and produces as output an additional ordered stream of events.

The input stream represents the given, the past events important for making the decision. The output
stream represents the future, the evolution of the state that my decision causes.

Any system that allows concurrent write operations, must admit the possibility that, in between the
loading of the input event stream and the appending of the output event stream, another append could
take place, which could potentially invalidate the decision made.

In order to guarantee the decision's consistency, **the output event stream must be appended if and
only if the input event stream at the time of the append is exactly the same as it was at the loading
time**. In other words, nothing relevant happened to influence the decision.

That's why the component responsible for loading the event stream relevant for making the proper
decision is also responsible for verifying that this event stream is still the same at the moment of
appending the decision outcome. In other words, it should perform the following operations:

1. dynamically retrieve the event stream relevant to the decision,
2. invoke the correct decision function, passing the relevant event stream as input,
3. guarantee consistency, appending conditionally the output event stream if and only if the event
   stream relevant for the decision, at the time of the append, corresponds to the one passed as an
   input to the decision function.

In order to support the Dynamic Consistency Boundary approach, an event store should provide the
following capabilities:

- dynamic query - read event stream based on specific criteria
- conditional append - write events only if a query result matches the expected one

The immutable nature of the event store makes the conditional append simple. Given a query, it is
sufficient to verify that the last event matches, to be sure that the whole stream matches.

There are many other details that I could provide. But I want to keep the concept as simple as
possible. And most of all, detached from any specific implementation. If you need more concrete
examples, please read the other post from the "Kill Aggregate" series.

*Labels: domain driven design, dynamic consistency boundary, event sourcing, kill aggregate,
optimistic lock. Author: Sara Pellegrini (Parma, Italy) — specializes in distributed architectures.
Origin context: the DCB concept comes out of her "Kill Aggregate" series (event-thinking.io, Apr 2023),
later presented with Milan Savić.*
