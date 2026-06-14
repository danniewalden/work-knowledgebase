---
title: Martin Dilger
type: entity
created: 2026-06-13
updated: 2026-06-14
sources: [dilger-faros-ai-report-amplifies-unclear-requirements, dilger-spec-driven-development-applied, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, dilger-hold-my-beer-engineer, dilger-craft-conf-idea-to-event-model-to-code]
tags: [person, event-modeling, event-sourcing, agentic-coding, spec-driven-development, focus]
---

# Martin Dilger

Event-sourcing / Event Modeling practitioner and consultant; founder of **[[nebulit]] GmbH**; author
of **"Understanding Eventsourcing"** (the first German-language book on Event Modeling) and **"Spec
Driven"**, and co-host of the **Event Modeling & Event Sourcing podcast**. He is building
**[[eventmodelers-ai]]** ("eventmodelers.ai"), an *agentic software modeling* platform meant to "bring
business, engineering and AI together." Associated with the [[prooph-board]] community. A prolific LinkedIn writer — his recent activity is one of the most
on-target running feeds for Dannie's focus area ([[event-modeled-agent-design]]), tracked in
`watch-config.json`.

## Position — Event Modeling as the spec for agents

Across the captured posts Dilger argues one consistent thesis from the [[event-modeling]] side of the
[[event-modeled-agent-design]] question, converging on the same conclusions as the harness thread
([[harness-engineering]], [[mitchell-hashimoto]], [[birgitta-bockeler]]) but arrived at independently:

- **AI amplifies unclear requirements, it doesn't fix them** — he reads the Faros AI Report's
  throughput-up / quality-down numbers as proof the fix must be upstream, a clear spec before code
  ([[dilger-faros-ai-report-amplifies-unclear-requirements]]).
- **You can't force an agent; you design the environment** — prompt engineering "didn't work"; Event
  Modeling supplies "clarity of intent before a single line of code," making good agent behavior the
  path of least resistance ([[dilger-spec-driven-development-applied]]). This is his
  [[spec-driven-development]] framing.
- **The model defines where logic may live** — a Claude Code anecdote where the agent ignored the
  event model and put a business rule in the routing layer; a written skill was necessary but not
  sufficient, so guardrails must be enforced ([[dilger-keep-command-handlers-pure]]).
- **Agents can do the discovery, too** — an agent that maps a product's UI into a visual storyboard,
  automating the Event Modeling discovery phase ([[dilger-automatic-domain-discovery-claude-code]];
  [[domain-discovery]]).
- **The spec is the work; the model is a *living* spec** — describes a background agent left in a
  loop that kept building from his board edits in real time ("one continuous flow," no hand-off), and
  his 24/7 pipeline: slice→`planned`→agent generates tests from the spec (the harness)→implements→PR,
  with an optional modeling-agent→builder-agent "full autopilot"
  ([[dilger-model-is-a-living-spec-always-on-agent]]; [[long-running-agents]],
  [[unattended-coding-agents]]).
- **"What if your requirements were something you could run?"** — his Craft Conference talk frames the
  whole thesis as one structured arc, idea→event model→code→back, with the model as a *living spec* that
  drives code generation and agentic coding; names the full **EM + [[event-sourcing]] + [[cqrs]] +
  [[agentic-coding]]** stack ([[dilger-craft-conf-idea-to-event-model-to-code]]).

## In the KB

He is the most active *practitioner-evangelist* voice for [[event-modeled-agent-design]], sitting
alongside [[adam-dymitruk]] (the method's creator) and [[john-wilger]] (the worked factory pipeline).
Where Dymitruk supplies the role-mapping claim and Wilger a shipping example, Dilger supplies the
day-to-day **why** — requirements, guardrails, and the spec-first operating model — plus a commercial
platform betting on it. Caveat: most of his captured material is LinkedIn marketing for
[[eventmodelers-ai]] and the *Spec Driven* book — strong on framing, light on independent evidence.

_Source pages: [[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] ·
[[dilger-automatic-domain-discovery-claude-code]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[dilger-hold-my-beer-engineer]] · [[dilger-craft-conf-idea-to-event-model-to-code]]._
