---
title: "Source: Dymitruk — Event Modeling Is Future Proof (agents as users/processors)"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [dymitruk-event-modeling-future-proof-agents]
tags: [event-modeling, agentic-ai, multi-agent, primary-source]
---

# Source: Dymitruk — Event Modeling Is Future Proof (agents as users/processors)

A short, primary statement by [[adam-dymitruk]] (creator of [[event-modeling]]) on X, dated
2025-05-31. The first **on-target** evidence in the KB that the *method* (not just event sourcing)
is meant to describe agent systems. Raw capture (verbatim):
`raw/notes/dymitruk-event-modeling-future-proof-agents.md`.

## Summary

Dymitruk's claim, in full: *"Event Modeling is future proof. #AI did not disrupt it. Since
automation was built into the methodology from the start, agents can be described as either users or
specific processors. You can combine that to show how a multi-agent system would work without
throwing away your existing system design."*

## Key points

- **No new notation needed.** Because [[event-modeling]] already has an **Automation** pattern (a
  processor that works a "todo list," issues commands, and stores replies as events), AI agents slot
  into the existing model.
- **Two roles for an agent:** a **user** (an actor in a swimlane, issuing commands like a human) or
  a **processor** (the Automation pattern). A multi-agent system is just several of these composed.
- **Continuity over disruption:** existing event models / event-sourced systems don't need to be
  thrown away to incorporate agents.
- It's a single social post (with an attached diagram image, no linked essay) — assertion, not a
  worked example. Treat as a directional primary source; a fuller written treatment is still wanted.

## Connections / contrast

Partially closes the "Open edge" flagged on [[event-sourced-agentic-patterns]] and in
[[overview]] — previously *no* ingested source connected [[event-modeling]] to agents. Grounds the
new synthesis page [[event-modeled-agent-design]]. The "agent as processor" mapping aligns with the
KB's harness thread, where the Automation pattern resembles the initializer-executor /
[[ralph-loop]] working a feature list ([[anthropic-effective-harnesses-long-running-agents]]) and
the [[unattended-coding-agents]] pattern. Contrast with [[qlerify-event-modeling-tool-ai]], which
runs the relationship the other way (AI *assists* Event Modeling).

_Source page: [[dymitruk-event-modeling-future-proof-agents]]._
