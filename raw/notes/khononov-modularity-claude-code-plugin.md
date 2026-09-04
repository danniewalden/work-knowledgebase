---
source_url: https://github.com/vladikk/modularity
title: "Modularity Skills — a Claude Code plugin for designing/reviewing modular systems with the Balanced Coupling model"
author: Vlad Khononov (vladikk)
publication: GitHub (vladikk/modularity)
published: 2026 (exact date unconfirmed — repo has 11 commits, no tagged releases; references Claude Code v1.0.33+ and Claude Opus 4.5+, so authored recently; new to this wiki as of this capture)
retrieved: 2026-06-22
type: note
---

> CAPTURE NOTE / PROVENANCE: This is a copyright-conscious SUMMARY, not a verbatim
> capture. The repository carries a CC BY-NC-SA 4.0 license AND an explicit "AI
> Training Restriction" ("may not be used for training, fine-tuning, or any other
> form of machine learning model development without explicit written permission").
> Following the wiki's established handling of Khononov's personal/licensed
> material (see [[khononov-golden-age-of-modularity]]), only the factual gist and
> structure are recorded here, in this maintainer's own words; quotations are kept
> minimal. Source-of-record is the repo itself at the URL above.
>
> NOTE on novelty: today's [[coupling-research-note]] already cites the model's
> `skills/balanced-coupling/SKILL.md` as a *reference for the Balanced Coupling
> dimensions*. What is NEW here is the plugin **as a shipped agent tool** — Khononov
> operationalizing Balanced Coupling into two runnable Claude Code skills aimed
> explicitly at the AI-coding era. That tool framing was not previously captured.

## What it is

A Claude Code **plugin** ("Modularity Skills") published by Vlad Khononov that brings
the [[balanced-coupling]] model to bear on software architecture, packaged as agent
skills. Install via the Claude Code plugin marketplace (`/plugin marketplace add
vladikk/modularity` → `/plugin install modularity@vladikk-modularity`) or by cloning
and loading with `--plugin-dir`. Requires Claude Code v1.0.33+; recommends Claude
Opus 4.5 or later "for nuanced architectural reasoning." Companion site:
coupling.dev. Licensed CC BY-NC-SA 4.0 (commercial use by arrangement).

## The AI-era framing (why it exists)

Khononov's pitch positions the tool against the grain of most AI coding assistants.
His argument: there is no shortage of AI tools giving *code-level* feedback (best
practices, edge cases, bugs), but "that's not where the costly mistakes hide." In
the AI era code is generated faster than ever, so technical debt accumulates faster
too — any misdrawn boundary or unmanaged coupling "will grow into a big ball of mud
at a pace that wasn't possible before." The plugin therefore operates at the
**architectural level**, not the line level. (This is the same thesis as his
[[khononov-golden-age-of-modularity]] post — good boundaries are what keep an
AI-accelerated codebase tractable — but now delivered as an executable harness skill
rather than an essay.)

## The two skills

1. **`/modularity:review`** — analyzes an existing codebase for coupling imbalances:
   what knowledge is properly encapsulated, what's leaking across component
   boundaries, and where cascading changes are waiting to happen. Workflow: reads
   code + functional requirements → asks about domain classification
   (core/supporting/generic), team structure, known pain points → maps integrations
   across the three dimensions (integration strength, distance, volatility) → applies
   the balance rule to flag imbalances → emits a review document (Markdown + HTML)
   with a coupling-overview table, issue descriptions, and concrete recommendations,
   each hyperlinked back to the relevant coupling.dev concept.

2. **`/modularity:high-level-design`** — the inverse: designs a modular architecture
   *from* functional requirements. Workflow: reads requirements + asks clarifying
   questions → classifies domain areas by volatility (core/supporting/generic
   subdomains) → designs the modules assessing coupling on all three dimensions →
   produces per-module design docs (responsibilities, encapsulated knowledge,
   integration contracts, change vectors) + test specifications + an architecture
   overview → **self-reviews the design for imbalances and iterates until clean**.
   Each step is gated on human approval.

## The model it encodes (recap)

Both skills are grounded in Balanced Coupling, which weighs coupling on three dials:
**Integration Strength** (knowledge shared: intrusive > functional > model >
contract), **Distance** (socio-technical cost of co-evolving: code structure / team
boundaries / runtime), and **Volatility** (probability of change, judged from the
business domain). The balance rule:
`BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY` — coupling is balanced when
strength and distance counterbalance, or when volatility is low enough to neutralize
the imbalance. Every recommendation "traces back to a concrete dimension … not gut
feel." See [[balanced-coupling]] and [[coupling-taxonomy]].

## Why it's on-thread for this wiki

This sits at the **coupling/cohesion-substrate × AI-agents** intersection (Thread 6,
"design for agents / AI-readable code"). It is a concrete instance of the recurring
pattern the wiki has been tracking — practitioners turning a design discipline into
an **agent harness skill** (cf. [[jwilger-agent-skills-event-modeling]],
[[proophboard-skills-ai-agent-event-modeling]], Fritzsche/Miller "skills encode the
conventions"). Here the discipline is Balanced Coupling rather than Event Modeling.
Notable that the self-reviewing `high-level-design` loop is a small instance of the
guides-and-sensors idea from [[harness-engineering]].

Related: [[vlad-khononov]] · [[balanced-coupling]] · [[business-capabilities]] ·
[[ai-readable-code]] · [[agent-legibility]] · [[coupling-research-note]]
