---
title: Model Context Protocol (MCP)
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [mcp-specification-2025-11-25, anthropic-building-effective-agents, svitla-agentic-ai-market-trends-2026]
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

_Source pages: [[mcp-specification-2025-11-25]] · [[anthropic-building-effective-agents]] · [[svitla-agentic-ai-market-trends-2026]]._
