---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "Done is Done — build without touching existing code (Open-Closed); a new concept is a new slice, not an extension"
author: Martin Dilger
publication: LinkedIn (post)
published: 2026-06-18
retrieved: 2026-06-18
type: note
---

# Martin Dilger — "Done is Done" (LinkedIn, ~12h post, captured 2026-06-18)

**Capture note:** verbatim text of a public LinkedIn post (same treatment as prior Dilger LinkedIn captures). In-window (posted ~12h before capture). On the tight EM×agents focus: he models a new slice so an agent can implement it, and frames slice-vs-extension as a coupling decision.

---

One question that engineers and architects don't ask often enough:
Can I build this without touching any of the existing code that already works?

We call this principle "Done is Done."
Engineers also know this as the Open-Closed-Principle - "Open for Extension, Closed for Modification"

It means: unless you have a very compelling reason to change existing behavior, you don't.

A concrete example.

Yesterday a client asked about adding Board Invitations for Guests for the Eventmodelers Plattform.

I already had that on the radar, so I spent about 30 minutes modeling it out so an agent could implement it today - while I´m doing the workshop teaching Event Modeling. (Yes, that part still feels slightly surreal.)

My first instinct was the usual one: just reuse the existing invitation logic, add a BoardId, and extend it.
But then I stopped.

This is a live system. Customers are using it. Any change to existing flows means retesting everything, potentially dealing with migrations or upcasters in a fully event-sourced setup.

So I asked the real question again:

"Done is Done" - can I build this without touching any existing code?

Turns out: yes.

"Guest Invitations" look similar to "Invitations" at first glance, but they are actually a different concept with different rules and lifecycle. Not an extension.

A new slice. An addition to the system, not an extension.

And this is the trap we fall into far too often: we default to reuse to save a few lines of code, and end up coupling concepts that should stay separate.
The cost doesn't show up immediately. That´s the trap. It shows up later - when change gets expensive, risky, and slow.

#eventmodeling #eventsourcing

---

## Wiki relevance / links

- Ties [[open-closed-principle]] (Event Modeling's flat feature-cost curve) directly to the [[vertical-slice-architecture]] "slice" as the unit of addition, and to [[event-modeled-agent-design]] (model a slice → an agent implements it autonomously while the human teaches/reviews).
- Reinforces the coupling-over-reuse theme already in the wiki via [[dilger-event-modeling-agent-harness]] ("coupling, not context-window") and [[balanced-coupling]] / [[business-capabilities]] (a distinct concept = a distinct boundary, not an extension).
- Concrete data point on [[event-versioning-and-upcasting]]: avoiding migrations/upcasters in a live event-sourced system is the practical reason to prefer a new slice over modifying an existing flow.
- Entity: [[martin-dilger]] / [[eventmodelers-ai]].
