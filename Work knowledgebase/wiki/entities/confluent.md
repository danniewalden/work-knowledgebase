---
title: Confluent
type: entity
created: 2026-06-12
updated: 2026-06-12
sources: [confluent-agentic-event-driven-systems-architecture]
tags: [vendor, kafka, event-streaming, eda]
---

# Confluent

Data-streaming company founded by the original creators of **Apache Kafka**; commercializes Kafka
(Confluent Cloud/Platform) plus Apache Flink stream processing, schema governance, and—relevant
here—"Streaming Agents" and an MCP server for AI tooling.

In this KB, Confluent is the publisher of [[confluent-agentic-event-driven-systems-architecture]]
(Mohtasham Sayeed Mohiuddin, May 2026), the most detailed external argument that [[agentic-ai]]
should run on an [[event-driven-architecture]] / [[event-sourcing]] backbone — see
[[agentic-event-driven-systems]]. Vendor stance: Kafka/Flink are the proposed backbone, so the
piece is partly promotional, but its architecture and design principles are general.

Adjacent to [[akka]] in the KB's Thread 2 (both argue event infrastructure underpins agents),
though Confluent frames it as event *streaming* rather than Akka's actor/event-sourcing framing.
