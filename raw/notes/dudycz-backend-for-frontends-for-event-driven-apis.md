---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7499184417773625344/
title: "Backend for frontends... why don't we do the same for other types of APIs? For instance, an event-driven API?"
author: Oskar Dudycz
publication: LinkedIn
published: 2026-08-29
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  Part of his #EventDrivenDiary LinkedIn series. PRACTITIONER ARGUMENT drawn from "my past
  projects, in my client work" - experience report, not measurement. Cites Gregor Hohpe for
  the events/commands/state message split.
---

Backend for frontends is a common way to satisfy the different needs of Web API users. We learned that a uniform API can be a good thing if our API is our product, or if it's generic enough that we can dictate its form. We also learned that it's worth having a discussion between backend and frontend needs and meeting somewhere in the middle.

Yet why do we limit that to only the Web API? Why don't we do the same for other types of APIs? For instance, an event-driven API?

The common motive I see (in my past projects, in my client work, etc.) is that people try to satisfy totally different customer needs by publishing uniform events. What's worse, those events aren't actually events; most of the time, they're just state notifications: SthSthCreated, SthSthUpdated, SthSthDeleted.

I'm calling them: Poor Man's replication through the queue.

Ok, so what can be the split for our messaging?

For instance, split for internal and external events:
- internal (also called private, or domain) are those that are meaningful inside the module context. They're typically smaller and more focused, as internally we know our domain.
- external (also called public or integration) are those that are meaningful in the whole system context. They're close to pivotal events from EventStorming or Summary Events I described in the previous #EventDrivenDiary

What else should we consider? That our messages are not only events, but also commands and state (as Gregor Hohpe calls it).

This is an important split, as:
- state change just tells us what has changed; consumers won't know why this state changed or what has happened. This is useful for the data sync between modules mentioned earlier,
- commands represent the intention to perform a certain business operation; they're directed, not broadcast as events. They can also be rejected. If we mistake them for events, we end up with passive-aggressive communication, which can lead to dropped communication if we accidentally throw an error.

We shouldn't lie to ourselves about our intentions, as that ends badly.

If we broadcast all internal events, we create a leaking abstraction and a spider web of dependencies.

If we broadcast events while ignoring other message types, our communication looks like parliament: a room filled with shouting people. This is a first step to a distributed monolith.

Do we want our communication to look like that?
