---
title: Atlan
type: entity
created: 2026-06-12
updated: 2026-06-12
sources: [atlan-event-driven-architecture-for-ai-agents]
tags: [vendor, metadata, data-governance, context-layer, eda]
---

# Atlan

Data-and-AI governance platform ("context layer"): metadata management, data lineage/catalog, and a
Kafka-based Metadata Change Log that streams metadata events to AI agents; ships an MCP server.

In this KB, Atlan is the publisher of [[atlan-event-driven-architecture-for-ai-agents]] (Emily Winks,
Mar 2026), a primer on [[event-driven-architecture]] for agents that explicitly names **event
sourcing** as one of four agent-coordination patterns — validating [[event-sourced-agentic-patterns]].
Its recurring theme — that the **semantic context layer** telling agents *what events mean* matters as
much as the event plumbing — connects to [[context-engineering]]. Vendor stance: sells the context
layer, so the framing is self-interested; the pattern taxonomy is general.
