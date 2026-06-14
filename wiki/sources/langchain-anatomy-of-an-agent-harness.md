---
title: "Source: LangChain — The Anatomy of an Agent Harness"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [langchain-anatomy-of-an-agent-harness]
tags: [harness-engineering, agent-harness, primitives, langchain]
---

# Source: LangChain — The Anatomy of an Agent Harness

Blog post by Vivek Trivedy, [[langchain]], published 2026-03-10. The clearest **first-principles
decomposition** of what an [[agent-harness]] contains and why each piece exists. Raw capture:
`raw/articles/langchain-anatomy-of-an-agent-harness.md`.

## Summary

**Agent = Model + Harness. "If you're not the model, you're the harness."** A harness is every
piece of code, config, and execution logic that isn't the model — system prompts, tools/Skills/
MCPs, bundled infrastructure (filesystem, sandbox, browser), orchestration logic, and
hooks/middleware. The post derives each core component by working backwards from a desired agent
behaviour to the harness feature that enables it.

## Key points

- **Why harnesses exist:** models take data in and emit text; out of the box they can't keep
  durable state, execute code, access realtime knowledge, or set up environments — all
  *harness-level* features.
- **Filesystem** is the most foundational primitive: workspace, offload/context management,
  cross-session persistence, and a shared collaboration surface; git adds versioning/rollback.
- **Bash + code execution** as a general-purpose tool ("give the model a computer") so it can
  build its own tools instead of relying on a fixed pre-configured set; the [[react-loop]] drives it.
- **Sandboxes** give safe, isolated, scalable execution; good environments ship good default
  tooling (runtimes, CLIs, browsers) enabling self-verification loops.
- **Memory & search:** the only way to add knowledge without changing weights is context
  injection — AGENTS.md-style memory files (continual learning) plus web search / Context7 for
  post-cutoff knowledge.
- **Battling [[context-rot]]:** harnesses are "delivery mechanisms for good context engineering" —
  **compaction**, **tool-call offloading** (keep head/tail, offload full output to disk), and
  **Skills** via **progressive disclosure**.
- **Long-horizon execution:** filesystems + git for cross-session state; **[[ralph-loop]]s** that
  intercept the model's exit and reinject the prompt in a clean window; planning + self-verification hooks.
- **Co-evolution of model & harness:** agent products are post-trained with their harness in the
  loop, which boosts in-harness skill but can cause overfitting (e.g. apply_patch tool logic). The
  best harness for *your* task isn't necessarily the one a model was trained with — Terminal Bench
  2.0 shows the same model scoring very differently across harnesses.
- **Future:** some harness duties get absorbed into models, but (like prompt engineering) harness
  engineering stays valuable; LangChain explores this in its `deepagents` library.

## Connections / contrast

The definitional backbone for the [[agent-harness]] page and the source of the "Agent = Model +
Harness" equation that [[fowler-bockeler-harness-engineering]] adopts. Its primitive inventory
(filesystem, sandbox, memory, compaction) underlies the concrete recipes in
[[anthropic-effective-harnesses-long-running-agents]] and [[openai-harness-engineering-codex]].
Harrison Chase's "harnesses grow, not shrink" argument is echoed in
[[firecrawl-what-is-an-agent-harness]]. Extends [[agent-engineering]] and
[[multi-agent-orchestration]] (parallel subagents).

_Source page: [[langchain-anatomy-of-an-agent-harness]]._
