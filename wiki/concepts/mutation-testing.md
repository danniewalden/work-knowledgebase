---
title: Mutation Testing
type: concept
created: 2026-06-14
updated: 2026-06-14
sources: [fowler-bockeler-maintainability-sensors]
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

## Related

[[fowler-bockeler-maintainability-sensors]] · [[feedforward-and-feedback-controls]] · [[harness-engineering]] ·
[[fitness-functions]] · [[agentic-coding]] · [[birgitta-bockeler]]

_Source: [[fowler-bockeler-maintainability-sensors]]._
