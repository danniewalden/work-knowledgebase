---
title: "Addy Osmani — Loop Engineering"
type: source
created: 2026-06-28
updated: 2026-06-28
sources: [addyosmani-loop-engineering]
raw_file: [raw/articles/addyosmani-loop-engineering.md]
tags: [loop-engineering, harness-engineering, unattended-coding-agents, long-running-agents, agentic-coding, focus]
---

# Addy Osmani — Loop Engineering

Blog post by **Addy Osmani** (addyosmani.com, 2026-06-07).
Source file: `raw/articles/addyosmani-loop-engineering.md`. The **definitional primary** for
[[loop-engineering]] — written the week the term crystallized (alongside
[[swyx-loopcraft-art-of-stacking-loops|swyx's Loopcraft]] and Steinberger's one-liner).

## Core thesis

**"Loop engineering is replacing yourself as the person who prompts the agent. You design the system
that does it instead."** A loop is a recursive goal: define a purpose and the AI iterates until
complete. Osmani positions it explicitly **one floor above [[harness-engineering|the harness]]** — "the
harness, but it runs on a timer, it spawns little helpers, and it feeds itself." He is deliberately
skeptical: still early, and you *have* to watch token costs (usage varies wildly).

He frames the shift via Steinberger ("you should be designing loops that prompt your agents") and
**Boris Cherny** ("I don't prompt Claude anymore. I have loops running that prompt Claude… my job is
to write loops"). The old way — write a good prompt, read the reply, type the next thing, holding the
tool the whole time — "is kind of over."

## The five primitives + memory

Notably, **the same shape now ships natively in both the Codex app and Claude Code** — Osmani's point
is you stop arguing about which tool and design a loop that works in either:

1. **Automations** — scheduled discovery + triage; *the heartbeat.* (`/loop` = re-run on cadence;
   `/goal` = run until a verifiable stop condition, with a *separate* small model grading "done" —
   maker≠checker applied to the stop itself.)
2. **Worktrees** — isolated checkouts so parallel agents don't collide (same headache as two engineers
   editing the same lines).
3. **Skills** — project knowledge in `SKILL.md`, written once where the agent reads it every run;
   without skills the loop "re-derives your whole project from zero every cycle." The cure for "intent
   debt." (A plugin is how you *ship* a skill.)
4. **Plugins / connectors** — [[model-context-protocol|MCP]]-based access so the loop opens the PR,
   links the ticket, pings the channel — *acts* instead of just describing.
5. **Sub-agents** — keep the maker away from the checker; a second agent (often a different model)
   catches what the first talked itself into. This is what `/goal` does under the hood.
6. **Memory (the sixth thing)** — on-disk state (markdown or Linear) outside the single conversation.
   **"The agent forgets, the repo doesn't."**

## What one loop looks like

A morning automation runs a triage skill over yesterday's CI failures / open issues / recent commits
and writes findings to a markdown file or Linear board; each worthwhile finding gets an isolated
worktree where one sub-agent drafts the fix and a second reviews it against the project skills + tests;
connectors open the PR and update the ticket; anything the loop can't handle lands in a triage inbox.
"You designed it one time. You did not prompt any of those steps."

## The honest caveats — three problems get *sharper*, not easier

- **Verification is still on you** — "a loop running unattended is also a loop making mistakes
  unattended"; "done" is a claim, not a proof.
- **Comprehension debt** — a smooth loop grows the gap between what exists and what you understand
  unless you read what it made.
- **Cognitive surrender** — designing the loop is the cure when done with judgement, the accelerant
  when done to avoid thinking; "same action, opposite result." Two people build the same loop and get
  opposite outcomes. **"Build the loop. But build it like someone who intends to stay the engineer."**

## Why it matters here

The cleanest articulation of the [[loop-engineering]] layer and a direct extension of the harness
thread: the five primitives map onto KB concepts already present ([[ralph-loop]], [[long-running-agents]],
[[unattended-coding-agents]], skills-as-[[harness-engineering|harness]]-guides, [[model-context-protocol|MCP]]
connectors, on-disk memory ≈ [[event-sourcing]]). Cross-references his own earlier writing on agent
harness engineering, the "orchestration tax," "intent debt," and "comprehension debt."

## Touches

[[loop-engineering]] · [[harness-engineering]] · [[ralph-loop]] · [[long-running-agents]] ·
[[unattended-coding-agents]] · [[agentic-coding]] · [[model-context-protocol]] ·
[[agent-observability-and-evals]] · [[andrej-karpathy]]

_Source: `raw/articles/addyosmani-loop-engineering.md`._
