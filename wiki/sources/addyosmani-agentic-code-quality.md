---
title: "Source: Osmani — Agentic Code Quality"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [addyosmani-agentic-code-quality]
raw_file: [raw/articles/addyosmani-agentic-code-quality.md]
tags: [agentic-coding, fitness-functions, feedforward-and-feedback-controls, software-factory, focus]
---

# Source: Osmani — Agentic Code Quality

Source: [[addy-osmani]], *"Agentic Code Quality"*, addyosmani.com (originally his Substack),
**2026-08-08**. Raw capture: `raw/articles/addyosmani-agentic-code-quality.md`. The **quality-gates**
member of his August 2026 trio, sitting under
[[addyosmani-practical-loop-engineering|Practical Loop Engineering]] (08-14) and
[[addyosmani-human-judgment-relocates|Human Judgment Relocates]] (08-21).

## Summary

*"Software quality now depends on the constraints you set around your agents."* Code review as the
quality mechanism does not scale — *"there's just too much code for anyone to read"* — so *"more and
more of our quality checks have to happen in the harness, environment, and operating system around the
agent."* The framing that carries: **an agent can propose anything; the constraints decide whether a
proposal is safe enough, correct, scoped, and useful to ship.** Quality is not a metric but *"a
collection of signals of varying importance to you and your team,"* and the constraints are what give
those signals **teeth** — implemented as **back-pressure** throughout the pipeline rather than as one
review at the end.

## Key points

- **Quality gates, enumerated.** Unit, property and acceptance tests; **mutation testing** (*"we generate
  variations of code, run it against the same tests, and make sure that people aren't sneaking bugs in
  that we're missing"*); metrics like cyclomatic complexity and line length; and **architecture rules
  enforced by linting tools** (his example: ESLint). *"Many of these tools have built-in hooks that can
  be used to pull in agents, or humans, when things break."*
- **Constraints act at three different times, and the distinction is load-bearing.** *"Some constraints
  shape work before it begins. Others give feedback while the agent is working. Others decide whether its
  output can cross the production boundary at all."* Feedforward, in-flight sensor, and admission
  control — three roles, not one gate.
- **Quality is multi-dimensional, and each dimension decomposes.** Beyond correctness:
  **maintainability, performance, security, efficiency, comprehensibility** — and *"just as correctness
  decomposes into many signal types, so does the rest of quality."* Then the sharpest line: *"while it
  matters **how many** constraints we have in place, it matters more **whether they're challenging
  enough** to meet our bar."*
- **Back-pressure, defined by its implementations.** *"compilers rejecting invalid code, tests failing,
  security policies blocking bad practices, CI declining to deploy. **Ideally it exists throughout the
  loop, not as a single review at the very end of all the work.**"*
- **The capacity argument, which is the most original part of the piece.** What happens when change
  volume exceeds what your tools can consume? *"We end up building a queue and relying on a verification
  system that moves at human speed."* Four levers, stated as a genuine choice: **(1) scale the
  verification system** ("create more capacity to constrain and push back"); **(2) reduce the rate at
  which agents generate changes** so verification catches up; **(3) lower the quality bar** so
  verification pushes back less hard; and **(4) deliberately un-constrain in some directions** — *"we
  could actually get more done by un-constraining in some directions… **By providing tighter constraints
  where we care the most, we can maximize our throughput without sacrificing quality.**"* *"From a
  scaling perspective, we need to be ready to do all of these things."*
- **Autonomy failures are usually environment failures.** *"Many of the reasons that humans fail to ship
  great code are shared with what agents might do: **brittle environments that don't hold up under
  script-driven stress, nondeterministic builds, missing permissions, and weak tests.**"* So the goal is
  *"a better environment that gives agents trustworthy feedback, allows for **low-damage failure
  modes**, and makes it easier to progressively build up success."* Restated: *"The environment we're after is one where an
  agent can do real work, get feedback it can trust, and **fail without doing much damage**."*
- **Human attention as the scarce input to be routed.** *"If you put a human check into a system that
  otherwise moves at machine speed, don't be surprised if that impacts productivity… **Downstream humans
  should only be pulled in when the automated guardrails for constraints break.**"* And routing by risk:
  *"a change is routed to high, gated, or human-decided autonomy according to its risk, evidence, and
  track record."*
- **Guillermo Rauch's not-reading test, and Osmani's reading of it.** Rauch lists low-stakes situations
  where skipping code review may be acceptable; Osmani's gloss is the useful part: *"Notice that every
  'yes' is really a statement about **how low the stakes are** — no users, throwaway code, prototype.
  Once the stakes go up, something has to read the code. **If it isn't you on every diff then it has to
  be the constraints.**"*
- **The honest admission about where we actually are.** *"For now, much of the difference between useful
  agent output and slop still comes down to **the skill of the team operating the loop**."*
- **The ultimate constraint is self-imposed.** *"The ultimate constraint in this system is the one we
  place on ourselves to stand behind the decisions and actions we've taken to build the system and to
  operate it. But like all other constraints, we need to make thoughtful trade-offs about how much we
  want our own judgment to restrain, to back-pressure, and to act as a final check."*
- **Limits.** A short conceptual essay — **no data, no case study, no worked example, and no numbers at
  all** (which, in this batch, is a virtue: nothing here needs an interested-claim marker for a figure
  because there are no figures). The four scaling levers are presented as available choices with **no
  evidence about their relative cost or effect**, and *"lower the quality bar"* is listed neutrally
  alongside the others. Its four illustrations are **images not transcribed in the capture**, so
  their content is unavailable and this page reflects only the prose. The Rauch list is referenced
  through an image, so its actual items are not in the capture. **NOT INDEPENDENT** for the general
  framing: Osmani is a Director at Google Cloud AI writing about the practice he also promotes
  commercially. Footnote worth recording as a period detail: *"This article was rated 100% human written
  by Pangram 4."*

## Connections / contrast

**This is the best conceptual anchor in the KB for [[fitness-functions]] and
[[feedforward-and-feedback-controls]] applied to agents**, and the three-times distinction (before /
during / at the boundary) maps directly onto that page's guides-vs-sensors vocabulary while adding a
third category the KB had not named before this source: **admission control** — the constraint that decides whether output
may cross the production boundary. That is the mechanism behind [[addyosmani-human-judgment-relocates|Vercel's]]
success/flawed/blocked/manual classification and [[miracle-my-loop-engineering-workflow|Miracle's]]
"PR only on PASS."

**The capacity argument is a real extension of [[software-factory]]'s back-pressure rule.** The KB
currently states back-pressure as a one-way constraint — *"you can only hand a loop as much autonomy as
you can cheaply and reliably verify."* Osmani turns it into a **four-way trade-off with an explicit
throughput term**: scale verification, throttle generation, lower the bar, or *selectively* un-constrain
where you don't care in order to spend the capacity where you do. The fourth lever is the one no other
KB source states, and it is what makes this an engineering budget rather than a moral position. It is
also the qualitative form of [[miracle-my-loop-engineering-workflow|Miracle's]] Amdahl argument
(generation parallelized, verification did not — the serial fraction sets the ceiling): Osmani names the
levers, Miracle names the bound.

**"If it isn't you on every diff then it has to be the constraints"** is the cleanest statement of the
KB's light-vs-dark factory distinction ([[addyosmani-software-factories-light-and-dark]]) and the direct
answer to [[dudycz-fork-can-you-own-it|Dudycz's]] ownership objection — cheap generation doesn't dissolve
responsibility, it relocates it into the constraint set. Pair it with
[[willison-understand-to-participate]] and [[comprehension-debt]]: constraints substitute for reading
**correctness**, not for reading **comprehension**, and this piece does not claim otherwise.

**"Brittle environments that don't hold up under script-driven stress"** converges with two other
sources on a single, under-filed claim: **environment reliability is an agentic-scale property.**
[[addyosmani-code-agent-orchestra|His own orchestra piece]] gives the mechanism (*"flaky environments…
become systemic blockers when forty agents hit the same flaky test simultaneously"*) and
[[edwards-alexander-an-accidental-blackboard|the accidental blackboard]] gives the field instance (CI
overload killed the coordination effect). Also converges with
[[tornhill-codescene-unhealthy-code-agentic-token-cost]] and
[[borg-tornhill-code-for-machines-not-just-humans]] from the code-health side, and with
[[breunig-fable-and-the-end-of-the-free-lunch|Breunig's]] economics: **the environment is a substitute
for model capability, and a flaky one is a tax.**

**"Architecture rules enforced by linting"** is the same move as
[[nick-tune-enforced-application-architecture-agents-humans|Tune's enforced application architecture]]
and [[dilger-keep-command-handlers-pure|Dilger's]] "a written skill had to be **enforced**, not just
stated" — three sources agreeing that architectural intent expressed as prose does not survive contact
with an agent, and must be expressed as a failing check.

## Links

[[agentic-coding]] · [[fitness-functions]] · [[feedforward-and-feedback-controls]] ·
[[software-factory]] · [[loop-engineering]] · [[harness-engineering]] · [[mutation-testing]] ·
[[comprehension-debt]] · [[autonomy-ladder]] · [[unattended-coding-agents]] · [[agent-governance]] ·
[[ai-readable-code]] · [[agent-observability-and-evals]] · [[addy-osmani]] ·
[[addyosmani-software-factories-light-and-dark]] · [[addyosmani-practical-loop-engineering]] ·
[[addyosmani-human-judgment-relocates]] · [[addyosmani-code-agent-orchestra]] ·
[[addyosmani-earning-taste-and-judgment]] · [[miracle-my-loop-engineering-workflow]] ·
[[edwards-alexander-an-accidental-blackboard]] · [[breunig-fable-and-the-end-of-the-free-lunch]] ·
[[dudycz-fork-can-you-own-it]] · [[willison-understand-to-participate]] ·
[[nick-tune-enforced-application-architecture-agents-humans]] · [[dilger-keep-command-handlers-pure]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-codescene-unhealthy-code-agentic-token-cost]]

_Source: [[addyosmani-agentic-code-quality]] (raw: `raw/articles/addyosmani-agentic-code-quality.md`)._
