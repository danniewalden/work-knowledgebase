---
title: "Source: Rachel Laycock — The Conductor Developer"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [laycock-the-conductor-developer]
raw_file: [raw/articles/laycock-the-conductor-developer.md]
tags: [attention-bottleneck, agentic-coding, multi-agent-orchestration, thoughtworks, careers, focus]
---

# Source: Rachel Laycock — The Conductor Developer

Essay by **[[rachel-laycock]]**, CTO of [[thoughtworks]], on martinfowler.com ("Rachel's Ramblings"),
**2026-07-31**. Raw capture: `raw/articles/laycock-the-conductor-developer.md` — a deliberate
**backfill** (published just outside a 14-day watch window, captured because it is the on-thread
predecessor of [[laycock-citizens-build-agents-execute-experts-govern]]). Subtitle: *"Why I think
software development is starting to feel a little more like conducting an orchestra."*

## Summary

She starts by discarding the productivity frame ("How much faster can it write code?… I think that's
the wrong question") and then discards her own prediction. She had expected the bottleneck to march
down the lifecycle — coding → design and specification → architecture → verification — and reports:
**"I was wrong."**

> **"AI didn't change what great software looks like. It changed what's scarce. Human attention is now
> the bottleneck."**

The evidence she offers is observational: "when I watch developers using AI today… The best developers
I know aren't spending all day in flow anymore. **They're orchestrating agents.**" Deep work and flow
were the thing developers protected; that is no longer where the work happens.

**The conductor analogy**, via Jacob Collier: a conductor "is first and foremost a great musician.
They could play the instruments themselves. That's not why they're standing on the podium. Their value
comes from understanding the whole score. The orchestra doesn't need the conductor because the
musicians aren't talented enough. **It needs the conductor because someone has to hold the whole
system in their head.**" So: agents are the musicians, the developer is the conductor — "deciding which
agent should tackle which problem… providing context… evaluating what comes back… spotting subtle
mistakes… deciding what deserves another iteration and what is ready to move on."

**The number, and its status.** "I was talking to an engineer recently who told me they regularly have
**eight** AI agents running in parallel. I've heard similar numbers from others. **Ten. Twelve.**
Beyond that, they become the bottleneck." Anecdote relayed in conversation — see Limits.

**The executive parallel** is the essay's real contribution: eight parallel streams "sounded like my
job." As CTO she rarely produces work herself; work arrives as "conversations, emails, documents, chat
messages and half-formed ideas," and her job is deciding where attention belongs. What she had to learn
was **not time management but energy management** — "the challenge wasn't the hours. It was the
constant context switching. The endless stream of decisions. The feeling that nothing was ever
completely finished." Her coach's rules, offered as the developer curriculum to come: *protect your
attention; manage your energy; reduce unnecessary decisions; create systems that help your brain, not
just your calendar.*

Her conclusion is about **the job, not the tooling**: "we've spent decades helping executives succeed
in this kind of environment… Yet we're still preparing developers for a world of individual execution.
**We're redesigning the tools, but we haven't started redesigning the job.**" Not managers, not
replacement — "engineering expertise is simply being applied in a different place, and much more
often, because execution has become so much faster." Closing question: **"How do we redesign
engineering careers when human attention becomes the scarce resource?"**

## Key points

- **The bottleneck did not move down the lifecycle; it moved to the human.** She states her earlier
  prediction and its failure explicitly, which makes this a rarer thing than a framing: a documented
  changed mind.
- **A conductor must still be a musician.** The analogy is load-bearing against the "you don't need to
  understand code any more" reading — the podium is earned by being able to play.
- **"Someone has to hold the whole system in their head"** is the same requirement
  [[willison-conceptual-integrity-and-counting-lines-of-code|Willison]] says has a hard ceiling
  ("cognitive capacity"), and the same one [[tune-no-rapport-with-a-model-you-didnt-code|Tune]] says
  agents erode. Three authors, three verdicts on one requirement, all within six weeks.
- **The transferable-skills claim is the practical payload**: energy management, decision reduction,
  attention protection — a curriculum that exists for executives and doesn't for engineers. Filed
  with a named organisational consequence (their Chief People and Leadership Officer's reaction).
- **She names one deferred topic** — FOSE discussion of "how we ensure good design, quality and
  resilience while agents increasingly write the code" — which she takes up five weeks later in
  [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]].

## Limits

- **NOT INDEPENDENT.** Thoughtworks' CTO on Thoughtworks' own channel (martinfowler.com); the flow /
  pairing / deep-work premises are Thoughtworks-adjacent orthodoxy. Not external corroboration for any
  Thoughtworks-originated framing.
- **The 8 / 10 / 12 parallel-agents figures are hearsay, twice over**: one unnamed engineer told her
  eight, and "I've heard similar numbers from others." No workload, task type, quality outcome or
  duration attached. **IMPRESSION NOT MEASUREMENT** — do not cite these as a capacity finding. And
  "beyond that, they become the bottleneck" is her inference from those anecdotes, not a measured
  ceiling.
- **"The best developers I know aren't spending all day in flow anymore"** is unquantified observation
  by a CTO watching an unspecified population, with obvious selection bias toward
  early-adopter contexts.
- **No data of any kind**: no study on attention, cognitive load or context switching is cited, despite
  a large existing literature (the one relayed second-hand in
  [[tornhill-compressed-cognition-cost-of-faster-coding]], for instance).
- The conductor analogy is an analogy; it neither predicts nor constrains anything testable.

## Connections / contrast

- **[[attention-bottleneck]]** — the concept's clearest statement in the KB ("AI didn't change what
  great software looks like. It changed what's scarce"), and the source of its
  organisational/career-design arm.
- **Direct collision with [[tornhill-compressed-cognition-cost-of-faster-coding|Tornhill]]**, and it is
  one of the batch's real disagreements. She treats eight-to-twelve parallel agents as the emerging
  shape of good practice; he runs **"one long-running maintenance task and one focus task. Never
  more,"** and calls the twenty-agent ambition "exactly the wrong thing to even consider" because "it
  is the parallelisation of human attention that does not scale." **Both are anecdote-grade.** They
  agree completely on the premise — attention is now the scarce input — and disagree on whether the
  response is to widen the span of control or to protect the span you have. Hold both; the KB has no
  measurement that settles it.
- **With [[willison-conceptual-integrity-and-counting-lines-of-code|Willison]]**: same premise,
  different remedy — he **load-balances cognitive capacity across a team**, she **re-skills the
  individual conductor**. Both are untested. Together with Tornhill's "narrow it," the KB now holds
  three distinct responses to one agreed constraint, which is the useful state for
  [[attention-bottleneck]] to be in.
- **[[multi-agent-orchestration]] / [[addyosmani-code-agent-orchestra]]** — Osmani's orchestra
  metaphor arrives at the same image from the tooling side; this is the *career and energy* version.
  Also [[addyosmani-own-the-outer-loop]] (the human owns the outer loop) and
  [[addyosmani-human-judgment-relocates]] (judgement relocates rather than leaves).
- **[[verification-burden]]** — the supply side of that ledger: if attention is the scarce input, every
  proposed remedy (pair more, read tests, spot-check, run twelve agents) is a claim on the same
  budget. Her own later prescription (pairing, mobbing, team design sessions) is attention-expensive,
  and she never reconciles the two essays. That unreconciled pair is worth keeping visible.
- **[[laycock-citizens-build-agents-execute-experts-govern]]** — the organisational view; this is the
  individual-role view. Together they are her two-rung argument: what the expert does, and what it
  costs them.
- Also: [[agent-vs-workflow]], [[loop-engineering]]'s "stay the engineer" caveats,
  [[comprehension-debt]], [[team-topologies]] (if the job changes, so does team design).

## Links

Entities: [[rachel-laycock]] · [[thoughtworks]] · [[martin-fowler]] · [[addy-osmani]] ·
[[adam-tornhill]] · [[simon-willison]]. Concepts: [[attention-bottleneck]] ·
[[multi-agent-orchestration]] · [[verification-burden]] · [[agentic-coding]] · [[loop-engineering]] ·
[[comprehension-debt]] · [[team-topologies]]. Related sources:
[[laycock-citizens-build-agents-execute-experts-govern]] ·
[[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] ·
[[tornhill-compressed-cognition-cost-of-faster-coding]] ·
[[willison-conceptual-integrity-and-counting-lines-of-code]] · [[addyosmani-code-agent-orchestra]].

_Raw source: `raw/articles/laycock-the-conductor-developer.md`._
