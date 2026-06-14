---
title: Claude Agent SDK
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-effective-harnesses-long-running-agents, firecrawl-what-is-an-agent-harness]
tags: [harness-engineering, agent-harness, anthropic, tooling]
---

# Claude Agent SDK

[[anthropic]]'s general-purpose [[agent-harness]] — described as "a powerful, general-purpose agent
harness adept at coding, as well as other tasks that require the model to use tools to gather
context, plan, and execute" ([[firecrawl-what-is-an-agent-harness]]). It supplies the machinery
around the model: context management (compaction), tool dispatch, session management, and progress
tracking, leaving the model to supply the reasoning.

It is the harness used in [[anthropic-effective-harnesses-long-running-agents]]: even a frontier
model (Opus 4.5) looping on the SDK across many context windows falls short on a high-level prompt
*without* the added initializer-executor structure — illustrating that a general-purpose harness
still needs task-specific [[harness-engineering]] on top (feature lists, progress files,
self-verification). See [[long-running-agents]].

Formerly known as the Claude Code SDK; it is the foundation beneath Anthropic's **Claude Code**
coding agent. Sits in the same category as other general-purpose harnesses/frameworks discussed in
[[langchain-anatomy-of-an-agent-harness]] (e.g. LangChain's `deepagents`).

_Sources: [[anthropic-effective-harnesses-long-running-agents]] · [[firecrawl-what-is-an-agent-harness]]._
