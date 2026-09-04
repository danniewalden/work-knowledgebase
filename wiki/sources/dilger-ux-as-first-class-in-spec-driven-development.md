---
title: "Source: Dilger — UX as a first-class citizen in Spec-Driven Development"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-ux-as-first-class-in-spec-driven-development]
raw_file: [raw/notes/dilger-ux-as-first-class-in-spec-driven-development.md]
tags: [spec-driven-development, event-modeling, given-when-then, agentic-coding, focus]
---

# Source: Dilger — UX as a first-class citizen in Spec-Driven Development

LinkedIn post by **[[martin-dilger]]**, **2026-08-31** (~100 words — the shortest capture in this
batch). Raw capture: `raw/notes/dilger-ux-as-first-class-in-spec-driven-development.md`, retrieved
2026-09-04 in a logged-in Chrome session; post date derived from LinkedIn's relative age stamp
(accurate to the day).

> **Short-form pointing at a fuller primary the KB does not hold.** The post's substance is a link to a
> **60-minute webinar showcasing the workflow** (`lnkd.in/etKrjyYW`, unresolved at capture). **The
> webinar is the fuller primary; this note is a trailer for it.** Anything load-bearing about *how* the
> workflow works should come from the webinar, not from here.

> **VENDOR SELF-REPORT** — "our Spec-Driven Development Workflow" is [[eventmodelers-ai]] / EM-Studio,
> his own commercial platform.

## Summary

The claim, in full: UX is a **first-class citizen** of his [[event-modeling]]-based
[[spec-driven-development|SDD]] workflow, and has been *"for years - because it works. With humans and
AI."* The contrast he draws is the operative part: *"Instead of deriving the UX from markdown files
( which become unreadable and impossible to maintain from a certain size on ), we focus on the
functionality, the UX and the business rules described as Given / When / Then ( BDD Style )."* Closing
line: *"Spec-Driven Development does not need Markdown Files."*

## Key points

- **Three things carry the spec, and markdown is not one of them:** functionality, **UX**, and business
  rules — the last expressed as [[given-when-then|Given/When/Then]], which he labels BDD-style. Note
  what this implies about the division of labour: **screens carry the interaction, GWT carries the
  rules.** That is a concrete answer to "what replaces the prose", and it is narrower than "use a DSL".
- **The failure mode he attributes to markdown-derived UX is a scaling one** — markdown becomes
  *"unreadable and impossible to maintain from a certain size on"* — not a correctness one. Same
  economy-of-description shape as [[dilger-markdown-is-a-suggestion-dressed-as-a-spec]].
- **"More and more people discover the Power of UX for Spec Driven Development"** is a claim about
  ecosystem drift with **no one named and nothing cited** — a rhetorical opener, not a datapoint.
- **"We are doing this for years - because it works"** is the only evidential claim in the post, and it
  is an unsupported self-report.

## Limits

- **Assertion only.** No worked example, no screenshot, no comparison, no measurement — the entire
  demonstration is deferred to the uncaptured webinar.
- **VENDOR SELF-REPORT** (above); "our workflow" is his product's workflow.
- **The "BDD Style" label is used loosely.** GWT-for-business-rules plus screens-for-UX is not what BDD
  or [[given-when-then|specification by example]] normally means by *executable* specification, and
  [[gojko-adzic]] — who wrote *Specification by Example* — is on record in this same batch that the SDD
  tools' GWT output *"is not a spec, it lacks a ton of detail"*
  ([[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]]). Dilger's claim may be stronger than
  the toolkits' and it is not established here.
- The webinar link is an unresolved `lnkd.in` shortlink.

## Connections / contrast

- **This is the clearest short statement of the batch's second-biggest mechanism claim: UX belongs
  *in* the spec, not derived *from* it.** Its worked instance is
  [[dilger-ui-only-interactions-filtering]] (HTML Views authored in the model, the mockup readable by a
  connected agent, filtering specified as a read-side Query scenario); its podcast statement is
  Dymitruk's *"screens are not a distraction … gatekeeping by architect wannabes"*
  ([[dilger-podcast-episode-47-agentic-modeling-audit-trails]]); its tooling neighbours are
  [[dilger-highlighting-markers-give-context-to-agents]] (region-scoped markers agents read and build UI
  from) and the **Screen Preview** — hand sketches, HTML mockups and Figma in one storyline — announced
  in [[dilger-only-engineers-care-about-consistent-systems]]. Together these are enough for a
  concept-level treatment — proposed as [[screens-as-specification]] in this batch's deltas;
  individually each is thin.
- **It answers the one thing the SDD sceptics asked for and did not expect from this camp.**
  [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto's]] single stated frustration is
  that *"coding agents use text, not visuals"* and that richer visual interaction is where tooling
  should go; [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] asks who the SDD target user
  even is, given the tools import product vocabulary while assuming a lone developer author. A screen is
  the artifact a designer, a PM or an end user can react to without opening a `.specify` folder — which
  is exactly [[ng-spec-driven-development-is-waterfall-in-markdown|Ng's]] *"a contract between you and
  the LLM that nobody else signed"* objection. **Still a partial answer:** the KB holds no evidence of
  non-developers actually participating in a model that later drove agents — a named gap on
  [[event-modeled-agent-design]].
- **Against [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]]:** his complaint about invented
  UI rationale (*"users … often with gloves or in suboptimal lighting"*) is markdown-derived UX doing
  exactly what Dilger says it does. That is the sceptics' evidence supporting Dilger's diagnosis while
  rejecting his conclusion.
- **Same-week Dilger cluster:** [[dilger-communicating-intent-to-an-agent-needs-a-dsl]] (09-03),
  [[dilger-git-as-primary-persistence-for-event-models]] (09-02),
  [[dilger-only-engineers-care-about-consistent-systems]] (09-01),
  [[dilger-agentic-engineer-program-stack-agnostic-spec]] (09-03).

_Related: [[martin-dilger]] · [[spec-driven-development]] · [[given-when-then]] · [[event-modeling]] ·
[[agent-readable-model-artifacts]] · [[eventmodelers-ai]] · [[event-modeled-agent-design]]._
