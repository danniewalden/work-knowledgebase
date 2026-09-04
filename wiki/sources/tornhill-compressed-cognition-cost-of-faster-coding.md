---
title: "Source: Adam Tornhill — Compressed Cognition: The Cost of Faster Coding"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-compressed-cognition-cost-of-faster-coding]
raw_file: [raw/articles/tornhill-compressed-cognition-cost-of-faster-coding.md]
tags: [attention-bottleneck, verification-burden, agentic-coding, cognitive-load, measurement, focus]
---

# Source: Adam Tornhill — Compressed Cognition: The Cost of Faster Coding

Essay by **[[adam-tornhill]]** on *Code for Humans and Machines* (**2026-05-07**), the series' most-shared
piece and the one previously known to the KB only as a line item in
[[tornhill-ai-readable-code-series]]. Now compiled in full from
`raw/articles/tornhill-compressed-cognition-cost-of-faster-coding.md`. **Read the capture's
`capture_note` before citing anything numeric from this page.**

## Summary

The thesis: **"Agentic coding is mentally expensive."** Agents let you stay with the high-level problem
longer, but "they also compress too many meaningful decisions into too little time." Pre-2025 work
"unfolded at human speed, which meant the decisions were naturally spaced out. Today, agents compress
the timeline. We have to deal with complexity and decisions that used to be spread over days in a
single coding session." Worse, the two effects stack: **more complex work** *and* a **compressed
decision timeline**.

He grounds this in three borrowed research strands — all cited **by author name only, with no link,
date or title**:

- **Decision fatigue** — "Danziger et al. looked at thousands of [judicial] rulings and found that
  favorable decisions dropped as judges moved through a work session… the decision quality then
  recovered after breaks." Manual coding had "a built-in pacing mechanism. That was our implicit
  recovery break. And it's now gone."
- **Cognitive load** — "Sweller's classic work": agents "remove lower-level serial coding work" but
  "increase the amount of high-level state you have to evaluate." His phrase for the result: **"It's a
  lot more architecture per minute."**
- **Working memory** — "seven plus or minus two… was over-optimistic. Modern cognitive scientists paint
  a more depressing picture: we can, at best, hold **3-4 things** in our head at once and still be able
  to reason effectively."

Then the mechanism specific to agents: **self-interruption**, which he says is more disruptive than
external interruption. The agent "asks a question, produces a diff, gets blocked by a missing tool,
fails a test, or suggests a change that looks *almost* right but touches too much. **Each event pulls
you into a new review-verify-steer decision.**"

**The measurement** (see Limits — this is the batch's only hard number, and it is unattributed):

> "One of my favourite studies gave experienced open-source developers access to AI tools. It was a
> controlled trial, so half the participants were still coding in the old school way… the developers
> with AI tools felt faster. Indeed, they claimed so themselves, **estimating a 20% speedup**. Only
> problem: they were not. They ended up **19% *slower*** than the non-AI group."

His reading: "even expert developers overestimate the AI impact on developer productivity," and "one
plausible contributor is self-interruption."

**His management rules**: keep agent tasks small "enough so that the review fits in your head";
automate everything automatable; **"Don't review details, verify them"** — "we need to accept that we
can no longer know every line of code. Again, automation and safeguards are the mechanisms for
delivering trust, not manual inspection"; and **"Avoid parallel work"** — "I typically have one
long-running agentic maintenance task that I just babysit, and then one focus task. **Never more.**"
On the twenty-agents hype: "I cannot even think about twenty *meaningful* things to build, and even
less so about the resulting cognitive tax… **It is the parallelisation of human attention that does not
scale.**"

He closes with re-investment advice for the recovered hours: train as an end-user, get away from the
laptop, do exploratory testing, learn your product metrics, get involved in sales — "deepen your
expertise while giving your brain a recovery window."

## Key points

- **The felt-vs-measured gap is the point of the piece**, and the reason both figures must be kept
  distinct: **20% is what developers *estimated*; 19% slower is what was *measured*.** Collapsing them
  into one "figure" destroys the finding.
- **The mechanism for why reading agent output doesn't scale is cognitive, not managerial.** Decision
  *density*, not decision *count*, is the constraint — which is what makes the
  [[verification-burden]] dispute a resource argument rather than a discipline argument.
- **"Don't review details, verify them"** is the same distinction Willison draws in
  [[willison-more-than-just-code-review]] and the same triage he operationalises three months later in
  [[tornhill-controlling-the-uncertainty-machine]]. This piece (May) is the earlier, cognitive
  justification for that (August) method.
- **A flat rejection of human-side parallelism**, and he pre-empts the obvious objection: "yes, I
  understand sub-agents and machine parallelisation. That is not what I'm objecting to."
- **Recovery is a first-class engineering practice here** — "take breaks from your agents. And take
  those breaks earlier than you think you need them" — with the non-coding hours reframed as
  domain-expertise building, i.e. the same "become the domain expert" move
  [[tune-no-rapport-with-a-model-you-didnt-code|Tune]] worries agents are eroding.

## Limits

- **The study is unattributed and cannot be followed from this capture.** Tornhill writes only "one of
  my favourite studies" and names no study, authors, institution, date or link. **Do not write
  "Tornhill cites METR" anywhere in this KB** — attaching any named study to this passage would be
  *our* identification, not his, and the capture supports none. Cite it as **an unnamed controlled trial as
  relayed by Tornhill**, and keep the uncitability visible. Likewise Danziger, Sweller and the
  "3-4 things" revision are name-only, unlinked; the Danziger judicial-rulings result in particular has a
  contested literature not acknowledged here.
- **IMPRESSION NOT MEASUREMENT for everything about the author's own experience**: "I can usually
  sustain the pace for a couple of hours. Then I need a break… based on conversations with other
  engineers, I do not think I am alone in that." Self-report plus hearsay.
- **NOT INDEPENDENT on the prescription.** "Automation and safeguards are the mechanisms for delivering
  trust, not manual inspection" is argued by the founder/CTO of **CodeScene**, which sells automated
  code-quality safeguards. The diagnosis is separable from the sales pitch; the marker still travels.
- **The borrowed psychology is analogy, not evidence about programmers.** Judicial parole decisions and
  Sweller's instructional experiments are not measurements of agentic coding; no study here observes a
  developer's decision density.
- No data on his own workflow: the "one maintenance task + one focus task, never more" rule is a
  personal ceiling, not a measured optimum.

## Connections / contrast

- **[[attention-bottleneck]]** — this is the mechanism page's primary source: *why* human attention is
  the scarce input, with a named cognitive cause (decision density + self-interruption).
- **Head-on collision with [[laycock-the-conductor-developer|Laycock's conductor developer]]**, and
  this is one of the sharpest disagreements in the batch. She reports engineers running **eight, ten,
  twelve agents in parallel** and treats orchestration-at-that-width as the emerging shape of the job;
  he says human-attention parallelisation "does not scale" and running twenty agents is "exactly the
  wrong thing to even consider." **Both are self-reports/anecdotes** — neither side has measurement —
  and the KB should hold both open. Note they agree on the *premise* (attention is the bottleneck) and
  differ on whether the response is to widen the conductor's span or to narrow it.
- **[[verification-burden]]** — supplies the cost side of the ledger. Laycock's remedy (pair, mob,
  design together) spends *more* human attention per unit of code; this is the argument that the
  budget is already overdrawn. Neither author addresses the other.
- **[[comprehension-debt]]** — the debt's *pricing mechanism* in cognitive units, complementing
  [[dilger-real-cost-of-ai-is-second-order]]'s pricing in money. Also the affective symptom recorded
  from [[dilger-describing-without-solving-burns-you-out]] (burnout from supervising parallel agent
  sessions) — same finding, two authors, independently.
- **The one number the loop-engineering thread lacked.** [[loop-engineering]] and [[agentic-coding]]
  carry many *impressions* of speedup; this relays a controlled trial in which the impression was
  positive and the measurement negative. It is the strongest available caution against
  self-reported-productivity claims anywhere in the KB — and it must be carried with its
  uncitability, not laundered into a citation.
- **[[token-budget-quality-cliff]] / [[context-rot]]** — machine-side limits; this is the human-side
  analogue ("3-4 things" as the human context window).
- Also: [[tornhill-merge-conflicts-agentic-bottleneck]] (the other Tornhill piece where
  parallel agents cost more than they pay), [[agent-harness]], [[loop-engineering]]'s "stay the
  engineer" caveats.

## Links

Entities: [[adam-tornhill]] · [[rachel-laycock]] · [[martin-dilger]]. Concepts:
[[attention-bottleneck]] · [[verification-burden]] · [[comprehension-debt]] · [[agentic-coding]] ·
[[loop-engineering]] · [[context-rot]] · [[token-budget-quality-cliff]]. Related sources:
[[tornhill-controlling-the-uncertainty-machine]] · [[tornhill-ai-readable-code-series]] ·
[[laycock-the-conductor-developer]] · [[dilger-real-cost-of-ai-is-second-order]] ·
[[dilger-describing-without-solving-burns-you-out]] · [[willison-more-than-just-code-review]].

_Raw source: `raw/articles/tornhill-compressed-cognition-cost-of-faster-coding.md`._
