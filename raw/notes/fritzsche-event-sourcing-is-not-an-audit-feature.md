---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7500092512603201537/
title: "Anyone who thinks Event Sourcing is an audit feature has misunderstood its purpose."
author: Rico Fritzsche
publication: LinkedIn
published: 2026-08-31
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  PRACTITIONER POSITION, not measurement ("In my experience", "For me, the real motivation").
  Links his own article on avoiding a centralized database schema.
---

Anyone who thinks Event Sourcing is an audit feature has misunderstood its purpose.

In my experience, the use of event sourcing is often justified on the grounds that it provides a complete history. Conversely, it is argued that event sourcing would not be necessary if a history were not needed.

I consider this to be fundamentally wrong.

Why? Because the fact that the history is preserved is a consequence of that very property, but it is not the reason for it.

For me, the real motivation is to provide domain capabilities that are independent of one another and not tied to a central, shared data structure. At the same time, this avoids entity-oriented thinking.

By using events, the domain language is brought to the forefront, and the actual processes become apparent.

In my latest article, I discuss the advantages of not being tied to a centralized database schema. The problem with entity-centric thinking is less of a technical nature.

https://lnkd.in/eRqNcKDd

#eventsourcing #softwareengineering
