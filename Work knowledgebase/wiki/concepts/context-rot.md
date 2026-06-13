---
title: Context Rot
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness]
tags: [context-engineering, harness-engineering, failure-mode]
---

# Context Rot

The degradation in a model's reasoning and task completion **as its context window fills up**.
History, tool outputs, and prior reasoning crowd the window; even at 200k+ tokens, dense content
buried in the middle gets ignored (the "Lost in the Middle" finding, Liu et al., Stanford 2023).
Context is "a precious and scarce resource."

It is one of the main reasons a stateless model needs an [[agent-harness]], and the problem
[[context-engineering]] exists to manage — via **compaction**, **tool-call offloading**, and
**Skills / progressive disclosure** ([[langchain-anatomy-of-an-agent-harness]]). It also drives
the [[long-running-agents]] failure modes ([[anthropic-effective-harnesses-long-running-agents]]):
running out of context mid-build and leaving undocumented work for the next session.

_Sources: [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]]._
