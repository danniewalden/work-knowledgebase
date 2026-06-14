---
title: Agent-to-Agent Protocol (A2A)
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [a2a-protocol-overview, svitla-agentic-ai-market-trends-2026]
tags: [agentic-ai, protocol, multi-agent, interoperability]
---

# Agent-to-Agent Protocol (A2A)

An open standard defining how agents **communicate and delegate tasks to each other** — the
**horizontal layer (agent → agent)** of [[multi-agent-orchestration]], complementing
[[model-context-protocol]] (the vertical, agent → system layer). Originally built by Google,
now governed by the **Linux Foundation** (v1.0); now primary-sourced ([[a2a-protocol-overview]]).

## How it works (from the spec)

Lets agents interoperate **without sharing internal memory, tools, or proprietary logic**
(secure & opaque), connecting agents across frameworks (LangGraph, CrewAI, Semantic Kernel,
custom). Spec is three layers: **Data Model** (Task, Message, AgentCard, Part, Artifact,
Extension), **Operations** (Send/Stream Message, Get/List/Cancel Task, Get Agent Card), and
**Protocol Bindings** (JSON-RPC, gRPC, HTTP/REST, custom). IBM's ACP has been folded in.
Reported **50+ technology partners** (Atlassian, Salesforce, SAP, PayPal).

A2A is the infrastructure for the still-early future where agents act *on behalf of other
agents* — e.g. a procurement agent negotiating with a supplier's sales agent within
pre-approved parameters — and for cross-vendor agent ecosystems replacing single-vendor
platforms. Gartner's stage 3 (2027) anticipates exactly this need for agent-to-agent standards.

_Source pages: [[a2a-protocol-overview]] · [[svitla-agentic-ai-market-trends-2026]]._
