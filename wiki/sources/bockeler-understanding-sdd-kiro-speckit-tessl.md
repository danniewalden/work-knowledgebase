---
title: "Source: Böckeler — Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [bockeler-understanding-sdd-kiro-speckit-tessl]
raw_file: [raw/articles/bockeler-understanding-sdd-kiro-speckit-tessl.md]
tags: [spec-driven-development, agentic-coding, model-as-code-vs-model-as-language, controversy, focus]
---

# Source: Böckeler — Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl

Article by **[[birgitta-bockeler]]** (Distinguished Engineer, [[thoughtworks]]) in the *Exploring Gen
AI* series on **martinfowler.com**, **2025-10-15**. Hands-on comparison of three self-labelled SDD
tools — **AWS Kiro**, **GitHub spec-kit**, **Tessl Framework** (then private beta). Raw capture:
`raw/articles/bockeler-understanding-sdd-kiro-speckit-tessl.md`.

> **NOT INDEPENDENT.** martinfowler.com is [[thoughtworks]]' own publishing channel and Böckeler is a
> Thoughtworks Distinguished Engineer. She is a *primary* here — this is her own hands-on trial — but
> she is **not** independent corroboration for any Thoughtworks-originated framing (harness
> engineering, the Radar's SDD placement, [[martin-fowler]]'s editorial line). The marker travels with
> every claim taken from this page.

## Summary

**This is where the KB's working vocabulary for SDD comes from.** Böckeler's central contribution is a
**three-level ladder** distinguishing what SDD tools actually aspire to, and it predates every other
primary in the critique cluster:

- **Spec-first** — a well-thought-out spec is written first and used for the task at hand.
- **Spec-anchored** — the spec is *kept* after the task, and used for evolution and maintenance.
- **Spec-as-source** — the spec is the main source file; only the spec is edited, the human never
  touches the code.

*"All SDD approaches and definitions I've found are spec-first, but not all strive to be spec-anchored
or spec-as-source. And often it's left vague or totally open what the spec maintenance strategy over
time is meant to be."* Her own working definition of a spec: *"a structured, behavior-oriented artifact
— or a set of related artifacts — written in natural language that expresses software functionality and
serves as guidance to AI coding agents."* She also separates **specs** (task-scoped) from the
**memory bank** (rules/context files relevant across all sessions) — Kiro calls it "steering",
spec-kit calls it a "constitution".

## Key points

- **Tool shapes differ far more than the label suggests.** Kiro: Requirements → Design → Tasks, three
  markdown docs in a VS Code fork, spec-first only. Spec-kit: Constitution → ⟳ Specify → Plan → Tasks,
  a CLI that instantiates many files plus AI-interpreted checklists ("a 'definition of done' for each
  workflow step … interpreted by AI, so there is no 100% guarantee"); it branches per spec, which she
  reads as spec-*first*, not spec-anchored, despite GitHub's living-artifact rhetoric. Tessl: the only
  one aspiring to **spec-as-source**, with generated files marked `// GENERATED FROM SPEC - DO NOT
  EDIT` at a 1:1 spec-to-file mapping.
- **"A sledgehammer to crack a nut."** Asked to fix a small bug, Kiro's requirements document turned it
  into **4 "user stories" with 16 acceptance criteria** — verified verbatim against this primary. Her
  spec-kit trial was a 3–5-point-story-sized feature, and *"in the same time it took me to run and
  review the spec-kit results I could have implemented the feature with 'plain' AI-assisted coding, and
  I would have felt much more in control."*
- **"I'd rather review code than all these markdown files."** The generated markdown was repetitive,
  duplicated existing code, verbose and tedious; *"an effective SDD tool would have to provide a very
  good spec review experience."*
- **False sense of control.** *"Even with all of these files and templates and prompts and workflows
  and checklists, I frequently saw the agent ultimately not follow all the instructions."* Both
  failure directions occurred: spec-kit's research step described existing classes, the agent read the
  descriptions as new specification and **regenerated them as duplicates**; elsewhere it went
  overboard by following a constitution article too eagerly. Bigger context windows do not fix this.
- **The MDD parallel — load-bearing and new to the KB from any source.** She worked on
  model-driven-development projects early in her career and Tessl reminded her of them: MDD models
  *were* specs, in UML or a textual DSL, fed to hand-built code generators. *"Ultimately, MDD never
  took off for business applications, it sits at an awkward abstraction level and just creates too much
  overhead and constraints."* LLMs remove MDD's parseable-language constraint and the need for
  generators — but *"the parseable structure also had upsides that we're losing now: We could provide
  the spec author with a lot of tool support to write valid, complete and consistent specs. I wonder if
  spec-as-source, and even spec-anchoring, might end up with the downsides of both MDD and LLMs:
  Inflexibility and non-determinism."*
- **Iterating a Tessl spec to make codegen repeatable** *"reminded me of some of the pitfalls and
  challenges of writing an unambiguous and complete specification"* — non-determinism showed up even at
  the one-file abstraction level.
- **Two open questions she poses and does not answer.** *Functional vs technical separation*: she was
  repeatedly unsure when to add technical detail, and "we don't have a good track record as a
  profession to do this well." *Who is the target user*: the tools import product vocabulary ("user
  story", feature goals) while presenting a developer as the sole author, with no cross-skilling or
  pairing model made explicit.
- **She is pro-spec-first herself.** *"In my personal usage of AI-assisted coding, I also often spend
  time on carefully crafting some form of spec first … So the general principle of spec-first is
  definitely valuable in many situations."* Her closing worry is *Verschlimmbesserung* — "are we making
  something worse in the attempt of making it better?" — aimed at the elaborate, many-file tools, not
  at specification.

## Limits

- **NOT INDEPENDENT** (above). Also: her own evaluation caveat is unusually explicit — *"It turns out
  to be quite time-consuming to evaluate SDD tools … in a way that gets close to real usage"*, she used
  the tools in September 2025 and notes they may already have changed, Tessl was in private beta, and
  *"until I hear usage reports from people using them for a period of time on a 'real' codebase, I
  still have a lot of open questions."*
- **No measurements at all.** "In the same time it took me" is an impression, not a timing; the 4-story
  / 16-criteria count is the only number in the piece and it is an artifact count, not an outcome.
- Kiro's design-document structure is from a single retained attempt; she flags she cannot say whether
  it is consistent.
- Four images in the original (Kiro design sections, spec-kit file topology, a reverse-engineered Tessl
  spec) are noted inline in the raw, not reproduced — so the file-topology claims are described, not
  shown.

## Connections / contrast

- **Provenance repair.** The KB's [[spec-driven-development]] page has carried this as "the
  Fowler/Böckeler Kiro analysis" reached second-hand through Ng. It is **Böckeler's sole authorship,
  published on Fowler's site**, and it is the *origin* of the spec-first/anchored/as-source taxonomy
  the KB already uses. Zaninotto and Eberhardt both cite it by name; Tornhill cites it for the
  weak-vs-strong SDD distinction he then argues against. Ng (2026-03) is five months downstream.
- **The MDD paragraph is the strongest external input [[model-as-code-vs-model-as-language]] has ever
  received**, and it cuts across both camps rather than joining one. Against
  [[martin-dilger|Dilger's]] model-as-language pole it is the historical-failure argument; *for* it,
  the observation that a **parseable structure buys tool support for validity and completeness** is
  precisely the property Dilger's structural-diff rubric exploits
  ([[dilger-one-million-tokens-self-training-modeling-agent]]). Read carefully, she says natural-language
  SDD may have thrown away the one thing MDD got right.
- **Her verdict on spec-kit's branching** (spec-per-change-request, not spec-per-feature) is the
  concrete mechanism behind the KB's open "what is the spec maintenance strategy" question, and it
  bears on [[dilger-spec-driven-development-needs-four-phases|Dilger's phase 4]] — operations and
  maintenance, still a hole in this KB.
- **Same author, adjacent findings:** [[bockeler-tdd-inside-the-agent-loop]] (agent-authored tests
  inside the loop buy no quality at 3–8.5× the tokens) and
  [[bockeler-context-engineering-coding-agents]]. The through-line across all three is *the agent
  following instructions is not the same as the instructions being right*.
- Sceptic cluster: [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] ·
  [[zaninotto-spec-driven-development-waterfall-strikes-back]] ·
  [[eberhardt-putting-spec-kit-through-its-paces]] ·
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]].

_Related: [[birgitta-bockeler]] · [[thoughtworks]] · [[spec-driven-development]] ·
[[model-as-code-vs-model-as-language]] · [[agentic-coding]] · [[context-engineering]]._
