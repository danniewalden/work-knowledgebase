---
source_url: https://sara.event-thinking.io/2026/03/the-dcb-tag-dilemma.html
title: "The DCB Tag Dilemma"
author: Sara Pellegrini
publication: Event Thinking (blog)
published: 2026-03-05
retrieved: 2026-09-04
type: article
capture_note: Out-of-window backfill (2026-03) filed on the 2026-09-04 sweep — a
  recency-bounded watch cannot reach it. Retrieved via WebFetch and transcribed verbatim;
  site nav, sidebar, footer and share/comment widgets stripped, the single lead image noted
  inline as [image: ...]. Full body present from title to closing "Want to learn more?" line;
  no portion missing or truncated. Byline and date are as the page states (Sara Pellegrini,
  March 5, 2026); source_url is the canonical post URL as observed, not reconstructed.
  Pellegrini ORIGINATED the Dynamic Consistency Boundary (see
  raw/articles/pellegrini-dynamic-consistency-boundary.md, her 2023 naming post), so this is
  the concept's author defining her own terms — authoritative on intent, and NOT INDEPENDENT
  as corroboration that DCB tags are the right mechanism. The piece is conceptual definition
  throughout: it contains no measurements, benchmarks or claims of outcome.
---

# The DCB Tag Dilemma

[image: The "crazy wall" in the 2001 film *A Beautiful Mind*]

DCB introduces tags as a consistency mechanism to identify the events required to enforce the consistency constraints. Along with the event type, tags are one of the two key attributes you can use to filter events relevant to a specific decision.

Type and tag describe two different sides of the same event—two complementary dimensions. Used together, they let you define very precisely which events you need to consider to make a particular decision.

Let's unpack what each dimension means.

## Event type: what happened

An event's type describes the nature of the fact itself: what happened.

"StudentSubscribedToCourse" is a typical event type. It doesn't tell you who was involved or provide any context. It only conveys the kind of thing that occurred, describing the fact without tying it to the specific entities involved.

The type is also semantically tied to the business logic used to process the event. It's easy to see why: events of the same type are generally handled by the same business logic.

## Tag: who/what was involved

A tag is the identifier of a historic route in the domain.

Tags are semantically tied to the business rules, which guide the domain's historic routes in the right direction, with consistency boundaries preventing them from going astray.

The same meaning of consistency boundary was the core of the aggregate itself. The limitation was that an aggregate is only one historic route. In reality, a single decision may advance more than one historic route. The tags of DCB make it possible for the consistency boundaries to involve more than one historical route. Involving types in the selections avoids unnecessary collisions between things that are actually irrelevant.

A tag is orthogonal to the type. It identifies the elements involved in the specific occurrence—whether they are active actors, passive objects, or even contextual details.

A tag captures a shared property across a set of facts. All events that share the same tag involve the same domain element. That domain element might be a concrete entity, or something more abstract.

### Examples

The actor who performed the action is typically represented by a tag.

In the student enrollment example, the student ID is a tag that marks the student's involvement in the event.

Likewise, the course—as the target of the enrollment action—is also involved, and should be captured via a tag.

Context can also be tagged.

Consider a username change use case. An event of type "UsernameChanged" obviously involves the user who changed it and the new username. But there is another contextual piece of information which could be important to tag: the previous username that was released. Whether you should tag the released username depends on your domain constraints. For example, if the username's state—taken vs available—matters when validating another user's claim on that username, then it should be a tag.

### In one sentence

For brevity (and with some loss of completeness), you can summarise the idea like this:

An event's type tells you what kind of thing happened; the tags tell you which historic routes were advanced by the event.

In the end, add a tag whenever you believe it will be a useful grouping key for protecting the consistency of your business model.

Want to learn more?
If you're curious about tags, you can dive deeper here: https://dcb.events/topics/tags
