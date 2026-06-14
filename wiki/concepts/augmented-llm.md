---
title: Augmented LLM
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-building-effective-agents]
tags: [agentic-ai, architecture, building-block]
---

# Augmented LLM

[[anthropic]]'s **foundational building block** of every agentic system: a single LLM
enhanced with three augmentations —

- **Retrieval** (e.g. [[retrieval-augmented-generation]]) — the model generates its own
  search queries,
- **Tools** — it selects and calls external services/APIs, and
- **Memory** — it decides what information to retain.

Everything more complex ([[agentic-workflow-patterns]], full agents, [[multi-agent-orchestration]])
is built by composing augmented-LLM calls. Anthropic recommends tailoring these capabilities
to the use case and exposing them through a clean, well-documented interface — one approach
being the **[[model-context-protocol]]**. For many applications, optimizing a single
augmented LLM call is all that's needed.

_Source pages: [[anthropic-building-effective-agents]]._
