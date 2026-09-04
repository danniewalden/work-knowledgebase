---
title: "Willison — Designing agentic loops"
type: source
created: 2026-07-06
updated: 2026-07-06
sources: [willison-designing-agentic-loops]
raw_file: [raw/articles/willison-designing-agentic-loops.md]
tags: [loop-engineering, agentic-coding, coding-agents, prompt-injection, focus]
---

# Willison — Designing agentic loops

Blog post by **[[simon-willison]]** (simonwillison.net, 2025-09-30).
Source file: `raw/articles/willison-designing-agentic-loops.md`. Surfaced by the
live-Chrome LinkedIn/X sweep of 2026-07-06 (out-of-window but genuinely new to the
wiki and on the tight [[loop-engineering]] thread).

## Why it matters

The **earliest named statement of loop design** in the KB — Willison coins **"designing agentic
loops"** as "a critical new skill to develop" nine months before the June-2026
[[loop-engineering]] crystallization ([[addyosmani-loop-engineering|Osmani]] /
[[swyx-loopcraft-art-of-stacking-loops|swyx]]). It gives that thread a **2025 origin** and, unlike the
2026 sources, a concrete **security + mechanics** dimension.

## Core thesis

- Coding agents are **brute-force problem solvers**: "reduce your problem to a clear goal and a set of
  tools that can iterate towards that goal" and the agent can often brute-force a working solution.
- His definition (same one the [[agentic-coding]] page uses): an LLM agent **"runs tools in a loop to
  achieve a goal"** — so *"the art of using them well is to carefully design the tools and loop for
  them to use."*

## The four practical moves

1. **YOLO mode + sandboxing.** Auto-approving every command is what makes brute force effective — and
   *"so dangerous."* Cites Solomon Hykes: *"An AI agent is an LLM wrecking its environment in a loop."*
   Three risks (destructive shell commands, **exfiltration**, machine-as-attack-proxy); three
   mitigations (secure sandbox / someone else's computer / accept the risk). Prefers **GitHub
   Codespaces** (disposable containers) and cites Anthropic's **Safe YOLO mode**
   (`--dangerously-skip-permissions` in a no-internet container + trusted-host allowlist). This is the
   [[prompt-injection]] / agent-safety angle largely absent from the 2026 loop sources.
2. **Pick the right tools for the loop.** Prefers **shell commands over [[model-context-protocol|MCP]]**
   ("coding agents are *really good* at running shell commands"); documents tools for the agent in an
   **AGENTS.md** file (one worked example is enough for the model to generalize). Complements Osmani's
   "Skills" primitive — knowledge written down once so the loop doesn't re-derive the project each cycle.
3. **Issue tightly scoped credentials.** Prefer test/staging creds where damage is contained; if a
   credential can spend money, **set a tight budget limit** (his Fly.io example: a dedicated org with a
   $5 cap and a scoped API key).
4. **Know when to loop.** Best fit = **clear success criteria + tedious trial-and-error** ("ugh, I'm
   going to have to try a lot of variations"): debugging, performance optimization, dependency
   upgrades, shrinking containers. The common enabler is a **cleanly passing automated test suite** —
   the same maker/verifier point as the [[loop-engineering|verification loop]] and
   [[feedforward-and-feedback-controls|sensors]].

## Relevance / links

Anchors [[simon-willison]] on the [[loop-engineering]] thread with priority of naming; pairs with
[[willison-agentic-engineering-patterns]] (his broader guide). Bridges loops to agent **safety**
([[prompt-injection]], sandboxing) — a dimension [[addyosmani-loop-engineering]] and
[[swyx-loopcraft-art-of-stacking-loops]] under-weight. Part of his "How I use LLMs" series (next post:
"Vibe engineering," 2025-10-07 — another Willison coinage, not yet captured).

_Raw source: `raw/articles/willison-designing-agentic-loops.md`._
