---
title: "Miller — JasperFx AI Skills 1.6.0 (vendor-maintained agent skills)"
type: source
created: 2026-07-13
updated: 2026-07-13
sources: [miller-jasperfx-ai-skills-agent-skills]
raw_file: [raw/articles/miller-jasperfx-ai-skills-1-6-0-agent-skills.md]
tags: [agentic-coding, harness-engineering, agent-legibility, skills, event-sourcing, dotnet, critter-stack, focus]
---

# Miller — JasperFx AI Skills 1.6.0

Blog post by **[[jeremy-miller]]** (*The Shade Tree Developer*, jeremydmiller.com, 2026-07-10).
Source file: `raw/articles/miller-jasperfx-ai-skills-1-6-0-agent-skills.md`. Filed by the 2026-07-13
live-Chrome sweep — the **agentic-angle** post the watch-config flags Miller for (his other in-window
posts are Critter Stack tooling, not filed).

## Why it matters

The most concrete vendor-side statement in the KB of **agent skills as a maintained product**: the tool
authors ship a curated, source-verified skill library so a coding agent "**stops guessing from stale
training data.**" It turns [[jeremy-miller]]'s "the codebase is the prompt" thesis
([[miller-codebase-is-the-prompt-vertical-slices-ai]]) into a shipping artifact and makes the **Skills
primitive** of [[loop-engineering]] / [[harness-engineering]] concrete on the event-sourcing substrate.

## What it is

- **JasperFx AI Skills** = a curated library of **81 agent skills** covering **Wolverine, Marten,
  Polecat, and CritterWatch** ([[critter-stack]]), "written and maintained by the people who build these
  tools." Ships as the paid `JasperFx.AiSkills` package; installed via `agentskills-cli add`.
- The stated problem it solves: the release cadence outpaces both blog docs *and* model training data, so
  an agent working from priors gives **actively wrong** advice (e.g. Marten 9 eliminated runtime codegen;
  Wolverine 6 moved the Roslyn compiler to an opt-in package — "most existing internet advice is actively
  wrong").
- Design principles (all on the [[agent-legibility]] seam): docs "**verified against the actual source
  code, current as of this month**," organized "the way agents actually consume knowledge: **task-shaped,
  example-heavy, and honest about the sharp edges**"; **error messages captured verbatim from source**
  (an agent pattern-matching on error text "needs the real text, not a paraphrase"); **self-contained** —
  if a skill shows a helper method it embeds the full source, so no agent hunts for a NuGet that doesn't
  exist.
- 1.6.0 specifics: re-audited codegen skills for the Roslyn-free production shape; a new
  troubleshooting category (message routing; service location & codegen with every `InvalidServiceLocation`
  reason string + fix); a consolidated **.NET Aspire** skill (per-provider/per-transport matrix); three
  **CritterWatch** operations skills. A CI trick surfaced: `dotnet run -- codegen test` fails the PR on any
  codegen error ("fails Tuesday's PR, not Friday's deploy").

## The maintenance loop

Miller frames the upkeep as a tight feedback loop that is itself a small **hill-climbing loop**
([[loop-engineering]]): "the skill told me something stale → **fixed, verified against source,
released** … is exactly the point of maintaining these ourselves." Half of 1.6.0 started as user
feedback; 24 merged PRs since 1.5.0.

## Relevance / links

Concrete instance of the **Skills primitive** in [[addyosmani-loop-engineering|Osmani's five
primitives]] and the "guides" side of [[harness-engineering]] — here as a *vendor-authored, versioned,
source-verified* library rather than a hand-rolled `SKILL.md`. Directly extends [[critter-stack]] and
[[jeremy-miller]]'s "codebase is the prompt" argument ([[miller-codebase-is-the-prompt-vertical-slices-ai]]:
"the skills are the constitution; the slices are the code"). Sits alongside other skills-as-harness
instances: [[jwilger-agent-skills-event-modeling]], [[khononov-modularity-claude-code-plugin]],
[[tornhill-cannot-trust-agent-codescene-mcp|CodeScene's deterministic MCP sensor]] (same "give the agent
a source of truth it can't hallucinate" instinct), and [[proophboard-skills-ai-agent-event-modeling]].
Also a data point for [[agent-legibility]] (source-verified, task-shaped docs as legibility) and the
stale-training-data problem behind [[context-engineering]]. Caveat: it's a **paid product announcement**
by the maintainer — canonical for the *pattern*, promotional in framing.

_Raw source: `raw/articles/miller-jasperfx-ai-skills-1-6-0-agent-skills.md`._
