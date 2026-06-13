---
title: Agent Harness
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, anthropic-effective-harnesses-long-running-agents]
tags: [harness-engineering, agent-harness, primitives, architecture]
---

# Agent Harness

**Agent = Model + Harness.** "If you're not the model, you're the harness"
([[langchain-anatomy-of-an-agent-harness]]). The harness is every piece of code, configuration,
and execution logic that isn't the model itself — the software infrastructure that turns a
stateless text generator into a capable [[agentic-ai|agent]]. The model supplies intelligence;
the harness makes that intelligence useful. *Building and improving the harness* is
[[harness-engineering]].

## Why it's needed

Out of the box, models take data in and emit text; they can't keep durable state across sessions,
execute code, fetch realtime knowledge, or set up environments. These are **harness-level
features**. Without one, long-running agents fail predictably — see [[context-rot]], hallucinated
tool calls, and lost state on failure ([[firecrawl-what-is-an-agent-harness]]).

## Core components / primitives

- **System prompts; tools, Skills, MCPs** ([[model-context-protocol]]) and their descriptions.
- **Bundled infrastructure:** filesystem (the most foundational primitive — workspace, offload,
  cross-session persistence, collaboration surface; git adds versioning), sandbox, browser.
- **Bash + code execution** as a general-purpose tool ("give the model a computer").
- **Memory & search:** context-injection memory files (AGENTS.md), web search for post-cutoff knowledge.
- **Context management:** compaction, tool-call offloading, Skills via progressive disclosure.
- **Orchestration logic:** subagent spawning, handoffs, model routing ([[multi-agent-orchestration]]).
- **Hooks/middleware:** deterministic checks, continuation ([[ralph-loop]]), verification.

## Architecture patterns ([[firecrawl-what-is-an-agent-harness]])

Single-agent supervisor · **initializer-executor split** (see [[long-running-agents]]) ·
multi-agent coordination.

## Not the same as…

- **Framework** = libraries/abstractions for building agents (LangChain, LlamaIndex).
- **Harness** = the runtime that *executes* agents with tools, memory, state.
- **Orchestrator** = the control flow deciding when/how to call the model.

LangChain's DeepAgents is a harness built on the LangChain framework. The [[claude-agent-sdk]] is
described as a general-purpose agent harness. Note the **model↔harness co-evolution**: products are
post-trained with their harness in the loop, so the best harness for a task isn't necessarily the
one a model shipped with ([[langchain-anatomy-of-an-agent-harness]]).

_Sources: [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[anthropic-effective-harnesses-long-running-agents]]._
