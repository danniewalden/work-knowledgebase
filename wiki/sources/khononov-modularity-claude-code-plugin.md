---
title: "Modularity Skills — Khononov's Claude Code plugin for Balanced Coupling"
type: source
created: 2026-06-22
updated: 2026-06-22
sources: [khononov-modularity-claude-code-plugin]
raw_file: [raw/notes/khononov-modularity-claude-code-plugin.md]
tags: [coupling-cohesion, modularity, balanced-coupling, agentic-coding, agent-harness, agent-skills, ai-readable-code, focus]
---

# Modularity Skills — Khononov's Claude Code plugin

**Author/source:** [[vlad-khononov|Vlad Khononov]] · GitHub `vladikk/modularity` ·
companion site [coupling.dev](https://coupling.dev) · captured 2026-06-22 (summary
note `raw/notes/khononov-modularity-claude-code-plugin.md`).

> Provenance & caveats: copyright-conscious **summary**, not a verbatim capture — the
> repo is CC BY-NC-SA 4.0 with an explicit AI-training restriction, handled like the
> other Khononov captures ([[khononov-golden-age-of-modularity]]). Exact publish date
> unconfirmed (11 commits, no tagged releases); the Claude Code v1.0.33+ / Claude Opus
> 4.5+ requirements indicate it is recent. It is **new to this wiki as a shipped tool**:
> the [[coupling-research-note]] (ingested earlier the same day) already cited the
> plugin's `balanced-coupling/SKILL.md` as a *reference for the model's dimensions*,
> but the plugin **as an agent harness skill** was not previously captured.

## What it is

A **Claude Code plugin** ("Modularity Skills") that packages Khononov's
[[balanced-coupling|Balanced Coupling]] model as two runnable agent skills operating
at the **architectural** level (not the line level). His framing is the AI-coding
era directly: there is no shortage of AI tools giving *code-level* feedback, "but
that's not where the costly mistakes hide" — code is now generated faster than ever,
so any misdrawn boundary or unmanaged coupling "will grow into a big ball of mud at a
pace that wasn't possible before." The plugin's job is to catch that at the boundary,
where it is cheap.

## The two skills

- **`/modularity:review`** — audits an existing codebase for coupling imbalances:
  what knowledge is properly encapsulated, what leaks across boundaries, where
  cascading changes are waiting. It reads the code + functional requirements, asks
  about domain classification (core/supporting/generic), team structure, and known
  pain points, maps each integration across the three dimensions (integration
  strength, distance, volatility), applies the balance rule to flag imbalances, and
  emits a **Markdown + HTML review** with a coupling-overview table, issue
  descriptions, and concrete recommendations — each hyperlinked to the relevant
  coupling.dev concept.
- **`/modularity:high-level-design`** — the inverse: designs a modular architecture
  *from* functional requirements. It classifies domain areas by volatility, designs
  the modules assessing coupling on all three dimensions, and produces per-module
  design docs (responsibilities, encapsulated knowledge, integration contracts,
  change vectors) + test specifications + an architecture overview — then
  **self-reviews the design for imbalances and iterates until clean**, gating each
  step on human approval.

## The model it encodes

Both skills are grounded in Balanced Coupling: **Integration Strength** (intrusive >
functional > model > contract), **Distance** (socio-technical cost of co-evolving),
**Volatility** (probability of change, judged from the business domain), and the
balance rule `BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY`. "Every
recommendation traces back to a concrete dimension … not gut feel." See
[[balanced-coupling]] and [[coupling-taxonomy]].

## Why it matters here

A concrete instance of the recurring pattern this wiki tracks — a design discipline
turned into an **agent harness skill**. Here the discipline is Balanced Coupling
rather than Event Modeling, making it the coupling-substrate cousin of
[[jwilger-agent-skills-event-modeling]] and
[[proophboard-skills-ai-agent-event-modeling]] (Event Modeling as a portable agent
skill / MCP). It is also the operational form of Khononov's own thesis from
[[khononov-golden-age-of-modularity]] ("boundaries are what AI depends on") — the
essay became an executable skill. The self-reviewing `high-level-design` loop is a
small instance of the guides-and-sensors idea from [[harness-engineering]], and the
whole thing sits on the [[ai-readable-code]] thread (Thread 6: design for agents).

Related: [[vlad-khononov]] · [[balanced-coupling]] · [[ai-readable-code]] ·
[[business-capabilities]] · [[agent-legibility]] · [[coupling-research-note]] ·
[[jwilger-agent-skills-event-modeling]] · [[proophboard-skills-ai-agent-event-modeling]]
