---
title: John deVadoss
type: entity
created: 2026-07-31
updated: 2026-07-31
sources: [devadoss-cead-capability-aligned-agent-design]
tags: [person, agentic-ai, enterprise-architecture, business-capabilities, multi-agent, focus]
---

# John deVadoss

Enterprise-architecture author affiliated with the **InterWork Alliance** (Washington DC; contact
`johnd@ieee.org` — i.e. active in the IEEE community). In this KB he is the author of the 2026 paper
**"Designing Intelligent Enterprise Agents: A Capability-Aligned Multi-Agent Architecture"**
([[devadoss-cead-capability-aligned-agent-design]], arXiv:2605.08258, 2026-05-07), which introduces
**CEAD** (Capability-Aligned Enterprise Agent Design) and the **Agent Capability Contract (ACC)**.

## Position — capability before agent

deVadoss's core claim is **design-first over governance-first**: an enterprise multi-agent system should
be decomposed around **durable [[business-capabilities|business capabilities]]** and their
ownership/authority/state/evaluation boundaries *before* deciding how many agents to build or what to
prompt them ("capability before agent," "boundary before topology"; "role names are not architecture").
He treats SOA as a design **exemplar** (contracts, registries, loose coupling) but insists services are
not agents, and reads microservices as a **warning**: undisciplined decomposition yields distributed
monoliths — and, for agents, **micro-agent proliferation**.

His signature artifact, the **ACC**, extends the SOA service contract/SLA for the agent era (autonomy
level, tool scopes, memory design, verification, escalation, evaluation evidence, retirement) — the
descendant of [[ulrich-homann|Homann's]] contracted capability **black box**, now carrying autonomy,
memory, and verification.

## In the KB

deVadoss is a new theory anchor on the **flagged-important** [[business-capabilities]] focus, extending
it explicitly into multi-agent architecture. He sits alongside [[ulrich-homann]] (capability black box /
contract lineage), [[yves-goeleven]] (capability owns decisions; contract between capabilities), and
[[rico-fritzsche]] (capability-as-home / RPU) — all independently landing on the durable capability as
the right boundary. On the organization side, his architecture argument is mirrored by
[[matthew-skelton]]'s value-flow-team-as-agent-boundary claim
([[skelton-team-topologies-foundation-ai-roi]]). Relevant to
[[multi-agent-orchestration]], [[agent-governance]], and [[coupling-taxonomy]].

## Where he appears

- [[devadoss-cead-capability-aligned-agent-design]] — CEAD: capability-aligned multi-agent architecture;
  the ACC; the 10,000-task evaluation (arXiv, 2026-05-07).

_Source pages: [[devadoss-cead-capability-aligned-agent-design]]._
