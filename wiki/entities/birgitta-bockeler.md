---
title: Birgitta Böckeler
type: entity
created: 2026-06-11
updated: 2026-08-16
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, bockeler-context-engineering-coding-agents, bockeler-tdd-inside-the-agent-loop, ng-spec-driven-development-is-waterfall-in-markdown]
tags: [person, thoughtworks, harness-engineering, generative-ai]
---

# Birgitta Böckeler

Distinguished Engineer and AI-assisted delivery expert at [[thoughtworks]], with 20+ years as a
developer, architect, and technical leader. Author of the KB's anchor [[harness-engineering]]
article ([[fowler-bockeler-harness-engineering]], 2026-04-02, published on [[martin-fowler]]'s
site), which supersedes her February 2026 memo.

Her contributions: the **guides (feedforward) vs. sensors (feedback)** and **computational vs.
inferential** taxonomy ([[feedforward-and-feedback-controls]]); the harness as a cybernetic
**governor**; the **steering loop**; three **regulation categories** (maintainability /
architecture fitness / behaviour); and **harnessability** / "ambient affordances." She frames a
coding-agent user harness as a specific form of [[context-engineering]] — a lineage she set up in the
**predecessor memo** [[bockeler-context-engineering-coding-agents]] (2026-02-05), the KB's taxonomy
primary for [[context-engineering]] (instructions vs guidance; context interfaces; the if/when and
how-much axes; the "illusion of control" caveat).

She then put the model into practice in **Maintainability Sensors for Coding Agents**
([[fowler-bockeler-maintainability-sensors]], May 2026) — a field report rebuilding an app with
agents using *sensors only, almost no guides*. Findings: computational sensors (ESLint,
`dependency-cruiser`) shine at the file/function level, especially with **custom lint messages as
self-correction guidance** and **threshold-raising** instead of binary suppression; raw coupling data
is too noisy for AI alone; an **inferential AI modularity review** ("garbage collection") was the most
valuable; and **[[mutation-testing]]** is crucial once you leave testing to AI (coverage ≠
effectiveness).

She then ran the KB's first captured **negative eval** from her side of the field:
**[[bockeler-tdd-inside-the-agent-loop|TDD inside the agent loop — theater or actual value?]]**
(2026-08-10). Instructing an agent to do TDD *within its own loop* produced no quality gain (blind-ranked
non-TDD solutions often scored higher), no mutation-score gain, and 3–8.5× the tokens; the hypothesised
cause is that TDD instructions suppress the **up-front design** step the non-TDD runs performed. Her
sharpest point is a [[feedforward-and-feedback-controls|maker≠checker]] observation: when the agent both
writes the test and confirms it failed, "a red test tells you the agent ran it and saw failure, not that
the failure was for the right reason." The generalised lesson — stop specifying *how* the model works,
monitor **outcomes**, and be deliberate about "where we insert ourselves as arbiters" — is the same
guides-vs-sensors trade-off she named, now with evidence pushing budget toward sensors.

## Referenced but not captured: the Kiro / SDD analysis

[[ng-spec-driven-development-is-waterfall-in-markdown]] cites a **"Fowler/Bockeler analysis" of AWS Kiro**
that the KB does not hold: for a *minor bug fix* Kiro generated four user stories with sixteen acceptance
criteria — "using a sledgehammer to crack a nut" — and the agents ignored portions of the spec and emitted
duplicate code despite explicit instructions. If accurate, this is a fourth Böckeler-line negative eval,
and it sits directly on the [[spec-driven-development]] thread rather than the harness one.

**CAPTURED 2026-08-31**, resolving a flag that had stood since 2026-08-16. It is
`raw/articles/bockeler-understanding-sdd-kiro-speckit-tessl.md` — *"Understanding Spec-Driven-Development:
Kiro, spec-kit, and Tessl"*, martinfowler.com "Exploring Gen AI", **2025-10-15**. The guessed venue was
right; the attribution was not — **she is the sole author**, so Ng's "the Fowler/Böckeler analysis," and
the KB's repetition of it, is wrong and should read Böckeler.

Three things this changes. It is the **earliest** of the four SDD critiques and the one the other two
cite, so it heads an Oct–Nov 2025 wave rather than sitting inside Ng's 2026-03 summary. It is **the origin
of the spec-first / spec-anchored / spec-as-source taxonomy** the KB already uses as working vocabulary
without attributing it. And it carries an argument nothing else in the KB holds — the **MDD parallel**:
spec-as-source risks inheriting "the downsides of both MDD and LLMs: inflexibility and non-determinism,"
and MDD's *parseable* structure at least bought tool support for writing valid, complete, consistent
specs, which natural-language specs give up. That lands directly on
[[model-as-code-vs-model-as-language]], and is simultaneously the strongest historical prior for the
model-as-language position and the sharpest warning against it. Awaiting ingest.

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[bockeler-context-engineering-coding-agents]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] (secondhand reference)._
