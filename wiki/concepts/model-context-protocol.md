---
title: Model Context Protocol (MCP)
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [mcp-specification-2025-11-25, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, anthropic-building-effective-agents, svitla-agentic-ai-market-trends-2026, proophboard-skills-ai-agent-event-modeling, fraktalio-event-modeler-connect-ai-agents-mcp, roden-event-sourcing-meets-mcp-whole-story-for-llms]
tags: [agentic-ai, protocol, tools, integration]
---

# Model Context Protocol (MCP)

An open protocol from [[anthropic]] that standardizes how an agent (or [[augmented-llm]])
connects to external tools, APIs, and data sources through a simple client implementation —
letting developers integrate with a growing ecosystem of third-party tools instead of
hand-wiring each one. Now primary-sourced from the spec ([[mcp-specification-2025-11-25]]).

## How it works (from the spec)

Uses **JSON-RPC 2.0** over stateful connections with capability negotiation, between three
roles: **Hosts** (LLM apps), **Clients** (connectors in the host), **Servers** (provide
context/capabilities). Servers expose **Resources, Prompts, Tools**; clients can offer
**Sampling, Roots, Elicitation**. Security is consent-centric — user consent/control, data
privacy, tool safety (tools are arbitrary code execution), and explicit sampling approval —
which makes MCP a protocol-level support for [[agent-governance]]. Analogized to the Language
Server Protocol.

In the [[multi-agent-orchestration]] picture, MCP is the **vertical layer (agent → system)**,
complementing the **horizontal** [[agent2agent-protocol]] (agent → agent). It is the
recommended way to deliver the tool/retrieval/memory augmentations that turn a plain LLM into
an augmented one, and most enterprise agent architectures being designed now assume both MCP
and A2A.

## In the focus area — MCP as the agent↔Event-Modeling bridge

MCP is the concrete connector behind several [[event-modeled-agent-design]] tools: it is how an agent
gets a typed handle on an Event Modeling canvas to *read schemas and author the model*. [[prooph-board]]
ships an MCP server + agent Skills teaching coding agents to create EM elements
([[proophboard-skills-ai-agent-event-modeling]]); [[fraktalio]]'s Event Modeler exposes a `/mcp`
endpoint where the agent builds the model and generates Given-When-Then specs per command
([[fraktalio-event-modeler-connect-ai-agents-mcp]]). In [[event-modeled-agent-design]]'s
construct-by-construct table, this is the **Translation pattern** (MCP tools converting external data
into local events) made literal.

## MCP as the bridge to an event store (2026-06-21)

[[golo-roden]] ([[roden-event-sourcing-meets-mcp-whole-story-for-llms]]) frames MCP at the **data
layer**: it is the *access* half of an ES×LLM pairing, **data-source agnostic** by design — so the
quality of what flows through it is set by the source behind it. "A CRUD database connected via MCP
still only provides snapshots. An event store provides the whole story." This complements the
focus-area use above (MCP as the agent↔Event-Modeling-canvas bridge): one rung up an agent *authors*
the model via MCP; one rung down it *reads the full event history* via MCP. The free EventSourcingDB
MCP server (natural-language event read/write, subject/type search, EventQL) is the concrete example —
though Roden stresses the principle is product-neutral. See [[event-sourcing]], [[context-engineering]].

## Antipattern — naive API-to-MCP conversion (2026-08)

The sharpest design critique of MCP surface area the KB holds
([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]]). Wrapping existing REST endpoints one-to-one so
that every endpoint becomes a tool produces **tool sprawl** — 50 barely-distinguished tools with names
like `get_po_payment_status`, `create_ticket_po_payment`, `create_ticket_po_payment_network` — and LLM
selection accuracy drops sharply as the tool count climbs. On the Thoughtworks Technology Radar at
**HOLD**.

The alternative is to *design capabilities, not endpoints*: a handful of parameterized operations with
descriptions rich enough for the model to know when to reach for each.

> "Five to ten well described business capabilities will outperform 50 thin API wrappers almost every
> time."

Two structural points worth carrying forward:

- **The primitives sit on a risk gradient.** Resources (read-only) → Prompts (shape behavior) → Tools
  (change state), which maps onto the retrieval → real-time-query → write-back access spectrum. The safe
  path is to expose Resources first and graduate to Tools under governance. See [[autonomy-ladder]].
- **The principle is protocol-agnostic.** "The definitions are the layer; the interface, MCP today, is
  just the door." Whatever succeeds MCP, the properties that make access agent-ready — rich descriptions,
  parameterized access, clear schemas — are the same. This is a useful hedge on how much of this page is
  about MCP specifically versus about tool design in general.

This is [[business-capabilities]] applied to protocol surface, and it is the reason MCP exposure is an
architecture decision rather than a wiring one.

_Source pages: [[mcp-specification-2025-11-25]] · [[anthropic-building-effective-agents]] · [[svitla-agentic-ai-market-trends-2026]] · [[proophboard-skills-ai-agent-event-modeling]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]]._
