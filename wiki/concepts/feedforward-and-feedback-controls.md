---
title: Feedforward and Feedback Controls (Guides & Sensors)
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [fowler-bockeler-harness-engineering, openai-harness-engineering-codex, stripe-minions-one-shot-coding-agents, fowler-bockeler-maintainability-sensors, addyosmani-agentic-code-quality, addyosmani-human-judgment-relocates, miracle-my-loop-engineering-workflow, zalando-agentic-engineering-snapshot, fowler-fragments-2026-09-01, miller-pondering-continuous-integration-ai-world-order]
tags: [harness-engineering, cybernetics, controls]
---

# Feedforward and Feedback Controls (Guides & Sensors)

[[birgitta-bockeler|Böckeler]]'s organising distinction for the controls inside a coding-agent
[[agent-harness]] ([[fowler-bockeler-harness-engineering]]). The harness acts as a cybernetic
**governor** combining both directions to regulate a codebase toward its desired state.

- **Guides (feedforward)** — anticipate behaviour and steer the agent *before* it acts. Raise the
  probability of a good result first time. Examples: AGENTS.md, Skills, reference docs, how-tos,
  codemods, language servers/CLIs.
- **Sensors (feedback)** — observe *after* the agent acts and let it self-correct. Most powerful
  when their output is optimised for LLM consumption (e.g. linter messages that embed the fix — a
  "positive prompt injection," exactly what [[openai-harness-engineering-codex]] does with custom
  lints). Examples: tests, linters, static analysis, logs, AI review.

Using only one direction fails: feedback-only repeats mistakes; feedforward-only never learns
whether the rules worked.

## Crossed with execution type

Each control is also **computational** (deterministic, fast, cheap — CPU: tests, linters, type
checkers) or **inferential** (LLM-based — semantic judgment, AI review; slower, costlier,
non-deterministic). Controls should be distributed across the change lifecycle by
cost/speed/criticality ("keep quality left"), plus continuous drift/health sensors outside the
lifecycle. This control system is the substance of [[harness-engineering]].

**Production example — [[stripe]]'s "shift feedback left"** ([[stripe-minions-one-shot-coding-agents]]):
a tiered computational-sensor stack — heuristic pre-push lints in <5s, then selective CI over 3M+
tests with **autofixes applied automatically** and only failures-without-autofix returned to the
agent, capped at "often one, at most two" CI rounds. A concrete illustration of running cheap sensors
as far left as possible and reserving expensive ones for later.

## Worked field report ([[fowler-bockeler-maintainability-sensors]])

Böckeler's sensors-only experiment sharpens the taxonomy with practice:

- **Computational sensors shine at the file/function level** (ESLint: max args/length/complexity;
  `dependency-cruiser` layer rules — an [[fitness-functions|architecture-fitness]] check used as a live
  sensor). The agent self-corrects on their feedback, and they can *replace* a markdown structure guide.
- **Self-correction guidance** is the key technique: custom lint/error messages that embed the *why*
  plus the exact fix ("positive prompt injection"), and **threshold-raising** instead of binary
  suppression so a rule re-fires if things degrade further.
- **Cross-file concerns need inferential sensors.** Raw coupling data fed to an LLM was noisy and
  over-flagged legitimate patterns; a full **inferential modularity review** ("garbage collection")
  was the most valuable, catching duplication and a date-range argument touching 40+ files. Good/bad
  isn't binary — it's *appropriate*, which needs context the import graph lacks.
- **[[mutation-testing]]** is the computational sensor behind the behaviour category: coverage ≠
  effectiveness (a 100%-covered file had 13 surviving mutants and no unit tests).
- **Sensor conflicts** are a real risk: `max-lines` vs `max-lines-per-function` pushed complexity out
  of functions and into long component-property chains.

## Constraints act at three times — and verification has a capacity ([[addyosmani-agentic-code-quality|Osmani, 2026-08-08]])

*"Software quality now depends on the constraints you set around your agents… **An agent can propose
anything. Your constraints decide whether a proposal is safe enough, correct, scoped, and useful, for you
and your team to ship.**"*

**A third category this page lacks.** *"Some constraints **shape work before it begins**. Others **give
feedback while the agent is working**. Others **decide whether its output can cross the production
boundary at all**."* The first two are this page's guides and sensors; the third is **admission
control**, and it is the mechanism behind [[addyosmani-human-judgment-relocates|Vercel's]]
success/flawed/blocked/manual gate and [[miracle-my-loop-engineering-workflow|Miracle's]] "PR only on
PASS."

**Quantity is not the metric.** *"While it matters how many constraints we have in place, **it matters
more whether they're challenging enough** to meet our bar."* Restated elsewhere as **"number of checks !=
quality"** — and the diagnostic: *"for any repeated checks, are they irrelevant? Are they noisy? Are they
actually making the system safer?"* Which is why the [[software-factory]] page now carries his
**per-stage timing** requirement: a sensor whose cost you don't measure can't be judged.

**The capacity argument — the genuinely new part, and it turns back-pressure into a budget.** What happens
when change volume exceeds what your tools can consume? *"We end up building a queue and relying on a
verification system that moves at human speed."* Four levers, offered as a real choice:

1. **Scale the verification system** — *"create more capacity to constrain and push back on changes."*
2. **Reduce the rate at which agents generate changes** so verification catches up.
3. **Lower the quality bar** so verification pushes back less hard.
4. **Deliberately un-constrain in some directions** — *"we could actually get more done by un-constraining
   in some directions… **By providing tighter constraints where we care the most, we can maximize our
   throughput without sacrificing quality.**"*

*"From a scaling perspective, we need to be ready to do all of these things."* The fourth lever is the one
no other KB source states, and it is what makes this an engineering budget rather than a moral position.
It is also the qualitative form of [[miracle-my-loop-engineering-workflow|Miracle's]] Amdahl bound
(*"Generation parallelized; verification did not"*): **Osmani names the levers, Miracle names the
ceiling.** The budget being drawn down is priced on [[attention-bottleneck]], and the argument about what
the human should read at all is on [[verification-burden]].

**Two supporting observations.** *"Back-pressure can be implemented through many tools: compilers
rejecting invalid code, tests failing, security policies blocking bad practices, CI declining to deploy.
**Ideally it exists throughout the loop, not as a single review at the very end.**"* And on where agent
autonomy actually breaks: *"Many of the reasons that humans fail to ship great code are shared with what
agents might do: **brittle environments that don't hold up under script-driven stress, nondeterministic
builds, missing permissions, and weak tests**"* — so the target is *"an environment where an agent can do
real work, get feedback it can trust, and **fail without doing much damage**."*

**And the line that decides when constraints are load-bearing at all**, on Guillermo Rauch's list of
situations where not reading the code is acceptable: *"every 'yes' is really a statement about **how low
the stakes are** — no users, throwaway code, prototype. Once the stakes go up, something has to read the
code. **If it isn't you on every diff then it has to be the constraints.**"*

*(A short conceptual essay: no data, no case study, **and no numbers at all** — which in this batch is a
virtue. The four levers come with no evidence about their relative cost or effect, and *"lower the quality
bar"* is listed neutrally among them. Nine illustrations, including the Rauch list, are images not
transcribed in the capture. **NOT INDEPENDENT** for the general framing: the author is a Director at
Google Cloud AI writing about a practice he also promotes commercially.)*

## A guide at the push boundary (Fowler / Miller, Sept 2026)

Both [[martin-fowler]] ([[fowler-fragments-2026-09-01]]) and [[jeremy-miller]]
([[miller-pondering-continuous-integration-ai-world-order]]) respond to Paul Stack's "AI Broke the
Assumptions Behind CI" and land on the same remedy from opposite premises. Fowler supplies the sentence
this page should keep:

> "CI with humans relies on them being disciplined to run commit tests locally before pushing to the CI
> server — **and that we can (and should) automate that when using agents.**"

That is a **computational guide** in this page's grid, sited at the push boundary: a pre-push gate the
agent cannot skip, replacing a human discipline that was never enforceable. It belongs in the
[[agent-harness]] rather than in team norms — and it is Osmani's **admission control** category above,
moved one boundary earlier. Miller's practice is the same control implemented by hand —
lighter local suites selected by *"what subset of tests are executing based on the changes in flight"*,
with the full **"HeavyGate"** reserved for pushes to `main` — plus a supervisor process (his "Bobcat", on
the Microsoft Testing Platform) that does *"selective test retries, process restarts, and even hard Docker
resets based on known test flakes."*

**They disagree about what is new, and the KB should hold that open.** Fowler: verifying locally before
pushing *"was always how Continuous Integration works"*, slow tests belong downstream in the deployment
pipeline, and *"Continuous Integration is a practice, not just the CI server."* Miller presents the same
move as a reversion — *"doing trunk based development like it's 2007 and Subversion is the latest
hotness!"* Two well-positioned sources, same remedy, incompatible accounts of whether anything broke.
**Neither measures anything**, and Miller's attribution of slow CI to agent load carries his own
unresolved confound (his team also added far more tests).

**One second-order effect worth recording, because it runs against the usual worry.** Miller: *"With CI
builds being so slow, that's forced us to be much more aggressive about stomping out flaky or otherwise
unreliable tests"* — because *"retrying a CI failure just in case it's just a test flake is just too damn
slow now."* When retry stops being cheap, unreliable sensors stop being tolerable. **His impression, not a
measurement.**

_Sources: [[fowler-bockeler-harness-engineering]] · [[openai-harness-engineering-codex]] · [[fowler-bockeler-maintainability-sensors]] · [[addyosmani-agentic-code-quality]] ·
[[addyosmani-human-judgment-relocates]] · [[miracle-my-loop-engineering-workflow]] ·
[[zalando-agentic-engineering-snapshot]] · [[fowler-fragments-2026-09-01]] ·
[[miller-pondering-continuous-integration-ai-world-order]]._
