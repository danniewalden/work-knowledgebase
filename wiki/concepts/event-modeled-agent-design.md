---
title: Event-Modeled Agent Design
type: concept
created: 2026-06-11
updated: 2026-06-14
sources: [dymitruk-event-modeling-future-proof-agents, qlerify-event-modeling-tool-ai, eventmodeling-what-is-event-modeling, anthropic-effective-harnesses-long-running-agents, stripe-minions-one-shot-coding-agents, proophboard-skills-ai-agent-event-modeling, jwilger-agent-skills-event-modeling, dilger-spec-driven-development-applied, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, fraktalio-event-modeler-connect-ai-agents-mcp]
tags: [event-modeling, agentic-ai, synthesis, focus]
---

# Event-Modeled Agent Design

**Focus-area synthesis** (an active focus area for Dannie, tracked in memory). Can [[event-modeling]] —
the design *method*, not just [[event-sourcing]] — be used to design agent and multi-agent systems?
[[adam-dymitruk]], the method's creator, says yes
([[dymitruk-event-modeling-future-proof-agents]]): "agents can be described as either **users** or
**specific processors**," composable into a multi-agent system "without throwing away your existing
system design." This page works out the mapping and marks where it's externally supported vs. the
KB's own extrapolation.

## The core mapping (Dymitruk's claim)

- **Agent as user** → an actor in a swimlane that issues **commands**, exactly like a human. Useful
  when an agent fronts a workflow (e.g. a Slack-invoked coding agent kicking off a task —
  [[stripe-minions-one-shot-coding-agents]]).
- **Agent as processor** → the **Automation pattern**: a processor works a "todo list," issues
  commands to other systems, and stores their replies back as **events**. This is the natural home
  for autonomous/background agents.
- **Multi-agent system** → several users/processors composed on one timeline, communicating through
  the shared event ledger.

## Construct-by-construct (KB extrapolation onto the harness thread)

| Event Modeling construct | Agent/harness analog (in-KB) |
| --- | --- |
| **Event** (state-changing fact on the timeline) | the append-only progress ledger: `claude-progress.txt` + git history + feature-list JSON ([[anthropic-effective-harnesses-long-running-agents]]); minion run records ([[stripe-minions-one-shot-coding-agents]]) |
| **Command** (an actor's intention) | the task prompt that starts a run (the Slack message to a minion) |
| **View / read model** (passive) | legibility surfaces: AGENTS.md map, progress files, run web UI ([[agent-legibility]]) |
| **Translation pattern** | MCP tools converting external data into local events ([[model-context-protocol]]; Stripe hydrates context over links before a run) |
| **Automation pattern** | the initializer-executor / [[ralph-loop]] working a feature list one item at a time |
| **Given-When-Then** (one per command/view) | feature-list specs + self-verification ([[feedforward-and-feedback-controls]]); Qlerify drafts GWT per event ([[qlerify-event-modeling-tool-ai]]) |
| **Swimlanes / Conway's Law** | subdirectory-scoped agent rules (Stripe); team-owned layered domains ([[openai-harness-engineering-codex]]) |
| **Flat cost curve via explicit contracts** | "enforce invariants, not implementations" + harness templates per topology ([[harness-engineering]]) |

## Why the fit is natural

Both [[event-modeling]] and agent harnesses treat **current state as a replay of an append-only
ledger** and isolate work behind explicit contracts. The KB already argued this for the *substrate*
in [[event-sourced-agentic-patterns]] (event sourcing as the agent backbone); this page adds the
*design-method* layer on top — the patterns become event schemas, [[guardian-agents]] become
subscribers that veto events before they commit, and governance audit trails are the log itself.

## What's solid vs. open

- **Externally supported (a ladder of increasing concreteness):** (1) agents map onto Event
  Modeling's user/processor roles ([[dymitruk-event-modeling-future-proof-agents]]); (2) AI and Event
  Modeling already interoperate in tooling ([[qlerify-event-modeling-tool-ai]]); (3) agents are being
  built to *practise* Event Modeling directly — [[prooph-board]] ships agent **Skills + an MCP server**
  teaching coding agents to create EM elements ([[proophboard-skills-ai-agent-event-modeling]]), and
  **[[fraktalio]]**'s Event Modeler now exposes an MCP endpoint where an agent authors the model *and
  generates Given-When-Then per command, including business exceptions*
  ([[fraktalio-event-modeler-connect-ai-agents-mcp]]) — a second independent vendor on this rung; and
  (4) **the event model now governs a multi-agent build** — [[john-wilger]]'s `agent-skills`
  ([[jwilger-agent-skills-event-modeling]]) makes the method's *output* (vertical slices + GWT
  scenarios) the machine-checkable contract for an autonomous "factory pipeline": GWT scenarios become
  the TDD acceptance gates, the `event_model_root` is loaded as pre-implementation context, and the
  human/agent boundary follows a Conservative→Standard→Full [[autonomy-ladder]]. This is the closest
  shipping evidence to date. And (5) a **practitioner-evangelist** thread: [[martin-dilger]] (building
  [[eventmodelers-ai]]) argues the *why* from the requirements side — AI amplifies unclear requirements
  rather than fixing them, so the event model is the spec that constrains the agent
  ([[dilger-faros-ai-report-amplifies-unclear-requirements]], [[spec-driven-development]]); the model
  defines *where logic may live* and must be enforced because agents drift
  ([[dilger-keep-command-handlers-pure]]); an agent can even *bootstrap* the model from a running
  UI ([[dilger-automatic-domain-discovery-claude-code]], [[domain-discovery]]); and he now describes
  the model run as a **live spec** — a background agent building continuously from board edits, with a
  slice→"generate tests from the spec (the harness)"→implement→PR loop, optionally a modeling-agent→
  builder-agent "full autopilot" ([[dilger-model-is-a-living-spec-always-on-agent]];
  [[long-running-agents]], [[unattended-coding-agents]]). Framing-rich but vendor-marketing, not
  independent evidence. **Direction of fit** now cuts both ways: agents that *author* the model
  (Fraktalio's MCP, Dilger's discovery) and the model that *governs* the agent (jwilger's gates,
  Dilger's slice loop) — together a closed authoring↔execution loop.
- **Still in-house extrapolation:** the full construct-by-construct mapping onto the harness thread
  above. No captured source yet gives a *worked* event model of a multi-agent/harness system — even
  jwilger's pipeline *consumes* an event model (`docs/event-model/`) it doesn't show. (A first in-house
  notation worked example exists as a deliverable: `outputs/denoting-an-agent-in-an-event-model.md` —
  user/processor roles, a multi-agent swimlane timeline, and a notation cheat-sheet.)
- **Adjacent cross-check (captured):** [[esaa-event-sourcing-for-autonomous-agents]] (arXiv, Feb 2026)
  gives a *worked* multi-agent system built on event *sourcing/CQRS* — agents emit JSON **intentions**,
  a deterministic orchestrator applies **effects** — which is strikingly close to Event Modeling's
  **command → event** flow and Automation pattern, even though it doesn't use the method or its
  notation. The nearest thing to a worked example, one substrate-level remove from this page's claim.
- **Wanted next:** a worked example using Event Modeling *the method* (Dymitruk long-form, a talk, or
  a paper); the broader academic formal/discrete-event agent-specification lineage (e.g. DEVS world
  models, "Formally Specifying the High-Level Behavior of LLM-Based Agents") as further cross-checks.

_Sources: [[dymitruk-event-modeling-future-proof-agents]] · [[qlerify-event-modeling-tool-ai]] · [[proophboard-skills-ai-agent-event-modeling]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[jwilger-agent-skills-event-modeling]] · [[dilger-spec-driven-development-applied]] · [[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] · [[dilger-automatic-domain-discovery-claude-code]] · [[dilger-model-is-a-living-spec-always-on-agent]] · [[eventmodeling-what-is-event-modeling]] · [[anthropic-effective-harnesses-long-running-agents]] · [[stripe-minions-one-shot-coding-agents]]._
