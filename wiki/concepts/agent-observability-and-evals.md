---
title: Agent Observability and Evaluation
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [langchain-state-of-agent-engineering-2026, anthropic-building-effective-agents, martinfowler-prince-building-reliable-agentic-ai-systems, wang-rethinking-evaluation-of-harness-evolution-for-agents, evo-bench-can-language-models-improve-agent-harness, sbco-verifier-grounded-harness-optimization, ning-code-as-agent-harness, guo-survey-question-answering-to-task-completion-harness-design, nick-tune-event-sourced-claude-code-workflows]
tags: [agentic-ai, observability, evaluation, reliability, agent-engineering]
---

# Agent Observability and Evaluation

The practices for making **nondeterministic** agents reliable enough to ship — central to
[[agent-engineering]] and, per [[langchain-state-of-agent-engineering-2026]], now table stakes.

## Observability

The ability to **trace multi-step reasoning chains and tool calls**. 89% of organizations
have some observability; 62% have detailed step/tool tracing — rising to 94% / 71.5% among
those already in production. Without visibility into how an agent reasons and acts, teams
can't debug failures, optimize, or build stakeholder trust.

**Observability derived from replay, not from a tracing SDK (Tune, 2026-03-04).**
[[nick-tune-event-sourced-claude-code-workflows]] persists **only events** from a Claude Code
workflow's state machine and rebuilds state by replay, which makes the loop's history the instrument.
Four observables fall out with no extra plumbing:

- **Per-state dwell time**, computed from transition events — *"when the workflow transitions from
  DEVELOPING to REVIEWING or COMMITTING to RESPAWNING we can deduce how long was spent in each state."*
- **Rejection count** — code review failed.
- **Hook-denial count** — the agent attempted something disallowed in that state. Both are read as
  defects in the *instructions*: *"Our goal is for these to always be 0, because they indicate a waste
  of time, waste of tokens, and indicate our agent has sub-optimal instructions."* This is the KB's
  clearest example of a **deterministic sensor pointed at the harness rather than at the code**
  ([[feedforward-and-feedback-controls]], [[harness-engineering]]).
- **A journal** as event-stream entries, with hard blocks enforcing ≥1 per iteration — post-hoc
  analysis, and context for newly spawned team members ([[decision-trace]]).

Then the eval step: *"Don't just build metrics from your events, feed them to your AI assistant… It can
identify why problems exist and suggest how to optimize the context or workflow"* — a CLAUDE.md edit or
a review-agent prompt change ([[loop-engineering]]). Named but **unbuilt**: cross-session trend analysis
and a real-time control centre over all in-progress sessions.

Two cautions. His one worked reading — *"my agents spent 15 minutes in the RESPAWN state whereas they
only spent 2 minutes actually building the feature"* — is an instrument reading from **one session of
his own personal-project harness, and he says so** (**IMPRESSION NOT MEASUREMENT · NOT INDEPENDENT**);
*"I've seen great results on real projects"* carries no number. And a **zero-denials target is a proxy an
agent can satisfy by attempting less**, which is precisely the metric-shaped-grader risk
[[loop-engineering]] warns about.

## Evaluation

Lags observability. **52.4%** run *offline* evals on test sets; **37.3%** run *online* evals
on live traffic (both rise once agents face real users). Methods skew to **human review
(59.8%)** for nuance and **LLM-as-judge (53.3%)** for scale; traditional metrics (ROUGE,
BLEU) see little use for open-ended outputs.

## Why it matters

**Quality is the #1 production blocker** (~1/3 of teams) — accuracy, consistency,
hallucinations, tone/policy adherence — with latency #2 and security #2 in large enterprises.
This is the operational answer to the nondeterminism flagged on the [[agentic-ai]] page, and
it overlaps with the monitoring/audit requirements of [[agent-governance]]. Anthropic's
"measure performance and iterate" advice ([[agentic-workflow-patterns]]) is the same instinct.

## Benchmark hygiene in the agent era (2026-07/08)

Two lessons from the harness-evolution literature that generalise well past harnesses. **All preprint
evidence — arXiv is not peer review.**

- **A search procedure must be compared against a budget-matched baseline.**
  [[wang-rethinking-evaluation-of-harness-evolution-for-agents|Wang et al. (arXiv:2607.12227v2)]] point out
  that if a method repeatedly evaluates and revises candidates using task feedback, it is *doing test-time
  scaling*, and its gains must be separated from "additional search alone" by giving a simple baseline the
  same feedback and inference budget. On Terminal-Bench 2.1 (GPT-5.4, Claude Opus 4.6) automatic harness
  evolution "does not consistently outperform simple test-time scaling methods". **Rule: whenever a result
  comes from iterating, ask what an equally expensive non-clever baseline scores.**
- **Searching and scoring on the same benchmark is contamination.** Same paper: "because the search and the
  final evaluation share the same benchmark, the reported gains risk overfitting to that specific task set" —
  hence held-out tasks. [[evo-bench-can-language-models-improve-agent-harness|Evo-Bench]] builds against this
  directly with "auxiliary-task evolution to identify tasks genuinely sensitive to framework improvements,
  followed by sensitivity-aware stratified splitting to ensure robust cross-suite generalization."
- **Verifiers can be learned rather than authored.** [[sbco-verifier-grounded-harness-optimization|SBCO]]
  learns "a decomposed bank of verifiers and a harness policy" from the agent's own graded feedback, "with a
  fixed meta-agent and no human labels" — evals as a co-optimised component. Useful and double-edged: a
  self-graded eval suite is precisely where a grader leak hides, and the capture gives no evidence about how
  that is controlled.

Both surveys list the same worry as unsolved: "harness-level evaluation and **oracle adequacy**"
([[ning-code-as-agent-harness]]), "value-aware evaluation" ([[guo-survey-question-answering-to-task-completion-harness-design]]).
The whole dispute lives on [[harness-evolution]].

## Production reference (PRINCE, 2026-06)

[[martinfowler-prince-building-reliable-agentic-ai-systems|Bayer's PRINCE]] shows this instrumented in a
regulated enterprise system: **Langfuse** traces every production run, with **RAGAS** metrics
(Faithfulness, Answer/Context Relevancy, Accuracy, Semantic Similarity) run as both **dataset evals** (on
significant change) and **daily live-traffic evals** (no reference answers) — "a testing pyramid" applying
metrics at different workflow stages, not just end-to-end. Pairs trace-based observability with
citation-based [[agent-explainability]]. This is also the *input* to [[loop-engineering]]'s hill-climbing
loop, where trace analysis feeds back into harness improvement.

_Source pages: [[langchain-state-of-agent-engineering-2026]] · [[anthropic-building-effective-agents]] · [[martinfowler-prince-building-reliable-agentic-ai-systems]] · [[wang-rethinking-evaluation-of-harness-evolution-for-agents]] · [[evo-bench-can-language-models-improve-agent-harness]] · [[sbco-verifier-grounded-harness-optimization]] · [[ning-code-as-agent-harness]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[nick-tune-event-sourced-claude-code-workflows]]._
