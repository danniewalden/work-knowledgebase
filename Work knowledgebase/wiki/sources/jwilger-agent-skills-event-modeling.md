---
title: "jwilger/agent-skills — event-modeling skill + factory pipeline"
type: source
created: 2026-06-13
updated: 2026-06-13
sources: [jwilger-agent-skills-event-modeling]
tags: [event-modeling, agentic-ai, agentic-coding, harness, skills, tdd, spec-driven-development, focus]
---

# jwilger/agent-skills — event-modeling skill + factory pipeline

GitHub repository by **[[john-wilger]]** (CC0-1.0; v4.1, 145 commits, 51 tags — small but
actively developed). A set of **portable Agent Skills** that teach *any* AI coding agent a
disciplined SDLC, harness-agnostic (Claude Code, Codex, Cursor/Windsurf, OpenCode, Goose, Amp,
Aider). The strongest evidence yet for [[event-modeled-agent-design]]: here [[event-modeling]] is
the human-driven *design* step whose **output — vertical slices + Given-When-Then scenarios —
becomes the machine-checkable contract** an autonomous multi-agent "factory" builds against. Raw
capture: `raw/articles/jwilger-agent-skills-event-modeling.md`.

## What it is

Skills are portable `SKILL.md` documents conforming to the [Agent Skills spec](https://agentskills.io/specification)
— the same pattern as [[prooph-board]]'s skills ([[proophboard-skills-ai-agent-event-modeling]]) and
the [[claude-agent-sdk]]/Claude Code skills model. They are the single source of truth for practice;
enforcement is **proportional to harness capability** (structural on harnesses with subagents,
advisory-by-convention elsewhere, optional mechanical **hooks** on Claude Code that block edits per
TDD phase). The repo spans a tiered inventory: a `bootstrap` entry point; core process skills (`tdd`,
`domain-modeling`, `code-review`, `architecture-decisions`, **`event-modeling`**, `ticket-triage`);
team workflows (`ensemble-team`, `task-management`); and a **factory pipeline** (`pipeline`,
`ci-integration`, `factory-review`).

## The `event-modeling` skill

The "understand"-phase skill: **discovery, swimlanes, GWT scenarios, model validation.** It activates
on phrases like "model this workflow", "write GWT scenarios", "decompose into slices"; covers
discovering domain actors, identifying automations, mapping integrations; and **decomposes workflows
into vertical slices**, one slice per pattern — *State Change* (Command → Event) and *State View*
(Events → Read Model). Paired with the `tdd` skill, the **GWT scenarios become the acceptance tests
that enforce the model**. Its stated value is *communication* — "a structured conversation that
surfaces hidden domain knowledge and creates shared understanding between humans and agents **before
any code is written**." This is [[event-modeling]]'s own vocabulary (commands, events, read models,
[[cqrs]], Automation, GWT, [[conways-law|Conway's Law]] swimlanes) restated as agent instructions.

## The factory pipeline (why it matters here)

A **three-phase workflow** with a deliberate human/agent boundary:

1. **Human-driven (understand + decide)** — the team helps with event modeling, domain modeling, and
   slice definition, but the human approves the plan.
2. **Agent-autonomous (build + ship)** — the pipeline runs each slice through *decompose → TDD pair →
   full-team code review → mutation test → push + CI → merge or escalate*, with **quality gates
   replacing human approval gates**. Decisions are classified gate-resolvable / judgment-required /
   blocking.
3. **Human review (inspect + tune)** — the human reviews shipped work and the audit trail; feedback
   feeds the next cycle.

v4.1 ties the event model directly into execution: a **pre-implementation context checklist** loads
the `event_model_root` and glossary before dispatching each TDD pair; **enriched slice context**
carries the event-model source path and boundary annotations on each GWT scenario; and the **TDD gate
rejects acceptance tests that don't exercise an external boundary** (HTTP/CLI/queue/websocket/UI).
Full-autonomy runs isolate parallel slices in git worktrees.

## Why it matters — closes part of the standing gap

This is the closest thing the KB has to a **worked example** of [[event-modeled-agent-design]]: not an
agent *modeled as* a user/processor ([[dymitruk-event-modeling-future-proof-agents]]), nor an agent
that merely *practises* modeling ([[proophboard-skills-ai-agent-event-modeling]]), but a full pipeline
where the **event model is the contract that governs autonomous agents** — slices schedule the work,
GWT scenarios are the gates, the audit trail is the ledger. It is also a concrete instance of the
[[autonomy-ladder]]: its Conservative / Standard / Full levels map onto Levels 2→4, with humans
climbing the ladder as gate quality proves out. It sits squarely on the **Thread 1 ↔ Thread 4** seam
— Event Modeling meeting [[harness-engineering]] / [[unattended-coding-agents]] / [[agentic-coding]].
Caveat: it's one developer's open-source project (≈2 stars), not a production case study, and the
*event model artifact itself* is assumed input (`docs/event-model/`) rather than shown — so a fully
worked multi-agent event model remains the open want.

## Links

Entities: [[john-wilger]]. Concepts: [[event-modeling]], [[event-modeled-agent-design]],
[[agentic-coding]], [[harness-engineering]], [[agent-harness]], [[unattended-coding-agents]],
[[autonomy-ladder]], [[cqrs]], [[agentic-ai]], [[claude-agent-sdk]].
Related sources: [[proophboard-skills-ai-agent-event-modeling]], [[qlerify-event-modeling-tool-ai]],
[[dymitruk-event-modeling-future-proof-agents]], [[esaa-event-sourcing-for-autonomous-agents]],
[[stripe-minions-one-shot-coding-agents]], [[anthropic-effective-harnesses-long-running-agents]].
