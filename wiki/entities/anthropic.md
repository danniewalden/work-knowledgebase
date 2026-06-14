---
title: Anthropic
type: entity
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-building-effective-agents, anthropic-effective-harnesses-long-running-agents]
tags: [entity, organization, ai-lab, agentic-ai, harness-engineering]
---

# Anthropic

AI safety and research company; maker of the **Claude** family of models and of agent
tooling. In the KB, Anthropic is the source of the foundational engineering guidance on
building agents ([[anthropic-building-effective-agents]]).

## Relevance to this KB

- Authored the canonical **[[agentic-workflow-patterns]]** post (Erik Schluntz, Barry Zhang),
  drawing the **[[agent-vs-workflow]]** distinction and advocating simple, composable patterns.
- Created the **[[model-context-protocol]]** (MCP), now a de-facto standard for connecting
  agents to tools/data and a pillar of [[multi-agent-orchestration]].
- Ships agent products/frameworks referenced across sources: the **[[claude-agent-sdk]]**
  (described as a general-purpose [[agent-harness]]), and coding agent **Claude Code** (the
  most-cited daily-driver agent in [[langchain-state-of-agent-engineering-2026]]).
- Published a key **[[harness-engineering]]** recipe for **[[long-running-agents]]**
  ([[anthropic-effective-harnesses-long-running-agents]]): the initializer-executor pattern with
  feature lists, progress files, and end-to-end self-verification.
- Listed among the key platform players building agentic capability into core products
  ([[svitla-agentic-ai-market-trends-2026]]).

_Source pages: [[anthropic-building-effective-agents]] · [[anthropic-effective-harnesses-long-running-agents]]._
