---
title: Mutation Testing
type: concept
created: 2026-06-14
updated: 2026-08-14
sources: [fowler-bockeler-maintainability-sensors, bockeler-tdd-inside-the-agent-loop]
tags: [testing, harness-engineering, sensors, coding-agents]
---

# Mutation Testing

**Mutation testing** measures *test-suite effectiveness* (not just coverage) by introducing small
code mutations and checking whether the tests catch them. A mutation the suite fails to detect is a
**surviving mutant** — evidence the tests execute the code without actually *verifying* its behaviour.
Tools: Stryker (JS/TS), PIT (Java), etc.

## Why it matters in this wiki

It's the answer to a specific [[agentic-coding]] risk surfaced by [[birgitta-bockeler|Böckeler]]
([[fowler-bockeler-maintainability-sensors]]): when teams let AI generate most tests without review,
**coverage becomes a false sense of security**. Her worked example — a `mappers.ts` file at 100%
statement coverage with **no unit tests** and **13 surviving mutants** (the lines ran only via a
broad acceptance test) — makes the point that *coverage tells you a line ran, not that its impact was
verified.*

In the [[feedforward-and-feedback-controls|guides-&-sensors]] taxonomy, mutation testing is a
**computational sensor** that sits behind the [[harness-engineering|harness]]'s hardest regulation
category — **behaviour** (the [[fitness-functions|maintainability/architecture/behaviour]] ladder),
where "too much faith is placed in AI-generated tests." It monitors the gap left by the industry's
drift toward assertion-light, end-to-end/acceptance tests. Practical limit: it is **resource
intensive**, so it's run on a slower cadence rather than continuously.

## Promoted from sensor to substitute (Böckeler, 2026-08)

In [[bockeler-tdd-inside-the-agent-loop]] mutation testing does double duty. It is the **measurement**
that makes the negative TDD result credible — mutation scores showed no meaningful difference between
TDD and non-TDD runs, so the case for TDD-in-the-loop can't fall back on "but the tests are better." And
it is the **replacement** she prescribes: rather than issuing elaborate TDD instructions "and hoping for
the best," she monitors and improves regression quality with mutation testing, on the principle *"I
don't really care **how** regression quality was achieved, as long as I have a mechanism to see how good
it is."* That is the guides→sensors shift stated as a budget decision, with mutation testing as the
concrete beneficiary — and it pairs naturally with an externally authored [[given-when-then]] gate,
which checks *what* was built while mutation score checks *whether the checks work*.

## Related

[[fowler-bockeler-maintainability-sensors]] · [[feedforward-and-feedback-controls]] · [[harness-engineering]] ·
[[fitness-functions]] · [[agentic-coding]] · [[birgitta-bockeler]] · [[loop-engineering]] ·
[[given-when-then]]

_Sources: [[fowler-bockeler-maintainability-sensors]] · [[bockeler-tdd-inside-the-agent-loop]]._
