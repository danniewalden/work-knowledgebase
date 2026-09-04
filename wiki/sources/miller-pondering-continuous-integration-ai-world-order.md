---
title: "Source: Miller — Pondering Continuous Integration in our new AI World Order"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [miller-pondering-continuous-integration-ai-world-order]
raw_file: [raw/articles/miller-pondering-continuous-integration-ai-world-order.md]
tags: [agentic-coding, feedforward-and-feedback-controls, ci-cd, critter-stack, focus]
---

# Source: Miller — Pondering Continuous Integration in our new AI World Order

Post by **[[jeremy-miller]]**, 2026-08-31. Raw capture:
`raw/articles/miller-pondering-continuous-integration-ai-world-order.md`. Written in response to Paul
Stack's "AI Broke the Assumptions Behind CI." The most substantive of the four Miller captures in this
batch, and the least product-shaped — though he is describing his own OSS project's practice, so it is
still a practitioner self-report about his own tooling.

## Summary

Miller's claim: CI's *purpose* is unchanged — *"constantly getting feedback on your code by building and
running tests against it as you change code"* — but its **economics have broken**, because agent-driven
development pushes far more work through shared CI infrastructure than that infrastructure was sized for.
His response is to move verification back onto the developer's machine and treat the remote CI run as a
gate on pushes to `main` rather than an inner-loop feedback mechanism.

## Key points

- **The stated cause is contention, not concept.** *"With the extreme load that's come from all of us
  yahoos using AI agents to code so much faster, GitHub Actions are very noticeably slower or flat out
  unreliable on the worst days. And of course, to make things worse, we've added a lot more tests and CI
  actions than we ever tried to do before."* Two compounding effects — more consumers of shared runners,
  and more tests per project — with the [[critter-stack]]'s database/broker integration tests making it
  worse for him specifically.
- **The adaptation, in his words:** *"Doing trunk based development like it's 2007 and Subversion is the
  latest hotness!"* — strictly local testing with a lighter suite for commits, *"trying to be very
  selective of what subset of tests are executing based on the changes in flight,"* and the full
  **"HeavyGate"** suite only on pushes to remote `main`. For public projects that need PRs for
  traceability, *"we're going to have to get more creative about test run filtering to avoid running test
  suites that aren't relevant to the changes in flight."*
- **A second-order effect worth keeping: slow CI forced flake elimination.** *"With CI builds being so
  slow, that's forced us to be much more aggressive about stomping out flaky or otherwise unreliable
  tests"* — because *"retrying a CI failure just in case it's just a test flake is just too damn slow
  now."* When retry stops being cheap, unreliability stops being tolerable. That is a real mechanism, and
  it runs opposite to the usual worry that agent-era volume degrades test suites.
- **He built a harness component for it.** A newly added *"critter"* named **"Bobcat"** — he notes the
  project itself predates the Critter Stack naming scheme, so it is new to this role rather than new
  code — uses the **Microsoft Testing Platform** to *"supervise test runs and selectively do test retries, process restarts, and even hard
  Docker resets based on known test flakes"* — helping both locally, *"where heavy development can break
  down when Docker containers have run too long in tests,"* and in CI. This is a **supervisor for the
  verification environment**, and it is the same shape as the AVO supervisor in
  [[fowler-fragments-2026-09-01]] (watch the run, intervene when it degrades) applied to test
  infrastructure rather than to an agent's search.
- **He explicitly disagrees with Stack's framing of CI** as something *"tied to the pull request workflow
  in GitHub et al"* — CI predates and is not equal to the PR, which is the same correction
  [[martin-fowler]] makes at greater length in [[fowler-fragments-2026-09-01]]. Miller keeps PRs *"in no
  small part just for traceability"* rather than for review, because GitHub release notes are generated
  from them.
- Closing note, characteristically unenthusiastic: *"AI assisted development continues to take up more of
  my gray matter than I wished it did and I don't think the adaptation is going to change any time soon."*

## Limits

- **A single maintainer's account of one OSS project's practice.** No measurements: no CI wait times, no
  before/after durations, no flake rates, no volume figures. "Very noticeably slower or flat out
  unreliable on the worst days" is an **IMPRESSION NOT MEASUREMENT** and must not become a figure.
- **The attribution to agent load is asserted, not shown.** GitHub Actions capacity, pricing and
  scheduling changes are equally consistent with what he observes; he offers no evidence isolating agent
  demand as the cause. He also concedes his own project is *"especially problematic in this regard."*
- **His own confound:** he says in the same paragraph that they *added* many more tests and CI actions
  than before. Some of the slowdown is his suite, not the shared runners.
- Bobcat's efficacy is *"hugely helpful"* — his judgement, unquantified, on his own tool.

## Connections / contrast

- **Read against [[fowler-fragments-2026-09-01]], which responds to the same Stack post and disagrees
  about what is new.** Fowler's position: verifying locally before pushing *"was always how Continuous
  Integration works"* — pull, build and test locally, then push; slow tests belong further down the
  [[fitness-functions|deployment pipeline]], not in the commit loop; and *"Continuous Integration is a
  practice, not just the CI server."* So Fowler says the practice already prescribed Miller's answer,
  while Miller presents it as a reversion ("like it's 2007"). **Both agree the fix is to push verification
  earlier; they disagree on whether anything about CI actually broke.** This is the batch's cleanest
  disagreement between two well-positioned sources, and the KB should hold it open rather than resolve it.
- Fowler adds the piece both Miller and Stack leave implicit, and it is the part that matters for this KB:
  *"CI with humans relies on them being disciplined to run commit tests locally before pushing — and we
  can (and should) automate that when using agents."* That is a [[feedforward-and-feedback-controls]]
  guide, and the natural home for it is the [[agent-harness]] (a pre-push hook the agent cannot skip),
  not team discipline.
- **Selective test execution based on changes in flight** is a [[locality-of-reference]] argument applied
  to verification, and it is the same economic logic Miller uses for code layout in
  [[miller-codebase-is-the-prompt-vertical-slices-ai]] — the agent (or the runner) should pay only for what
  the change touches.
- Compare [[zalando-agentic-engineering-snapshot]]'s answer to the same pressure — LLM PR-risk scoring
  with auto-approval for low-risk changes — which optimizes the *merge* side while Miller optimizes the
  *verify* side. Also relevant to [[laycock-maybe-we-shouldnt-be-reviewing-all-this-code]] and
  [[unattended-coding-agents]]: if agent volume is what breaks shared verification, the ceiling on
  unattended throughput may be CI capacity rather than agent capability.
- Contrast with [[miller-ai-assisted-production-support-with-critterwatch]] (published the next day):
  the tooling he sells for the agent era, and the tooling he uses buckling under it.

## Related

[[agentic-coding]] · [[feedforward-and-feedback-controls]] · [[jeremy-miller]] · [[critter-stack]] ·
[[fowler-fragments-2026-09-01]] · [[martin-fowler]] · [[locality-of-reference]] ·
[[unattended-coding-agents]] · [[zalando-agentic-engineering-snapshot]] · [[harness-engineering]] ·
[[software-factory]]
