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

## [2026-06-13] query    | how should a beginner get started with Event Modeling — filed: outputs/event-modeling-getting-started.md
