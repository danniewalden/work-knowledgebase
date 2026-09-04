---
title: "Nick Tune — Graphs + Memory + Skills + Agents"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [nick-tune-graphs-memory-skills-agents]
raw_file: [raw/articles/nick-tune-graphs-memory-skills-agents.md]
tags: [context-engineering, agent-harness, agentic-ai, knowledge-graph, focus]
---

# Nick Tune — Graphs + Memory + Skills + Agents

LinkedIn feed post by **[[nick-tune]]** (2026-06-12, captured via logged-in Chrome). Raw capture:
`raw/articles/nick-tune-graphs-memory-skills-agents.md`. Reshares a carousel from a PayFit "Monthly AI
Day — Context Engineering for AI-Native …" talk by **Stéphane Jourdan** (Anyshift.io).

## Summary

The post advances a **four-layer model of "what you build underneath an agent"** — the substrate that
has to exist *before* "reason, act, learn" means anything:

1. **Graph** — the world model: *what exists, and how it connects.*
2. **Memory** — continuity: *what was true Tuesday at 3am, and what changed.*
3. **Skills** — encoded judgment the agent can run; *the hands.*
4. **Agent** — the loop that ties the three together to reach a goal.

The slide's thesis: *"A good agent is mostly good context engineering. The model is the commodity. The
context is the product"* — and "not more data: the edges." Tune's own gloss makes the **graph** point
concrete: an agent *grepping around* a codebase/system is a poor substitute for a queryable **graph of
the system** that can return current and historical state — for diagnosing production issues or
**anticipating the blast radius of a change**. He concludes the four blocks "are the key building
blocks we are all going to be using."

## In the KB

This is an independent, vendor-neutral restatement of **[[context-engineering]]** as the real product
("the model is the commodity"), corroborating the harness-thread claim that a harness is "largely a
delivery mechanism for good context engineering" ([[langchain-anatomy-of-an-agent-harness]],
[[fowler-bockeler-harness-engineering]]). Two threads connect tightly:

- **Memory = an append-only history you can query at a point in time** ("what was true Tuesday at 3am,
  and what changed") is **[[event-sourcing]]** described in agent-substrate language — the same instinct
  the KB tracks in [[event-sourced-agentic-patterns]] and Akka's event-sourced agent memory
  ([[akka-event-sourcing-backbone-agentic-ai]]).
- **"Blast radius of a change"** is the coupling/cohesion concern at the heart of
  [[business-capabilities]] (capabilities give an agent a contracted blast-radius) and
  [[agent-legibility]] ("what the agent can't see doesn't exist") — Tune wants that legibility delivered
  as a **system graph**, not ad-hoc grepping.

Caveat: it's a short feed post amplifying someone else's slide (Jourdan/Anyshift), not an original
worked method — useful as a crisp framing and a corroborating outside voice, not as evidence.

## Links

Entities: [[nick-tune]]. Concepts: [[context-engineering]], [[agent-harness]], [[agent-legibility]],
[[event-sourcing]], [[business-capabilities]]. Related: [[langchain-anatomy-of-an-agent-harness]],
[[event-sourced-agentic-patterns]].
