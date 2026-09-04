---
title: "Worked Event Model — An Autonomous Coding Factory (multi-agent / harness system)"
type: deliverable
created: 2026-06-15
sources: [dymitruk-event-modeling-future-proof-agents, event-modeled-agent-design, jwilger-agent-skills-event-modeling, anthropic-effective-harnesses-long-running-agents, stripe-minions-one-shot-coding-agents, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-model-is-a-living-spec-always-on-agent, esaa-event-sourcing-for-autonomous-agents, confluent-agentic-event-driven-systems-architecture, rico-fritzsche-autonomous-domain-capabilities-ccc]
tags: [event-modeling, agentic-ai, harness-engineering, worked-example, multi-agent, focus]
---

# Worked Event Model — An Autonomous Coding Factory

This is the KB's **standing gap** made concrete: a *worked* Event Model of a **multi-agent / harness
system itself**, using Event Modeling *the method* (not just event sourcing). The system modeled is an
**autonomous coding factory** — the recurring archetype across [[jwilger-agent-skills-event-modeling]]
(EM output governs an autonomous factory), [[stripe-minions-one-shot-coding-agents]] (Slack-invoked
one-shot agents), [[anthropic-effective-harnesses-long-running-agents]] (initializer-executor across
context windows), and [[dilger-model-is-a-living-spec-always-on-agent]] (board edit → slice → tests →
PR loop). It applies the agent-as-user / agent-as-processor mapping from
[[dymitruk-event-modeling-future-proof-agents]] (see [[event-modeled-agent-design]] and the notation
primer `outputs/denoting-an-agent-in-an-event-model.md`).

> **Visual:** a rendered swimlane diagram of this model is in
> `outputs/worked-event-model-autonomous-coding-factory.mermaid` (command→event→read-model flow across
> all seven slices, including the fail/reject loops back to the Builder).

> **Status / honesty:** this is an **in-house worked model**, an illustration — not an externally
> published artifact. It is internally consistent with the captured sources but has not been built or
> validated against a running system. It closes the "we have no worked example at all" gap; it does not
> substitute for an independent, real-world one.

---

## 1. The system and its scope

**Goal:** turn a human **feature request** into a **merged pull request**, autonomously, with a human
only setting intent and holding a veto. One feature = one **vertical slice** (per
[[vertical-slice-architecture]] / jwilger). The factory must be **legible** ([[agent-legibility]]),
**replayable** (every step is an event), and **governed** (a guardian can veto before merge).

**Consistency boundary (DCB-style, [[dynamic-consistency-boundaries]]):** each *slice* is its own
decision scope — the relevant events are "this slice's history," not a global aggregate. A capability
(per [[rico-fritzsche-autonomous-domain-capabilities-ccc]]) owns its slices.

---

## 2. Swimlanes (actors on top, automation/capabilities below)

Event Modeling puts **roles/actors in the top swimlanes** and **automations/capabilities in the
bottom swimlanes**. Here:

```
 TOP (actors who issue intent)
 ─ Product Owner (human, USER)                — requests features, approves/vetoes
 ─ Reviewer (human or Guardian Agent)         — final gate

 BOTTOM (automations / capability processors)
 ─ Modeling Agent        (PROCESSOR)          — turns a request into model slices + GWT
 ─ Orchestrator          (PROCESSOR, det.)    — schedules ready slices, enforces autonomy policy
 ─ Builder Agent         (PROCESSOR)          — implements one slice (the ralph-loop executor)
 ─ Verification Harness   (PROCESSOR, det.)   — runs GWT acceptance + sensors (lint, tests, mutation)
 ─ Guardian Agent        (PROCESSOR)          — subscribes to results, vetoes/approves merges
 ─ Merge/CI Automation   (PROCESSOR, det.)    — opens PR, merges on green + approval
```

Deterministic processors (Orchestrator, Verification, Merge) are the **guardrails**; the LLM-driven
processors (Modeling, Builder, Guardian) are where nondeterminism lives — the classic harness split
(deterministic loop *around* a nondeterministic model, [[stripe-minions-one-shot-coding-agents]]).

---

## 3. The event-modeled timeline

Notation: `[Command]` (intent, blue) → `(Event)` (fact on the ledger, orange) → `{Read Model}`
(view/projection, green). Actor or processor shown at left. Time flows downward.

### Slice A — Capture intent  *(state-change pattern; agent-as-user)*

```
Product Owner ─ [Request Feature] ─────────────▶ (Feature Requested)
                                                      │
                                                      ▼
                                                 {Backlog View}  ← Modeling Agent reads this
```
The human issues a command exactly like any user. The fact `Feature Requested` lands on the ledger and
projects into a `{Backlog View}`.

### Slice B — Model the feature into slices + GWT  *(automation pattern; Fraktalio/Dilger discovery)*

```
{Backlog View} ─▶ Modeling Agent ─ [Draft Slice Model] ─▶ (Slice Modeled)
                                   [Generate GWT]       ─▶ (Acceptance Defined)
                                                              │
                                                              ▼
                                                        {Ready-Slices View}
```
The Modeling Agent is a **processor**: it reads the backlog, authors the slice's command/event/
read-model design and its **Given-When-Then** acceptance scenarios (per
[[fraktalio-event-modeler-connect-ai-agents-mcp]], where the agent generates GWT-per-command including
business exceptions). `Acceptance Defined` is the **contract** the rest of the factory is held to.

### Slice C — Schedule under an autonomy policy  *(translation + policy; deterministic)*

```
{Ready-Slices View} ─▶ Orchestrator ─ [Assign Slice] ─▶ (Slice Assigned)
        ▲                                                    │
        │ autonomy policy (Conservative│Standard│Full)       ▼
        └──────────────────────────────────────────── {Work-In-Progress View}
```
The Orchestrator applies the **autonomy ladder** ([[autonomy-ladder]], jwilger's Conservative→Standard→
Full): in Conservative mode it emits `Human Approval Requested` before assigning; in Full mode it
assigns directly. Deterministic — no model call.

### Slice D — Build the slice  *(automation pattern; the ralph-loop executor)*

```
{Work-In-Progress View} ─▶ Builder Agent ─ [Implement Slice] ─▶ (Implementation Drafted)
                                          (loops in a clean context window per attempt — ralph-loop)
                                                                      │
                                                                      ▼
                                                              {Diff / Progress Ledger}
```
The Builder is the **executor** across context windows ([[anthropic-effective-harnesses-long-running-agents]]):
it loads the slice's `event_model_root` as context, writes code, and appends progress as events. The
`{Diff / Progress Ledger}` *is* the append-only working memory the next session replays — event
sourcing applied to the agent's own state (the Thread-4↔1 rhyme in [[overview]]).

### Slice E — Verify against the contract  *(automation pattern; deterministic sensors)*

```
(Implementation Drafted) ─▶ Verification Harness ─ [Run Acceptance] ─▶ (Checks Passed)
                                                                    └▶ (Checks Failed)
                                                                              │
                                  ┌───────────────────────────────────────────┘
                                  ▼
                          {Slice Health View}     ← Builder & Guardian both read this
```
The harness runs the **GWT scenarios as TDD gates** plus computational sensors — lint, dependency
rules, tests, **mutation testing** ([[mutation-testing]], [[fowler-bockeler-maintainability-sensors]]).
`Checks Failed` re-enters the Builder loop (Slice D); the failure event is the feedback signal. This is
the "treat every failure as a permanent fix" loop of [[harness-engineering]].

### Slice F — Govern the merge  *(automation pattern; guardian-as-subscriber, the veto)*

```
(Checks Passed) ─▶ Guardian Agent ─ [Review Slice] ─▶ (Slice Approved)
                                                    └▶ (Slice Rejected) ─▶ back to Slice D
                                                            │
                                                            ▼
                                                     {Merge Queue View}
```
The Guardian is a **subscriber that vetoes before commit** — the [[guardian-agents]] pattern and the
Confluent "agents subscribe→reason→publish, never call each other directly"
([[confluent-agentic-event-driven-systems-architecture]]) closed loop. It can only act on facts already
on the ledger (`Checks Passed`), and its decision is itself an event.

### Slice G — Merge  *(state-change pattern; deterministic)*

```
{Merge Queue View} ─▶ Merge/CI Automation ─ [Open PR] ─▶ (PR Opened)
                                            [Merge]   ─▶ (PR Merged)
                                                              │
                                                              ▼
                                                        {Backlog View}  (slice marked done)
```
Closing the loop: `PR Merged` updates the same `{Backlog View}` Slice A started from. The Product Owner
sees the feature delivered without having touched anything between request and review.

---

## 4. The four Event Modeling patterns, located in the factory

| EM pattern | Where it appears here |
| --- | --- |
| **State change** (command → event) | Request Feature→Feature Requested; Merge→PR Merged (Slices A, G) |
| **State view** (events → read model) | {Backlog}, {Ready-Slices}, {WIP}, {Slice Health}, {Merge Queue} |
| **Translation** (external → events) | Verification harness turning CI/test output into Checks Passed/Failed; MCP tools turning repo/tool state into events ([[model-context-protocol]]) |
| **Automation** (processor works a view → issues commands) | Modeling, Orchestrator, Builder, Guardian, Merge — every bottom-swimlane agent |

Every agent is expressed in the **same vocabulary** as a human user — no new notation, exactly
Dymitruk's claim. The only distinction is *which* swimlane and whether the processor is deterministic.

---

## 5. Specifying behavior — Given-When-Then per step

The GWT scenarios authored in Slice B are the machine-checkable contract (jwilger's TDD gates). Examples:

> **Build slice**
> **Given** a slice is in `{Work-In-Progress View}` with `Acceptance Defined`
> **When** the Builder issues `Implement Slice`
> **Then** an `Implementation Drafted` event is appended with a diff reference

> **Guardian veto**
> **Given** a slice has `Checks Passed`
> **When** the Guardian issues `Review Slice` and finds a policy violation
> **Then** a `Slice Rejected` event is appended and the slice returns to the Builder — **no** `PR Merged`
> event may exist for a slice without a preceding `Slice Approved`

That last invariant is a **DCB-style conditional-append rule** ([[dynamic-consistency-boundaries]]):
`Merge` may append `PR Merged` *iff* the slice's relevant event stream contains `Slice Approved` and no
later `Slice Rejected`. The consistency boundary is the slice, not a global aggregate.

---

## 6. Harness-thread mapping (why this is also a harness design)

| Event Modeling construct | Harness analog |
| --- | --- |
| Event ledger (all the orange facts) | the append-only progress record the next session replays ([[long-running-agents]]) |
| {Diff / Progress Ledger} read model | `claude-progress.txt` + git history + feature-list JSON |
| Acceptance Defined (GWT) | feature-list specs + self-verification gates ([[feedforward-and-feedback-controls]]) |
| Verification Harness sensors | lint / dependency rules / tests / mutation ([[mutation-testing]]) |
| Orchestrator autonomy policy | the steering loop / autonomy dial ([[autonomy-ladder]]) |
| Guardian veto event | governance + audit trail ([[agent-governance]]) — the log *is* the audit |
| Swimlane = capability | agent ownership boundary (RPU, [[rico-fritzsche-autonomous-domain-capabilities-ccc]]) |

---

## 7. What this demonstrates — and what it doesn't

**Demonstrates:** Event Modeling the *method* can express a whole multi-agent/harness system on one
timeline; agents drop into existing user/processor roles; GWT gives executable per-step contracts;
guardian governance is just a subscriber appending veto events; the autonomy ladder is an Orchestrator
policy; and DCB-style conditional append enforces the safety invariant. It connects every focus thread
(EM × agents, event sourcing/DCB/CQRS/VSA, business capabilities, harness engineering) in one artifact.

**Doesn't:** prove the design works in practice (untested), and remains an *in-house* example — the KB
still lacks an **independent, published** worked event model of a multi-agent system. The closest
external corroboration stays [[esaa-event-sourcing-for-autonomous-agents]] (intentions→effects via a
deterministic orchestrator — the same shape, one substrate-level remove since it uses event *sourcing*,
not the method).

---

*Sources: [[dymitruk-event-modeling-future-proof-agents]] · [[event-modeled-agent-design]] ·
[[jwilger-agent-skills-event-modeling]] · [[anthropic-effective-harnesses-long-running-agents]] ·
[[stripe-minions-one-shot-coding-agents]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] ·
[[dilger-model-is-a-living-spec-always-on-agent]] · [[esaa-event-sourcing-for-autonomous-agents]] ·
[[confluent-agentic-event-driven-systems-architecture]] · [[rico-fritzsche-autonomous-domain-capabilities-ccc]].
Companion: `outputs/denoting-an-agent-in-an-event-model.md`.*
