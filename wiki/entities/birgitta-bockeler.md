---
title: Birgitta Böckeler
type: entity
created: 2026-06-11
updated: 2026-09-04
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors, bockeler-context-engineering-coding-agents, bockeler-tdd-inside-the-agent-loop, bockeler-understanding-sdd-kiro-speckit-tessl, ng-spec-driven-development-is-waterfall-in-markdown]
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

## She originated the KB's SDD vocabulary (2025-10-15, ingested 2026-09-04)

**[[bockeler-understanding-sdd-kiro-speckit-tessl]]** — *"Understanding Spec-Driven-Development: Kiro,
spec-kit, and Tessl"*, martinfowler.com "Exploring Gen AI", **2025-10-15** — is now a source page,
resolving a flag that stood from 2026-08-16.

**Attribution correction, twice over.** [[ng-spec-driven-development-is-waterfall-in-markdown]] cites it
as *"the Fowler/Böckeler analysis"* and this wiki repeated that. **She is the sole author**, published on
[[martin-fowler]]'s site; any page saying "Fowler/Böckeler" on this piece is wrong and should read
Böckeler.

**It is the source of the spec-first / spec-anchored / spec-as-source ladder** the wiki uses as working
vocabulary, mostly without attribution — and it **predates every other primary in the critique cluster**:
[[francois-zaninotto|Zaninotto]] and [[colin-eberhardt|Eberhardt]] both cite her,
[[adam-tornhill|Tornhill]] uses her distinction to scope his own critique, and
[[ng-spec-driven-development-is-waterfall-in-markdown|Ng]] is five months downstream. (Only
[[gojko-adzic|Adzic]], 2025-09-29, is earlier.) So it heads an Oct–Nov 2025 wave rather than sitting
inside Ng's 2026-03 summary.

**Its MDD parallel is the strongest external input [[model-as-code-vs-model-as-language]] has received,
and it cuts both ways:** model-driven development *"never took off for business applications, it sits at
an awkward abstraction level"*, **but** *"the parseable structure also had upsides that we're losing now:
We could provide the spec author with a lot of tool support to write valid, complete and consistent
specs"* — so spec-as-source risks *"the downsides of both MDD and LLMs: Inflexibility and
non-determinism."* Simultaneously the strongest historical prior for the model-as-language position and
the sharpest warning against it.

The Kiro finding the KB previously held only through Ng is now first-party: for a *minor bug fix* Kiro
generated **four user stories with sixteen acceptance criteria** — "using a sledgehammer to crack a nut"
— and agents ignored portions of the spec and emitted duplicate code despite explicit instructions.
That count is an **artifact count, not an outcome**. Her *"in the same time it took me to run and review
spec-kit I could have implemented the feature"* is an **IMPRESSION NOT MEASUREMENT** and **NOT
INDEPENDENT** (see below).

**Two markers, and they matter for how she is cited.** **NOT INDEPENDENT** — martinfowler.com is
[[thoughtworks]]' own publishing channel and she is a Thoughtworks Distinguished Engineer; she is a
*primary* for her own trials, and **never external corroboration for a Thoughtworks-originated framing**
(harness engineering above all, which she named). And **she is pro-spec-first herself** — *"the general
principle of spec-first is definitely valuable in many situations"* — so **filing her as an SDD opponent
is wrong.**

**Through-line across her four captured pieces:** an agent following instructions is not the same as the
instructions being right.

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]] ·
[[bockeler-context-engineering-coding-agents]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[bockeler-understanding-sdd-kiro-speckit-tessl]] (2025-10-15, **sole author**) ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] (secondhand reference — unreliable on the
attribution)._
