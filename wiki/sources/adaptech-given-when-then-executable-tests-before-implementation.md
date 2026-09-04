---
title: "Adaptech — Given/When/Then scenarios become executable tests before implementation begins"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [adaptech-given-when-then-executable-tests-before-implementation]
raw_file: [raw/notes/adaptech-given-when-then-executable-tests-before-implementation.md]
tags: [event-modeling, given-when-then, slice, testing, focus]
---

# Adaptech — GWT scenarios become executable tests before implementation begins

LinkedIn post by **[[adaptech-group]]** (2026-08-28), reposted by [[adam-dymitruk]]. Raw capture:
`raw/notes/adaptech-given-when-then-executable-tests-before-implementation.md`.

**The method's own consultancy stating the GWT→test pipeline plainly** — which the KB had only from
tool vendors and practitioners, never from Adaptech itself.

## What it says

> "Given/When/Then scenarios define the starting state, the action being taken, and the expected result.
> **These become executable tests before implementation begins.** The developer starts with failing tests
> and builds the slice until those tests pass."

The stated payoff is agreement plus a completion test: *"a clear agreement about what the software is
supposed to do and an objective way to know when the work is finished… fewer surprises late in
development and less debate about whether a feature actually meets the requirement."*

Opening framing is worth keeping: *"How much ambiguity is still left when a developer starts building a
feature?"* — the value proposition stated as ambiguity reduction rather than as testing.

## Why it matters here

- It is **first-party confirmation** of the slice→GWT→failing-test→implement loop that
  [[jwilger-agent-skills-event-modeling]] automates and [[dilger-event-modeling-agent-harness]] runs
  24/7. Those are downstream implementations; this is the method's originators saying it is the intent.
- "Builds **the slice** until those tests pass" makes the [[slice]] the unit of the test loop
  explicitly, not by inference.
- It is effectively **TDD with the tests derived from a model rather than written by the implementer** —
  which is the distinction that matters against [[bockeler-tdd-inside-the-agent-loop]]'s finding that TDD
  *inside* the agent loop buys no quality: there, the agent writes and confirms its own test; here the
  test predates the implementer entirely. Whether that difference survives contact with evidence is
  untested, but it is the right place to look. See [[given-when-then]].

## The loose thread

The capture note records that Mohsen B. (Adaptech) reposted this on 2026-08-29 with one comment —
**"This is why Scenario Hunting works."** That term appears nowhere else in this KB or in any captured
source. It is used as if it were established Adaptech vocabulary. Too thin to write from; flagged for a
targeted search.

## Caveats

- Marketing copy from the consultancy that sells the method; no evidence, no worked example.
- Short, and it asserts the benefit rather than demonstrating it.

## Related

[[given-when-then]] · [[slice]] · [[event-modeling]] · [[adaptech-group]] · [[adam-dymitruk]] ·
[[jwilger-agent-skills-event-modeling]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[event-modeled-agent-design]]
