---
title: Conway's Law
type: concept
created: 2026-06-13
updated: 2026-07-31
sources: [eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, coupling-research-note, skelton-team-topologies-foundation-ai-roi]
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

## The homomorphic force — why software boundaries are also team boundaries

Allan Kelly's framing of Conway's Law as a **homomorphic force** (team-communication structure and
software architecture tend to assume the *same shape*) carries a consequence the [[coupling-research-note]]
leans on: **edge weights on a software-boundary graph are also, implicitly, a model of team-coordination
friction** — even when the editor is thinking purely about software seams. This is *why* boundaries on a
user-needs map are **interpretive** (team / system / domain / make-buy can be read off the same
partition). It also explains why [[team-topologies]] — a *team*-shaped lens — bears on what is nominally a
software-boundary tool, while still being a partition-side constraint rather than an edge weight.

## Agent-era reading — value-flow team boundaries scope agents (Skelton, 2026)

[[matthew-skelton]] extends the homomorphic force into the AI era
([[skelton-team-topologies-foundation-ai-roi]]): a **stream-aligned team organized around a continuous
flow of value** doubles as an **agent boundary** — an end-to-end team gives autonomous agents "clear
objectives and anchoring points … to understand what to build and how." The Conway shape (team
communication structure ↔ software architecture) now also scopes *which agent owns what*. This is the
organization-side twin of [[john-devadoss|deVadoss's]] architecture-side "capability before agent"
([[devadoss-cead-capability-aligned-agent-design]]), and it reinforces the KB's existing move of giving
each agent its own [[event-modeling]] swimlane ([[event-modeled-agent-design]]).

## Related

[[event-modeling]] · [[domain-driven-design]] · [[business-capabilities]] (teams own capabilities;
the swimlane boundary) · [[event-modeled-agent-design]] · [[team-topologies]] · [[coupling-taxonomy]] ·
[[balanced-coupling]] · [[matthew-skelton]] · [[devadoss-cead-capability-aligned-agent-design]]

_Sources: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] ·
[[coupling-research-note]] · [[skelton-team-topologies-foundation-ai-roi]]._
