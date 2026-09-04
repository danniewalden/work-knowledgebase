---
title: Token-Budget Quality Cliff
type: concept
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-modeling-agent-improved-by-learning-loop, dilger-one-million-tokens-self-training-modeling-agent]
tags: [agentic-coding, loop-engineering, autonomy, failure-modes, focus]
---

# Token-Budget Quality Cliff

**A model's output quality degrades as a function of its remaining context or token budget rather than
of the task's difficulty — and it degrades by taking shortcuts and skipping steps rather than by
failing or refusing.** The result looks like a completed attempt, which is what makes it dangerous in an
unattended loop.

## The observation

The KB's only direct evidence is [[martin-dilger]]'s, from watching his self-training modeling agent run
continuously ([[dilger-modeling-agent-improved-by-learning-loop]], 2026-08-28):

> "[E]ver 5th iteration or so is really bad, making stupid modeling mistakes, skipping steps.. digging into
> the reasoning, it's always the model taking shortcuts when it reaches certain budget thresholds. Most
> models are obviously trained to make the best with the budget they have, actively taking shortcuts when
> budgets get depleted, to deliver at least something."

Three parts worth separating — the first two are his, the third is a reading of what he describes:

1. **He attributes the trigger to budget, not difficulty.** "It's *always* the model taking shortcuts
   when it reaches certain budget thresholds." Note what he does *not* report: any comparison against
   fresh-budget runs, or any measurement. The attribution comes from reading the reasoning traces after
   the fact, which is his account of the model's account of itself.
2. **The mechanism he proposes is learned economizing.** "Deliver at least something" is rational
   behavior under a budget constraint — arguably trained-in, and therefore not something a better prompt
   fixes.
3. **The failure is silent** (inference, not his words). Skipped steps and shortcuts produce a plausible
   artifact; nothing in his description involves an error, a refusal, or a low-confidence signal.

## Why it matters

**It is an autonomy bound, and it binds at a rate that matters.** Roughly one iteration in five is far
above the error rate any unattended pipeline can absorb without a check, and it is invisible to
outcome-blind monitoring. It belongs with the other empirical limits on unattended operation —
[[unattended-coding-agents]], and the *exposure* and *capability* bounds from
[[simon-willison]]'s late-August pair ([[willison-breaking-claude-code-auto-mode]],
[[willison-just-a-rumour-of-a-bug]]) — as a third, independent limit: **degradation**.

**It is a reason to grade, not just to watch.** Dilger noticed the bad iterations while running a loop
that diffs each round against a corpus of known-good models
([[dilger-one-million-tokens-self-training-modeling-agent]]) — he does not say the rubric is what
surfaced it, and by his own account the "ever 5th iteration or so" figure is an impression from watching runs.
But the point stands structurally: a loop with no rubric has nothing that *would* catch a bad fifth
iteration, because the artifact looks fine. This is the strongest practical argument in the KB for
[[event-modeling]]-as-rubric: the value is not that the agent models well on average, it is that you can
*detect the run where it didn't*. Compare [[bockeler-tdd-inside-the-agent-loop]]'s finding that a
self-confirmed red test proves nothing — the check has to be external to the thing being checked.

**It complicates the hill-climbing loop.** [[loop-engineering]]'s hill-climbing pattern assumes each
iteration is a fair sample of the agent's ability. If quality is a function of budget position, then
iteration results are **not independent** and a naive "did it improve?" comparison can be measuring
budget state rather than skill. Dilger's own loop compares each round against the previous one, which is
exactly the comparison this contaminates. He says he intends to feed the cliff back into the loop; how
you'd correct for it is open.

## Open questions

- **Is the trigger absolute or proportional?** A fixed remaining-token threshold and a fraction-of-budget
  threshold have different mitigations (chunk smaller vs. reset earlier).
- **Does compaction help or hurt?** Context compaction frees budget but discards detail; if the cliff is
  driven by *perceived* remaining budget, compaction may reset the behavior at the cost of the material
  the model needs.
- **Is it detectable from the inside?** Dilger diagnosed it by reading reasoning traces after the fact.
  Whether a run can be flagged as budget-degraded *while it happens* — before the artifact is accepted —
  would decide whether this is a monitoring problem or a scheduling one.
- **Does it reproduce across models?** The budget-cliff post names no model; the loop it reports on was
  described three days earlier as running QWEN3.7:27b locally, so that is an inference, not a stated
  fact. Either way nothing in the KB tests this on a frontier model, and the "trained to make the best
  with the budget they have" explanation would predict it generalizes.

## Evidential status

**Weak but specific.** One practitioner, self-reported, unquantified ("ever 5th iteration or so" is an
impression from watching runs, not a measured rate), on one presumed local model, with the causal
attribution resting on the model's own reasoning traces. It is recorded here because the failure *shape* is precise and checkable,
not because the rate is established. Treat it as a hypothesis worth instrumenting rather than a finding.

## Related

[[loop-engineering]] · [[unattended-coding-agents]] · [[agent-harness]] · [[autonomy-ladder]] ·
[[event-modeled-agent-design]] · [[context-engineering]] · [[long-running-agents]] ·
[[harness-engineering]]

_Sources: [[dilger-modeling-agent-improved-by-learning-loop]] · [[dilger-one-million-tokens-self-training-modeling-agent]]._
