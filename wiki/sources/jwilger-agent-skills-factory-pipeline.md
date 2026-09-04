---
title: "jwilger/agent-skills — event model as the spec that drives the factory pipeline"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [jwilger-agent-skills-factory-pipeline]
raw_file: [raw/articles/jwilger-agent-skills-event-modeling-factory-pipeline.md]
tags: [event-modeling, agentic-ai, agentic-coding, software-factory, harness, skills, tdd, spec-driven-development, given-when-then, focus]
---

# jwilger/agent-skills — event model as the spec that drives the factory pipeline

A second, later verbatim capture of **[[john-wilger]]**'s `jwilger/agent-skills` README (CC0-1.0;
v4.1 factory pipeline; `domain-modeling` skill listed as of 2026-02-12). Companion to the earlier
capture [[jwilger-agent-skills-event-modeling]] — this one is read for a single, sharper claim: in
this repo **[[event-modeling]] is the *upstream, human-authored spec* that constrains and drives a
whole team of coding agents**, the exact *opposite direction of fit* from
[[dymitruk-event-modeling-future-proof-agents|Dymitruk's]] "agents as users/processors inside a
model" and from the "AI assists modeling" framing of [[qlerify-event-modeling-tool-ai|Qlerify]] /
[[fraktalio-event-modeler-connect-ai-agents-mcp|Fraktalio]]. Raw capture:
`raw/articles/jwilger-agent-skills-event-modeling-factory-pipeline.md`.

## The one thing this capture adds

Direction of fit. Most [[event-modeled-agent-design]] sources point *into* the model — an agent
*authors* the model, or is *modeled as* a user/processor on a swimlane. Here the arrow reverses:
the event model is written by humans **first**, and its output is what a **[[software-factory|factory]]
of autonomous coding agents** is measured against. Event Modeling is not a thing the agents do; it is
the **spec that governs the agents**. This makes the repo the cleanest KB instance of "EM as the
human-in-the-loop contract at the top of the autonomy ladder."

## How the coupling works (v4.0 → v4.1)

The **Tier 4 factory pipeline** (`pipeline`, `ci-integration`, `factory-review`) automates build+ship
while keeping humans on plan+review, in three phases:

1. **Human-driven (understand + decide).** The team facilitates **event modeling**, domain modeling,
   and vertical-slice definition via a Robert's-Rules consensus protocol; **the human approves the plan.**
2. **Agent-autonomous (build + ship).** Each slice runs *decompose → TDD pair → full-team code review →
   address feedback → mutation test → push + CI → merge or escalate*, with **quality gates replacing
   human approval gates.** Decisions are classified gate-resolvable / judgment-required / blocking.
3. **Human review (inspect + tune).** The human reviews shipped work, batched judgment calls, and the
   audit trail; feedback feeds the next planning cycle.

v4.1 wires the event model **directly into execution** — the mechanics that make "EM is the spec" literal:

- **Enriched slice context** — each slice carries a `context` block with an **event-model source path**,
  boundary annotations on its [[given-when-then|GWT]] scenarios, related slices, and referenced domain
  types / UI components.
- **Pre-implementation context checklist** — before dispatching each TDD pair the pipeline gathers
  architecture docs, glossary, domain types, and **event model context**, passed as `project_references`
  (with a recommended `event_model_root: docs/event-model/`) and `slice_context`.
- **Boundary-level acceptance-test enforcement** — the TDD gate rejects tests that only call internal
  functions; a [[given-when-then|GWT]] scenario must exercise an external boundary (HTTP/CLI/queue/
  websocket/Playwright UI/manual), recorded as `boundary_type` + `boundary_evidence`.
- **Enqueue validation** — a slice **missing a GWT scenario with a `boundary` field is rejected**; an
  incomplete event model (missing GWT, undefined automations) **blocks slice decomposition**. The model's
  completeness is a hard gate on the agents.
- **Git-worktree isolation** — at Full autonomy, parallel slices run in isolated worktrees at
  `.factory/worktrees/<slice-id>` (falls back to sequential).

## Progressive autonomy — the ladder, restated

**Conservative** (agent proposes, human approves each slice) → **Standard** (agent builds, human reviews
each batch, rework autonomous up to 2 cycles/gate) → **Full** (agent selects pairs, orders slices,
optimizes on factory memory; human reviews completed batches only). A concrete instance of the
[[autonomy-ladder]] where **gate quality is what earns the next rung** — the same "back pressure"
governing rule the [[software-factory]] page states.

## Why it matters here

- It is a **worked [[software-factory]]** in the [[event-modeled-agent-design]] key: many harnessed TDD
  loops fed by a **slice queue** and drained through **GWT gates + mutation + CI + a human review gate** —
  "an org chart made of loops" whose work-items and oracles come straight out of an event model.
- It is the load-bearing evidence for the [[given-when-then|GWT]]-as-acceptance-gate claim: GWT is
  simultaneously the slice's spec *and* the pipeline's machine-checkable pass/fail oracle.
- Caveat unchanged from the first capture: one developer's open-source repo (small, actively evolving),
  and the **event-model artifact itself is assumed input** (`docs/event-model/`) rather than shown — so a
  fully worked, published multi-agent event model remains the open want.

## Links

Entities: [[john-wilger]]. Concepts: [[event-modeling]], [[event-modeled-agent-design]],
[[software-factory]], [[given-when-then]], [[agentic-coding]], [[harness-engineering]],
[[unattended-coding-agents]], [[autonomy-ladder]], [[loop-engineering]], [[mutation-testing]],
[[vertical-slice-architecture]].
Related sources: [[jwilger-agent-skills-event-modeling]] (the first capture),
[[proophboard-skills-ai-agent-event-modeling]], [[fraktalio-event-modeler-connect-ai-agents-mcp]],
[[dymitruk-event-modeling-future-proof-agents]], [[dilger-event-modeling-agent-harness]],
[[addyosmani-software-factories-light-and-dark]], [[stripe-minions-one-shot-coding-agents]].

_Raw source: `raw/articles/jwilger-agent-skills-event-modeling-factory-pipeline.md`._
