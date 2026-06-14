---
title: Event Modeling
type: concept
created: 2026-06-11
updated: 2026-06-14
sources: [eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, goeleven-event-model-to-code-series]
tags: [event-modeling, methodology, event-sourcing, software-design, ddd]
---

# Event Modeling

A method (from [[adam-dymitruk]], developed at [[adaptech-group]]) for designing
information systems by describing them as a **timeline of events** rather than as current
state. The output is a **blueprint** — read like a story — that follows every field of
information from the UI, into storage, and back out to a screen or report. Deliberately
minimal: **3 building blocks, 4 patterns, 2 ideas**, produced in a **7-step workshop**.

## The 3 building blocks

- **Events** — state-changing facts placed on the timeline ("what was stored"). Only
  state changes count; "user viewed the calendar" is not an event.
- **Commands** — a user's *intention* to change state (vs. blindly saving form data).
  Drives a "command-based UI" and clear transactional boundaries.
- **Views / read models** — how the system *informs* the user; updated as events are
  stored. **Passive** — a view cannot reject an event after it's been stored.

Wireframes/mockups sit across the top in **swimlanes** (one per user or system).

## The 4 patterns

Command and View (above), plus two **integration** patterns:

- **Translation** — convert external data into locally meaningful events (e.g. GPS coords
  → "Guest left hotel").
- **Automation** — a processor works a "todo list," issuing commands to external systems
  and storing their replies back as events (queues, reactive, or even manual lists).

Specifications are written **Given-When-Then** (≈ Arrange-Act-Assert), each tied to
*exactly one* command or view.

## The 7-step workshop

1. Brainstorm events → 2. Plot them into an ordered story → 3. Storyboard with wireframes
→ 4. Identify inputs (commands) → 5. Identify outputs (views) → 6. Apply [[conways-law|Conway's Law]]
(organize events into team-owned swimlanes) → 7. Elaborate scenarios. Ends with a
**completeness check**: every field has an origin and a destination.

## Why it matters — the flat cost curve

Because explicit **contracts** isolate each workflow step, building one step doesn't ripple
into others, so **average feature cost stays flat** as the system grows. Consequences:
features can be built in any order, velocity can be measured empirically, and work can be
scoped, reprioritized, or even **fixed-price** contracted without breaking estimates. Also
aids **security** (shows where/when sensitive data crosses boundaries) and **legacy
migration** (freeze the old system; add a side-car via the translate pattern + a Y-valve).

## Relationships

- Evolved from [[event-storming]] (kept the workshop format); builds on [[greg-young]]'s
  CQRS/ES long-running process specs. See [[cqrs]].
- Pairs naturally with [[event-sourcing]] — the blueprint defines what each step leaves on
  the ledger vs. what it projects for a screen.
- Complements [[domain-driven-design]] (swimlanes mirror bounded contexts / subsystems) and
  leans on the [[open-closed-principle]] (each state transition independently extendable).
- Cross-domain echo: the same append-only-ledger logic underpins [[event-sourcing]] as the
  "backbone" of [[agentic-ai]] ([[akka-event-sourcing-backbone-agentic-ai]]).
- **Applied to AI agents:** [[adam-dymitruk]] argues the method already describes agent systems —
  an agent is either a **user** or an **Automation processor**
  ([[dymitruk-event-modeling-future-proof-agents]]). Worked out in [[event-modeled-agent-design]];
  AI can also *assist* the modeling itself ([[qlerify-event-modeling-tool-ai]]), and the model's
  output can *drive* autonomous coding agents — [[john-wilger]]'s `agent-skills`
  ([[jwilger-agent-skills-event-modeling]]) turns vertical slices + GWT into acceptance gates for a
  factory pipeline.

## Practitioner lens — Event Model as business process, and as code (Goeleven)

[[yves-goeleven]] sharpens two points ([[goeleven-event-model-to-code-series]]): (1) Event Modeling
visualizes **business processes, even manual ones** — top swimlanes are **roles** (and *any*
interaction: screens, paper, PDFs, cash, Excel), bottom swimlanes are **[[business-capabilities|business
capabilities]]** (the long-term-stable boundaries); decisions become events recorded in the capability
lane "even when taken
in the mind of an authorized person." (2) The **code mapping**: command (intent) → **Event Sourced
Aggregate Root** (decision) → events → **Outbox** → **Projection** → read model (state, rebuilt from
full history — his "black dot" notation). This is the concrete answer to *what implementing a slice is*
— the unit an agent would generate ([[event-modeled-agent-design]], [[vertical-slice-architecture]]).
He also flags a coupling rule: a context's internal events shouldn't double as integration events; a
**contract between capabilities** is required ([[domain-driven-design]]).

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[goeleven-event-model-to-code-series]]._
