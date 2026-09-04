---
title: "Dilger — Local-LLM distributed agent setup for Event Modeling"
type: source
created: 2026-07-18
updated: 2026-07-18
sources: [dilger-local-llm-distributed-agent-setup-event-modeling]
raw_file: [raw/notes/dilger-local-llm-distributed-agent-setup-event-modeling.md]
tags: [event-modeling, agentic-coding, long-running-agents, ralph-loop, vertical-slice-architecture, focus]
---

# Dilger — Local-LLM distributed agent setup for Event Modeling

Source: [[martin-dilger]], two-part LinkedIn series *"How I use Local-LLMs to build software systems"* +
*"what's actually running under the hood"*, **2026-07-02**. Raw capture:
`raw/notes/dilger-local-llm-distributed-agent-setup-event-modeling.md`. A concrete **implementation
report** of the always-on, board-driven build/modeling factory he had described in the abstract — it puts
real hardware, models, and a synchronization mechanism behind
[[dilger-event-modeling-agent-harness|the Event Modeling Agent Harness]] and
[[dilger-model-is-a-living-spec-always-on-agent|the model-as-living-spec]].

## Key points

- **The hardware/model stack.** Three **Asus GX10** boxes in the office, running **independently — no
  clustering**. Models: **Gemma4** (~60 tok/s) and **Qwen3.6:27B** (~30 tok/s) served via **Ollama**;
  harness is **Claude Code or OpenCode** (+ one Hermes agent). "Not superfast, but good enough… it all
  happens in the background, nobody cares." Claude Code adds ~1s/loop-iteration overhead (negligible).
- **6–10 agents in [[ralph-loop|ralph-loops]] 24/7**, most building, 1–2 for modeling support, spread
  across machines. "Agents only wake up when there's work. Otherwise they silently wait — no cost, no
  tokens."
- **The claim-lock synchronization trick (the core mechanism).** Every project is tied to **one Board**;
  the moment a slice moves to **"Planned," exactly one agent claims it and moves it to "In Progress" —
  locked.** Any other agent sees it's taken and picks another. "**No collisions… no merge conflicts, no
  coupling hell.**" Location-independent — an agent may run locally or in the office; "I couldn't tell from
  where, and typically I don't care."
- **The [[vertical-slice-architecture|slice]] is the unit of work.** Agents work slices in parallel
  precisely because slices are **decoupled** — "they don't have to know anything from each other." Move a
  slice **"Done" → "Planned"** and an agent **reconciles code to the spec** (adds specs, changes
  projections, adds/removes fields).
- **Board events spawn tasks.** A comment for an agent → a new **Modeling Task**; someone **starts talking
  → live voice-to-text** transcription triggers a Modeling Task ("no one touches a keyboard").
- **Self-provisioning Kits.** Each project has a **Build-Kit** and **Modeling-Kit** matched to its stack,
  connected live to the Eventmodelers platform through a real-time agent; new projects **provision
  themselves** ("no setup ceremony… model to running code in minutes"), Kits ship **"batteries included"**
  with opinionated, production-ready per-stack skills on a **blueprint architecture**.
- **The mindset shift + the thesis.** "At some point you stop thinking about the code… focus is completely
  on the **Spec-Side** — specifying *what*, not *how*." He credits the **"triplet of flexible
  architectures" = [[event-modeling|Event Modeling]] + [[event-sourcing|Event Sourcing]] +
  [[vertical-slice-architecture|Slice-Based Architecture]]**. "The real work happened long before —
  modeling and decomposing the software into slices is what enables this."

## Why it matters

The most concrete evidence to date behind Dilger's [[event-modeled-agent-design|event-modeled agent]]
factory claims: the earlier posts asserted a 24/7 slice-driven harness; this names the **hardware (3× Asus
GX10), the models (Gemma4 / Qwen3.6:27B on Ollama), the harness (Claude Code / OpenCode), and — most
valuably — the concurrency mechanism**: a board-level **claim-lock on the slice** ("Planned" → one claimant
→ "In Progress") that makes parallel multi-agent work collision-free *without* code-level coordination,
because the [[vertical-slice-architecture|slices are decoupled by design]]. That closes a gap the KB's own
worked models only assumed (a DCB-style conditional-append guard) with a real, running instance. It also
sharpens the **local-model economics** angle (cheap on-prem models are "good enough" for background work;
idle = zero tokens). Caveat: a self-reported vendor demo (promotes the Eventmodelers platform / Build-Kits);
no external verification, no failure/quality data, single practitioner.

## Links

[[martin-dilger]] · [[event-modeled-agent-design]] · [[dilger-event-modeling-agent-harness]] ·
[[dilger-model-is-a-living-spec-always-on-agent]] · [[event-modeling]] · [[event-sourcing]] ·
[[vertical-slice-architecture]] · [[ralph-loop]] · [[long-running-agents]] · [[unattended-coding-agents]] ·
[[eventmodelers-ai]]

_Source: [[dilger-local-llm-distributed-agent-setup-event-modeling]] (raw: `raw/notes/dilger-local-llm-distributed-agent-setup-event-modeling.md`)._
