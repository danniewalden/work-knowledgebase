---
source_url: https://arxiv.org/abs/2602.23193
title: "ESAA: Event Sourcing for Autonomous Agents in LLM-Based Software Engineering"
author: Elzo Brito dos Santos Filho
publication: arXiv (preprint 2602.23193)
published: 2026-02
retrieved: 2026-06-11
type: paper
---

# ESAA: Event Sourcing for Autonomous Agents in LLM-Based Software Engineering

Elzo Brito dos Santos Filho (elzo.santos@cps.sp.gov.br). arXiv:2602.23193, February 2026.

> Captured from the arXiv HTML version (https://arxiv.org/html/2602.23193); the PDF has no
> machine-readable text. Abstract reproduced verbatim; the remainder is a structured summary with
> the paper's tables (factual data). Full paper at the source URL.

## Abstract (verbatim)

Autonomous agents based on Large Language Models (LLMs) have evolved from reactive assistants to
systems capable of planning, executing actions via tools, and iterating over environment
observations. However, they remain vulnerable to structural limitations: lack of native state,
context degradation over long horizons, and the gap between probabilistic generation and
deterministic execution requirements. This paper presents the ESAA (Event Sourcing for Autonomous
Agents) architecture, which separates the agent's cognitive intention from the project's state
mutation, inspired by the Event Sourcing pattern. In ESAA, agents emit only structured intentions in
validated JSON (agent.result or issue.report); a deterministic orchestrator validates, persists
events in an append-only log (activity.jsonl), applies file-writing effects, and projects a
verifiable materialized view (roadmap.json). The proposal incorporates boundary contracts
(AGENT_CONTRACT.yaml), metaprompting profiles (PARCER), and replay verification with hashing (esaa
verify), ensuring the immutability of completed tasks and forensic traceability. Two case studies
validate the architecture: (i) a landing page project (9 tasks, 49 events, single-agent composition)
and (ii) a clinical dashboard system (50 tasks, 86 events, 4 concurrent agents across 8 phases), both
concluding with run.status=success and verify_status=ok. The multi-agent case study demonstrates real
concurrent orchestration with heterogeneous LLMs (Claude Sonnet 4.6, Codex GPT-5, Antigravity/Gemini 3
Pro, and Claude Opus 4.6), providing empirical evidence of the architecture's scalability beyond
single-agent scenarios.

**Keywords:** autonomous agents; event sourcing; software engineering; LLM; orchestration; constrained
output; auditability; multi-agent systems.

## Core thesis

The problem is not "improving the prompt" but **restructuring the system around verifiable
invariants.** ESAA applies Event Sourcing to the agent's lifecycle: the source of truth is not the
current repo snapshot but an **immutable log of intentions, decisions, and effects**, from which
current state is deterministically projected. It adopts CQRS to separate write (changes) from read
(derived state). Paradigm shift: treat LLMs as **intention emitters under contract**, not developers
with unrestricted write permission.

## Architecture

Strict separation between (i) the LLM's heuristic cognition and (ii) the system's deterministic
execution. The agent has **no direct write permission**; it emits structured intentions validated by
JSON Schema. Orchestration cycle: agent emits `agent.result` (intention) → orchestrator validates
against **boundary contract + JSON Schema** → appends event to the store → applies file effects →
projects the read-model → agent receives only a **purified view**, never raw state. Violations emit
`output.rejected`.

Canonical artifacts (in `.roadmap/`):

- **Event store** (`activity.jsonl`) — append-only ordered log (`event_seq`) of intentions,
  dispatches, effects, run closures.
- **Materialized view** (`roadmap.json`) — read-model derived by pure projection; tasks,
  dependencies, indexes, and `projection_hash_sha256`.
- **Boundary contracts** (`AGENT_CONTRACT.yaml`, `ORCHESTRATOR_CONTRACT.yaml`) — permitted actions
  per task type (spec/impl/qa), output patterns, hard prohibitions (e.g. deny direct `file.write`).
- **PARCER profiles** — metaprompting (Persona, Audience, Rules, Context, Execution, Response) that
  force a strict JSON envelope per role.

Key mechanisms: **trace-first** (event recorded as fact before any irreversible effect);
**immutability-of-done** (completed tasks can't regress; defects spawn an `issue.report` hotfix path
without rewriting history); **determinism via canonicalization + SHA-256 hashing** of the read-model
(`esaa verify` replays the log and compares hashes); **multi-agent dispatch** where concurrent agents
are serialized at the event level (total ordering preserved; conflicts detected before effects apply).

## Case studies

| Metric | CS1: Landing Page | CS2: Clinic ASR |
| --- | --- | --- |
| Total tasks | 9 | 50 |
| Total events | 49 | 86 |
| Distinct agents | 3 (composition) | 4 (concurrent) |
| Phases | 1 pipeline | 15 (8 completed) |
| Components | 3 (spec/impl/QA) | 7 (DB, API, UI, tests, config, obs, docs) |
| Duration | Single session | ~15 hours |
| output.rejected | 0 | 0 |
| verify_status | ok | ok (partial — 31/50) |
| Concurrent claims | No | Yes (6 in 1 min) |
| Dependency graph | Linear | DAG with critical path |

CS2 (clinic-asr) used four heterogeneous LLMs by specialization: **Claude Sonnet 4.6** (specs/contracts),
**Codex GPT-5** (UI/testing/API impl), **Antigravity/Gemini 3 Pro** (persistence/repository/services),
**Claude Opus 4.6** (security/observability/deployment docs). 86 events over ~15h; append-only
semantics naturally serialized concurrent claims (six in one minute) while preserving replay ordering.
Event vocabulary simplified from 15 → 5 action types between CS1 and CS2.

ESAA is also compared against AutoGen, MetaGPT, LangGraph, CrewAI: it claims to be unique in combining
immutable event log + deterministic replay + boundary contracts + hash-verified projection +
"done"-immutability + blast-radius containment.

## Results / discussion (highlights)

- **Structural compliance:** zero `output.rejected` across both studies — the constrained JSON
  envelope kept four different LLM providers in-contract.
- **Auditability via replay:** "time-travel debugging" — reprocess the log from event zero to
  reconstruct the read-model and detect divergence via SHA-256.
- **Multi-agent coordination via the event store:** serialized accountability, forensically
  recoverable specialization, phase-gated progression without agents being aware of each other.
- **Context efficiency:** the agent gets a **purified view** (roadmap + relevant facts) instead of a
  long raw prompt — directly mitigating *lost-in-the-middle* degradation.
- **Security / blast radius:** denying direct writes + per-task-type boundaries limits the damage of
  a compromised/prompt-injected agent (least privilege).
- **Overhead:** ~200–500 tokens/invocation envelope, sub-second validation/persistence per event,
  ~15 KB log for 86 events — negligible vs. inference cost.

## Threats to validity

Only two case studies (n=2); controlled scopes; temperature 0.0; a landing page + clinical POC may
not generalize to CI pipelines, migrations, or monorepos; compliance/reproducibility metrics don't
measure design quality or business value. Conclusion: technical feasibility and verifiable invariants
demonstrated, not benchmark-maximal performance.

## Conclusion & future work

Treat LLMs as intention emitters under contract; Event Sourcing as source of truth + replay-verifiable
projections give native auditability, operational immutability, and state reproducibility; formal
contracts + constrained output close the "structure gap." Future: official `esaa init/run/verify`
CLI with remote-repo integration; concurrent-edit conflict detection/resolution; visual time-travel
diff; SWE-bench / enterprise-scale evaluation; formal verification of orchestrator invariants via
model checking.

## Notable references

Fowler — Event Sourcing (martinfowler.com/eaaDev/EventSourcing.html) and CQRS
(martinfowler.com/bliki/CQRS.html); SWE-bench (Jimenez et al., ICLR 2024); MetaGPT (Hong et al., 2023);
LangGraph; AutoGen; "lost-in-the-middle" context-degradation work; Outlines (structured generation);
JSON Schema Draft 2020-12; JSON Canonicalization Scheme.
