---
title: "Source: Agent2Agent (A2A) Protocol — Overview"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [a2a-protocol-overview]
raw_file: [raw/articles/a2a-protocol-overview.md]
tags: [protocol, a2a, primary-source, agentic-ai, interoperability]
---

# Source: Agent2Agent (A2A) Protocol — Overview

The **primary** documentation home for [[agent2agent-protocol]], originally developed by
Google and now governed by **the Linux Foundation** (v1.0). Replaces reliance on the
secondary Svitla/IBM descriptions. Raw capture: `raw/articles/a2a-protocol-overview.md`.

## Summary

A2A is an open standard for **communication and collaboration between AI agents** built on
different frameworks or by different vendors — "the definitive common language for agent
interoperability." Tagline: build with any framework (e.g. ADK), equip with any tools (e.g.
[[model-context-protocol]]), and communicate via A2A to remote agents, local agents, and humans.

## Key points

- **Three value props:** *Interoperability* (connect agents across LangGraph, CrewAI,
  Semantic Kernel, custom builds); *Complex workflows* (delegate sub-tasks, exchange info,
  coordinate); *Secure & opaque* (agents interact without sharing internal memory, tools, or
  proprietary logic).
- **Explicitly complementary to MCP:** MCP = agent→tool; A2A = agent→agent. A2A "acts as the
  public internet" letting agents (including MCP users) interoperate. IBM's ACP has been
  folded into A2A; Cisco's agntcy leverages both.
- **Spec structure (3 layers):** Data Model (Task, Message, AgentCard, Part, Artifact,
  Extension); Operations (Send/Stream Message, Get/List/Cancel Task, Get Agent Card); Protocol
  Bindings (JSON-RPC, gRPC, HTTP/REST, custom). Official SDKs in Python, JS, Java, C#/.NET, Go.
- Topics include Agent Discovery, Life of a Task, Enterprise Features, Streaming/Async,
  Multi-Tenancy.

## Connections / contrast

The horizontal (agent→agent) layer of [[multi-agent-orchestration]], the infrastructure for
agents acting on behalf of other agents (e.g. procurement↔supplier). Linux Foundation
governance is a notable contrast to the single-vendor framing in the secondary sources.
Primary source — supersedes the A2A description in [[svitla-agentic-ai-market-trends-2026]].
