---
title: ReAct Loop
type: concept
created: 2026-06-13
updated: 2026-06-13
sources: [langchain-anatomy-of-an-agent-harness]
tags: [agentic-ai, agent-harness, pattern]
---

# ReAct Loop

**ReAct** ("Reasoning + Acting") is the basic control loop of an LLM agent: the model
alternates between **reasoning** (thinking about what to do next) and **acting** (calling a
tool), feeding each tool's result back into context before reasoning again. It repeats until
the task is done. The pattern is what turns a one-shot text generator into an agent that can
take a sequence of steps toward a goal.

## Why it matters in this wiki

In [[langchain-anatomy-of-an-agent-harness]]'s decomposition of **Agent = Model + Harness**,
the ReAct loop is the engine that **drives the harness's tool-use primitives**. Specifically,
once you "give the model a computer" — bash plus code execution — the model can build and
invoke its own tools rather than relying on a fixed pre-configured set, and it's the ReAct
loop (reason → act → observe → repeat) that sequences those calls. So ReAct is the runtime
behaviour; the [[agent-harness]] is the surrounding environment (filesystem, sandbox, memory)
that each loop iteration reads from and writes to.

This is the granular, per-step counterpart to the larger-scale patterns elsewhere in the KB:
the [[ralph-loop]] re-runs a whole prompt in a clean context window, and the
[[agentic-workflow-patterns]] compose multiple model calls — but each individual agentic step
is a turn of the ReAct loop.

## Related

[[agent-harness]] · [[augmented-llm]] · [[agentic-workflow-patterns]] · [[ralph-loop]] · [[langchain]]

_Source: [[langchain-anatomy-of-an-agent-harness]]._
