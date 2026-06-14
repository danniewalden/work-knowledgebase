---
source_url: https://www.linkedin.com/posts/goeleven_i-use-event-modeling-to-visualize-business-activity-7125089090164662273-3L6B
title: "I use Event Modeling to visualize business processes (even when manual)"
author: Yves Goeleven
publication: LinkedIn
published: 2023-10-24
retrieved: 2026-06-14
type: article
---

# I use Event Modeling to visualize business processes — even when they are performed manually

**Yves Goeleven** — *LinkedIn post (2023). Part of the run-up to his "translate an event model into
code" mini-series. Captured via logged-in Chrome.*

---

I use Event Modeling to visualize business processes. Even when they are performed manually!

Many people seem to believe Event Modeling is a tool to visualize how Event Sourced software works.
But that is the wrong way to think about it. It is an excellent tool to visualize the implementation
of the business processes, in an organization, even when those processes are NOT automated through
software (yet).

At the top of the drawing, you can find a swimlane for each role involved in the business process.
Inside these swimlanes you can draw any interaction point that this role has with the organization /
system. Next to screens, this included any paper documents they need to fill out, pdf files that get
emailed to them, dollar bills that are exchanged in cash... and excel files used in the process.

At the bottom of the drawing, you can find a swimlane for each business capability leveraged during
the process. Business capabilities offer the long term stable boundaries within which part of the
business process gets performed. Each organization will realize a business capability in a different
way. Certain business decisions will be taken to progress the state of this section of the process.
Record these decisions as events inside the capability swimlane. Record it there even when the
decision is taken in the mind of an authorized person in the organization. Different roles in the
organization may have the authority to take this decision on behalf of the organization. Ownership of
the decision belongs to the (capability of) the organization, not to the individual.

In between the swimlanes you draw the information exchanged between the humans and the capabilities of
the organization. Humans typically send their intent to the capabilities of the organization, this
intent is represented by commands. A purchase order document on paper, or an HTTP POST containing the
purchase order details, are equivalent from a process perspective. The booking process will decide if
the intent can be fulfilled or not. The organization will report back to the humans by showing the
current state of the things they care about. This state can take many different shapes, all derived
from the same decisions taken during the realization of the business capability.

Once you understand the flow of the business process, you can turn sections of it into software...

---

*Notable comment exchange — Dannie Walden asked what the "big black dot" notation means (used on read
models not connected to events). Yves Goeleven: "It means the state has to be rebuilt from the
complete history and not just the last event." Adam Dymitruk commented that the strength is how much
other diagrams/methodologies it makes redundant — "everyone on the same page so much sooner."*
