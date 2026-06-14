---
title: Eventmodelers.ai
type: entity
created: 2026-06-13
updated: 2026-06-14
sources: [dilger-spec-driven-development-applied, dilger-automatic-domain-discovery-claude-code, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-model-is-a-living-spec-always-on-agent]
tags: [tool, platform, event-modeling, agentic-ai, spec-driven-development, focus]
---

# Eventmodelers.ai

An **agentic software modeling platform** being built by **[[martin-dilger]]**, positioned to "bring
business, engineering and AI together" — i.e. [[event-modeling]] as the shared spec that drives
[[agentic-coding]]. Known only from Dilger's LinkedIn posts so far (no captured product docs), so this
page is provisional.

## What's claimed

- A platform where **Domain Discovery runs on autopilot**: an agent explores a product's live UI and
  produces a visual storyboard / timeline of how it actually works
  ([[dilger-automatic-domain-discovery-claude-code]]; [[domain-discovery]]).
- Built on composable agent **skills** ("it´s just another skill") that can be extended to comment on
  screens or find UX flaws — the same [[claude-agent-sdk|skills]] pattern as
  [[prooph-board]]/[[jwilger-agent-skills-event-modeling]].
- Embodies Dilger's [[spec-driven-development]] thesis: design the environment so the agent's good
  behavior is the path of least resistance, with the Event Model as the source of truth.
- Operated as a **live spec**: Dilger describes a background agent that builds continuously from board
  edits, and a slice→tests-as-harness→implement→PR loop, optionally fully autonomous
  ([[dilger-model-is-a-living-spec-always-on-agent]]; [[long-running-agents]]).

## Where it sits

One of a small cluster of **AI-assisted Event Modeling tools** in the KB — alongside [[qlerify]]
(generates models + code from descriptions) and [[prooph-board]] (online EM tool + Cody Engine +
agent skills/MCP). Distinctive angle: **discovery-from-running-UI** and a spec-driven agentic build
loop, rather than diagram-authoring assistance. Evidence is vendor-self-report; no demo, pricing, or
independent review captured.

_Source pages: [[dilger-automatic-domain-discovery-claude-code]] ·
[[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] ·
[[dilger-model-is-a-living-spec-always-on-agent]]._
