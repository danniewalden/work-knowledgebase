---
source_url: https://www.linkedin.com/in/goeleven/recent-activity/all/
title: "Event sourcing does not deliver auditing 'for free'"
author: Yves Goeleven
publication: LinkedIn
published: 2026-04-14
retrieved: 2026-06-14
type: article
---

# Event sourcing does not deliver auditing "for free"

**Yves Goeleven** ("I help software engineering teams get better at delivering value"; NServiceBus
core team; creator of MessageHandler.net & ClubManagement.io) — *LinkedIn feed post, ~2 months ago
(≈April 2026). Captured via logged-in Chrome session as part of a deeper-than-14-day people backfill
(Yves posts infrequently). Attached image: "Event Sourcing ≠ [Auditing]".*

---

It's a common misconception that event sourcing delivers auditing "for free".

This is not the case.

But it does offer a great starting point for auditing though.

When practicing event sourcing, you are forced to store decisions to change, and all related data, as
individual events before actually applying these changes to the system.

This ensures every decision is stored on a log already, which is a great start.

However, the decision log needs to be augmented with additional context before it qualifies as an
audit log.

This context includes:
- Who made (the request for) the decision
- When was the decision made
- Where was it made
- What the decision was
- And why it was made (both causation and correlation)

Once all this context is captured, on every event, you have an audit log.

If you design the same way I do, around business capabilities, then each stream in this log
represents the full audit of the business process used to realize said capability.
