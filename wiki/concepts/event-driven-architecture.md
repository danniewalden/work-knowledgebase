---
title: Event-Driven Architecture (EDA)
type: concept
created: 2026-06-12
updated: 2026-06-12
sources: [atlan-event-driven-architecture-for-ai-agents, confluent-agentic-event-driven-systems-architecture, solace-multi-agent-systems-real-time-context-eda, akka-agentic-systems-are-distributed-systems]
tags: [eda, event-sourcing, agentic-ai, architecture, multi-agent]
---

# Event-Driven Architecture (EDA)

A design style where components communicate by **producing and consuming discrete events**
(immutable, timestamped facts) through a message broker, rather than by synchronous calls or
polling. Producers and consumers are **decoupled**: a producer doesn't know who consumes its
events, and new consumers attach to a topic without changing anything upstream.

EDA is the architectural genus; [[event-sourcing]] is a specific pattern within it (store state
*as* the ordered event log and replay to reconstruct), and [[cqrs]] (separate write/read models)
and [[event-modeling]] (design the system as a timeline of events) sit in the same family.

## Why agent systems converge on EDA

Across three independent 2026 sources ([[atlan-event-driven-architecture-for-ai-agents]],
[[confluent-agentic-event-driven-systems-architecture]],
[[solace-multi-agent-systems-real-time-context-eda]]), the same argument recurs: agents are
inherently event-driven — they **perceive events, reason, and emit actions that become new events**.
EDA gives them:

- **Real-time context without polling** — agents subscribe and react in milliseconds (Atlan claims
  70–90% lower latency vs polling; complexity drops O(N²)→O(N)).
- **Loose coupling & independent scaling** — agents swap in/out; each scales on its own workload.
- **Fault isolation & replay** — events persist in a durable log; a failed agent restarts from its
  last committed offset with no data loss.
- **Auditability** — the event log is the governance/audit substrate ([[agent-governance]]).

Common brokers: Apache Kafka (the default — [[confluent]]), Apache Pulsar, AWS EventBridge; Solace
markets an event mesh. This is the infrastructure half of [[agentic-event-driven-systems]].

## Recurring agent coordination patterns

[[atlan-event-driven-architecture-for-ai-agents]] names four (matching the KB's hand-built mapping in
[[event-sourced-agentic-patterns]]): **event chaining** (pipeline), **fan-out** (parallel),
**event sourcing** (stateful audit/replay), **saga orchestration** (long-running, compensating
events). Confluent adds competitive and hierarchical coordination.

## Significance in this KB

EDA is the **external bridge** that connects Thread 3 (agent patterns/[[multi-agent-orchestration]])
to Thread 2 ([[event-sourcing]] backbone). Before June 2026 the link was the KB's own synthesis
([[event-sourced-agentic-patterns]]); these three vendor/analyst sources now assert it explicitly
(see [[agentic-event-driven-systems]]). Caveat: all three publishers sell EDA tooling, so treat the
"EDA is necessary" conclusion as motivated — though [[solace]]'s analyst citations ([[gartner]],
[[idc]]) are independent. EDA (streaming/messaging) is also not the same as [[event-modeling]] the
*design method*, which remains the focus-area frontier ([[event-modeled-agent-design]]).

_Sources: [[atlan-event-driven-architecture-for-ai-agents]] · [[confluent-agentic-event-driven-systems-architecture]] · [[solace-multi-agent-systems-real-time-context-eda]] · [[akka-agentic-systems-are-distributed-systems]]._
