---
title: "Source: Tune — Event-sourced Claude Code workflows"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [nick-tune-event-sourced-claude-code-workflows]
raw_file: [raw/articles/nick-tune-event-sourced-claude-code-workflows.md]
tags: [event-sourcing, agentic-coding, loop-engineering, agent-observability, harness, focus]
---

# Source: Tune — Event-sourced Claude Code workflows

Blog post by **[[nick-tune]]**, **2026-03-04**, third in a series (workflows-as-state-machines →
declarative DSLs → **fully event-sourced**). Code in his `autonomous-claude-agent-team` repo. He
credits **Yves Reynhout** for the suggestion to store only events. Raw capture:
`raw/articles/nick-tune-event-sourced-claude-code-workflows.md`.

> **NOT INDEPENDENT** — this is the originator's account of his own harness and his own workflow
> architecture, not third-party corroboration. **IMPRESSION NOT MEASUREMENT** for every timing below:
> they are instrument readings from *one session* of a *personal project*. His own scoping: *"So far
> this is just something I've tried out on personal projects."*

**This is the Event-Modeling-adjacent × coding-agents seam the KB's watch exists to find**, and it is a
different seam from every other source on the thread: [[event-sourcing]] applied to the **agent loop**
rather than to the domain the agent is building.

## Summary

A Claude Code workflow is already modelled as a state machine (DEVELOPING → REVIEWING → COMMITTING →
RESPAWNING). Persist **only the events**, not the current state, and derive state by replay. The
implementation is deliberately dull — *"a pretty boring event-sourcing implementation using SQLite for
storage"* — and the payoff is entirely downstream: *"in-depth observability of how my agents performed
and where they spent their time implementing a feature, and the potential for cross-session trends
analysis."*

## Key points

- **The event stream is the instrument.** A report UI is generated at session end from the persisted
  events (`/autonomous-claude-agent-team:view-report <sessionId>`), answering two questions: *"What
  actually happened?"* and *"How can I optimize my workflow / harness / context so that my agents
  perform better next time?"*
- **The reading that makes the case, and its caveat.** *"My agents spent 15 minutes in the RESPAWN
  state whereas they only spent 2 minutes actually building the feature."* Diagnosis: spawn all team
  members up front for every iteration. **IMPRESSION NOT MEASUREMENT** — one session, his own harness.
- **Two counters he says should always be zero: rejections** (code review failed) and **hook denials**
  (Claude attempted something disallowed in that state). *"Our goal is for these to always be 0,
  because they indicate a waste of time, waste of tokens, and indicate our agent has sub-optimal
  instructions."* This is the cleanest **deterministic sensor on the loop itself** the KB holds — a
  count of the harness refusing the agent, read as a defect in the *instructions*, not the agent.
- **Feed the events back to the agent, not just to a dashboard.** *"Don't just build metrics from your
  events, feed them to your AI assistant … Claude is able to take the events and also able to combine
  the event analysis with code, prompts, and any other context that explain the trends. It can identify
  why problems exist and suggest how to optimize the context or workflow"* — e.g. a CLAUDE.md change or
  a tweak to the review agent's system prompt. *"I've seen great results on real projects"* is a
  self-report with **no numbers attached**.
- **The event stream doubles as the journal.** Agents log decisions and milestones as events, with
  **hard blocks enforcing at least one journal entry per iteration** — useful post-hoc and for bringing
  newly spawned team members up to speed. Plus free-text and type-faceted event search.
- **Standard event-sourcing engineering applies unchanged**: replay cost is acknowledged as a potential
  problem, with snapshots, multiple streams, audit-only events (journal entries not needed for state),
  projections, or an MCP server holding projections in memory listed as the mitigations. *"At the end of
  the day, they are events like those produced by any other software application, so all the same
  principles and patterns apply."*
- **Unbuilt but named:** cross-session analysis over thousands of events (*"why do certain types of
  feature take longer? what is common across sessions where code review fails repeatedly?"*) and a
  real-time control centre over all in-progress sessions with anomaly alerts.
- **He scopes the value honestly, and the scoping is the interesting part.** *"I don't think
  event-sourced aggregates are going to offer much value to the developer that uses Claude Code as a
  chatbot, or the developer that hand-holds Claude through every session … more suited to developers
  implementing an autonomous coding loop."* And the self-undermining possibility: *"An open question is
  whether we can reach a point where our workflows just work … If we get to that point, the
  observability and analysis doesn't provide any value."*

## Limits

- **NOT INDEPENDENT · IMPRESSION NOT MEASUREMENT** (above). Personal projects only; the one quantified
  claim about real projects ("great results") carries no measurement.
- **No baseline.** Nothing compares event-sourced persistence against state-based persistence on any
  outcome; the argument is that the events *enable* analysis, which is a capability claim, not an
  efficacy claim.
- Cross-session analysis, the control centre, and the trend work are explicitly **not built** —
  *"Something I have not even started to flirt with yet."*
- Three images (session-overview UI, event search, architecture diagram) are noted inline in the raw
  and not reproduced, so the metrics UI is described rather than shown.

## Connections / contrast

- **It inverts the KB's whole event-sourcing-for-agents thread.** [[event-sourced-agentic-patterns]],
  [[akka-event-sourcing-backbone-agentic-ai]], [[esaa-event-sourcing-for-autonomous-agents]] and
  [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]] all argue events are the right
  substrate for the *system the agents run*. Tune event-sources the **harness**, so the log's consumers
  are harness-optimisation questions, not domain queries. Closest neighbour is
  [[dymitruk-move-prompts-into-scripts-deterministic]]'s "evidence as intermediate files in
  step-shaped directories" — the same instinct reached from the filesystem side.
- **It gives [[agent-observability-and-evals]] its most concrete mechanism**: per-state dwell time,
  rejection counts and hook-denial counts derived from replay, with the *stated target of zero* for the
  last two. And it closes a loop [[loop-engineering]] describes but had no shipping instance of — the
  **hill-climbing / improvement** rung, where loop telemetry is fed back to rewrite the harness.
  Compare [[dilger-modeling-agent-improved-by-learning-loop]], where the agent rewrites its own skill
  files: Dilger's grader is a structural diff against a corpus, Tune's is the event log of its own
  execution.
- **Dymitruk's "audit trail, not a snapshot" now has an instrumented instance.** In
  [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] Dymitruk argues events give an agent a
  traceable history rather than a state to debug blind; Tune's report UI is what that looks like when
  someone builds it — though note the divergence in *purpose*: Dymitruk's use is *"follow the event
  trail, find the divergence, fix it, replay"* (correctness), Tune's is time and waste accounting
  (efficiency).
- **The productive tension with his own separate position, which must travel with this page.** In
  [[tune-no-rapport-with-a-model-you-didnt-code]] (2026-08-28)
  the same author doubts he can build rapport with a domain model he did not hand-code — *"the domain
  model is going to be worse because I'm clearly missing some nuances … Maybe it's not even possible."*
  So: meticulous instrumentation and automated optimisation of the **loop**, deep scepticism about
  delegating the **domain model**. That is not a contradiction — it is a boundary, and it happens to be
  the same boundary [[dilger-describing-without-solving-burns-you-out]] and
  [[bockeler-tdd-inside-the-agent-loop]] arrive at: own the problem, delegate the process. It does,
  however, cut against the Dilger thesis that a good enough spec DSL lets agents do the modelling.
- **Third position on notation, same author:** his
  [[nick-tune-enforced-application-architecture-agents-humans|model-as-constraint]] stance in
  [[model-as-code-vs-model-as-language]] is the *structural* enforcement counterpart to this post's
  *behavioural* telemetry. Together they describe a harness that constrains at build time and measures
  at run time, with no authored model of the domain in either.

_Related: [[nick-tune]] · [[event-sourcing]] · [[agent-observability-and-evals]] ·
[[loop-engineering]] · [[harness-engineering]] · [[event-sourced-agentic-patterns]] ·
[[unattended-coding-agents]] · [[decision-trace]] · [[cqrs]]._
