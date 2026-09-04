---
title: "Adam Tornhill — Why Merge Conflicts became the new Agentic Bottleneck"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [tornhill-merge-conflicts-agentic-bottleneck]
raw_file: [raw/notes/tornhill-merge-conflicts-agentic-bottleneck.md]
tags: [ai-readable-code, agentic-coding, architecture, conways-law, code-health, focus]
---

# Adam Tornhill — Why Merge Conflicts became the new Agentic Bottleneck

Substack post by **[[adam-tornhill]]** ("Code for Humans and Machines"), 2026-06-02. In-window pickup
from the weekly watch. Summarized at `raw/notes/tornhill-merge-conflicts-agentic-bottleneck.md`
(personal Substack — not verbatim).

## What it says

**Agentic coding reinforces engineering fundamentals:** the less humans hand-code, the more
design/architecture and a **socio-technical fit** matter, because coordinating many agents in one
codebase pressures the architecture. **Recurring merge conflicts are a socio-technical signal** — and
it doesn't matter that the "social agent" is now an AI. PR tooling (stacked PRs, queues, smart conflict
resolution) patches symptoms; the root cause is usually *technical* ("no org chart can dig you out of
an architectural blob"). Via Brooks (*Mythical Man-Month*), coordination cost grows quadratically
(n(n−1)/2) and work parallelizes only when tasks are **independent at the problem-domain level** — and
that independence must exist **in the code** (separate features/capabilities → separate homes). Merge
conflicts are "the canary": work misaligned with the architecture that supports it. He cites the leaked
Claude Code repo (`extractToolStats()` accreting git analytics, diffs, telemetry, UX timing) as
architectural convergence; GenAI "delivered on the 10x promise" for merge conflicts via speed.

**Behavioral code analysis** (from *Your Code as a Crime Scene* / *Software Design X-Rays*) makes
coordination cost visible: **hotspots**, **coordination analysis** (contributor congestion), and
**change coupling** (boundaries that fail to support independent evolution). Remedies: split a congested
hotspot along domain boundaries; consolidate a local change-coupling cluster (package cohesion); and the
bad case — change coupling *across* architectural elements, typically caused by **technical** separation
of concerns (thin MVC/MVP layering) instead of domain-communicating building blocks.

## Why it matters here

Extends [[ai-readable-code]] to the **multi-agent / architecture** scale: it's the parallel-work,
[[conways-law]]/[[business-capabilities]] face of the same "good boundaries make agents cheaper" thesis
— here measured by **merge conflicts** rather than tokens. Strong tie to [[locality-of-reference]] and
[[vertical-slice-architecture]] (domain-aligned homes prevent collision) and to
[[unattended-coding-agents]]/[[harness-engineering]] (parallel agents become a serial bottleneck without
it). Notably bridges Tornhill's **behavioral code analysis** lineage to the agent era, complementing his
code-health × token-cost finding ([[tornhill-codescene-unhealthy-code-agentic-token-cost]]) with a
code-health × coordination-cost finding.

## Caveats

Personal Substack; argument-by-example (the Claude Code repo) plus his own tools' framing — persuasive,
not a controlled study.
