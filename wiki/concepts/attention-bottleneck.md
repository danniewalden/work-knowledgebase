---
title: Attention as the Bottleneck
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [laycock-the-conductor-developer, willison-conceptual-integrity-and-counting-lines-of-code, tornhill-compressed-cognition-cost-of-faster-coding, laycock-maybe-we-shouldnt-be-reviewing-all-this-code, tune-no-rapport-with-a-model-you-didnt-code]
tags: [attention-bottleneck, verification-burden, comprehension-debt, agentic-coding, live-dispute, focus]
---

# Attention as the Bottleneck

**Agents moved the constraint off code production and onto the human's attention.** Three independent
authors state that premise within six weeks of each other in 2026 — and then disagree about what to do
with it. This page holds the premise, the mechanism, and the three-way split on the remedy.

## The premise, three times

- **[[rachel-laycock]]** ([[laycock-the-conductor-developer]], 2026-07-31): *"AI didn't change what
  great software looks like. It changed what's scarce. **Human attention is now the bottleneck**."* She
  records a failed prediction of her own — she had expected the bottleneck to march down the lifecycle
  (coding → design → architecture → verification) — *"I was wrong."*
- **[[simon-willison]]** ([[willison-conceptual-integrity-and-counting-lines-of-code]], 2026-08-19):
  *"the new limiting factor is **cognitive capacity**. I can churn out code a hundred times faster. I
  don't have the cognitive capacity to stay on top of 100 times the amount of code."*
- **[[adam-tornhill]]** ([[tornhill-compressed-cognition-cost-of-faster-coding]], 2026-05-07): *"It is
  the **parallelisation of human attention** that does not scale."*

## The mechanism (Tornhill, 2026-05)

Why attention, and not time, is the binding constraint:

- **The timeline collapses.** Pre-2025 work "unfolded at human speed, which meant the decisions were
  naturally spaced out. Today, agents compress the timeline" — "complexity and decisions that used to be
  spread over days in a single coding session." His phrase: **"a lot more architecture per minute."**
- **Decision fatigue.** Decision quality decays across a session and recovers after breaks — and
  *"manual coding had a built-in pacing mechanism. That was our implicit recovery break. And it's now
  gone."*
- **Working memory is smaller than folklore says.** "Seven plus or minus two… was over-optimistic…
  we can, at best, hold **3-4 things** in our head at once and still be able to reason effectively."
- **Self-interruption, which he says is worse than external interruption.** The agent "asks a question,
  produces a diff, gets blocked by a missing tool, fails a test, or suggests a change that looks
  *almost* right but touches too much. **Each event pulls you into a new review-verify-steer
  decision.**"

*Sourcing discipline:* the psychology is cited **by author name only, unlinked** (Danziger et al. on
judicial rulings, Sweller on cognitive load, the "3-4 things" revision) and is analogy, not measurement
of programmers. His own pace claims ("I can usually sustain the pace for a couple of hours… based on
conversations with other engineers") are **IMPRESSION NOT MEASUREMENT**. And **NOT INDEPENDENT** on the
prescription — "automation and safeguards are the mechanisms for delivering trust, not manual
inspection" is argued by CodeScene's founder/CTO, who sells them.

## The one relayed measurement, and how to cite it

The same essay relays a controlled trial of experienced open-source developers: the AI-assisted group
**estimated a 20% speedup** and were **19% slower**. *"Even expert developers overestimate the AI impact
on developer productivity."* **Keep the two figures apart — one is felt, one is measured, and the gap is
the finding.** Tornhill **names no study, authors, date or link** ("one of my favourite studies"), so
this KB cites it as *an unnamed controlled trial as relayed by Tornhill* and **never attributes it to a
named study, lab or set of authors, however tempting the guess.** It is the strongest available caution
against the self-reported-speedup claims that fill [[agentic-coding]] and [[loop-engineering]].

## Three remedies for one constraint — unresolved

| | Remedy | Source | Status |
|---|---|---|---|
| **Widen the span** | Become a conductor: orchestrate 8–12 agents; re-skill for attention, energy and decision management | Laycock | Anecdote + analogy |
| **Distribute it** | Keep a team so cognitive capacity can be load-balanced across people | Willison | Assertion |
| **Narrow it** | "One long-running agentic maintenance task… and one focus task. Never more" | Tornhill | Personal rule |

**The collision worth keeping visible.** Laycock reports an engineer "who regularly have eight AI agents
running in parallel. I've heard similar numbers from others. Ten. Twelve. Beyond that, they become the
bottleneck," and treats conducting at that width as the emerging shape of the job. Tornhill: *"I cannot
even think about twenty meaningful things to build, and even less so about the resulting cognitive
tax… It's exactly the wrong thing to even consider."* He pre-empts the obvious objection — "yes, I
understand sub-agents and machine parallelisation. That is not what I'm objecting to." **Both are
anecdote-grade: her 8/10/12 is hearsay from one unnamed engineer plus "others"; his ceiling of two is a
personal rule.** The KB has no measurement that settles it, and should not pick.

## The conductor model (Laycock, 2026-07)

The image, via Jacob Collier: a conductor "is first and foremost a great musician. They could play the
instruments themselves. That's not why they're standing on the podium… **It needs the conductor because
someone has to hold the whole system in their head.**" Agents are the musicians; the developer decides
which agent takes which problem, supplies context, evaluates what comes back, spots subtle mistakes, and
decides what deserves another iteration.

Its real payload is a **career** claim, not a metaphor: eight parallel streams "sounded like my job" as
CTO, and what she had to learn was **energy management, not time management** — "the challenge wasn't the
hours. It was the constant context switching. The endless stream of decisions." Hence the transferable
curriculum (*protect your attention; manage your energy; reduce unnecessary decisions; create systems
that help your brain, not just your calendar*) and the line the page exists for: **"We're redesigning
the tools, but we haven't started redesigning the job."** Her closing question — *"How do we redesign
engineering careers when human attention becomes the scarce resource?"* — is open in this KB.
**NOT INDEPENDENT** (Thoughtworks' CTO on Thoughtworks' own channel) and evidence-free by her own
framing. Note "a conductor must still be a musician" is the analogy's load-bearing constraint against
the "nobody needs to read code any more" reading.

## Consequences elsewhere in the KB

- **[[verification-burden]]** — this is the budget. Every proposed substitute for reading code (pair,
  mob, review tests, spot-check, run twelve agents) is a claim on the same scarce input, which is why
  Laycock's own two 2026 essays are unreconciled: attention is the bottleneck (July), and the remedy is
  attention-expensive pairing and team design sessions (September). She never addresses the tension.
- **[[comprehension-debt]]** — attention is the currency the debt is denominated in; the cognitive
  ceiling is *why* the "read the diffs" defence has a limit.
- **[[multi-agent-orchestration]]** — the human-side ceiling on fan-out, next to CEAD's
  machine-side ceiling (~32 agents).
- **[[context-rot]] / [[token-budget-quality-cliff]]** — the machine analogues; "3-4 things" is the
  human context window.
- **[[tune-no-rapport-with-a-model-you-didnt-code|Tune]]** — the same scarce attention, spent upstream:
  the modelling insight that typing used to buy.
- **[[loop-engineering]]** — the "stay the engineer" caveats now have a stated resource limit rather
  than only a discipline argument.
- **[[feedforward-and-feedback-controls]]** — Osmani's four capacity levers are this budget stated as an
  engineering choice rather than a constraint to be suffered.

## Related

[[verification-burden]] · [[comprehension-debt]] · [[multi-agent-orchestration]] ·
[[loop-engineering]] · [[agentic-coding]] · [[context-rot]] · [[token-budget-quality-cliff]] ·
[[team-topologies]] · [[software-factory]] · [[rachel-laycock]] · [[adam-tornhill]] ·
[[simon-willison]]
