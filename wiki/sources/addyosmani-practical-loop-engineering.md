---
title: "Source: Osmani — Practical Loop Engineering"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [addyosmani-practical-loop-engineering]
raw_file: [raw/articles/addyosmani-practical-loop-engineering.md]
tags: [loop-engineering, agentic-coding, verification, claude-agent-sdk, focus]
---

# Source: Osmani — Practical Loop Engineering

Source: [[addy-osmani]], *"Practical Loop Engineering"*, addyosmani.com (originally his Substack,
*Elevate*), **2026-08-14**. Raw capture: `raw/articles/addyosmani-practical-loop-engineering.md`. The
hands-on sequel to his definitional primary [[addyosmani-loop-engineering]] and its accountability
follow-on [[addyosmani-own-the-outer-loop]].

## Summary

Two months after the essay, what actually got used. Osmani's working definition: *"A loop is an
autonomous, self-correcting feedback cycle where an AI agent repeatedly acts, tests its results and
adjusts its approach until a specific goal is met."* He reports the discipline has **collapsed into two
primitives** — `/goal` (drive a bounded task to a measurable finish line, with a **separate evaluator
model** grading the stop) and `/loop` (re-run on a cadence, "think of it a little bit like a cron") —
where six months earlier it meant hand-rolled bash loops and [[ralph-loop|Ralph]] experiments on
personal projects. He runs **5–10 agents a day, maxing at ~5 concurrent**, and spends the piece on
**which work he delegates, what he watches, and what loops are not for.**

## Key points

- **The primitives have real, different jobs.** `/goal` is for *"building any specific piece of work
  until it's provably done"* — e.g. *"make this page load 50% faster,"* *"review and close the last 10
  issues"* (which he flags as semi-open-ended). `/loop` is *"a little bit more of a scheduler… best for
  doing things like polling logs or monitoring external states."* Composed: **loop supplies the
  heartbeat, goal supplies the hands** — *"loop for every 24 hours, check GitHub for issues labeled bug.
  If one exists, use goal to implement a fix until all local tests pass and push the branch."*
- **The most important technical correction in the piece: the `/goal` evaluator is not a quality
  checker.** *"The evaluator sitting behind goal is not that checker, by the way. **It doesn't look at
  the content** to see if it's good or bad in any way, shape, or form. All it does is **examine the
  conversation transcript** to see if the hard rules you specified have been met."* This distinguishes
  **stop-condition grading** from **output review** — two things the KB's maker ≠ checker framing has
  been running together.
- **A model `/goal` invocation, worth keeping as a template**, because it shows five separate
  constraints in one line: a target metric with a named measurement tool (*"Lighthouse performance score
  is >= 92 and LCP under 1.8s **as shown by the Lighthouse CLI output**"*), an invariant (*"Do not change
  the public API of any hooks"*), a **per-turn progress requirement** (*"Each turn must improve at least
  one reported metric"*), a **no-progress abort** (*"abort if two consecutive turns show no
  improvement"*), and a **turn cap** (*"Stop after 10 turns"*).
- **Delegation calibrated by blast radius, stated concretely.** Safe to hand off fully: *"I implemented
  this feature, go write the documentation for it,"* *"go double check that we have sufficient test
  coverage."* Watched closely: complex problems where *"even if I've given it a good spec… there is still
  a reasonable chance it may not get everything right,"* and **anything touching authentication,
  security, finance, or a system he has granted access to.** *"This is why there's nuance when deciding
  to use it for an evergreen codebase without users or as much historical complexity vs. say a brownfield
  bank codebase."*
- **Maker ≠ checker, plus a concrete example of what it catches.** *"The other habit that matters here is
  not letting the agent that did the work decide the work is good. One sub-agent drafts the change. A
  separate one verifies it."* His example is a **dimension** failure, not a correctness failure: the
  agent judged performance fine *"only evaluating performance based on desktop, but you're actually
  caring about the experience on mobile… very confident about one dimension of the problem, but not the
  other."*
- **His own near-miss — delegating judgment, not the task.** He asked an agent to survey competitors and
  produce local (unpushed) PRs for the gaps. *"I almost pushed some of those changes. But I didn't
  actually look at them closely enough. I read through its research, but I didn't look at the
  implementations closely enough."* On inspection they *"would introduce a lot of additional complexity
  for our users, for… not all that much gain."* Conclusion: *"you need to sometimes check yourself, that
  you are not delegating the taste and the judgment to your agent. You're delegating the task, and then
  you are actually checking back that it's meeting your bar."* **IMPRESSION NOT MEASUREMENT** — one
  anecdote — but it is the batch's cleanest illustration of the failure mode.
- **What loops are not for.** *"If you don't have a clear idea of what the end-state/done/good means for
  your completion, it may not be the right pattern."* The named anti-goal: *"keep going until this UI
  design is good"* — *"What does that mean? Good to who? How is it being evaluated?"* **Tasks requiring
  human taste, subjective design, or open-ended creative exploration are excluded.**
- **A spin detector.** *"One classic sign that you've got a loop spinning in place is the same command
  being tried over and over without any change in the result. Give the same command a third time with no
  change from the second and it's probably time to stop."*
- **The verification skill he lifts from the Claude Code team is a good artifact** — a `SKILL.md` that
  forbids declaring a UI change done on a successful edit alone and instead requires: start the dev
  server and open the page, **interact with the change and screenshot before/after**, **zero new console
  errors or warnings**, a performance trace with Core Web Vitals — *"If any step fails, fix the issue and
  rerun from step 1 — do not hand back partially verified work."* This is a verification loop encoded as
  project knowledge rather than as a prompt.
- **Operational fine print worth recording** (product-specific, Aug 2026): recurring loops **expire
  seven days after creation** — *"I'd been telling people this was three days. It's seven"* — and loops
  are **session-scoped**, stopping when a new conversation starts, though `--resume`/`--continue` brings
  back recurring tasks still inside the window. `/schedule` runs in the cloud for anything that must
  outlive the session.
- **Limits.** A practitioner self-report about **his own use of his own employer's ecosystem's tooling**
  (Osmani is a Director at Google Cloud AI; the piece is largely about Anthropic's Claude Code
  primitives, which he uses and promotes). **No measurement anywhere**: "5 to 10 agents," "80–90 pull
  requests a day," "over 80,000 stars" are workload and popularity figures, not outcomes; there is no
  before/after, no defect rate, no time saved. Several claims are hedged by the author himself
  (*"Sometimes that works well, sometimes it doesn't, but it's really about the experimentation"*). A
  long block quote of the **Claude Code team's own write-up** carries that team's **VENDOR SELF-REPORT**
  framing of its own product's primitives. Everything about `/goal`, `/loop`, `/schedule`, auto mode and
  dynamic workflows is **date-bound to one product in Aug 2026** and includes research previews.

## Connections / contrast

**The stop-condition/output-review distinction is the most valuable delta to [[loop-engineering]].** The
KB page had described `/goal` as *"a separate evaluator model grades the stop — maker≠checker applied to
'done'"* and filed it under the verification loop. Osmani here says explicitly that this evaluator
**never looks at content**. So `/goal` is not maker ≠ checker at all in the quality sense; it is a
**stop-condition referee**. The KB had been crediting it with more than it does — which matters, because
the whole back-pressure argument rests on knowing which instrument is checking what. This converges with
[[wong-loop-engineering-teaching-ai-agents-how-to-think|Wong's]] ordering rule (deterministic check
first, second model only when forced) and with
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] finding that a self-graded red test proves the agent
ran the test, not that the failure was for the right reason.

**The exclusion criterion sharpens the [[software-factory]] "do you need one" question.** Loops require
a writable check; taste does not have one — which is the operational form of
[[addyosmani-earning-taste-and-judgment|"anything gradeable by someone else is getting automated"]] and
of [[addyosmani-human-judgment-relocates|"human judgment relocates"]]. Together the three Osmani pieces
in this batch make one argument in three registers: **the loop takes the gradeable, the human keeps the
ungradeable, and the interesting engineering is deciding which is which per task.**

**It supplies the concrete instance [[loop-engineering]]'s five-primitives section lacks.** His daily
workflow — `/loop every 1h "Check the GitHub repository for any new open issues. Provide a bulleted
summary of their urgency."` over a repo receiving up to 80–90 PRs/day, with **the project's own written
contribution guidelines becoming the enforceable triage stopping condition** ("we currently don't accept
translations" → close PRs touching that) — is the most economical example in the KB of a **policy
document used as a loop's exit criterion.** That is the same move
[[macmanus-prs-not-welcome-software-factories|Astro and Flue]] make at project scale, and it belongs next
to it: written policy is a machine-checkable gate.

**The "third identical attempt = stop" heuristic** is the human-facing counterpart to
[[miracle-my-loop-engineering-workflow|Miracle's]] "if a fix fails twice, stop — no third attempt at the
same idea," and to [[addyosmani-code-agent-orchestra|his own]] "kill and reassign after 3+ stuck
iterations." Three independent statements of the same bound; the KB can state it as a convergent
practitioner rule (while noting none of them measured it).

## Links

[[loop-engineering]] · [[addyosmani-loop-engineering]] · [[addyosmani-own-the-outer-loop]] ·
[[addyosmani-earning-taste-and-judgment]] · [[addyosmani-human-judgment-relocates]] ·
[[addyosmani-code-agent-orchestra]] · [[addyosmani-agentic-code-quality]] · [[ralph-loop]] ·
[[harness-engineering]] · [[software-factory]] · [[unattended-coding-agents]] · [[autonomy-ladder]] ·
[[feedforward-and-feedback-controls]] · [[agent-observability-and-evals]] · [[claude-agent-sdk]] ·
[[anthropic]] · [[addy-osmani]] · [[anthropic-getting-started-with-loops]] ·
[[wong-loop-engineering-teaching-ai-agents-how-to-think]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[miracle-my-loop-engineering-workflow]] · [[macmanus-prs-not-welcome-software-factories]]

_Source: [[addyosmani-practical-loop-engineering]] (raw: `raw/articles/addyosmani-practical-loop-engineering.md`)._
