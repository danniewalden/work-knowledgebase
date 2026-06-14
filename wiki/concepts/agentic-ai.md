---
title: Agentic AI
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, anthropic-building-effective-agents, deloitte-ai-agents-scaling-faster-than-guardrails, langchain-state-of-agent-engineering-2026, svitla-agentic-ai-market-trends-2026]
tags: [agentic-ai, llm, distributed-systems, event-sourcing, market, patterns, governance]
---

# Agentic AI

Software that **acts with agency** — independent, stateful, decision-making behavior aimed
at goals — with an LLM in the loop. Per [[kevin-hoffman]], "agentic" is the broader idea and
"agentic AI" is the subset where AI drives the goal-seeking. [[anthropic]] draws the sharper
architectural line ([[agent-vs-workflow]]); the market grades the same spectrum by degree on
the [[autonomy-ladder]].

> **Hub page.** This thread began from [[akka]]'s infrastructure view (distribution + event
> sourcing, below) and now also covers engineering patterns, market state, use cases, and
> governance. Map of sub-pages in the next section.

## The agentic-AI landscape (map)

- **How to build them** — [[agentic-workflow-patterns]] (the [[augmented-llm]] + five
  patterns), [[agent-vs-workflow]], [[multi-agent-orchestration]] over
  [[model-context-protocol]] and [[agent2agent-protocol]], and the discipline of
  [[agent-engineering]] — whose environment-and-controls arm is [[harness-engineering]]
  (build the [[agent-harness]]; [[context-engineering]]; [[feedforward-and-feedback-controls]]).
- **What they're used for** — [[customer-support-agents]], [[agentic-coding]] (now reaching
  [[unattended-coding-agents]]), research/data analysis, and the emerging [[agentic-commerce]].
- **Where the market is** — [[svitla-agentic-ai-market-trends-2026]]: fast growth but a
  ~79%-adoption / ~11%-production gap explained by [[agentwashing]]; ~57% production among
  technical builders ([[langchain-state-of-agent-engineering-2026]]).
- **Keeping them safe & reliable** — [[agent-observability-and-evals]] (quality is the #1
  blocker), [[agent-governance]] (only ~21% mature, per [[deloitte]]), and
  [[guardian-agents]].

## Characteristics

- **Context-driven, goal-oriented, autonomous, learning, adaptable.** Agents usually have
  narrow goals; an **orchestrating supervisor** weaves several together.
- **Prompt / [[context-engineering|context engineering]] is the single most important success
  factor** — precision in what you feed the LLM determines outcomes.
- LLM mechanics: tokenization → model-specific vocabulary → vectors; token streams in/out;
  hosted models **charge per token**.
- Agents need: **memory** (conversation history), query augmentation via
  [[retrieval-augmented-generation]], async streaming, and **tool callbacks**.
- LLMs/agents are **nondeterministic** — you can't predict call-to-call behavior, so you
  need ways to reproduce, audit, and evaluate them.

## Agentic systems are distributed systems

[[akka]]'s thesis ([[akka-agentic-systems-are-distributed-systems]]): at enterprise scale,
agentic systems are inherently distributed — distributed memory, streaming I/O with LLMs,
per-agent and multi-agent orchestration, semantic search over vector DBs, and regional
resilience. A demo on a laptop is not a production system.

## Why event sourcing is the proposed backbone

Because behavior is nondeterministic, an immutable event log ([[event-sourcing]]) gives
**perfect recall, auditability, durable inter-agent communication, and versioning via
replay** — and storing agent memory as replicated events provides a distributed backbone.
This is the conceptual bridge to the KB's other thread, [[event-modeling]]: the same
append-only-ledger idea, applied to agents instead of information systems. The KB's own
synthesis, [[event-sourced-agentic-patterns]], works out how [[anthropic]]'s control-flow
patterns map onto that ledger.

_Source pages: [[akka-event-sourcing-backbone-agentic-ai]] · [[akka-agentic-systems-are-distributed-systems]] · [[anthropic-building-effective-agents]] · [[deloitte-ai-agents-scaling-faster-than-guardrails]] · [[langchain-state-of-agent-engineering-2026]] · [[svitla-agentic-ai-market-trends-2026]]._
