---
source_url: https://a2a-protocol.org/latest/
title: "Agent2Agent (A2A) Protocol — Home / Overview"
author: The Linux Foundation (originally Google)
publication: a2a-protocol.org
published: 2026 (v1.0)
retrieved: 2026-06-11
type: article
---

# Agent2Agent (A2A) Protocol

## What is A2A Protocol?

Welcome to the **official documentation** for the **Agent2Agent (A2A) Protocol**, an open standard designed to enable seamless communication and collaboration between AI agents.

Originally developed by Google and now donated to the Linux Foundation, A2A provides the definitive common language for agent interoperability in a world where agents are built using diverse frameworks and by different vendors.

Build with **ADK** *(or any framework)*, equip with **MCP** *(or any tool)*, and communicate with **A2A**, to remote agents, local agents, and humans.

## Why use the A2A Protocol

```
graph LR
    User(User) <--> ClientAgent(Client Agent)
    ClientAgent --> A2A1(A2A) --> RemoteAgent1(Remote Agent 1)
    ClientAgent --> A2A2(A2A) --> RemoteAgent2(Remote Agent 2)
```

- **Interoperability** — Connect agents built on different platforms (LangGraph, CrewAI, Semantic Kernel, custom solutions) to create powerful, composite AI systems.
- **Complex Workflows** — Enable agents to delegate sub-tasks, exchange information, and coordinate actions to solve complex problems that a single agent cannot.
- **Secure & Opaque** — Agents interact without needing to share internal memory, tools, or proprietary logic, ensuring security and preserving intellectual property.

## How does A2A work with MCP?

A2A and Model Context Protocol (MCP) are complementary standards for building robust agentic applications:

- **Model Context Protocol (MCP)**: Provides agent-to-tool communication. It's a complementary standard that standardizes how an agent connects to its tools, APIs, and resources to get information.
- **IBM ACP**: Incorporated into the A2A Protocol.
- **Cisco agntcy**: A framework that provides components to the Internet of Agents with discovery, group communication, identity and observability and leverages A2A and MCP for agent communication and tool calling.
- **A2A**: Provides agent-to-agent communication. As a universal, decentralized standard, A2A acts as the public internet that allows AI agents—including those using MCP, or built with frameworks like agntcy—to interoperate, collaborate, and share their findings.

## Documentation structure (from site navigation)

Topics: What is A2A?, A2A and MCP, Core Concepts, Life of a Task, Agent Discovery, Enterprise Features, Streaming & Asynchronous Operations, Multi-Tenancy. Specification: Overview, What's New in v1.0, Protocol Definition. SDKs available in Python, JavaScript, Java, C#/.NET, and Golang.

*(Per the published specification overview, the A2A spec is organized into three layers — the A2A Data Model: Task, Message, AgentCard, Part, Artifact, Extension; A2A Operations: Send Message, Send Streaming Message, Get Task, List Tasks, Cancel Task, Get Agent Card; and Protocol Bindings: JSON-RPC Methods, gRPC RPCs, HTTP/REST Endpoints, Custom Bindings.)*

Copyright 2026 The Linux Foundation. Licensed under the Apache License, Version 2.0.

---

*Capture note: this is the A2A home/overview page plus the spec layer summary from the specification overview. The full Protocol Definition was not captured verbatim.*
