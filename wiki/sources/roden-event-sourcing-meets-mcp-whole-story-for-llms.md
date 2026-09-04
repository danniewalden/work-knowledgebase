---
title: "Golo Roden — Event Sourcing meets MCP: The whole story for LLMs"
type: source
created: 2026-06-21
updated: 2026-06-21
sources: [roden-event-sourcing-meets-mcp-whole-story-for-llms]
raw_file: [raw/notes/roden-event-sourcing-meets-mcp-whole-story-for-llms.md]
tags: [event-sourcing, model-context-protocol, context-engineering, agentic-ai, agent-explainability, focus]
---

# Golo Roden — Event Sourcing meets MCP: The whole story for LLMs

Article by **[[golo-roden]]** (founder & CTO, the native web GmbH), heise online developer blog,
2026-04-02. Summary note (heise+ is monetized — captured per the copyright-conscious convention).
Source file: `raw/notes/roden-event-sourcing-meets-mcp-whole-story-for-llms.md`. English translation of
the German original "Event Sourcing trifft MCP: Die ganze Geschichte für LLMs."

## Thesis

A sequel to Roden's Aug-2025 "Event Sourcing is the perfect foundation for AI." The pairing solves
two complementary problems: **[[event-sourcing]] solves the *data* problem** (complete, context-rich,
business-language history) and **[[model-context-protocol|MCP]] solves the *access* problem** (a
standardized interface that makes that data reachable by any LLM in natural language). Neither
suffices alone.

## Key points

- **Context > model.** *"An average model with excellent context delivers better results than a top
  model lacking context."* Context means above all the *data* the model can access — a
  [[context-engineering]] claim.
- **CRUD = the last chapter only.** State-based databases store only current state; for an LLM that is
  "like handing it a book containing only the last chapter." Event sourcing turns the last chapter
  back into the whole book — each event records *what* happened, *when*, and in what *business
  context*.
- **MCP as a data-agnostic bridge.** The protocol doesn't care whether a relational DB, file system,
  API, or event store sits behind it — so *the data source determines how sturdy the bridge is*. "A
  CRUD database connected via MCP still only provides snapshots. An event store provides the whole
  story." This is the [[event-modeled-agent-design|agent↔system]] seam made literal at the data layer
  (cf. [[fraktalio-event-modeler-connect-ai-agents-mcp|MCP as the agent↔model bridge]] one layer up).
- **Worked library domain.** Events (`BookAcquired`, `BookBorrowed`, `ReaderAccepted`…) implemented
  with **CloudEvents** (business-named reverse-domain `type`; each book/reader a *subject* = its own
  stream). An LLM with MCP access can enumerate subjects and event types, learn the domain unaided,
  and answer questions impossible against CRUD ("books acquired but never borrowed"; a reader's full
  borrowing history) — and even formulate hypotheses — with **no pre-built read model**.
- **Events are the natural language for LLMs** — (1) phrased in business language (semantics in the
  data, not cryptic status codes); (2) chronological → readable as a *narrative*, closer to text than
  to a relational table; (3) self-contained and context-rich. Explicit tie to [[context-engineering]]:
  events deliver the richest context "already written in the language LLMs understand best."
- **EventSourcingDB MCP Server (Mar 2026).** A free MCP server: read/write events, search subjects &
  event types, register schemas, run EventQL, query the built-in docs — natural-language access to an
  event store. Roden stresses the principle is **product-neutral**; EventSourcingDB is "merely a
  concrete example."
- **Durability.** Models, prompts, even MCP will evolve; "what will not change are the stored events."
  Storing events is investing in data that "gains value with every new model and every future access
  method."
- **Closing caution.** "Standardized access to insufficient data yields standardized insufficient
  results" — CRUD-over-MCP lets an LLM *describe* the present; an event store lets it *explain*.

## Why it matters here

The cleanest articulation of the **event-sourcing × MCP × context-engineering** bridge, and a new
event-sourcing-vendor voice ([[golo-roden]]/EventSourcingDB) distinct from [[akka]],
[[critter-stack]], and [[axoniq]]. Pairs with the [[akka-event-sourcing-backbone-agentic-ai|Akka
"backbone"]] thesis, the [[confluent-agentic-event-driven-systems-architecture|Confluent]]/[[atlan-event-driven-architecture-for-ai-agents|Atlan]]
EDA sources, and the academic [[esaa-event-sourcing-for-autonomous-agents|ESAA]] preprint — and it
sits next to [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] (same-week
filing): both argue the event **store** (full causal history), not the event **stream**/CRUD
snapshot, is what LLMs/agents need — Roden for *context quality*, AxonIQ for *explainability/audit*.
Resonates with [[dilger-event-modeling-knowledge-hub-emlang|Dilger's "EM as an MCP-fed knowledge
hub"]] from the same digest. See [[agent-explainability]].

## Caveats

Summary (not verbatim) of a paywalled, monetized publication. Vendor-authored (the native web makes
EventSourcingDB), so "event store > CRUD over MCP" is motivated — though the argument is
infrastructure-neutral and corroborated by AxonIQ and the EDA thread.

## Touches

[[golo-roden]] · [[event-sourcing]] · [[model-context-protocol]] · [[context-engineering]] ·
[[agentic-event-driven-systems]] · [[event-driven-architecture]] · [[agent-explainability]] ·
[[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] · [[event-modeled-agent-design]]

_Source: `raw/notes/roden-event-sourcing-meets-mcp-whole-story-for-llms.md`._
