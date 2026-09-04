---
title: Harness Engineering
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [dymitruk-move-prompts-into-scripts-deterministic, fowler-bockeler-harness-engineering, openai-harness-engineering-codex, anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, hashimoto-my-ai-adoption-journey, stripe-minions-one-shot-coding-agents, fowler-bockeler-maintainability-sensors, dilger-harness-is-20-percent-requirements-are-80, martinfowler-prince-building-reliable-agentic-ai-systems, tornhill-cannot-trust-agent-codescene-mcp, ahe-agentic-harness-engineering]
tags: [harness-engineering, agentic-ai, reliability, coding-agents]
---

# Harness Engineering

**Hub page.** Harness engineering is the practice of building and continuously improving the
[[agent-harness]] — everything around an LLM except the model itself — so that a non-deterministic
model does reliable work. Its defining stance, shared across sources: **treat every agent failure
as a system problem to permanently fix, not a prompt to retry** ([[mitchell-hashimoto]], via
[[firecrawl-what-is-an-agent-harness]]). When the agent makes a mistake, you engineer the
environment so it (mechanically) can't make that mistake again.

## Why it emerged

The term spread in early 2026: [[mitchell-hashimoto]] named it in
[[hashimoto-my-ai-adoption-journey|his adoption essay]] (Feb 5) — "anytime you find an agent makes a
mistake, you take the time to engineer a solution such that the agent never makes that mistake again"
— [[openai]] published a flagship case study days later, and
[[birgitta-bockeler]]/[[thoughtworks]] gave it a mental model. It names something practitioners were
already doing — the scaffolding that turns a stateless model into a
[[long-running-agents|long-running agent]]. As [[langchain]]'s Harrison Chase argues, better models
*expand* what harnesses must do rather than shrinking them (Claude Code is 512k+ LOC and growing).

[[mitchell-hashimoto|Hashimoto]]'s two concrete forms set the template: (1) **better implicit
prompting** via AGENTS.md (each line derived from an observed bad behavior); (2) **actual programmed
tools** (screenshot scripts, filtered test runners) that let the agent verify itself.

## The mental model ([[birgitta-bockeler|Böckeler]])

Two control directions × two execution types (see [[feedforward-and-feedback-controls]]):

- **Guides (feedforward)** steer *before* the agent acts; **Sensors (feedback)** let it
  self-correct *after*.
- **Computational** controls are deterministic/fast/cheap (tests, linters, type checkers);
  **Inferential** controls use an LLM (AI review, "LLM as judge") — richer but slower and
  non-deterministic.

The human's job is the **steering loop**: when an issue recurs, improve the controls. Three
regulation categories — *maintainability* (easiest), *architecture fitness*, and *behaviour*
(hardest, still unsolved). Not every codebase is equally **harnessable** ("ambient affordances":
strong typing, clear module boundaries, boring frameworks).

[[fowler-bockeler-maintainability-sensors|Böckeler's follow-up field report]] supplies the first
worked example of the **maintainability** category: computational sensors (ESLint,
`dependency-cruiser`) work well at the file/function level — especially with custom messages as
self-correction guidance and threshold-raising over binary suppression — but cross-file modularity
needs an **inferential** "garbage-collection" review, and **[[mutation-testing]]** is what catches
the coverage-illusion once testing is left to AI. Left unmanaged, the agent **compounds inadvertent
technical debt**.

## How it shows up in practice

- **Repository as system of record** ([[openai-harness-engineering-codex]]): a ~100-line AGENTS.md
  *table of contents* over a structured `docs/` tree (**progressive disclosure**), custom linters
  whose error messages inject remediation instructions, and "garbage-collection" agents that fix
  drift. The goal is **[[agent-legibility]]** — "what the agent can't see doesn't exist."
- **Initializer + coding-agent structure** ([[anthropic-effective-harnesses-long-running-agents]]):
  feature lists (JSON), progress files, git, `init.sh`, and end-to-end self-verification.
- **Core primitives** ([[langchain-anatomy-of-an-agent-harness]]): filesystem, bash/sandbox,
  memory, compaction, [[ralph-loop]]s.
- **Shift-left feedback at scale** ([[stripe-minions-one-shot-coding-agents]]): heuristic <5s
  pre-push lints + selective CI over millions of tests with autofixes, capped at "often one, at most
  two" CI runs — powering [[unattended-coding-agents]] (1,000+ merged PRs/week, *Stripe's own figure*).
- **Production enterprise harness** ([[martinfowler-prince-building-reliable-agentic-ai-systems]],
  Bayer/Thoughtworks): a LangGraph control layer that bounds which agent can act, which tools it may
  use, where the workflow pauses, how failures retry, and how **state persists so a failed run resumes
  from the failed node** — plus cross-provider **LLM fallbacks**, three reflection loops, and
  Langfuse/RAGAS evals. A worked, regulated-domain instance of "engineer the context *and* the harness."
- **Deterministic external sensors over LLM self-review** ([[tornhill-cannot-trust-agent-codescene-mcp]]):
  an agent can't reliably assess its own code health, so give it a *computational* sensor (CodeScene
  [[model-context-protocol|MCP]]) as an external source of truth — the [[feedforward-and-feedback-controls|sensor]]
  argument applied to [[ai-readable-code]].
- **The harness as a self-evolving surface** ([[ahe-agentic-harness-engineering|AHE, Lin et al. 2026]]):
  the manual "inspect trajectories → revise prompts/tools/middleware" loop, **automated**. An evolution
  agent rewrites a decoupled **seven-component** harness (system prompt, tool description, tool
  implementation, middleware, skill, sub-agent config, long-term memory) with the base model frozen,
  lifting Terminal-Bench 2 pass@1 69.7% → 77.0% and beating the hand-built Codex-CLI harness. Empirically
  the gain lives in **tools, middleware, and memory — not the system prompt** (prompt-only regressed),
  refining which harness surfaces actually carry reliability. This is [[loop-engineering|loop engineering's]]
  hill-climbing loop applied *to the harness itself*.

## Relationship to neighbours

- **[[loop-engineering]]:** the layer *one floor above* the harness (June-2026 term). Harness
  engineering makes a *single* agent run reliable; loop engineering wraps that harness in automated,
  repeating, self-improving loops (it "runs on a timer, spawns helpers, and feeds itself"). The harness
  is the unit the loop multiplies — see [[loop-engineering]] for the stacked-loop model and the five
  primitives + memory.
- **[[context-engineering]]:** harness engineering *uses* context engineering. Context engineering
  optimises *what the model sees*; harness engineering controls *the environment it operates in* —
  what it can access, what gets verified, what forces a retry. Building a coding-agent user harness
  is a specific form of context engineering ([[birgitta-bockeler|Böckeler]]).
- **[[agent-engineering]]:** the broader discipline of iterating LLMs into reliable systems;
  harness engineering is its environment-and-controls arm.
- **[[agent-governance]]:** the harness acts as a cybernetic *governor*; enforcement of invariants
  and audit trails overlaps with governance.
- Distinct from **prompt engineering** (a single call) and from agent **frameworks/orchestrators**
  (see [[agent-harness]]).

## Counterpoint — "the harness is the easy 20%" ([[martin-dilger|Dilger]])

[[dilger-harness-is-20-percent-requirements-are-80|Dilger]] (2026-06-29) accepts harness engineering as
real but **subordinate**: the harness and the code are only ~20% of the solution; the other **80% is
clarifying requirements and understanding business processes** — "a human, communications problem" with
no technical fix. No quantity of agents, roles, skills, and guardrails rescues unclear requirements
("which trees to cut"). His charge is that the field over-invests in the fun 20% (taming the agent) and
under-invests in the 80% that [[event-modeling]] / [[spec-driven-development]] target. Not a refutation —
Böckeler's own view is that a harness can't *force* a non-deterministic model either — but a sharp claim
about **where the leverage is**: upstream of the harness, in the spec.

## Open questions

How to keep a growing harness coherent (guides/sensors not contradicting — [[ahe-agentic-harness-engineering|AHE]]
finds harness components **interact non-additively**, so stacking good edits can *cap* the aggregate gain);
how to evaluate harness coverage/quality (a "code coverage" for harnesses — AHE's **change manifest +
next-round attribution** is one concrete answer, though it suffers "regression blindness"); whether single
general-purpose vs. specialised agents work best; the unsolved **behaviour harness**; and how much migrates
into models over time (AHE's weaker-base transfer suggests the harness *substitutes* for capability the
model lacks — the gain shrinks as the base saturates).

## The convergence claim, running the other way (Dymitruk, 2026-08-15)

Nearly everything in this KB argues *from* [[event-modeling]] *to* agent practice.
[[dymitruk-move-prompts-into-scripts-deterministic]] argues the reverse in three sentences — do harness
engineering well enough and you reinvent the method:

> "Move as much from your prompts and agent md files into scripts. Deterministic behaviour is your goal.
> Evidence of how things work should be intermediate text files in directories that correspond to steps
> in your processes - even inboxes and outboxes. You'll naturally arrive at #EventModeling and
> #EventSourcing."

Three moves: prompts → scripts (this page's "engineer the environment, don't trust the prompt", stated as
a migration path); evidence as append-only intermediate files per step (a [[decision-trace]] arrived at
from the filesystem side, and the same instinct as
[[anthropic-effective-harnesses-long-running-agents]]'s progress files); and **"even inboxes and
outboxes"** — the tell, because once steps have inboxes and outboxes you have processors consuming and
emitting, which is Event Modeling's Automation pattern and event sourcing's transactional outbox.

It is an assertion by the method's creator about his own method's inevitability, so maximally motivated —
but it has an obvious test: do harnesses built with no Event Modeling exposure develop event-shaped
intermediate state? The un-ingested loop-engineering cluster is full of practitioners describing exactly
these file-and-directory conventions without the vocabulary, which is where to check.

## Related

[[token-budget-quality-cliff]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[openai-harness-engineering-codex]] · [[anthropic-effective-harnesses-long-running-agents]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]]._
