---
title: "Source: Dilger — Loop Engineering, or Why You Should Never Argue With an Agent"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-loop-engineering-never-argue-with-agent]
raw_file: [raw/articles/dilger-loop-engineering-never-argue-with-agent.md]
tags: [loop-engineering, event-modeling, agent-harness, agentic-coding, context-engineering, focus]
---

# Source: Dilger — Loop Engineering, or Why You Should Never Argue With an Agent

Article by **[[martin-dilger]]** on the eventmodelers.ai blog, **2026-06-10**, ~10 min read. Raw
capture: `raw/articles/dilger-loop-engineering-never-argue-with-agent.md`.

> **VENDOR SELF-REPORT.** eventmodelers.ai / EM-Studio is Dilger's own commercial platform
> ([[eventmodelers-ai]], [[nebulit]]); the piece ends by selling his book *Spec Driven*, the platform's
> build-kits, and a paid training engagement (*"I can teach your team how to do this, as I did for
> hundreds of engineers already"* — **his own figure, an impression, not a count the KB can verify**).

**Chronology note this ingest establishes:** the KB dates the **Event Modeling Agent Harness** to
[[dilger-event-modeling-agent-harness]], 2026-06-17. This article is **one week earlier (06-10)** and
already contains the full board mechanic with claim-locking and timeout recovery (the statuses named in
the text are Planned, In Progress, Blocked and Done, plus assignment; the harness diagram's caption is
described in the raw as "Draft to Ready to Working to Done"). It is the **earlier and fuller primary** for that harness, and the KB's dating of the
idea should move to 06-10.

## Summary

Dilger's answer to loop engineering's arrival as a named discipline: he was already doing it. The
article does three things — defines the loop minimally, argues that **long conversations are the
failure mode and context-clearing is the fix**, and then claims [[event-modeling]] *is* loop
engineering applied, because the method already produces the task list a loop needs.

## Key points

- **The loop, minimally:** define a task list, run tasks one at a time, **record what you learned after
  each**, then **clear the context completely**. *"The next iteration starts from scratch. No bias. No
  bad decisions lingering. No wrong information. Just the learnings - and the next task."*
- **Provenance he states himself:** he read Geoffrey Huntley's papers in **2025** and dismissed the
  [[ralph-loop|RALPH loop]] at first (*"running an agent in a loop? Nonsense"*), then realised he was
  already doing it without a name. He also positions loop engineering as *"the 'new thing' after
  Spec-Driven Development"* — his own framing of the sequence.
- **Context is the enemy, and hallucination is its predictable output.** *"The context fills up with
  every bad decision, every reversal, every disagreement, every dead end … The longer this goes on, the
  more confused the model becomes. And confusion is what produces hallucination. It's not a random
  event. It's the predictable result of a polluted context window."* A mechanism claim, asserted, with
  no evidence offered — cf. [[context-rot]], which the KB holds better-evidenced versions of.
- **"I never argue with an agent."** *"Every agent will immediately tell you how right you are. That's
  not learning. That's hand-waving agreement."* And: *"The agent isn't learning from your corrections.
  It's just agreeing with you - and carrying the confusion forward."* Operational rule: each iteration
  has defined goals and rules; **a broken rule ends the iteration with no discussion** — throw
  everything away except the learnings and retry.
- **Do not engineer the loop.** Someone proposed that an agent should stop, revert and restart if its
  task changes mid-flight; his answer is that **the loop already handles it**. *"The moment you start
  overengineering it - adding more state, more memory, more decision-making between iterations - you
  start reintroducing exactly the problems the loop was designed to eliminate. You're building back the
  noise. Simplicity isn't a limitation of loop engineering. It is loop engineering."*
- **Event Modeling supplies the hard part.** *"The hard part in Loop Engineering is not implementing
  the loop, it's defining the list of tasks. In Event Modeling this happens naturally and is part of the
  process. Every 'slice' of functionality becomes a task."* Mechanics: slices carry status; **Planned**
  means an agent may pick it up; agents subscribe to `slice:changed` on a board (Claude Code, Codex and
  Hermes named); one agent claims a slice and moves it to In Progress, which **locks it against other
  agents** — *"much like assigning a ticket to an engineer."*
- **Three terminal outcomes per slice:** Done; **Blocked** (something is missing); or **the agent dies,
  the slice times out in progress, and another agent picks it up.** The timeout is the recovery
  mechanism, and it is what makes an unattended fleet safe to leave running
  ([[unattended-coding-agents]], [[long-running-agents]]).
- **No prompting at all is the design goal.** *"Just change a slice and wait until the agent did the
  work."* Editing a done slice: move Done → In Progress, edit, move to Planned; an agent then **diffs
  the specified slice against the code and reconciles the code to the spec** — adding scenarios, adding
  fields. Implementation hints go in **comments on the slice or element**, which the agent checks off.
- **The failure attribution is the load-bearing claim of the whole piece.** *"If something fails, the
  problem is in the spec, not the prompt."* Throw away the attempt, record the learning, adjust the
  model, return the slice to Planned.

## Limits

- **VENDOR SELF-REPORT** throughout (above). Every mechanism described is a feature of his own platform,
  and the article is a product explainer as much as a method argument.
- **No evidence of any kind.** No timings, no comparison of clean-iteration vs long-conversation
  outcomes, no failure rates — yet the central claim is stated as absolute: *"Clean iterations with
  recorded learnings will outperform long, polluted conversations every single time. Not sometimes.
  Every time."* That is an unfalsifiable formulation of an otherwise testable claim, and the KB should
  carry it as a position, not a finding.
- **"Hundreds of engineers"** trained is his own figure. The related *"battle-tested over hundreds of
  projects"* claim appears in [[dilger-communicating-intent-to-an-agent-needs-a-dsl]] and is likewise
  his own — **not independently corroborated anywhere in the KB**.
- Eight inline screenshots (slice statuses, subscribing agents, the harness diagram, a slice comment)
  are noted in the raw, not reproduced, so the board mechanics are described rather than shown.

## Connections / contrast

- **The fullest primary for [[dilger-event-modeling-agent-harness]]** and one week its senior; also the
  fullest statement of the claim-lock mechanism the KB currently sources to
  [[dilger-local-llm-distributed-agent-setup-event-modeling]] (2026-07-02).
- **It gives [[loop-engineering]] its Event-Modeling entry, which the page currently lacks.** The
  page's open question — *what supplies the task list?* — is answered here by construction: the
  [[slice]] is the loop's unit of work. That is the same "unit of work" claim
  [[vertical-slice-architecture]] and [[dilger-triplet-flexible-agent-enabled-architecture]] make from
  the structural side.
- **"The problem is in the spec, not the prompt" is [[spec-driven-development]]'s central thesis stated
  as a debugging rule** — and it is exactly what
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] and
  [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] deny: Eberhardt hit a trivial null-data bug
  that Copilot itself judged *not* a spec problem, and Tornhill's requirements-explosion argument says
  most such failures cannot be spec failures because the spec cannot contain the implicit design
  decisions. **This article and those two are the cleanest head-on disagreement in the batch**, and the
  disagreement is about *where defects live*, not about markdown.
- **Against [[bockeler-context-engineering-coding-agents]] and
  [[dymitruk-move-prompts-into-scripts-deterministic]]:** all three treat conversation as the thing to
  eliminate. Dymitruk's route is prompts → scripts (determinism); Böckeler's is deliberate context
  curation; Dilger's is discard-and-restart. Compatible, and worth stating as three routes rather than
  one consensus.
- **Tension inside his own position:** *"never argue with an agent"* forbids mid-loop correction, while
  [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] describes agents **posting comments back
  on the model** and Dilger answering them — argument relocated from the code loop to the modelling
  loop, which is consistent only because the model, not the conversation, is where the state lives.

_Related: [[martin-dilger]] · [[loop-engineering]] · [[ralph-loop]] · [[agent-harness]] ·
[[event-modeling]] · [[slice]] · [[spec-driven-development]] · [[context-rot]] ·
[[unattended-coding-agents]] · [[eventmodelers-ai]]._
