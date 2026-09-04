---
title: "Source: The Event Modeling and Event Sourcing Podcast (Eps 1–46)"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [event-modeling-event-sourcing-podcast]
raw_file: [raw/notes/event-modeling-event-sourcing-podcast-show-notes.md]
tags: [event-modeling, event-sourcing, podcast, agentic-coding, dcb, vertical-slices, source]
---

# Source: The Event Modeling and Event Sourcing Podcast (Eps 1–46)

**Raw file:** `raw/notes/event-modeling-event-sourcing-podcast-show-notes.md`
**Origin:** [podcast.eventmodeling.org](https://podcast.eventmodeling.org/) · channel
[youtube.com/@eventdrivenpodcast](https://www.youtube.com/@eventdrivenpodcast) ·
[playlist](https://www.youtube.com/playlist?list=PLYNJUeYuZDAP0luNOf5MZAbnzPWRCnZyp)
**Hosts:** [[adam-dymitruk]] ([[adaptech-group]]) & [[martin-dilger]] ([[nebulit]]) ·
**Run:** 2024-11-04 → 2026-04-27 (Season Two from Ep 23) · **Captured:** 2026-06-17

> **Provenance / caveat.** Dannie asked to *transcribe* the videos and ingest them. Full transcripts
> were **not retrievable** — YouTube's bot-protection blocked transcript access from the automated
> browser (transcript API `failedPrecondition`; UI transcript panel hangs; caption fetch empty) and the
> sandbox can't reach YouTube/MP3s. This page is therefore built on the **published show notes**
> (verbatim in the raw file), **not** the spoken content. Eps 32–46 carry an AI-generated Summary +
> timestamped chapters (from the RSS feed); Eps 1–31 carry shorter notes (from the episode pages). Treat
> episode-level claims as *show-note-level*, not verified against audio.

## What it is

A weekly conversational podcast in which Event Modeling's creator [[adam-dymitruk]] and book author /
[[eventmodelers-ai]] founder [[martin-dilger]] talk through [[event-modeling]] and [[event-sourcing]]
practice — workshop debriefs, design arguments, tooling, and (increasingly through 2025–26) how AI /
[[agentic-coding]] changes the picture. It is the **running practitioner commentary** behind the more
polished sources already in this KB (Dilger's posts/talks, Dymitruk's interviews) — same two people,
thinking out loud weekly.

## Recurring themes (the through-lines across 46 episodes)

- **Kill / shrink the aggregate.** The very first episodes are literally "Destroying the Aggregate"
  (Eps 1–2); the thread resurfaces as [[dynamic-consistency-boundaries|DCB]] vs. aggregate coupling
  (Eps 18, 38, 41, 43). Consistent stance: don't reuse models across workflows; coupling is the enemy.
- **Simplicity as the goal.** "Keeping things simple" (Ep 4), "Avoiding the Patterns Soup" (Ep 10),
  "Simplicity is the Goal" (Ep 21), "Simplicity Builds Confidence" (Ep 33). Remove sagas, prefer
  to-do lists, minimal infrastructure, pure command handlers.
- **[[vertical-slice-architecture|Slices]] as the unit of work.** "Slice, slice baby!" (Ep 12),
  "Learning Using Slices" (Ep 20), "Slicing the Solution" (Ep 34), vertical slices vs CRUD (Ep 26).
  Slices map to Event Modeling slices and become the lifecycle/billing unit (definition-of-ready,
  pay-per-slice).
- **[[given-when-then|Given-When-Then]] specifications.** GWT on a timeline (Eps 3, 7), and as the
  testing backbone that recurs into the agent-harness framing (Ep 24, Event Modeling 2.0).
- **Sagas → to-do lists.** Removing sagas (Ep 4), simplifying sagas (Ep 15), the to-do-list pattern
  (Eps 10, 21) — Dymitruk's standing claim that long-running processes are better modeled as a
  reactive to-do list than a saga.
- **[[event-versioning-and-upcasting|Schema migration / event versioning]].** "A Case Against
  Upcasters" (Ep 5, crediting [[yordis-prieto]]), "Version 2 of Everything: The Looming Schema
  Migration Nightmare" (Ep 37), and event versioning/upcasting (Ep 46).
- **AI / [[agentic-coding]] (the dominant Season-Two arc).** From "AI Nightmares" (Ep 14, messy AI
  output) to "Event Modeling 2.0 / Cheap AI Is All You Need" (Ep 24), the [[ralph-loop]] coding
  experiment (Eps 35, 37), reverse-engineering legacy code with AI (Ep 41), and "the model is the new
  programming language" (Eps 26, 37). The podcast is where Dilger/Dymitruk's
  [[event-modeled-agent-design]] thesis is worked out conversationally.
- **[[vibe-modeling|Vibe coding → vibe modeling]].** Ep 19 coins the contrast; Ep 30 has Adam's
  Yahtzee-with-LLMs experiment showing AI breaks scope without the model's structure.
- **Event sourcing as old/foundational, not exotic.** "Event Sourcing Predates Anything in Computing"
  (Ep 39); the accounting-ledger analogy; "SQL is an Anti-Pattern" (Ep 22); Git as an event store
  (Eps 26, 40).
- **Business / consulting model.** Fixed-price "pay-per-slice" delivery, "Tech Saves You From
  Inflation" (Ep 30), workshops as the main go-to-market, and (Ep 23) the launch of a new event
  modeling company + push for tool **standardization** ([[eventmodelers-ai]]).

## Notable episodes (anchors)

- **Ep 1–2 "Destroying the Aggregate"** — the founding argument; sets up GWT/BDD and source-control
  (branch-per-feature vs trunk) discussions.
- **Ep 5 "A Case Against Upcasters"** — early statement of the anti-upcaster / no-model-reuse stance
  ([[event-versioning-and-upcasting]]), credited to [[yordis-prieto]].
- **Ep 18 "The Future of Event Sourcing"** — first heavy [[dynamic-consistency-boundaries|DCB]]
  treatment; commands-as-objects; AI integration mooted.
- **Ep 24 "Cheap AI Is All You Need"** — introduces **Event Modeling 2.0** (sharper *what* vs *how*,
  information-flow focus, GWT/refinements/projections), aimed at both devs and business.
- **Ep 26 "A New Programming Language"** — Git ≅ event sourcing (immutability), vertical slices vs
  CRUD, model-as-language.
- **Ep 37 "Version 2 of Everything"** — the schema-migration "nightmare" + the [[ralph-loop]] as an
  AI coding loop; "event modeling as the new programming language."
- **Ep 39 "Event Sourcing Predates Anything in Computing"** — slice-based architecture, event
  tagging/indexing debate, accounting framing.

## How it fits the KB

This podcast is the **conversational primary** under [[adam-dymitruk]] and [[martin-dilger]]'s
already-captured material. It corroborates and dates the design substrate of [[event-modeling]] /
[[event-sourcing]] (Threads 1–2 and 6 in [[overview]]) and the [[event-modeled-agent-design]] focus
from the practitioners' own mouths. **Limits:** show-notes only (no verified transcript); AI-generated
summaries are lossy and occasionally mislabel terms (e.g. "DCB" glossed as "Domain Command Bus" in the
Ep 38/43 notes, where the hosts mean [[dynamic-consistency-boundaries|Dynamic Consistency Boundaries]]);
heavy overlap/repetition between episodes; and much of the AI commentary is opinion, not evidence.

## Per-episode index

S1 (2024–2025): 1 Destroying the Aggregate · 2 Destroying the Aggregate pt2 · 3 AI, GWTs on a timeline,
Security · 4 Keeping things simple · 5 A Case Against Upcasters · 6 Event Modeling Scope · 7 Pure
Command Handlers & Sparse Timelines · 8 Event Sourcing Frameworks · 9 Maintaining Event Models · 10
Avoiding the Patterns Soup · 11 No Code Reviews · 12 Slice, slice baby! · 13 Stop. Collaborate and
Listen! · 14 AI Nightmares and Expert Help · 15 Skills Issues and Simplifying Sagas · 16 Varieties of
APIs and millions of events · 17 Too many events! · 18 The Future of Event Sourcing · 19 Vibe Modeling,
Event Models for the C-Suite · 20 Learning Using Slices.
S2 (2025–2026): 21 Simplicity is the Goal · 22 SQL is an Anti-Pattern · 23 AI Takes Your Job (S2
kickoff) · 24 Cheap AI Is All You Need (Event Modeling 2.0) · 25 Conceptual Structure of Code · 26 A
New Programming Language · 27 AST: An Endangered Species · 28 Scientific Proof That Event Modeling
Works · 29 Leading Your Thoughts · 30 Tech Saves You From Inflation · 31 The Issue Trackers Are The
Issue · 32 2026 is the Year of the Event Modeling Desktop! · 33 Simplicity Builds Confidence · 34
Slicing the Solution · 35 Programming Languages Don't Matter · 36 Getting Left Behind · 37 Version 2 of
Everything · 38 Co-Evolution In Software · 39 Event Sourcing Predates Anything in Computing · 40
Specification Driven Development, the New Thing from 2006 · 41 Reverse Engineering Using Event
Modeling · 42 Who Trusts Event Modeling with Billion Dollar Projects · 43 Working Without Electricity ·
44 Hermes Crab · 45 Mind-Reading as a Job Description · 46 Power Lines in Sim City.

## Touches

[[event-modeling-event-sourcing-podcast]] · [[adam-dymitruk]] · [[martin-dilger]] · [[adaptech-group]] ·
[[nebulit]] · [[eventmodelers-ai]] · [[event-modeling]] · [[event-sourcing]] · [[cqrs]] ·
[[dynamic-consistency-boundaries]] · [[vertical-slice-architecture]] · [[given-when-then]] ·
[[event-versioning-and-upcasting]] · [[vibe-modeling]] · [[ralph-loop]] · [[spec-driven-development]] ·
[[event-storming]] · [[domain-driven-design]] · [[agentic-coding]] · [[event-modeled-agent-design]] ·
[[yordis-prieto]]
