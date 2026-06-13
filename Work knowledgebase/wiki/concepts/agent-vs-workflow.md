---
title: Agents vs Workflows
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-building-effective-agents, svitla-agentic-ai-market-trends-2026]
tags: [agentic-ai, architecture, definitions]
---

# Agents vs Workflows

[[anthropic]]'s foundational distinction within the umbrella of **agentic systems**:

- **Workflows** — LLMs and tools orchestrated through *predefined code paths*. Predictable,
  consistent; best for well-defined tasks.
- **Agents** — systems where the LLM *dynamically directs its own process and tool usage*,
  maintaining control over how it accomplishes the task. Better when flexibility and
  model-driven decisions are needed at scale.

The guidance: use the simplest thing that works. Often a single augmented LLM call is enough;
add a workflow when the task decomposes cleanly; reach for a true agent only for open-ended
problems where you can't hardcode the path (accepting higher cost and compounding-error risk).

## Why it matters

This is the conceptual root of two other KB ideas. The market's **[[autonomy-ladder]]**
(chain → workflow → partially/fully autonomous) is the same spectrum operationalized, and
**[[agentwashing]]** is what happens when low-autonomy workflows/assistants are marketed as
agents. See the full pattern catalog in [[agentic-workflow-patterns]].

_Source pages: [[anthropic-building-effective-agents]] · [[svitla-agentic-ai-market-trends-2026]]._
