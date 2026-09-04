---
title: Slice
type: concept
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-element-slice-chapter-story-context-ladder, eventmodeling-what-is-event-modeling, dilger-done-is-done-open-closed-new-slice, dilger-event-modeling-agent-harness, jwilger-agent-skills-event-modeling, dilger-model-is-a-living-spec-always-on-agent, dilger-local-llm-distributed-agent-setup-event-modeling, dilger-triplet-flexible-agent-enabled-architecture, bogard-vertical-slice-architecture, dilger-todo-lists-storylines-one-scenario]
tags: [event-modeling, slice, method, agentic-coding, vocabulary, focus]
---

# Slice

**The smallest thing you can model in [[event-modeling]]: one step of a business process, from the
screen that triggers it through to what it writes or reads.** Every slice either *writes* something
(a command producing an event) or *reads* something (a read model feeding a view). That is the whole
definition — a slice is the atom, not the architecture.

> **Written 2026-08-31 to resolve a conflation.** Until now the wiki aliased every mention of "slice"
> to [[vertical-slice-architecture]]. Those are two different things, and almost every agent-facing
> claim in this KB rests on the one that had no page. See *Two senses of the word* below.

## Two senses of the word

| | **Slice** (this page) | **Vertical slice** ([[vertical-slice-architecture]]) |
| --- | --- | --- |
| What it is | A unit of the **model** | A unit of **code organisation** |
| Named by | [[adam-dymitruk]] / Event Modeling | [[jimmy-bogard]], 2018 |
| Contents | Screen → command → event, or event → read model → screen, plus its [[given-when-then]] | All the code for one request, front to back, in one place |
| Exists when | Before any code | In the codebase |
| Answers | "What should happen here?" | "Where does the code for this live?" |

They are complementary rather than competing, and in practice one becomes the other: an Event Modeling
slice is the *specification* that a vertical slice of code *implements*. [[martin-dilger]]'s Triplet
([[triplet-architecture]]) pairs them deliberately — Event Modeling plans in slices, VSA structures in
slices, so the unit survives the trip from model to code without translation. That correspondence is
exactly why the two words collapsed into one in this wiki, and also why keeping them apart matters:
**the claims the KB makes about agents are about the model unit, not the code unit.**

## The ladder — Element → Slice → Chapter → Story → Context

Dilger's sharpest statement of the method's shape, and the reason this page exists
([[dilger-element-slice-chapter-story-context-ladder]], 2026-08-25):

> "Slice-based architecture is not really about slices. Same as Event Sourcing is not really about
> Events. People struggle with this one a lot. They hear slice, they learn to draw one, and they think
> that's the whole method."

- **Element** — a card on the board. *(He names the rung but does not define it; "an event, a command,
  a read model, a screen" is the wiki's gloss from Event Modeling's building blocks.)*
- **Slice** — the smallest modellable unit. Writes (via a command) or reads (via a read model).
- **Chapter** — a group of slices forming "a consistent part of a business process or a customer
  journey."
- **Story** — chapters connected in the right order: "the whole flow from start to end."
- **Context** — many stories on a board, "describing a complete system."

His diagnosis of where teams get stuck: *"Most teams get stuck right there. They model slice after slice
and never climb up to see the story, let alone the context around it… You need the tiny building blocks,
but also the big picture to be effective."*

This ladder gives the KB vocabulary it had been missing at both ends. **Chapter** and **story** appear
across a dozen pages without definition; **context** connects the method to
[[domain-driven-design]]'s bounded context without the page having to guess at the mapping.

## Why the slice is the load-bearing unit for agents

Nearly every agent claim in this KB is really a claim about slices. Collected here because they are
otherwise scattered:

- **Slice = unit of work.** The agent harness runs a board where a slice moves Draft → Ready → In
  Progress → Done, and an agent claims exactly one ([[dilger-event-modeling-agent-harness]],
  [[dilger-model-is-a-living-spec-always-on-agent]]).
- **Slice = the context boundary.** One slice is one agent's context — it needs that slice, the event
  log, and the model, not the codebase. This is the whole token-economics argument
  ([[dilger-triplet-flexible-agent-enabled-architecture]]; and independently
  [[miller-jasperfx-critterstack-ai-event-modeling-strategy]], where layered code "forces AI agents to
  burn more tokens traversing the code").
- **Slice = the collision-avoidance mechanism.** A board-level claim-lock on the slice lets 6–10 agents
  work in parallel without code-level coordination, *because slices are decoupled by design* — "no merge
  conflicts, no coupling hell" ([[dilger-local-llm-distributed-agent-setup-event-modeling]]).
- **Slice + GWT = the acceptance gate.** The slice's given/when/then becomes the test the agent must
  pass ([[jwilger-agent-skills-event-modeling]]). For TODO lists a **storyline** — one narrative scenario
  replacing several repetitive ones — often replaces plain GWT
  ([[dilger-todo-lists-storylines-one-scenario]]); his self-training agent generalised that to Read Models
  attached to Automations ([[dilger-one-million-tokens-self-training-modeling-agent]]).
- **Slice = the unit of estimation.** Build-time-per-slice as a planning measure, and the flat
  feature-cost curve stated as a property of slicing: *"building a feature in 5 years costs exactly as
  much or less as today… The only way I found too keep the cost curve flat ( even slowly declining ) is
  consistently slicing the system. This must happen in while specifying already."* (sic) ([[dilger-slicing-keeps-the-cost-curve-flat]]).
- **Slice = the rollback unit.** When a guard fails, "we throw away everything, record a learning 'why'
  this was not good enough and start from scratch ( my [sic] moving the Slice back into 'planned' )"
  ([[dilger-lights-off-software-factory-dead-end]]). Cheap disposal is a property of the slice boundary.

The common thread: **a slice is small enough to be built without knowing the rest of the system, and
specified precisely enough to be checked without reading the code.** Those two properties together are
what the KB's agent thread actually depends on — see [[event-modeled-agent-design]].

## Redundant data is a precondition, not a compromise

A slice owns its own tailor-made read model, which means the same data is stored more than once. Dilger
makes this explicit and enjoys the reaction ([[dilger-join-considered-harmful]], 2026-08-24):

> "Every SQL statement is essentially a 'select * from ? where ?'. As the data views are special and
> tailor made to each use case, there is simply no need to join in 99.9% of all use cases. Does that mean
> we embrace redundant data? Yes. That's actually a precondition for sliced architectures."

Worth stating on this page because it is the most common objection to slicing from a data background, and
because the redundancy is *derived* — projections rebuilt from the event log — rather than duplicated
authoritative state. See [[event-sourcing]], [[cqrs]].

## Open questions

- **Where does a chapter boundary come from?** The ladder says chapters are "a consistent part of a
  business process," which is a judgement, not a rule. Nothing captured says how to tell a chapter
  boundary from an arbitrary grouping — and if chapters are the zoom level teams are missing, that
  matters.
- **Does the agent claim-lock work at chapter level?** All the parallelism evidence is slice-level. A
  chapter spans slices that share business context, so it is exactly where the "decoupled by design"
  assumption would be tested.
- **Is "one slice = one agent's context" measured anywhere?** It is asserted by both Dilger and Miller
  and measured by neither. See [[vertical-slice-architecture]]'s standing caveat on the same claim.

## Related

[[event-modeling]] · [[vertical-slice-architecture]] · [[triplet-architecture]] · [[given-when-then]] ·
[[event-modeled-agent-design]] · [[event-sourcing]] · [[cqrs]] · [[open-closed-principle]] ·
[[martin-dilger]] · [[adam-dymitruk]] · [[jimmy-bogard]] · [[dynamic-consistency-boundaries]]

_Sources: [[dilger-element-slice-chapter-story-context-ladder]] · [[eventmodeling-what-is-event-modeling]] ·
[[dilger-done-is-done-open-closed-new-slice]] · [[dilger-event-modeling-agent-harness]] ·
[[jwilger-agent-skills-event-modeling]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[dilger-local-llm-distributed-agent-setup-event-modeling]] ·
[[dilger-triplet-flexible-agent-enabled-architecture]] · [[bogard-vertical-slice-architecture]] ·
[[dilger-todo-lists-storylines-one-scenario]]._
