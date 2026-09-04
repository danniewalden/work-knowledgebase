---
title: "Dilger — Describing a problem without solving it leaves a hole that keeps growing"
type: source
created: 2026-08-14
updated: 2026-08-14
sources: [dilger-describing-without-solving-burns-you-out]
raw_file: [raw/notes/dilger-describing-without-solving-burns-you-out.md]
tags: [spec-driven-development, agentic-coding, comprehension-debt, loop-engineering, focus]
---

# Dilger — "Describing your way through a day can feel just as hollow as mindlessly typing through one"

Source: [[martin-dilger]], LinkedIn post, 2026-08-14. Raw:
`raw/notes/dilger-describing-without-solving-burns-you-out.md`. Hashtags #eventmodeling
#specdrivendevelopment.

## Summary

The most self-critical post in the captured Dilger series, and the first from him that names a **failure
mode of [[spec-driven-development]] itself**. He opens with the agent-era exhaustion report: burned out
after days of "just" instructing agents, "somehow more productive on paper, but at what cost" — he ran
5 parallel agent sessions "overseeing my agents like a kindergartner" and "my brain was mud every
evening." The observation underneath it:

> "A few years ago, we were obsessed with protecting people from context switching. Now we call the same
> thing productivity."

To the "I love writing code, I don't want agents to do that anymore" objection he answers that most
people don't love writing code, they love **solving problems** — the two only feel fused because for a
whole career solving always arrived together with typing. "You cannot outtype an agent. That's like
trying to outrun a car."

Then the load-bearing claim:

> "This is also where spec-driven development goes wrong for a lot of teams. They stop solving problems
> and just describe them, and then hand it to AI and hope it figures out the solution. That's not being
> in charge, that's checking out before it gets interesting. And that's what slowly burns you out.
> Describing a problem without solving it leaves a hole that keeps growing."

Done right, SDD "still means you're in charge of solving the problem. You hand over the boring part."
His closing test: ask when you last felt the kick of actually solving something — "if you can't
remember, that's not AI's fault."

## Key points

- **Describing ≠ designing.** The failure is not writing specs; it is treating the spec as a *hand-off
  of the thinking* rather than the record of thinking already done. This is the requirements-side
  restatement of [[comprehension-debt]] — you can accrue it by over-delegating the *problem*, not just
  by not reading the generated code.
- **A caveat from inside the movement.** Every prior captured Dilger source argues *for* spec-first
  ([[dilger-harness-is-20-percent-requirements-are-80]],
  [[dilger-is-code-still-the-source-of-truth]], [[dilger-spec-driven-development-applied]]). This one
  supplies the missing counter-weight the KB previously had only from outside voices —
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]]'s *SDD and the Illusion of Known Scope*, and
  the "stay the engineer" caveats in [[loop-engineering]].
- **Parallel-agent supervision has a human cost.** "Overseeing agents like a kindergartner" across 5
  sessions is a concrete cost datapoint against the [[unattended-coding-agents|run-more-agents]] framing
  — including his own 6–10-agent [[dilger-local-llm-distributed-agent-setup-event-modeling|ralph-loop
  rig]]. The context-switching inversion ("we protected people from it; now we call it productivity")
  is the sharpest line in the post.
- **The verification burden restated as motivation loss.** Where [[birgitta-bockeler]] asks *where do we
  insert ourselves as arbiters* ([[bockeler-tdd-inside-the-agent-loop]]), Dilger asks the same question
  from the practitioner's side and answers it with **problem-solving ownership**: keep the design
  decision, delegate the typing.

## Connections

[[spec-driven-development]] (a named failure mode) · [[comprehension-debt]] ·
[[dilger-real-cost-of-ai-is-second-order]] (his own second-order-cost argument, of which this is the
human half) · [[loop-engineering]] ("stay the engineer") · [[agentic-coding]] ·
[[unattended-coding-agents]] · [[vibe-modeling]] (the boundary where model-then-generate becomes
describe-and-hope) · [[bockeler-tdd-inside-the-agent-loop]] (same week, same question from the
verification side).

## Caveat

A LinkedIn reflection, not research: no data on burnout, and it doubles as positioning for his *Spec
Driven* book and [[eventmodelers-ai]] — the fix he implies is his own method. Still, a vendor
publishing the failure mode of the thing he sells is a more credible caveat than most.
