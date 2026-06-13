---
title: Agent Engineering
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [langchain-state-of-agent-engineering-2026, anthropic-building-effective-agents, fowler-bockeler-harness-engineering, langchain-anatomy-of-an-agent-harness]
tags: [agentic-ai, discipline, engineering, reliability]
---

# Agent Engineering

[[langchain]]'s framing of an emerging discipline: **the iterative process of harnessing LLMs
into reliable systems**. Because agents are nondeterministic, engineers must rapidly iterate
to refine and improve agent quality, rather than expecting correctness by construction.

In practice it spans the activities the KB's sources describe: choosing the right
[[agentic-workflow-patterns]] and avoiding unnecessary complexity ([[anthropic]]), managing
context ("context engineering"), building [[agent-observability-and-evals]], and routing
across multiple models by complexity/cost/latency. The market analog is the gap between a
working demo and a production system — "that's when the work begins"
([[svitla-agentic-ai-market-trends-2026]]).

Its environment-and-controls arm is **[[harness-engineering]]** — building and continuously
improving the [[agent-harness]] (everything around the model) so a non-deterministic model does
reliable work. The "context engineering" mentioned above now has its own page:
[[context-engineering]].

_Source pages: [[langchain-state-of-agent-engineering-2026]] · [[anthropic-building-effective-agents]] · [[fowler-bockeler-harness-engineering]] · [[langchain-anatomy-of-an-agent-harness]]._
