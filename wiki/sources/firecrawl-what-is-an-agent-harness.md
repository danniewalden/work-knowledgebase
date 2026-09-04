---
title: "Source: Firecrawl — What Is an Agent Harness?"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [firecrawl-what-is-an-agent-harness]
raw_file: [raw/articles/firecrawl-what-is-an-agent-harness.md]
tags: [harness-engineering, agent-harness, survey, vendor]
---

# Source: Firecrawl — What Is an Agent Harness?

Blog post by Ninad Pathak, Firecrawl, published 2026-04-16. A **definitional survey** that
collates the harness discourse and adds a useful taxonomy. Vendor blog — product-pitch sections
trimmed in the raw capture. Raw capture: `raw/articles/firecrawl-what-is-an-agent-harness.md`.

## Summary

An agent harness is "the software infrastructure surrounding an AI model that manages everything
except the model's actual reasoning" — tool execution, memory, state persistence, error recovery.
Traces the term's spread: [[mitchell-hashimoto]]'s Feb 2026 post formalised it, then
[[openai-harness-engineering-codex]] gave it a flagship case study days later.

## Key points

- **Why long-running agents fail without one:** statelessness, plus context rot, hallucinated
  tool calls, and lost state on failure. Cites Anthropic's Opus 4.5 web-app failure.
- **How it works:** intercept → validate → route → record at each step; a once-at-start setup
  phase + a repeated session phase that loads state, picks the next task, works, saves progress.
- **Four core components:** (1) tool integration layer, (2) memory/state — working context,
  session state, long-term memory ("memory isn't a plugin, it's the harness" — Sarah Wooders,
  Letta), (3) context engineering/compression (compaction, RAG, "Lost in the Middle"), (4)
  verification & guardrails (test-before-complete, human-in-the-loop for sensitive actions).
- **Three architecture patterns:** single-agent supervisor; **initializer-executor split**
  (Anthropic's approach); **multi-agent coordination** ([[multi-agent-orchestration]]).
- **Harness vs. framework vs. orchestrator:** framework = components/libraries (LangChain,
  LlamaIndex); harness = runtime that executes agents with tools/memory/state; orchestrator =
  control flow deciding when/how to call the model. LangChain DeepAgents = a harness on a framework.
- **Harness engineering** = treat every failure as a system problem to permanently fix
  (Hashimoto): update the instruction file, or build a tool that makes correct behaviour
  mechanically verifiable. Distinct from [[context-engineering]] (which optimises *input*).
- **Won't models absorb harnesses?** Harrison Chase argues the opposite — Claude Code is 512k+
  LOC and growing; even API "built-in web search" is itself an invisible harness.

## Connections / contrast

A good consolidator/glossary tying the cluster together; weaker as primary evidence (vendor,
secondary). Its harness-vs-framework-vs-orchestrator table sharpens the [[agent-harness]] page;
its three architecture patterns name the structure that
[[anthropic-effective-harnesses-long-running-agents]] demonstrates. Definition of
[[harness-engineering]] (failure → permanent fix) matches [[fowler-bockeler-harness-engineering]]'s
steering loop and [[openai-harness-engineering-codex]]'s "make it enforceable." Reinforces the
harness/[[context-engineering]] distinction.

_Source page: [[firecrawl-what-is-an-agent-harness]]._
