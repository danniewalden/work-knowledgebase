---
title: the native web (thenativeweb)
type: entity
created: 2026-07-18
updated: 2026-07-18
sources: [esdm-event-sourced-domain-modeling, roden-event-sourcing-meets-mcp-whole-story-for-llms]
tags: [org, vendor, event-sourcing, domain-driven-design, tool, focus]
---

# the native web (thenativeweb)

German software company (**the native web GmbH**) founded and led by [[golo-roden]] (founder & CTO).
An [[event-sourcing]]-focused developer-tools vendor and developer-education outlet whose thesis is
that **event sourcing is the right foundation for AI/LLM systems**.

## Products in the KB

- **EventSourcingDB** — a purpose-built event store with a free **[[model-context-protocol|MCP]]
  server** (natural-language read/write of events, subject/event-type search, schema registration,
  an EventQL query language; uses CloudEvents). The "store the events" half of the pitch
  ([[roden-event-sourcing-meets-mcp-whole-story-for-llms]]).
- **[[esdm-event-sourced-domain-modeling|ESDM]]** (Event-Sourced Domain Modeling) — an **MIT-licensed
  YAML language + offline toolchain** (`esdm lint` / `esdm view` / glossary) for describing
  event-sourced domains as version-controlled files. The "describe the domain" half — a fixed core
  schema of [[domain-driven-design]]/[[cqrs]]/[[event-sourcing]] kinds (incl.
  [[dynamic-consistency-boundaries|DCB]]) plus [[given-when-then]] and Domain Storytelling extensions.
  Repo `thenativeweb/esdm`.

## Position in the KB

Across the two products, thenativeweb now spans both layers of making event-sourced systems legible to
LLMs: the **event store** (EventSourcingDB — the *what happened*) and the **modeling language** (ESDM —
the *shape of the domain that produces it*). Both bet on plain, business-language artifacts an LLM can
read and write directly. Distinct vendor voice from the other ES-for-agents camps: [[akka]]
([[kevin-hoffman]]), [[axoniq]] ([[allard-buijze]]), and [[critter-stack]] ([[jeremy-miller]]).

ESDM specifically lands on the [[event-modeled-agent-design]] / [[spec-driven-development]] focus as the
open, tool-backed **file-format + linter** rung — the shipped counterpart to
[[dilger-event-modeling-knowledge-hub-emlang|Dilger's EmLang]] ambition.

## Related

[[golo-roden]] · [[esdm-event-sourced-domain-modeling]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] ·
[[event-sourcing]] · [[model-context-protocol]] · [[event-modeled-agent-design]] · [[axoniq]] · [[akka]] · [[critter-stack]]

_Source pages: [[esdm-event-sourced-domain-modeling]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]]._
