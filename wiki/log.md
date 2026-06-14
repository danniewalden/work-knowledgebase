# Log

Append-only chronological record of what happened in the wiki and when — ingests,
queries, lint passes. One line per event, newest at the bottom.

Each entry uses a greppable prefix so `grep "^## \[" wiki/log.md | tail -5` returns
the last 5 events.

Format (each real entry is an `## [date] type | detail` heading):

- `[date] ingest | <Source title> — touched: <N pages>`
- `[date] query  | <question in a few words>`
- `[date] lint   | <count> issues found`

---

## [2026-06-11] init     | Wiki 
## [2026-06-11] research | agentic AI trends & problems solved — filed: 4 raw sources
## [2026-06-11] ingest   | Anthropic — Building Effective Agents — touched: 9 pages
## [2026-06-11] ingest   | LangChain — State of Agent Engineering 2026 — touched: 9 pages
## [2026-06-11] ingest   | Svitla — Agentic AI Market Trends 2025–2026 — touched: 12 pages
## [2026-06-11] ingest   | Deloitte — AI Agents Scaling Faster Than Guardrails — touched: 5 pages
## [2026-06-11] research | harness engineering for coding agents — filed: 5 raw sources
## [2026-06-11] research | primary MCP/A2A specs + Gartner press release — filed: 3 raw sources
## [2026-06-11] ingest   | MCP, A2A, Gartner primary sources — touched: 6 pages
## [2026-06-11] synth    | event-sourced agentic patterns — bridges threads 2 & 3
## [2026-06-11] ingest   | Böckeler — Harness Engineering for Coding Agent Users — touched: 11 pages
## [2026-06-11] ingest   | OpenAI — Harness Engineering (Codex) — touched: 8 pages
## [2026-06-11] ingest   | Anthropic — Effective Harnesses for Long-Running Agents — touched: 7 pages
## [2026-06-11] ingest   | LangChain — The Anatomy of an Agent Harness — touched: 8 pages
## [2026-06-11] ingest   | Firecrawl — What Is an Agent Harness? — touched: 6 pages
## [2026-06-11] research | Hashimoto AI-adoption + Stripe minions — filed: 2 raw sources
## [2026-06-11] ingest   | Hashimoto — My AI Adoption Journey — touched: 7 pages
## [2026-06-11] ingest   | Stripe — Minions (One-Shot Coding Agents) — touched: 8 pages
## [2026-06-11] lint     | 5 issues found (3 fixed: agentic-ai hub cross-refs, context-engineering link, claude-agent-sdk page; 2 flagged: open-closed-principle gap, single-ref markers)
## [2026-06-11] research | Event Modeling applied to agents — filed: 2 raw sources (Dymitruk X post, Qlerify AI tool)
## [2026-06-11] research | Event Modeling × agents (deeper pass) — confirmed Dymitruk quote; eventmodeling.org has no agents post; surfaced academic agent-spec lineage as candidate branch
## [2026-06-11] ingest   | Dymitruk — Event Modeling Is Future Proof (agents) — touched: 7 pages
## [2026-06-11] ingest   | Qlerify — Intelligent Event Modeling Tool — touched: 6 pages
## [2026-06-12] research | daily auto-capture (agents/event-modeling/MCP) — filed: 4 raw sources
## [2026-06-12] ingest   | Confluent — Agentic Event-Driven Systems Architecture — touched: 8 pages
## [2026-06-12] ingest   | Solace — Multi-Agent Systems Need Real-Time Context and EDA — touched: 8 pages
## [2026-06-12] ingest   | Atlan — Event-Driven Architecture for AI Agents — touched: 7 pages
## [2026-06-12] ingest   | prooph board — AI Agent Skills (proophboard/skills) — touched: 6 pages
## [2026-06-12] synth    | agentic event-driven systems — external sources close the patterns↔event-sourcing bridge edge
## [2026-06-12] research | ESAA paper (Event Sourcing for Autonomous Agents, arXiv 2602.23193) — filed: 1 raw source (raw/papers/) via arXiv HTML
## [2026-06-12] ingest   | ESAA — Event Sourcing for Autonomous Agents — touched: 6 pages
## [2026-06-13] query    | how to denote an agent in an event model — filed deliverable: outputs/denoting-an-agent-in-an-event-model.md
## [2026-06-13] lint     | 4 issues found & fixed: created missing pages conways-law, open-closed-principle, react-loop, fitness-functions (resolving 9 dangling links); 0 orphans; index re-synced. Also repaired log.md lines 41-42 corrupted by a stale-mount bash write (Confluent touched-count reconstructed)
## [2026-06-13] research | EM×agents weekly watch — filed: 1 raw source (jwilger/agent-skills: event-modeling skill + factory pipeline)
## [2026-06-13] ingest   | jwilger/agent-skills — Event Modeling skill + factory pipeline — touched: 9 pages

## [2026-06-13] query    | how should a beginner get started with Event Modeling — filed: outputs/even
## [2026-06-13] research | Martin Dilger LinkedIn post "Automatic Domain Discovery using Claude Code" — filed: 1 raw source (raw/articles/)
## [2026-06-13] research | Martin Dilger LinkedIn recent activity (via Chrome, logged in) — filed: 3 raw sources (Faros AI report, Spec-Driven Development applied, Keep Command Handlers pure)
## [2026-06-13] ingest   | Martin Dilger (4 LinkedIn posts: Faros report, Spec-Driven Dev, Command Handlers pure, Auto Domain Discovery) — touched: 11 pages (4 sources; entities martin-dilger + eventmodelers-ai; concepts spec-driven-development + domain-discovery new, event-modeled-agent-design + agentic-coding updated; index)
## [2026-06-14] research | EM×agents + people watch (live Chrome for Dilger LinkedIn) — filed: 3 raw sources (Dilger "living spec / always-on agent" 12h post, Dilger "Hold my Beer Engineer" 3h teaser, Fraktalio "Connect AI Agents to Your Board via MCP" 1d post). Added Fraktalio to watch-config people list. Flagged (not filed, off focus-scope): AAIF/Angie Jones "Karpathy's LLM Wiki as Agent Memory" (2026-06-08).
## [2026-06-14] ingest   | Dilger living-spec/always-on-agent + Dilger Hold-my-Beer (stub) + Fraktalio Event Modeler MCP — touched: 11 pages (3 source pages new; entity fraktalio new; entities martin-dilger + eventmodelers-ai updated; concepts event-modeled-agent-design, spec-driven-development, model-context-protocol updated; index + overview)
## [2026-06-14] research | Nick Tune LinkedIn (live Chrome) — added to watch-config; filed: 1 raw source (Nick Tune "Graphs+Memory+Skills+Agents / what you build underneath an agent", 2d post). Rest of his recent feed = reposts of AI-sovereignty news (off-thread, not filed).
## [2026-06-14] research | Jeremy Miller (Shade Tree Developer) blog + LinkedIn (live Chrome) — added to watch-config (blog jeremydmiller.com + LinkedIn). filed: 0 — recent posts (Markdown Snippets docs, Polecat SQL Server event store, JasperFx 3rd-anniversary, F# support blog 06-01) are Critter Stack tooling/docs/business; on the event-sourcing substrate but none on the EM×agents focus. Watching for a future agentic angle.
## [2026-06-14] research | Focus broadened to ES/DCB/CQRS/vertical-slice (new watch-config topic, scope anything-substantive). Backfill (14d) found the notable DCB releases OUT of window (Axon Framework 5 DCB Jun-2025; Marten 9.0 DCB May-25-2026), so filed 2 FOUNDATIONAL seed sources instead: pellegrini-dynamic-consistency-boundary (DCB origin, 2023), bogard-vertical-slice-architecture (VSA origin, 2018).
## [2026-06-14] ingest   | DCB + VSA concept seeds — touched: 8 pages (2 source pages: pellegrini-dcb, bogard-vsa; 2 concept stubs: dynamic-consistency-boundaries, vertical-slice-architecture; 2 entities: sara-pellegrini, jimmy-bogard; cross-links added to event-sourcing + cqrs; index)
## [2026-06-14] research | Adam Tornhill (CodeScene) LinkedIn (live Chrome) — added to watch-config. filed: 1 raw source (Tornhill reshare of CodeScene "What Unhealthy Code Costs in the Agentic Era" — research claim: unhealthy code +35–45% agent token spend; agents worst in high-debt legacy code). Off-thread, not filed: his "Writing with LLMs / what's lost" post + a code-naming post.
## [2026-06-14] ingest   | Tornhill/CodeScene "Unhealthy Code in the Agentic Era" — touched: 4 pages (source page; entity adam-tornhill new; concept agentic-coding updated with code-health↔agent-cost finding + harness/maintainability-sensors link; index)
## [2026-06-14] research | Yves Goeleven LinkedIn (live Chrome, deep/120-day backfill — infrequent burst poster) — added to watch-config (LinkedIn + blogs goeleven.com, cloudshaper.wordpress.com, lookback_override 120d). filed: 1 raw source (Goeleven "event sourcing ≠ auditing for free", ≈Apr 2026). Many more long-form posts available (data mesh/autonomous capabilities, business capabilities) + a 2023 Event-Model-into-code series — flagged to ingest from his blog next. Created source page + entity yves-goeleven.
## [2026-06-14] research | Goeleven "translate an Event Model into code" series (live Chrome, post permalinks via get_page_text) — filed: 3 raw sources (EM-visualizes-business-processes 2023-10; interaction-design Aggregate/Outbox/Projection 2023-08; Event-Sourced-Projection part-3 2023-11).
## [2026-06-14] ingest   | Goeleven Event-Model-to-code series — touched: 6 pages (3 raw → 1 consolidated source page goeleven-event-model-to-code-series; entity yves-goeleven updated; concept event-modeling updated with the practitioner "process + code mapping" lens; index). Series has more parts than the 3 captured.
## [2026-06-14] ingest   | New concept business-capabilities (flagged important by Dannie) — touched: 6 pages (concept business-capabilities new; cross-links from event-modeling, event-sourcing, domain-driven-design, conways-law; index). Also added business capabilities as sub-area (5) of the design-substrate watch topic + noted in focus memory. Grounded on Goeleven; wanted next: a primary on capability-based design + the EM↔Wardley link.
## [2026-06-14] research | Business-capabilities primary + EM×Wardley — filed: 2 raw (Homann 2006 "A Business-Oriented Foundation for Service Orientation" — summary/copyright-trimmed, raw/papers/; Daniel "Event Modeling and Wardley Mapping" 2020 series pointer, raw/articles/).
## [2026-06-14] ingest   | Homann business capabilities + EM×Wardley — touched: 8 pages (2 source pages homann-business-capabilities + daniel-event-modeling-wardley-mapping; entity ulrich-homann new; concept wardley-mapping new stub; concept business-capabilities fleshed out w/ Homann primary + Wardley strategy lens; index). business-capabilities now grounded on the seminal primary, not just Goeleven.
## [2026-06-14] ingest   | Böckeler — Maintainability Sensors for Coding Agents — touched: 8 pages (source page new; concept mutation-testing new; updated feedforward-and-feedback-controls, harness-engineering, fitness-functions, birgitta-bockeler, overview, index)
## [2026-06-14] research | EM×agents + people watch (lookback 14d) — filed: 0 — nothing new. Topic quiet (latest on-topic: Event-B Agent arXiv 2605.17475 dated May 17 — Abrial's Event-B ≠ Dymitruk's Event Modeling, off-topic + stale). People all quiet in-window: Dilger blog tops at Mar 28 + podcast Ep.34 Jan 12, Karpathy blog Apr 30, Böckeler last article May 19. Only in-window hit = Fowler "Fragments: June 2" — off-thread, not on watch list. NOTE: Dilger LinkedIn not fetchable headless (needs live Chrome) — possible uncovered posts there.
## [2026-06-14] ingest   | Dilger — From Idea to Event Model to Code (Craft Conf talk) — touched: 6 pages (source page new; entity nebulit new; entity martin-dilger updated; overview + index; cross-links to event-modeling/event-sourcing/cqrs/agentic-coding)
## [2026-06-14] ingest   | Nick Tune — Graphs + Memory + Skills + Agents — touched: 5 pages (source page new; entity nick-tune new; concept context-engineering updated w/ substrate view; overview + index)
