---
title: "Source: Anthropic — Building Effective Agents"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-building-effective-agents]
tags: [agentic-ai, agent-patterns, anthropic, engineering]
---

# Source: Anthropic — Building Effective Agents

Engineering post by Erik Schluntz and Barry Zhang of [[anthropic]], published 2024-12-19. The
foundational, vendor-but-practitioner reference on *how* to build agents. Raw capture:
`raw/articles/anthropic-building-effective-agents.md`.

## Summary

Drawn from working with dozens of teams, the central claim is that **the most successful
agent implementations use simple, composable patterns rather than complex frameworks**.
Start with the simplest thing that works and add complexity only when it demonstrably
improves outcomes.

## Key points

- **The core distinction — [[agent-vs-workflow]]:** *Workflows* orchestrate LLMs and tools
  through predefined code paths; *agents* let the LLM dynamically direct its own process and
  tool use. Both are "agentic systems."
- **The building block is the [[augmented-llm]]** — an LLM with retrieval, tools, and memory.
- **Five composable [[agentic-workflow-patterns]]:** prompt chaining, routing,
  parallelization (sectioning/voting), orchestrator-workers, and evaluator-optimizer — each
  with explicit "when to use" guidance.
- **Agents** = LLMs using tools in a loop against environmental feedback; suited to
  open-ended problems where you can't hardcode the path. They cost more and can compound
  errors, so test in sandboxes with guardrails.
- **Frameworks** (Claude Agent SDK, AWS Strands, Rivet, Vellum) speed the start but add
  abstraction that obscures prompts and invites premature complexity. Prefer calling LLM
  APIs directly; understand what's under the hood.
- **Three principles:** simplicity, transparency (show the planning steps), and a carefully
  crafted **agent-computer interface (ACI)** — invest in tool docs/testing as much as HCI.
- **Two proven domains** ([[agentic-ai]] in practice): [[customer-support-agents]] and
  [[agentic-coding]] — both have conversation + action, clear success criteria, feedback
  loops, and human oversight.

## Connections / contrast

This is the *engineering* counterpart to the market sources. Where [[langchain-state-of-agent-engineering-2026]]
measures what teams do, this prescribes what they *should* do. Its "agents vs workflows"
distinction maps onto the [[autonomy-ladder]] in [[svitla-agentic-ai-market-trends-2026]]
(chain/workflow vs partially/fully autonomous), and "agentwashing" ([[agentwashing]]) is the
market's word for systems Anthropic would classify as low-autonomy workflows. Complements
the KB's existing [[akka]] thread, which addresses the *infrastructure* (event sourcing,
distribution) under these patterns.
