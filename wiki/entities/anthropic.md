---
title: Anthropic
type: entity
created: 2026-06-11
updated: 2026-09-04
sources: [anthropic-building-effective-agents, anthropic-effective-harnesses-long-running-agents, anthropic-getting-started-with-loops, willison-claudes-new-system-prompt, willison-claude-fable-5-1-animated-pelican, fowler-fragments-2026-09-01]
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
- Published the **vendor-canonical [[loop-engineering]] taxonomy** ([[anthropic-getting-started-with-loops]],
  Claude Code team): loops = agents cycling until a stop condition, classified into turn-based /
  goal-based (`/goal`) / time-based (`/loop`, `/schedule`) / proactive — the primitive-level counterpart
  to the LangChain/Osmani/swyx primaries.
- Listed among the key platform players building agentic capability into core products
  ([[svitla-agentic-ai-market-trends-2026]]).
- **Publishes consumer system prompts, with revision history — and not the rest.** Anthropic publishes the
  system prompts for claude.ai and the mobile apps, including historic revisions, on a documentation site
  designed to be LLM-readable (append `.md` to any page). Willison built a diffable Git timeline of them
  ([[willison-claudes-new-system-prompt]]) and is unambiguous that this is good practice: *"I love that
  they do this."* The limit is equally clear: **Claude Code and Cowork prompts are not published**, and —
  per the model's own account of its context — the published core prompt is followed by unpublished
  *"feature- and tool-specific blocks"* loaded per enabled feature. **That second claim is a MODEL
  SELF-REPORT, not an Anthropic statement.** So the agentic products are *less* legible than the consumer
  ones. See [[agent-legibility]] and [[agent-harness]].
- **Fable 5.1** (2026-09-01) exposes **five reasoning-effort levels with no way to disable reasoning**, and
  the cost span across them on one fixed prompt is ~33× (**65,927 output tokens / 13m54s / $3.30 at `max`
  vs 1,998 tokens / 23.8s / ~10¢ at `low`**), with the two lowest levels apparently skipping reasoning
  entirely — see [[token-budget-quality-cliff]] and
  [[willison-claude-fable-5-1-animated-pelican]]. The launch's own benchmark claims (Terminal-Bench-Science
  0.1 at 52.6%, on a benchmark announced five days earlier) are **VENDOR SELF-REPORT**.
- Claude Opus 5 is the base model in NVIDIA's AVO harness result — **100% on ARC-AGI-3** — but the result
  is attributed to the harness, not the model, and is **NVIDIA's own self-report relayed secondhand**
  ([[fowler-fragments-2026-09-01]]); no methodology, cost, attempt count or replication. See [[nvidia]].
- **Its own figures about its own products carry the vendor marker.** The Claude-Code-team practice
  numbers the KB cites via [[willison-fireside-chat-claude-code-team]] — Claude Tag landing **65%** of the
  product team's PRs, automated review "catching 100% of the issues" in selected files — and the Opus 4.1
  reward-hacking deltas (**52% → 18%**, "65% less likely… if you simply asked it not to") are
  **VENDOR SELF-REPORT**: Anthropic's own models, own system card, own internal benchmark, no replication,
  and the reward-hacking delta sits inside a programme of other post-training changes. The marker travels
  with each figure onto every page that cites it.

_Source pages: [[anthropic-building-effective-agents]] ·
[[anthropic-effective-harnesses-long-running-agents]] · [[anthropic-getting-started-with-loops]] ·
[[willison-claudes-new-system-prompt]] · [[willison-claude-fable-5-1-animated-pelican]] ·
[[fowler-fragments-2026-09-01]] (secondhand relay of the NVIDIA AVO result)._
