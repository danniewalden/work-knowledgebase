---
title: Golo Roden
type: entity
created: 2026-06-21
updated: 2026-08-14
sources: [roden-event-sourcing-meets-mcp-whole-story-for-llms, esdm-event-sourced-domain-modeling, roden-too-many-islands-em-conf-2026, dilger-eventmodelers-supports-esdm-export]
tags: [person, vendor, event-sourcing, model-context-protocol, domain-driven-design, focus]
---

# Golo Roden

Founder & CTO of **[[thenativeweb|the native web GmbH]]**, the company behind **EventSourcingDB** — a
purpose-built event store — and **[[esdm-event-sourced-domain-modeling|ESDM]]**, an event-sourced
domain-modeling language. Active developer-educator who publishes on [[event-sourcing]] and AI; the
heise blog series argues event sourcing is "the perfect foundation for AI."

## Position in the KB

A new **event-sourcing-vendor voice** on the ES × agents thread, distinct from [[akka]]
([[kevin-hoffman]]), [[critter-stack]] ([[jeremy-miller]]), and [[axoniq]] ([[allard-buijze]]). His
contribution ([[roden-event-sourcing-meets-mcp-whole-story-for-llms]]) is the cleanest statement of the
**[[event-sourcing]] × [[model-context-protocol|MCP]] × [[context-engineering]]** bridge: event
sourcing supplies the complete, business-language history ("the whole book, not the last chapter"),
MCP makes it reachable in natural language, and **events are "the natural language for LLMs."**

## Product — EventSourcingDB

A standalone event store with a free **MCP server** (Mar 2026): natural-language read/write of events,
subject/event-type search, schema registration, and an **EventQL** query language; uses **CloudEvents**
(business-named types, per-entity *subjects*). Roden frames the ES×MCP principle as product-neutral —
EventSourcingDB is "merely a concrete example."

## Product — ESDM

A second product, **[[esdm-event-sourced-domain-modeling|ESDM]]** (Event-Sourced Domain Modeling), an
**MIT-licensed** YAML language + offline toolchain (`esdm lint` / `esdm view` / glossary) for describing
event-sourced domains as version-controlled files. Where EventSourcingDB stores the events, ESDM
describes the domain's *shape* — a fixed core schema of [[domain-driven-design]]/[[cqrs]]/[[event-sourcing]]
kinds (incl. [[dynamic-consistency-boundaries|DCB]]) with [[given-when-then]] and Domain Storytelling
extensions, and "modeling with AI" as a first-class use case. It puts Roden's "events are the natural
language for LLMs" thesis one layer up, at the *modeling* layer.

## At the EM Conference 2026 (Munich)

Roden attended and spoke at the 2nd Event Modeling Conference and wrote its published recap,
[[roden-too-many-islands-em-conf-2026|"Too Many Islands, Too Few Bridges"]] (2026-06-29). His talk,
*"Your Domain Model Belongs in the Repository,"* argued the model must live as versioned plain text
in Git beside the code (models otherwise "die the moment the workshop ends"), and he demoed
[[esdm-event-sourced-domain-modeling|ESDM]] round-tripping live — an AI reverse-engineered an ESDM
model from an existing app, then generated Kotlin *and* Python implementations from that one model.
His recap is also the primary framing of the fragmentation problem and "The Munich Event" foundation
proposal (see [[em-standardization-foundation]]).

## First adopter of ESDM outside thenativeweb (2026-08-13)

That Munich conversation produced a concrete bridge: **[[martin-dilger]]'s [[eventmodelers-ai]] now
exports any Event Model to ESDM** via UI, API, [[model-context-protocol|MCP]] and CLI, so an agent can
"request any modeled slice or chapter in the format it needs" — and the two are working on an **Event
Modeling extension to ESDM** to carry the timeline notion ESDM currently lacks
([[dilger-eventmodelers-supports-esdm-export]]). It is the first captured case of a competing tool-maker
adopting Roden's format, and the most tangible thing yet to come out of his own "too many islands, too
few bridges" complaint ([[agent-readable-model-artifacts]], [[em-standardization-foundation]]).

## Related

[[thenativeweb]] · [[esdm-event-sourced-domain-modeling]] · [[event-sourcing]] · [[model-context-protocol]] ·
[[context-engineering]] · [[agent-explainability]] · [[event-modeled-agent-design]] · [[em-standardization-foundation]] · [[axoniq]] · [[akka]] · [[critter-stack]]

_Source pages: [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] · [[esdm-event-sourced-domain-modeling]] · [[roden-too-many-islands-em-conf-2026]] · [[dilger-eventmodelers-supports-esdm-export]]._
