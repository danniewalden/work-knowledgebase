---
title: Event Modeling
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [dilger-element-slice-chapter-story-context-ladder, eventmodeling-what-is-event-modeling, semaphore-dymitruk-event-modeling, goeleven-event-model-to-code-series, event-modeling-event-sourcing-podcast, dilger-how-does-dcb-affect-event-modeling, adaptech-workflow-not-inside-giant-process-manager, dilger-extending-event-modeling-query-when, dilger-99-percent-software-boring-two-patterns, dilger-the-shapes-event-modeling-anti-patterns]
tags: [event-modeling, methodology, event-sourcing, software-design, ddd]
---

# Event Modeling

A method (from [[adam-dymitruk]], developed at [[adaptech-group]]) for designing
information systems by describing them as a **timeline of events** rather than as current
state. The output is a **blueprint** — read like a story — that follows every field of
information from the UI, into storage, and back out to a screen or report. Deliberately
minimal: **3 building blocks, 4 patterns, 2 ideas**, produced in a **7-step workshop**.

## The zoom levels — Element → Slice → Chapter → Story → Context

The method's own vocabulary for scale, named by [[martin-dilger]]
([[dilger-element-slice-chapter-story-context-ladder]], 2026-08-25): an **element** is a card, a
**[[slice]]** the smallest modellable unit, a **chapter** a consistent part of a business process, a
**story** the chapters in order end to end, and a **context** the whole board describing a system.

> "Slice-based architecture is not really about slices. Same as Event Sourcing is not really about
> Events… Most teams get stuck right there. They model slice after slice and never climb up to see the
> story, let alone the context around it."

Worth stating early on this page because the KB — and, he argues, most teams — operate almost entirely at
the slice rung. See [[slice]] for why that rung nonetheless carries all the agent claims.

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
  and storing their replies back as events (queues, reactive, or even manual lists). Worked out
  as a design pattern in [[process-managers-and-todo-lists]] / [[adaptech-workflow-not-inside-giant-process-manager]]:
  prefer a **projected to-do list + several single-responsibility processors** over one large
  saga/process manager, so workflow state stays inspectable.

Specifications are written **Given-When-Then** (≈ Arrange-Act-Assert), each tied to
*exactly one* command or view.

### Dilger's reduction — "really only two patterns" (2026-08-08)

[[dilger-99-percent-software-boring-two-patterns|Dilger]] argues that under the surface the four collapse to
**two**: **State change** (how information gets into the system) and **State view** (how it's used and
pulled back out) — i.e. the [[cqrs|CQRS]] write/read split; he teaches "four" only "to not be too boring."
His agent-facing point: this *repetitiveness* is a feature — it gives an AI **tight guardrails and clear
instructions instead of an open-ended blank page**, which is why event-modeled code is safe to hand to an
agent (the guardrail half of [[vibe-modeling]] / [[spec-driven-development]]). (Provocative simplification —
it elides the Translation/Automation integration patterns the method treats as first-class.)

### Reading a model by its shape — anti-patterns (Dilger, 2026-08)

Complementing the constructive patterns, Dilger names an **anti-pattern taxonomy, "The Shapes"** — the bed,
left/right chairs, and shelf — readable off a board's silhouette, with only the *bed* a hard red flag. It is
built to be **agent-operable** (the `/wdyt` AI-skill flags them; a reference-catalog "linter" grades
structure). See [[event-modeling-anti-patterns]].

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

## Under DCB — swimlanes become integration points (Dilger, 2026-07-06)

[[dilger-how-does-dcb-affect-event-modeling|Dilger]] argues adopting [[dynamic-consistency-boundaries|DCB]]
leaves the *method* untouched and actually simplifies it: with aggregates no longer the modeling unit, you
draw **one swimlane per system / bounded context**, and swimlanes revert to their original job — showing
**integration between systems and teams** ("whenever information crosses a lane, pay attention"), not
stream design. Crucially there is **no separate "Decision Model"** to draw: the events a command handler
must read are exactly the **GIVEN** clause of the slice's [[given-when-then|GWT]] scenarios, from which the
Axon **Build Kit** generates the handler's query + tests. **Tags** are treated as indices (not domain
concepts), added only in a Detailed-Modeling pass before a slice is handed to an agent. See
[[dynamic-consistency-boundaries]] and [[event-modeled-agent-design]].

## Proposed method extension — an optional read-side "Query" (WHEN) (Dilger, 2026-06-29)

[[dilger-extending-event-modeling-query-when|Dilger proposes the first change to the method]] captured in
this KB — and frames it as exactly that: his **first deliberate deviation from the EM "Standard"** (he had
kept strictly to it for *Understanding Eventsourcing* and [[eventmodelers-ai]]). Specifications are written
[[given-when-then|Given-When-Then]], but on the **read side** he had long taught practitioners to *drop the
WHEN* (GIVEN an event → THEN this data is available). The extension adds an **optional WHEN named "Query"**:

> GIVEN a user was registered / **WHEN we query with the user's email-address** / THEN we expect the user to
> be returned.

The motivation is to **express complex queries in read-side scenarios** — stating *how* a read model is
interrogated, not merely that its data exists. Status matters: it is **optional and proposed, not ratified**
— it surfaced independently in several **Munich Event Modeling Conference** discussions (and a prior chat
with [[adam-dymitruk]]), and Dilger is explicit he "wouldn't add this myself — I'm seeking feedback." It is
live (opt-in) on [[eventmodelers-ai]] with early-positive reception. For [[event-modeled-agent-design]] the
Query gives the [[cqrs|CQRS]] read side its own testable contract — another acceptance gate an agent can
generate tests from — consistent with the "living, runnable spec" line of [[spec-driven-development]].

## Practitioner lens — the weekly podcast (Dymitruk & Dilger)

The [[event-modeling-event-sourcing-podcast]] (46 eps) is the method's creators thinking out loud. Beyond
the substrate themes, it adds **method evolution** worth tracking: **"Event Modeling 2.0"** (Ep 24) —
sharpen the *what* vs *how* split, focus on **information flow**, and recast GWT with refinements and
projections; the **[[vibe-modeling]]** front-end to AI vibe-coding (Eps 19, 30); the **"musical score"**
analogy for reading a model (Ep 30); [[given-when-then]] on a timeline (Eps 3, 7); slices as the unit of
work, lifecycle, and billing (Eps 12, 19, 20, 34); and swim lanes / value-stream + BPMN framing (Eps 20,
32). Show-notes-level only — transcripts were blocked (see the source page's caveat).

## Related

[[model-as-code-vs-model-as-language]] · [[triplet-architecture]]

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[goeleven-event-model-to-code-series]] · [[event-modeling-event-sourcing-podcast]] · [[dilger-how-does-dcb-affect-event-modeling]] · [[dilger-extending-event-modeling-query-when]]._
