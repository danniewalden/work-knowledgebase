---
title: Agentic Workflow Patterns
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-building-effective-agents]
tags: [agentic-ai, patterns, architecture, engineering]
---

# Agentic Workflow Patterns

The five composable patterns [[anthropic]] observed in production, building up from the
[[augmented-llm]] toward full agents ([[anthropic-building-effective-agents]]). Each has
explicit "when to use" guidance; combine and customize rather than treat as prescriptive.

1. **Prompt chaining** — decompose a task into a fixed sequence of LLM calls, each processing
   the prior output, with programmatic "gate" checks. For cleanly decomposable tasks; trades
   latency for accuracy.
2. **Routing** — classify an input and send it to a specialized follow-up (e.g. support-query
   triage; routing easy questions to a cheaper model, hard ones to a stronger model).
3. **Parallelization** — *sectioning* (independent subtasks in parallel) or *voting* (same
   task run multiple times for confidence). Good for speed or multiple perspectives;
   e.g. one model answers while another screens for guardrails.
4. **Orchestrator-workers** — a central LLM dynamically breaks down a task, delegates to
   worker LLMs, and synthesizes results. Subtasks aren't pre-defined (vs parallelization);
   suits coding changes across many files, or multi-source search.
5. **Evaluator-optimizer** — one LLM generates, another evaluates and gives feedback in a
   loop. For tasks with clear criteria where iterative refinement helps (e.g. literary
   translation, deep search).

Beyond these, a true **agent** is just an LLM using tools in a loop against environmental
feedback. Three guiding principles: **simplicity, transparency** (show planning steps), and a
well-crafted **agent-computer interface (ACI)** — invest in tool documentation and testing.

## Connections

These are the engineering primitives beneath every other thread: [[multi-agent-orchestration]]
generalizes orchestrator-workers across systems; [[agentic-coding]] and
[[customer-support-agents]] are Anthropic's two showcase domains; the
nondeterminism that motivates evaluator-optimizer and ACI care is the same property the
[[agentic-ai]] and [[event-sourcing]] threads address. For how each pattern maps onto an
event-sourced substrate, see [[event-sourced-agentic-patterns]].

_Source pages: [[anthropic-building-effective-agents]]._
