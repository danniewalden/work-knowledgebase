---
source_url: https://www.heise.de/en/blog/Event-Sourcing-meets-MCP-The-whole-story-for-LLMs-11244252.html
title: "Event Sourcing meets MCP: The whole story for LLMs"
author: Golo Roden (founder & CTO, the native web GmbH)
publication: heise online — Developer blog ("the next big thing")
published: 2026-04-02
retrieved: 2026-06-18
type: note
---

# Event Sourcing meets MCP: The whole story for LLMs — summary note

**Capture caveat:** heise online is a monetized publication (article sits behind a heise+ wall on the page). Per the wiki's copyright-conscious convention for paid/personal publications (cf. the Tornhill Substack and Khononov blog captures), this is a SUMMARY with short representative quotes, NOT a verbatim reproduction. Out of the 14-day watch window (published Apr 2, 2026) but flagged in the 2026-06-18 scheduled run as a genuinely-new, on-thread ES×agents×context-engineering primary worth an extended-lookback capture. Article is the English translation of the German original "Event Sourcing trifft MCP: Die ganze Geschichte für LLMs." 14-min read.

## Thesis

A sequel to Roden's Aug-2025 piece "Event Sourcing is the perfect foundation for AI." That earlier thesis: without complete, context-rich data, even the most powerful model is blind; event sourcing supplies that data because it stores the entire business history, not just current state. The open question left then — *how do you make that data accessible to an LLM?* — is answered here: the **Model Context Protocol (MCP)**.

The pairing solves two complementary problems at once: **Event Sourcing solves the data problem** (complete, context-rich, business-language data) and **MCP solves the access problem** (a standardized interface that makes that data reachable by any LLM). Neither suffices alone.

## Key points

- **Context > model.** "An average model with excellent context delivers better results than a top model lacking context." Context means above all the *data* the model can access, not just the prompt.
- **CRUD = the last chapter only.** Most databases store only current state. A relational DB says a customer is "Premium" but not since when, why, or through what interactions; says an order is "open" but not that it was changed three times, canceled, and re-placed. "For an LLM, this is like handing it a book containing only the last chapter." Event Sourcing turns the last chapter back into the entire book — each event records what happened, when, and in what business context.
- **MCP as a universal bridge.** Open standard from Anthropic (Nov 2024), now broadly supported (OpenAI, Google, others). JSON-RPC-based; an MCP server exposes tools/data an LLM uses via an MCP client, in natural language. Crucially **data-source agnostic** — the protocol doesn't care whether a relational DB, file system, API, or event store sits behind it. So the open question becomes: *what quality is the data flowing through the channel?* "If MCP is the bridge... then the data source determines how sturdy this bridge can be. A CRUD database connected via MCP still only provides snapshots. An event store, on the other hand, provides the whole story."
- **Worked example — a public library domain.** Events: `BookAcquired` (title/author/ISBN), `BookBorrowed`, `BookReturned`, `ReaderApplied`, `ReaderAccepted`. Implemented with the **CloudEvents** standard — business-named `type` in reverse-domain notation (`io.eventsourcingdb.library.book-borrowed`); each book and reader is a *subject* (its own event stream / full history). An LLM with MCP access to the store can enumerate subjects and event types, learn the domain structure unaided, and answer questions that are hard/impossible against CRUD:
  - "Which books were acquired in the past twelve months but never borrowed?" (presence of `BookAcquired` + absence of `BookBorrowed`).
  - "Show the complete borrowing history of reader 23." (every borrow/return/late-return/fee, not just the current loan).
  - "Which books are frequently borrowed but rarely returned on time?" — and the LLM can then *formulate hypotheses* (length? popularity? specific late readers?).
  - No pre-built read model or pre-programmed analysis required; flexibility comes from the raw data being business-complete and historical.
- **Events are the natural language for LLMs** — three reasons: (1) events are phrased in business language (semantics are *in the data*; no cryptic status codes / `type=3` / foreign keys to guess at); (2) chronological order lets the LLM read events as a *narrative* — structurally closer to text than to a relational table, which is exactly what LLMs handle best; (3) each event is self-contained and context-rich, carrying its business context (a `BookBorrowed` sits within the subject = the book's whole history), reducing the need for extra explanation. Explicit tie to **context engineering**: events deliver the richest, most structured, most relevant context "without requiring additional preparation... already written in the language that LLMs understand best."
- **From idea to practice.** Mid-March 2026, a free **MCP server for EventSourcingDB** was released: interact with the store in natural language via any LLM — read/write events, search subjects & event types, register event schemas, run EventQL queries, even query the built-in EventQL docs. Runs as a standalone process alongside the DB; TLS + token auth; Docker image. "What previously required experienced developers with knowledge of the query language and data structure becomes accessible to a broader audience through natural language." Roden stresses the principle is **not product-specific** — it applies to any event store that offers (or will offer) an MCP server; EventSourcingDB is "merely a concrete example."
- **Durability of the combination.** Models, prompts, and even MCP will keep evolving; "what will not change are the stored events. They remain the immutable foundation." Storing events today is investing in data "that gains value with every new model and every future access method."
- **Closing caution.** "Standardized access to insufficient data yields standardized insufficient results." CRUD-over-MCP gives an LLM the current state (better than nothing); an event store gives it the whole business history — so it can *explain*, not just describe.

## Wiki relevance / links

- Direct **event-sourcing × agents × context-engineering** bridge — pairs with [[akka-event-sourcing-backbone-agentic-ai]], [[confluent-agentic-event-driven-systems-architecture]], [[atlan-event-driven-architecture-for-ai-agents]], and the academic [[esaa-event-sourcing-for-autonomous-agents]].
- Strong corroboration for the new [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] capture (same week's filing): both argue the event STORE (full causal history), not the event STREAM/CRUD snapshot, is what agents/LLMs need — Roden for context quality, Axoniq for explainability/audit.
- Concepts touched: [[event-sourcing]], [[model-context-protocol]], [[context-engineering]], [[event-driven-architecture]], [[agentic-event-driven-systems]].
- Entity to create on ingest: **Golo Roden / the native web GmbH** (EventSourcingDB) — a new event-sourcing-vendor voice on the ES×LLM thread, distinct from Axon/Critter Stack/Marten.
