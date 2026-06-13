---
title: Conway's Law
type: concept
created: 2026-06-13
updated: 2026-06-13
sources: [eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling]
tags: [software-design, organization, event-modeling]
---

# Conway's Law

**Conway's Law** (Melvin Conway, 1967): organizations design systems that **mirror their
own communication structure**. The shape of the software ends up matching the shape of the
teams that build it.

## Why it matters in this wiki

Conway's Law is invoked at a specific step of the [[event-modeling]] workshop: after the
timeline of events, commands, and views is laid out, **step 6 applies Conway's Law to draw
swimlanes** — partitioning the model along the boundaries of the teams (or systems) that
will own each part ([[eventmodeling-what-is-event-modeling]]). Swimlanes are where Event
Modeling expresses organizational structure on the same canvas as the system design, which
is also how it surfaces [[domain-driven-design]] boundaries
([[semaphore-dymitruk-event-modeling]]).

This connects to the agent-design thread: in [[event-modeled-agent-design]], giving each
agent its own swimlane is the Conway's-Law move — aligning an autonomous component's scope
with a team-or-ownership boundary, the same way [[openai-harness-engineering-codex]] scopes
agent rules to subdirectories.

## Related

[[event-modeling]] · [[domain-driven-design]] · [[event-modeled-agent-design]]

_Sources: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]]._
