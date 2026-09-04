---
title: "Source: ESAA — Event Sourcing for Autonomous Agents (LLM-Based SWE)"
type: source
created: 2026-06-12
updated: 2026-06-12
sources: [esaa-event-sourcing-for-autonomous-agents]
raw_file: [raw/papers/esaa-event-sourcing-for-autonomous-agents.md]
tags: [event-sourcing, cqrs, agentic-ai, multi-agent, academic, focus]
---

# Source: ESAA — Event Sourcing for Autonomous Agents (LLM-Based SWE)

Academic preprint by **Elzo Brito dos Santos Filho** (arXiv:2602.23193, Feb 2026). The first
**non-vendor, peer-style** source in the KB to apply [[event-sourcing]] + [[cqrs]] directly to
multi-agent LLM software engineering — the academic counterpart to the vendor
[[agentic-event-driven-systems]] sources. Raw capture (from arXiv HTML; the PDF has no extractable
text): `raw/papers/esaa-event-sourcing-for-autonomous-agents.md`.

## Summary

ESAA reframes the reliability problem as **restructuring the system around verifiable invariants**,
not prompt-tuning. LLMs are treated as **intention emitters under contract**, never developers with
write access: an agent emits only validated JSON intentions (`agent.result` / `issue.report`); a
**deterministic orchestrator** validates them against boundary contracts + JSON Schema, appends to an
append-only log (`activity.jsonl`), applies file effects, and projects a hash-verified materialized
view (`roadmap.json`). Replay (`esaa verify`) reconstructs state and detects divergence via SHA-256.

## Key points

- **Event sourcing as the source of truth** for an agent's lifecycle: current state is a *projection*
  of an immutable log of intentions/decisions/effects, not the repo snapshot — explicitly citing
  Fowler's Event Sourcing and CQRS.
- **Agent ≠ writer.** The agent gets only a **purified view** (roadmap + relevant facts), never raw
  state — directly mitigating *lost-in-the-middle* [[context-rot]].
- **Boundary contracts + PARCER metaprompting** force a strict JSON envelope per role; violations emit
  `output.rejected` (zero across both case studies, across four LLM providers) — a deterministic,
  contract-bounded analog of [[feedforward-and-feedback-controls]].
- **Immutability-of-done**; defects spawn an `issue.report` hotfix path without rewriting history —
  forensic traceability (cf. [[agent-governance]] audit trails).
- **Multi-agent concurrency** serialized at the event level: total ordering preserved, conflicts
  detected before effects apply ([[multi-agent-orchestration]]).
- **Case studies:** (1) landing page — 9 tasks, 49 events, single-agent composition; (2) clinical
  dashboard "clinic-asr" — 50 tasks, 86 events, **4 concurrent heterogeneous LLMs** (Claude Sonnet 4.6,
  Codex GPT-5, Antigravity/Gemini 3 Pro, Claude Opus 4.6) over ~15h, 8/15 phases done. Both
  `verify_status=ok`.
- Claims uniqueness vs. AutoGen/MetaGPT/LangGraph/CrewAI on: immutable event log, deterministic
  replay, hash-verified projection, "done" immutability, blast-radius containment.
- **Limits:** n=2 case studies, controlled scopes, temperature 0.0; not yet tested on SWE-bench /
  enterprise repos. Feasibility + verifiable invariants demonstrated, not benchmark performance.

## Connections / contrast

The **external, non-vendor corroboration** the KB's [[event-sourced-agentic-patterns]] synthesis was
missing: an independent academic source arrives at "append-only ledger + replay + projections as the
reliable substrate for nondeterministic agents." Sits alongside [[agentic-event-driven-systems]]
(Confluent/Atlan/Solace) but without the product-pitch caveat. **Nuance for the focus area:** ESAA
uses event *sourcing/CQRS*, **not** [[event-modeling]] the design method — so it strengthens Thread 2,
not [[event-modeled-agent-design]] directly, though its "agent emits intentions, orchestrator applies
effects" split is strikingly close to Event Modeling's **command → event** flow and the Automation
pattern. Its purified-view + contract design also rhymes with the [[harness-engineering]] thread
(initializer-executor, [[long-running-agents]]).

_Source page: [[esaa-event-sourcing-for-autonomous-agents]]._
