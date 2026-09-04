---
title: Critter Stack (Wolverine + Marten)
type: entity
created: 2026-06-15
updated: 2026-09-04
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy, miller-codebase-is-the-prompt-vertical-slices-ai, miller-jasperfx-ai-skills-agent-skills, miller-new-stuff-in-critter-stack-ai-skills-1-10, miller-ai-assisted-production-support-with-critterwatch, miller-open-core-model-sustainable-oss-dotnet]
tags: [product, dotnet, event-sourcing, vertical-slice-architecture, cqrs, dcb, focus]
---

# Critter Stack (Wolverine + Marten)

The **JasperFx** family of .NET libraries maintained by **[[jeremy-miller]]**:

- **Marten** — a document database + **[[event-sourcing]]** store on PostgreSQL (read models /
  projections, aggregate streams). **Marten 9.0** (May 2026) added a higher-performance
  **[[dynamic-consistency-boundaries|DCB]]** option via PostgreSQL HSTORE (noted on the DCB page).
- **Wolverine** — a messaging / command-handling framework with convention-discovered handlers, method
  injection, a transactional outbox (`[Transactional]`), cascading-message returns, `Wolverine.Http`
  endpoints-as-handlers, and Marten `[AggregateHandler]` event-sourcing handlers.

## Why it's in the KB

Miller's argument ([[miller-codebase-is-the-prompt-vertical-slices-ai]]) positions the Critter Stack —
Wolverine specifically — as the most thorough .NET expression of **[[vertical-slice-architecture]]** and
therefore the AI-friendliest .NET foundation: it compresses a slice down to the business decision,
removing the ceremony an agent would otherwise read and reproduce ([[locality-of-reference]],
[[agent-legibility]]). JasperFx now sells **Critter Stack AI Skills** that encode the conventions
([[harness-engineering]] guides) so the implicit macrostructure isn't left to agent guesswork. Gives
[[cqrs]] / event sourcing "out of the gate." (Vendor context: this is the maintainer's own product.)

**AI Skills 1.6.0** ([[miller-jasperfx-ai-skills-agent-skills]], 2026-07-10) fleshes this out: **81
skills** across Marten, Wolverine, Polecat, and **CritterWatch** (the monitoring/ops console),
source-verified and versioned so an agent stays off stale training data — critical because **Marten 9**
eliminated runtime codegen and **Wolverine 6** moved the Roslyn compiler to an opt-in package, making
"most existing internet advice actively wrong." Shipped as the paid `JasperFx.AiSkills` package
(`agentskills-cli add`). See [[jeremy-miller]] and [[loop-engineering]] (the Skills primitive).

## Event Modeling into the core (2026-08-21)

The stack's AI strategy ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]) commits it to Event Modeling as a
first-class runtime concern rather than a design-time diagram:

- **`JasperFx.Events`** gains a model + fluent API for declaring event types, read model types "and any
  other common elements of Event Storming or Event Modeling."
- **Bobcat** — the spiritual successor to Miller's old Storyteller — visualizes the resulting EM slices,
  carries a Gherkin capability for executable specs, and ships a **"Supervisor"** on the Microsoft
  Testing Platform that manages parallelism, selective retries, and recycling Docker containers or test
  processes when long agent-driven runs degrade. Test output records the Wolverine messages, appended
  events and HTTP calls of each run, with timings, so failures help diagnose themselves.
- **`dotnet watch`** integration to "interactively doodle with slice definitions and see the model change."
- EM concepts pushed **directly into Wolverine and the Marten/Polecat/Fisher stores**, with the code
  authoritative over the declared model.
- **CLI export of slice definitions for AI agent usage**; codegen to scaffold a slice shell from the model.

**CritterWatch 1.0** is live: a commercial MCP *and* CLI surface where "every single bit of information
… and every single action" is exposed through MCP endpoints — static configuration and runtime-discovered
views, dead-letter storage, domain-centric queries against OTel tooling, event-store access and a
projection step-through ([[model-context-protocol]]). Wolverine 9.0's CLI output is explicitly optimized
for agents (message routing, generated handler source, missing-handler diagnosis).

Also announced, without detail: **LLM callouts** from Wolverine and projections via
`Microsoft.Extensions.AI`, and a commercial **agent orchestrator + durable agent memory** on the stack
with **Fisher** (SQLite event sourcing) as substrate — KurrentDb's Capacitor named as the prior art he
rates. Much of this is unshipped; Miller frames the lot as "spaghetti against the wall."

See [[model-as-code-vs-model-as-language]] for why the direction of fit here is contested.

## Shipped state, September 2026

- **AI Skills 1.10.0** (2026-09-02, [[miller-new-stuff-in-critter-stack-ai-skills-1-10]]) brings the
  catalogue to a claimed **102 skills**, up from the **81** of 1.6.0 in July — roughly +26% in eight weeks,
  and **superseding the 81 figure recorded above as a *count*, not as evidence**. New coverage: Wolverine
  Sagas (including from HTTP endpoints), two projection-troubleshooting skills, Marten event
  versioning/upcasting, archiving and stream compaction, full-text/NGram search, `Marten.PgVector`, gRPC,
  MCP servers for your own app, CritterWatch alerts. Also new: a **`projection-run` "projection stepper"
  CLI** in `JasperFx.Events`, shipped in Marten and Polecat. **VENDOR SELF-REPORT on a priced product
  ($250 solo / $1,000 team / $2,000 large team, or bundled with CritterWatch Professional and
  Enterprise); the count is inventory, and no evaluation of skill efficacy exists.**
- Two skill *contents* are checkable facts about the libraries and worth carrying: in `Wolverine.HTTP` the
  **first return value of an endpoint method is the response body**, so returning a `Saga` serializes saga
  state to the caller (the `Saga` must be a later tuple member; `[EmptyResponse]` exists for no-body
  cases); and in Marten **`ArchiveStream` only sets a flag — "archiving alone doesn't shrink anything"** —
  it is `UseArchivedStreamPartitioning` that moves archived events to separate physical storage and buys
  the query performance, *"and it quietly weakens a stream-identity guarantee on the way."* Compare
  [[dudycz-archiving-events-stream-lifetime-slicing]] and [[event-versioning-and-upcasting]].
- **CritterWatch's MCP surface is now demonstrated, not just announced**
  ([[miller-ai-assisted-production-support-with-critterwatch]]): **48 tools — 21 read, 27 action** — mounted
  in two lines of host code, stateless so authorization sees the actual caller, with a **license gate** and
  **opt-in capability-scoped RBAC** (`dlq.replay`, `dlq.discard`, `chaos-monkey.configure`) scoped per
  service, and dead-letter *reads* gated separately from actions. Plus the **projection stepper**
  (before/after state per applied event) and `describe_lifecycle`, which returns a message type's path
  across every monitored service as JSON **and a Mermaid sequence diagram**. **All of it paid-tier, all of
  it VENDOR SELF-REPORT demonstrated over failures the vendor injected with its own chaos monkey, and
  none of it measured** — no baseline, no time-to-diagnosis, no error rate; the agent's diagnoses were
  correct because the answer was planted. See [[model-context-protocol]] and [[agent-governance]].
- **Why the stack ships commercial AI tooling at all**: JasperFx runs an explicit **open-core** model —
  Marten and Wolverine stay MIT, revenue comes from consulting/support plus AI Skills and CritterWatch, and
  as of 2026-08-28 *"another set of commercial tools related to AI assisted development and Event Modeling
  coming soon"* remains **announced, not shipped** ([[miller-open-core-model-sustainable-oss-dotnet]]).

_Source pages: [[miller-codebase-is-the-prompt-vertical-slices-ai]] ·
[[miller-jasperfx-ai-skills-agent-skills]] · [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] ·
[[miller-new-stuff-in-critter-stack-ai-skills-1-10]] (102 skills — VENDOR SELF-REPORT, inventory not
efficacy) · [[miller-ai-assisted-production-support-with-critterwatch]] ·
[[miller-open-core-model-sustainable-oss-dotnet]]._
