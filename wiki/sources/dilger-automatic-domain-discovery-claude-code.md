---
title: "Dilger — Automatic Domain Discovery using Claude Code"
type: source
created: 2026-06-13
updated: 2026-06-13
sources: [dilger-automatic-domain-discovery-claude-code]
tags: [event-modeling, agentic-coding, domain-discovery, skills, ux, focus]
---

# Dilger — Automatic Domain Discovery using Claude Code

LinkedIn post by **[[martin-dilger]]** (2026-06-12, edited). Pitches an agent that performs **domain
discovery from a running product's UI** and renders it as a visual storyboard — built as a Claude
Code **skill** and wired into the Event Modelers platform ([[eventmodelers-ai]]). Raw capture:
`raw/articles/dilger-automatic-domain-discovery-claude-code.md`.

## Key points

- **Point an agent at the system's UI, not its code or docs.** It clicks through flows "the way a
  real user would" and builds a **visual timeline of how the product actually works, not how you
  think it works** — surfacing confusing navigation, contradictory screens, flows that don't make
  sense. "It's a mirror, and mirrors aren't always flattering."
- Replaces the tedious workshop-prep he normally asks clients for — hours of screenshots and flow
  documentation "before anyone can even start improving them." Now it "can happen automatically, on
  autopilot," so you arrive at the workshop with "a real, honest starting point."
- **"Domain Discovery doesn't have to mean writing boring documentation."** It's the discovery phase
  of [[event-modeling]] / [[event-storming]] done by an agent against the live UI.
- Meta-point he stresses: **building the discovery took ~15 minutes — "it´s just another skill."**
  Extensible to commenting on screens or finding UX flaws. A data point on how cheap bespoke agent
  [[claude-agent-sdk|skills]] have become.

## Why it matters

The other Dilger posts use Event Modeling to *constrain* an agent that writes code; this one uses an
agent to *bootstrap the model* from an existing system — automating the discovery/understand phase
rather than the build phase. It widens [[event-modeled-agent-design]] to the front of the workflow and
introduces [[domain-discovery]] as a concept.

## Caveats

Marketing post for [[eventmodelers-ai]]; no demo artifact, accuracy figures, or detail on how UI
exploration maps to event-model elements. "15 minutes" is unverified.

## Links

Entities: [[martin-dilger]], [[eventmodelers-ai]], [[anthropic]]. Concepts: [[domain-discovery]],
[[event-modeling]], [[event-storming]], [[event-modeled-agent-design]], [[agentic-coding]],
[[claude-agent-sdk]].
Related sources: [[dilger-spec-driven-development-applied]], [[dilger-keep-command-handlers-pure]],
[[qlerify-event-modeling-tool-ai]], [[proophboard-skills-ai-agent-event-modeling]].
