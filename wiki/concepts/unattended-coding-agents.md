---
title: Unattended Coding Agents
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [willison-breaking-claude-code-auto-mode, willison-just-a-rumour-of-a-bug, dilger-trust-needs-to-be-engineered, dilger-lights-off-software-factory-dead-end, stripe-minions-one-shot-coding-agents, hashimoto-my-ai-adoption-journey, openai-harness-engineering-codex]
tags: [harness-engineering, coding-agents, autonomy, workflow, agent-safety, focus]
---

# Unattended Coding Agents

Coding agents that run **without a human in the loop during execution** — kicked off with a task,
then left to plan, code, test, and open a pull request on their own. They sit at the high end of the
[[autonomy-ladder]] and are the practical payoff of good [[harness-engineering]]. In
[[loop-engineering]] terms they are the **event-driven loop** (level 3) — the harness put on a trigger
and left to run.

This page used to say that the maker≠checker verifier sub-agent "is what makes unattended safe."
**Rewritten 2026-08-31: that no longer survives the evidence.** Three independent limits have since been
captured, none of which a verifier catches, and the back-pressure finding on [[software-factory]] —
*you can only hand a loop as much autonomy as you can cheaply and reliably verify, and not one inch
more* — reframes verification as a **budget** rather than a solution.

## Two scales, same idea

- **Enterprise / at scale:** [[stripe]]'s **minions** ([[stripe-minions-one-shot-coding-agents]]) are
  built to **one-shot** tasks — start from a Slack message, end at a CI-passing PR, a reported 1,000+ merged per
  week with no human-written code. Parallelized across isolated devboxes; especially useful during
  on-call. [[openai-harness-engineering-codex]] is the same pattern taken to a whole product.
- **Individual developer:** [[mitchell-hashimoto]] ([[hashimoto-my-ai-adoption-journey]]) runs
  background/"end-of-day" agents and aims to "always have an agent running," but deliberately keeps to
  *one* agent and report-only triage — a deliberately modest, human-in-control version.

## What makes it work

A constrained, well-instrumented environment: deterministic steps interleaved with the agent loop,
**self-verification** ([[anthropic-effective-harnesses-long-running-agents]]), and **shift-left
feedback** — fast computational sensors run as early as possible
([[feedforward-and-feedback-controls]]). The recurring constraint is **human attention**: unattended
agents exist to parallelize work without spending the scarce resource of developer focus. A shared
discipline across sources — control *when* you check on the agent; don't let it interrupt you
(Hashimoto: turn off notifications).

## The counter-position: constrain the decision, not the review (Dilger, 2026-08)

This page assumes verification capacity is the binding constraint on unattended work.
[[dilger-trust-needs-to-be-engineered]] accepts the constraint and attacks the other end:

> "AI can write good code. The thing is, you just can't trust it to do so reliably. The real issue is
> trust… Modeling upfront, making the important decisions, defining the structure before anything gets
> built, that's not bureaucracy. It's engineering trust… That's how you work around the review
> bottleneck. Not by doing more reviews, but by **making most of them obsolete**."

The mechanism is a **blueprint**: the agent does not structure the system, it fills in a structure already
fixed by the event model and its slicing, so the class of mistakes review exists to catch is narrowed
before the agent starts. His stated failure mode without it — "one tiny dependency in the wrong place, a
little too much coupling in another, and that's the start of a downward spiral" — is a claim that
unattended work fails *structurally* rather than functionally.

He is not, however, arguing for the dark factory. [[dilger-lights-off-software-factory-dead-end]] is
explicit that "every single team I know who went down that route circled back," and keeps a 2–3 minute
structural review — **for comprehension, not correctness**: "I keep connected to the code base… If
something goes wrong, I roughly know where to look." See [[software-factory]], [[comprehension-debt]].

*Both are self-reported and vendor-adjacent, and the proof offered is an n=1 anecdote — a non-developer
shipping working slices — which he says himself: "Not a benchmark, not a demo."*

## Three independent limits

As of late August 2026 the KB holds three bounds on unattended operation, found by different people
looking at different things, and **no verifier catches any of them.** They are worth holding together
because each defeats a different assumption.

| Bound | What fails | Source |
| --- | --- | --- |
| **Exposure** | The guardrail itself becomes part of the failure | [[willison-breaking-claude-code-auto-mode]] |
| **Capability** | Other people's agents, not yours | [[willison-just-a-rumour-of-a-bug]] |
| **Degradation** | Output quality decays with budget, silently | [[token-budget-quality-cliff]] |

**Exposure.** Johann Rehberger's bypass of Claude Code's auto mode — which he says works 80% of the
time, unverified independently — is bad enough; the part
that bounds autonomy is what happened next — *"Claude tried to terminate the malware process once it
noticed the compromise, but Auto Mode denied the cleanup command."* The classifier permitted the
irreversible act and blocked the remedial one, because it reasons about command shape rather than
consequence. **A safety mechanism that can prevent recovery is not a partial control, it is a new
failure mode.** The endorsed remedies are entirely environmental — container/VM/OS sandbox, restricted
egress, no home directories or credentials in the agent runtime, monitoring — which is
[[harness-engineering]]'s "engineer the environment, don't trust the prompt" applied to security. See
[[prompt-injection]].

**Capability.** OCaml patches drew automated exploit probes within **about ten minutes** of being shared
for discussion, and rclone went from ~20 security disclosures in ten years to **over 40 in a single month**,
about 75% of them substantive. This bound is shaped differently from the other two: it is not about what
your agent does, it is about what everyone else's agents do to code you have just touched. The knock-on
is process collapse — GitHub CVE assignment stretched from 2–3 days to 3–4 weeks — and Madhavapeddy's
point, in Willison's paraphrase, is that this rate of discovery *"appears incompatible with existing open
source embargo practices for new issues."*
Note also that he got the task done by switching models when one refused: **vendor refusal is not a
control.**

**Degradation.** Roughly every fifth iteration of a continuously-running loop degrades as the model
nears its token budget, taking shortcuts "to deliver at least something" — producing a plausible
finished artifact with steps skipped. Invisible to outcome-blind monitoring, and at 1-in-5 far above
what an unattended pipeline absorbs without a check. *(Weakest of the three evidentially — one
practitioner, unquantified. See the page for its evidential status.)*

**What they have in common** is that each defeats a different comfortable assumption: exposure defeats
"the guardrail will catch it," capability defeats "we control the timeline," degradation defeats "the
runs are alike." Together they say the question is not *is the agent good enough to run unattended* but
*what happens on the run where it isn't* — which is the same conclusion
[[dilger-lights-off-software-factory-dead-end]] reaches from practice, and why he keeps a human review
he explicitly does not need for correctness.

## Open questions

- **Does anything catch degradation from the inside?** Exposure has sandboxing and capability has
  process change, but nothing captured detects a budget-degraded run before its artifact is accepted.
- **Are these three the whole set?** They were found by accident, by three people looking at unrelated
  things. That is not a survey, and the absence of a fourth is not evidence.

_Sources: [[stripe-minions-one-shot-coding-agents]] · [[hashimoto-my-ai-adoption-journey]] ·
[[openai-harness-engineering-codex]] · [[dilger-trust-needs-to-be-engineered]] ·
[[dilger-lights-off-software-factory-dead-end]] · [[willison-breaking-claude-code-auto-mode]] ·
[[willison-just-a-rumour-of-a-bug]]._
