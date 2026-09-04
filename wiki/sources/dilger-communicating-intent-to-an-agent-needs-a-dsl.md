---
title: "Source: Dilger — Communicating intent to an agent needs a DSL, not raw markdown"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-communicating-intent-to-an-agent-needs-a-dsl]
raw_file: [raw/notes/dilger-communicating-intent-to-an-agent-needs-a-dsl.md]
tags: [spec-driven-development, model-as-code-vs-model-as-language, event-modeling, controversy, focus]
---

# Source: Dilger — Communicating intent to an agent needs a DSL, not raw markdown

LinkedIn post by **[[martin-dilger]]**, **2026-09-03** (~200 words). Raw capture:
`raw/notes/dilger-communicating-intent-to-an-agent-needs-a-dsl.md`, retrieved 2026-09-04 in a
logged-in Chrome session; the post date is derived from LinkedIn's relative age stamp, so it is
accurate to the day, not the hour.

**Short-form, and it restates a longer argument.** The fuller primary for the same position is
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec]] (2026-08-25), which carries the
economy-of-description test and the "code is a formal language" concession. What is **new here** is the
positive half: a name for what is missing (**a DSL**), a list of properties it must have, and an
explicit indifference to file format.

## Summary

Four moves. (1) The industry has settled on **raw markdown** as the medium for communicating intent to
an agent, and he is *"not a fan … suboptimal for anything beyond a project kickoff."* (2) Requirements
must be **specific, unambiguous, information complete, structured** — and *"just writing some markdown
files doesn't solve any of the problems we faced in the past."* (3) The diagnosis, and the batch's most
quotable line: *"What used to be a Jira Ticket became Markdown Files. Same old stuff, some new paint."*
(4) The prescription: *"What's missing is a DSL to unambiguously describe flow, behavior + business
rules."*

## Key points

- **The medium is explicitly not the point.** *"The medium itself - nobody cares in the end ( you can
  export Json, Markdown, Toon.. from my tools )."* This is a sharpening, not a repetition: his
  objection is to markdown as a **language**, not as a file format — and he says so while noting his own
  tools export markdown. Anyone reading him as anti-markdown-file is reading him wrong.
- **Event Modeling *is* the DSL, and it has a documented interchange.** *"There are several attempts to
  standardize how to describe behavior. For me, Eventmodeling is that DSL … I documented the standard
  Json-Format in 2024 and all my workflows use it internally."* The 2024 JSON format is referenced via
  an `lnkd.in` shortlink and is **not captured in `raw/`** — the format itself is therefore an
  uncaptured primary this claim rests on.
- **"Battle-tested over hundreds of projects by many companies" — VENDOR SELF-REPORT and his own
  figure.** No projects are named, no companies, no methodology, and he sells the platform and training
  the claim underwrites ([[eventmodelers-ai]], [[nebulit]]). **The KB has no independent corroboration
  for it from any source.** The marker travels with the claim onto every page.
- The post ends by asking readers *"How do you structure your Agent Instructions?"* — it is a discussion
  prompt, not an argued case.

## Limits

- **Short-form assertion.** No worked example, no comparison against a markdown baseline, no
  measurement. The four required properties (specific / unambiguous / information complete /
  structured) are stated, not defended, and nothing here shows Event Modeling satisfies them better than
  the alternatives it dismisses.
- **VENDOR SELF-REPORT** throughout (above), including the only quantified claim in the post.
- The one external artifact it points at (the 2024 JSON format) is unresolved from this capture.
- **"Several attempts to standardize"** are alluded to and none is named — including
  [[esdm-event-sourced-domain-modeling|ESDM]], which his own platform now exports to
  ([[dilger-eventmodelers-supports-esdm-export]]).

## Connections / contrast

- **This is the Dilger side of [[model-as-code-vs-model-as-language]] stated as a *requirement on the
  medium*** rather than as a critique of prose — and it names the thing the KB's page had to infer:
  a **DSL for flow, behaviour and business rules**. It should be read alongside
  [[jeremy-miller]]'s counterposition
  ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]), which rejects exactly this —
  *"intermediate DSL approaches … using YAML, XML, or custom built textual DSLs"* — and
  [[nick-tune-enforced-application-architecture-agents-humans|Tune's model-as-constraint]] third
  position, whose DSL describes permitted *structure* rather than behaviour.
- **"Same old stuff, some new paint" is the same observation the sceptics make, with the opposite
  conclusion.** [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto's]] *Faux Agile*
  and [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler's]] *"I've even recently heard people use
  'spec' basically as a synonym for 'detailed prompt'"* are the same finding; Dilger infers **a better
  language is needed**, they infer **less document is needed**. Presenting them as allies would be a
  category error.
- **[[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler's MDD paragraph is the strongest available
  reply]]:** a parseable spec language buys tool support for validity and completeness (which is
  Dilger's whole point) *and* historically failed on abstraction level and overhead (which is his
  problem). She frames the risk as inheriting *"the downsides of both MDD and LLMs: Inflexibility and
  non-determinism."* [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] makes the
  same argument from lived MDA experience.
- **The structural-diff evidence is what actually supports this post**, and it is not in it: a schema'd
  model can be graded against known-good models
  ([[dilger-one-million-tokens-self-training-modeling-agent]]), which markdown cannot. Cite that, not
  this, when the claim needs support.
- **Same-week cluster, and the position it sharpens:**
  [[dilger-only-engineers-care-about-consistent-systems]] (2026-09-01, *"Engineers talking to AI,
  writing tons of markdown.. one more handover"*), [[dilger-ux-as-first-class-in-spec-driven-development]]
  (2026-08-31, *"Spec-Driven Development does not need Markdown Files"*),
  [[dilger-git-as-primary-persistence-for-event-models]] (2026-09-02) and
  [[dilger-agentic-engineer-program-stack-agnostic-spec]] (2026-09-03). Read as one week's argument:
  **the medium is wrong, the handovers are the reason, the model is the replacement, and here is where
  it is stored.**

_Related: [[martin-dilger]] · [[model-as-code-vs-model-as-language]] · [[spec-driven-development]] ·
[[event-modeling]] · [[agent-readable-model-artifacts]] · [[em-standardization-foundation]] ·
[[eventmodelers-ai]] · [[context-engineering]]._
