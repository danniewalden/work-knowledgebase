---
source_url: https://solace.com/blog/analysts-say-mas-needs-real-time-context-eda/
title: "Top Analysts: Multi-Agent Systems Need Real-Time Context and Event-Driven Architecture"
author: Roger Sabourin
publication: Solace
published: 2026-03-24
retrieved: 2026-06-12
type: article
---

# Top Analysts: Multi-Agent Systems Need Real‑Time Context and Event-Driven Architecture

By Roger Sabourin. March 24, 2026. Category: Artificial Intelligence.

Gartner® predicts that by 2028, 33% of enterprise software applications will include agentic AI, and 15% of day-to-day work tasks will be handled autonomously through agentic AI. If those numbers sound low, consider that as recently as 2024 they were 1% and 0%, respectively. IDC forecasts that "By 2027, 80% of agentic AI use cases will require real‑time, contextual, and ubiquitous data access, forcing a majority of G2000 to transform data models from a gatekeeper to a federated approach."

So it's pretty safe to say that agentic AI has burst on to the scene as a serious game changer, but most organizations today are playing with single AI agent systems and experiencing mixed success. The more innovative organizations are trying their hand at multi-agent systems (MAS), which is more complex, but yields much bigger payoffs in the long term.

Single AI agents hit reliability and complexity limits fast. MAS overcomes these limits by dividing work among specialized agents, but they only perform as well as the context they have, and in fast-moving enterprise that context better be based on real-time data. That demands an event‑based system that streams information across apps, cloud services, data platforms, and identity systems. In our opinion, when we look at research from Gartner and IDC, you can summarize to three imperatives:

- Design multi-agent systems for interoperability and governance;
- Ensure agents have real‑time context; and
- Modernize connectivity with EDA, utilize API management principles, and leverage emerging AI protocols like A2A and MCP.

## Limitations of Single-Agent AI

Individual agents are great for contained tasks where they can draw on an LLM and a couple data sources, but enterprise workflows are too complex. Today's task‑level agents reliably select from only a small set of actions per step (single digits, maybe double in some cases). Larger action menus can lead to planning errors and workflow failures, so it's essential to limit each agent's scope.

Errors also compound across multi‑step processes because models are probabilistic. Without structure, validation and guardrails, even modest per‑step error rates multiply—making autonomous end‑to‑end execution brittle.

Bottom line, in Gartner's words: "Most business workflows are too complex for simple agents with limited actions. To prevent agents from choosing incorrect tasks among many options, enterprises should use multiagent solutions to automate complex workflows."

## What Is a Multi-Agent System? Definition & Context

A multi-agent system (MAS) is a coordinated network of autonomous, intelligent agents working together to solve complex problems that single agents can't reliably handle alone.

Think of it like a specialized team: instead of one person doing everything, each member contributes specific expertise while collaborating toward a shared goal. MAS divides complex workflows among specialized agents, each designed to excel at particular tasks.

> Multiagent systems (MAS) are collections of AI agents that interact to achieve individual or shared goals. Agents may be delivered in a single environment or developed and deployed independently across distributed environments.

### Why Multi-Agent Systems Matter

Individual AI agents work well for simple tasks, but enterprise workflows are too complex. LLM-based agents can reliably select from only a small set of actions per step—expand that menu and planning errors multiply. Errors also compound across multi-step processes because models are probabilistic.

Multi-agent systems overcome these limits by specializing agents for narrow roles (data retrieval, validation, execution), limiting action spaces to reduce errors, and coordinating through an orchestrator that manages workflow logic.

### Tool-Using Agents and Architecture

Modern MAS leverages LLM-based agents powered by large language models for reasoning and adaptability. As tool-using agents, they can query databases, call APIs, and invoke specialized functions. Different agents specialize in different toolsets: a data agent handles SQL queries, a compliance agent validates policies, and a communication agent manages notifications.

Gartner describes this as "inner" architecture (runtime, memory, tools within each agent) and "outer" architecture (identity management, observability, guardrails across the platform). Multi-agent systems make complex, multi-step enterprise workflows reliable and scalable.

## Advantages of Multi‑Agent Systems

Think of MAS like an orchestra: a conductor (orchestrator) coordinates sections (agents) with distinct instruments (tools) to execute the score (workflow). Some of the key advantages of this approach include:

- **Reusability** — Modular agents that have been built to perform one function very well can be reused in many workflows, enabling rapid time to value and improving the reliability of the system as a whole.
- **Scalability** — Composing a workflow of multiple agents makes it easier to expand their scope and capacity.
- **Interoperability** — The use of standard protocols (e.g., MCP for model‑to‑tool context, and A2A for communication between agents) paves the way for workflows that involve agents across environments and organizations.
- **Governance and observability** — Clear interfaces and role boundaries enable auditability, runtime evaluation, and guardrails — essential for compliance, safety, and trust.

## Architecture

Gartner notes that "LLM-based agents exhibit an architecture that can be conceptualized through 'inner' and 'outer' structures akin to microservices" (Source: Gartner "Reference Architecture Brief: LLM-Based AI Agent (Inner Architecture)", 7 Nov 2025, Steve Deng, Gary Olliffe).

We interpret this "Inner" architecture as having components enterprises need inside each agent: agent runtime (secure sandbox); agent orchestrator (planning/execution); memory management (short‑term and long‑term); tool use (function/API/MCP); model client (LLM); runtime evaluation for safety and accuracy.

On their own, these inner components aren't enough; organizations also need the outer architecture, consisting of identity and access (IAM) for agents and tools, AI gateways for model access, observability/evals, and guardrails — all coordinated across a multi‑agent platform.

## Real‑Time Context: The Missing Ingredient

MAS won't deliver results if agents act on stale snapshots. Agentic workloads require ubiquitous, real‑time context to plan correctly, select the right tools, meet policy constraints, and avoid rogue actions. For example:

- **Operational state:** Agents need live signals to decide "should we act now?" or "has this condition changed?"
- **Identity, permissions, and risk:** AI agents are non‑human identities that must be authenticated and authorized dynamically, with fine‑grained, temporary entitlements.
- **Policy, governance, and safety:** Enterprise policies (e.g., compliance, data residency, escalation rules) must be enforced at runtime, not only in development; telemetry and immutable audit are also essential.

This reframes "data for AI" from static lakes/warehouses to live, governed interfaces that ensure agents are either fed new information in real-time, as events occur, or is reliably up to the moment when they query for it.

## Why MAS Needs Event‑Driven Architecture

If multi‑agent systems are the orchestra, EDA is the stage, the acoustics, and the conductor's cues. MAS require a fabric where agents and the information sources they rely on publish, subscribe, and react to business events. This is how you give them real‑time context and can coordinate agent actions without coupling agents to every system. Four key attributes of EDA are particularly relevant to MAS:

- **Real‑time signals.** Applications are either instrumented to publish information when events occur, or change data capture (CDC) tracks transactional changes (e.g., "invoice posted") and turns them into events that brokers distribute to applications and agents that have subscribed to receive that kind of information.
- **Loose coupling.** Agents listen for relevant events rather than polling APIs. Systems evolve independently; agents swap in/out with minimal impact.
- **Scalable coordination.** Orchestrators and agents push commands and receive outcomes as events, enabling parallelism and backpressure handling.
- **Observability and replay.** Event logs provide end‑to‑end traceability for audits, time‑travel debugging, and eval‑driven improvement.

Gartner notes the "Success of MAGS (multiagent generative systems) will require specialized software engineering with a data-centric, event-driven architecture." And further states "Event-driven design is ideal for MAGS as it treats AI agents as reactive components that communicate through standardized messages. This approach promotes reusability, seamless integration and scalability, similar to microservices." (Source: Gartner "Emerging Tech: AI Vendor Race: Charting the Path to Enterprise-Scale Multiagent Generative Systems" 2 Dec 2025, Kiumarse Zamanian)

## Five Key Design Requirements for MAS

Within all of these observations and recommendations around real-time data and event-driven architecture, there are five things you must do to ensure the success of multi-agent systems:

- **Adopt a federated data architecture with a semantic layer.** Keep data in domain systems; expose governed data products and standardized events. Implement a semantic layer (ontology + policies) that agents and orchestrators use to interpret data consistently.
- **Standardize event streams and materialized views.** Use CDC and streaming databases to create low‑latency views of operational state for agents. Materialized views offer consistent, queryable snapshots aligned to agent tasks (e.g., "eligible offers now").
- **Instrument the agent runtime for safety and observability.** Treat every agent as a potential semi‑hostile workload: sandbox execution, enforce least‑privilege IAM, log everything (actions, decisions, tool calls), and run runtime evaluations in‑line to gate actions.
- **Use proven orchestration patterns; limit action spaces.** Start with hierarchical or hub‑and‑spoke designs (coordinators + worker agents). Reduce each agent's available actions and validate outputs between steps to avoid error compounding.
- **Implement zero‑trust identity for human and non‑human actors.** Manage users, agents, tools, and devices as identities. Issue dynamic, time‑bounded credentials; log delegation chains; and enforce policy guardrails across data, tools, and actions.

## Executive Takeaway

When it comes to enterprise AI, MAS isn't "nice to have" for enterprise automation — it's required once workflows involve multiple steps, constraints, and systems. But MAS succeeds only if agents have real-time context and can interact with other agents and applications via an event‑driven fabric.

Analyst consensus is clear: multi-agent systems are necessary for enterprise AI; real‑time data access and zero‑trust identity are prerequisites; and EDA is the only way to achieve them.

One of Gartner's suggested recommended actions for the next 6 to 18 months is to "Ensure scalability and reusability by adopting an event-driven architecture that uses standardized messages, events, or commands, and clearly defines agent roles, responsibilities and interfaces."

## References (Footnotes)

1. Gartner "Emerging Tech: AI Vendor Race: Charting the Path to Enterprise‑Scale Multiagent Generative Systems" 2 Dec 2025, Kiumarse Zamanian
2. IDC "FutureScape: Worldwide Data and Analytics 2026 Predictions" Oct 2025, Stewart Bond
3. Gartner "Reference Architecture Brief: LLM‑Based AI Agent (Inner Architecture)" 7 Nov 2025, Steve Deng, Gary Olliffe
4. Gartner "Top Strategic Technology Trends for 2026: Multiagent Systems", 18 Oct 2025
5. Gartner "Quick Answer: How Do Multiagent Systems Overcome a Major Limitation of AI Agents?" 8 Oct 2025, Van Baker, Tom Coshow
