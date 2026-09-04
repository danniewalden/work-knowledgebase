---
title: "Source: Dilger — The Agentic Engineer programme, and the stack-agnostic spec claim"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-agentic-engineer-program-stack-agnostic-spec]
raw_file: [raw/notes/dilger-agentic-engineer-program-stack-agnostic-spec.md]
tags: [spec-driven-development, event-modeling, event-sourcing, vertical-slices, focus]
---

# Source: Dilger — The Agentic Engineer programme, and the stack-agnostic spec claim

LinkedIn post by **[[martin-dilger]]**, **2026-09-03** (~330 words). Raw capture:
`raw/notes/dilger-agentic-engineer-program-stack-agnostic-spec.md`, retrieved 2026-09-04 in a logged-in
Chrome session; post date derived from LinkedIn's relative age stamp (accurate to the day).

> **VENDOR SELF-REPORT and a sales post, start to finish.** It sells a **priced 3-week programme** (a
> sold-out September cohort, an October cohort with a €160 discount code, and an in-house corporate
> version), bundles a **12-month EM-Studio licence** (commercial use; on-prem hostable for enterprises),
> and includes his books *Understanding Eventsourcing* and early access to **_Spec Driven_, dated
> 2026-10-16**. Nothing in it is a result. Its value to the KB is (a) one substantive method claim and
> (b) a set of dated facts about the ecosystem.

**Short-form, and it restates a curriculum sold in fuller form elsewhere** —
[[dilger-goto-cph-2026-event-modeling-ai-native-software-design]] is the same body of work as a two-day
GOTO Copenhagen masterclass, and [[dilger-ui-only-interactions-filtering]] closes by advertising this
same programme.

## Summary

A 3-week programme teaching *"step by step how to build an agentic Spec-Driven Development Pipeline"*,
with participants having **implemented slices by the end of week 1**, *"fully specified using Event
Modeling … built with Event Sourcing and Vertical Slices"* — the [[dilger-triplet-flexible-agent-enabled-architecture|Triplet]]
as curriculum. The one claim worth extracting is about **stack independence**.

## Key points

- **The stack-agnostic spec claim, which is the substantive content.** *"The Implementation-Stack itself
  almost doesn't matter. Participants can pick one of the many Build Kits available - #axon, #marten,
  #cratis, #emmet (node), #python ( or simply build one for their own stack of choice ). Fully taking
  advantage of the 'Spec' in Spec-Driven-Development - they can even switch stacks mid-course or build
  in parallel in all Stacks."*
  This is a **falsifiable, high-value claim**: if one event model drives builds in five runtimes in
  parallel, the model is genuinely a specification of behaviour rather than a description of an
  implementation. It is also **exactly the aspiration
  [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] identifies and doubts** — *"ultimately, we
  could have AI fill in all the solutioning and details, and switch to different tech stacks with the
  same spec"* — and her finding is that separating functional from technical spec in practice is
  something *"we don't have a good track record as a profession"* at. **Nothing here demonstrates it**;
  it is an offer to course participants.
- **Build Kits as the mechanism.** Named: Axon, Marten, Cratis, Emmett (Node), Python. This is the KB's
  most explicit statement of build-kit coverage; compare [[dilger-build-kits-model-to-generated-code]]
  and [[axoniq]]'s DCB Build Kit ([[dilger-how-does-dcb-affect-event-modeling]]).
- **"Participants will model every single day ( thus getting into the habit of Software Modeling )"** —
  the programme's theory of change is **habit**, not technique.
- **Boards are private-per-participant but visible to all, deliberately** — *"Multiplying the
  learning-effect - see how others model and even start to model together."* A pedagogical claim about
  the model as a **shared, readable artifact** — the same legibility property the agent-facing argument
  rests on.
- **Dated ecosystem facts worth keeping:** *Spec Driven* releases **2026-10-16**; the September cohort
  was sold out by 2026-09-03; EM-Studio has an enterprise on-prem option. The sold-out-September signal
  is also one of the dating clues for the undated
  [[dilger-podcast-episode-47-agentic-modeling-audit-trails|Episode 47]] capture.
- *"It includes everything I learned in the last 5 years"* dates his Event Modeling practice to ~2021,
  consistent with the *"7 Insights I Learned Building Event Models Since 2021"* article referenced in
  [[dilger-ui-only-interactions-filtering]].

## Limits

- **Marketing. No outcomes, no cohort results, no participant reports, no comparison.** The KB should
  cite this only for the stack-agnostic *claim* and the dated facts, never as evidence that the pipeline
  works.
- **The stack-agnostic claim is hedged twice by its own author** — *"almost doesn't matter"* — and is
  offered as a course affordance, not a demonstrated property.
- **"Slices implemented by end of week 1"** is a curriculum promise.
- Registration links are in the comments, uncaptured; the discount code and prices are time-bound.

## Connections / contrast

- **It is the price tag on the [[spec-driven-development]] thesis.** The KB's Dilger material is heavy
  on framing and light on evidence, and this post shows why the marker matters: the position
  ("requirements are the hard 80%", "the spec is the work") is also the product. That is not a reason to
  discount it — he is the practitioner closest to the thing — but every Dilger claim in this batch is
  commercially interested and the marker travels.
- **The stack-agnostic claim is the sharpest available test of
  [[model-as-code-vs-model-as-language]].** If the same model builds in Axon *and* Marten *and* Emmett,
  the model-as-language camp has the property [[jeremy-miller]]'s model-as-code position structurally
  cannot have (a code-derived model is derived from *one* implementation). If it doesn't, Miller's cost
  objection stands. **Nobody has published the comparison** — the page's standing open question, now
  with a concrete experimental design attached.
- **It also bears on
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's obstacle (3)]]:** the more a
  model must say to drive five stacks, the closer it comes to *being* an implementation — *"the moment a
  model becomes the implementation, it ceases to be a good model."* Build Kits are the proposed escape
  (stack-specific generation from a stack-agnostic model), which is precisely the MDA architecture
  Tornhill and Böckeler both say failed. **This is the most direct live test of the MDA-repeats
  objection in the KB.**
- The "everyone's board is visible" design is a small datapoint on the
  [[event-modeled-agent-design]] gap about whether models are actually read by more than their author —
  though a training cohort is not a stakeholder group.

_Related: [[martin-dilger]] · [[spec-driven-development]] ·
[[dilger-triplet-flexible-agent-enabled-architecture]] · [[model-as-code-vs-model-as-language]] ·
[[event-modeling]] · [[event-sourcing]] · [[vertical-slice-architecture]] · [[eventmodelers-ai]] ·
[[nebulit]] · [[axoniq]] · [[critter-stack]]._
