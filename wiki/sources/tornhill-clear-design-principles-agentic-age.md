---
title: "Adam Tornhill — CLEAR: Software Design Principles for the Agentic Age"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [tornhill-clear-design-principles-agentic-age]
raw_file: [raw/notes/tornhill-clear-design-principles.md]
tags: [agentic-coding, code-health, agent-legibility, ai-readable-code, harness, focus]
---

# Adam Tornhill — CLEAR: Software Design Principles for the Agentic Age

Substack essay by **[[adam-tornhill]]** ("Code for Humans and Machines"), 2026-06-09. Summarized at
`raw/notes/tornhill-clear-design-principles.md` (not captured verbatim — personal publication).

## What it says

Tornhill proposes **CLEAR**, a small set of design principles for **AI-readable code** — code that is
*safe for agents to evolve and cheap for humans to verify*. His premise: SOLID optimized for human
maintainability, but agentic development creates a new bottleneck he calls **reconstruction work** —
an agent infers structure from local context via search/tools/statistical guesswork, so code can be
perfectly SOLID yet still hard for an agent to reason about when intent, ownership, and change
boundaries are implicit. The unifying goal is to **limit the blast radius** of a change.

The five principles:
- **C — Conceptual alignment** — align behavior with the domain concepts it belongs to.
- **L — Local reasoning** — enable reasoning from local context, for humans and agents.
- **E — Explicit intent** — make purpose visible *structurally*.
- **A — Avoid search luck** — express similar problems with consistent structures/patterns/extension points.
- **R — Reduce the edit surface** — design to contain change by making boundaries explicit.

Framed as *principles, not rules* (design must stay mouldable to the domain), and as a re-emphasis of
classics (Tell Don't Ask, Law of Demeter, DDD, Parnas's information hiding) that matter *more* under
agentic coding — not novelty for its own sake.

## Why it matters here

The flagship articulation of [[ai-readable-code]] and a named, memorable take on the [[agent-legibility]] thesis from the code-health side: it turns
"optimize the repo for the agent's understanding" into five concrete levers and explicitly ties them to
**reconstruction work / token cost**, connecting Tornhill's earlier
[[tornhill-codescene-unhealthy-code-agentic-token-cost|code-health × token-spend]] finding to design
guidance. Strong overlap with [[locality-of-reference]] (L, R),
[[fritzsche-functional-core-imperative-shell-agentic-coding|Fritzsche]] (repo shape instructs the
agent), [[miller-codebase-is-the-prompt-vertical-slices-ai|Miller]] ("codebase is the prompt"),
[[vlad-khononov|Khononov's]] modularity/coupling argument, and the [[harness-engineering]] thread. Sits
on his new personal primary, the **"Code for Humans and Machines"** Substack (now in `watch-config`).

## Caveats

Personal Substack; self-reported from his own agentic-coding practice. "AR" principles and deeper
"C" guidance were promised as upcoming posts (this is an evolving framework).
