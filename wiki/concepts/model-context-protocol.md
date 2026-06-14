---
title: Model Context Protocol (MCP)
type: concept
created: 2026-06-11
updated: 2026-06-14
sources: [mcp-specification-2025-11-25, anthropic-building-effective-agents, svitla-agentic-ai-market-trends-2026, proophboard-skills-ai-agent-event-modeling, fraktalio-event-modeler-connect-ai-agents-mcp]
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

_Source pages: [[mcp-specification-2025-11-25]] · [[anthropic-building-effective-agents]] · [[svitla-agentic-ai-market-trends-2026]] · [[proophboard-skills-ai-agent-event-modeling]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]]._
