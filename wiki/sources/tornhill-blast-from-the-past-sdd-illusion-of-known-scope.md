---
title: "Source: Tornhill — A Blast from the Past: SDD and the Illusion of Known Scope"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-blast-from-the-past-sdd-illusion-of-known-scope]
raw_file: [raw/articles/tornhill-blast-from-the-past-sdd-illusion-of-known-scope.md]
tags: [spec-driven-development, agentic-coding, ai-readable-code, controversy, focus]
---

# Source: Tornhill — A Blast from the Past: SDD and the Illusion of Known Scope

Substack post by **[[adam-tornhill]]** (*Code for Humans and Machines*), **2026-05-28**. Raw capture:
`raw/articles/tornhill-blast-from-the-past-sdd-illusion-of-known-scope.md`.

> **NOT INDEPENDENT for the alternative it prescribes.** Tornhill is founder and CTO of CodeScene, and
> the closing recommendation — *"intention-revealing software design, automated safeguards for our code
> and its behavior, and rapid visual feedback"* — is the problem space his own commercial product
> addresses. The critique of SDD itself is **argument from career experience, not measurement: there
> are no figures anywhere in this piece.**

The KB has referenced this article since 2026-06-17 as a counter-weight on the SDD thread. Until now it
had **no source page, and the wikilink used for it on [[spec-driven-development]] and
[[adam-tornhill]] pointed at the wrong article** ([[tornhill-merge-conflicts-agentic-bottleneck]]) —
repaired by this ingest.

## Summary

Tornhill scopes his target precisely and then makes one argument. The target is **strong-form SDD**,
which he identifies using Böckeler's ladder: *"as Birgitta Böckeler points out, SDD seems to come in
several forms. It can be anything from a relatively lightweight way to drive agents to a strong form
where the spec itself is the ground truth. It's the latter I'm concerned with."* The argument is that
**implementation is not the execution of a known scope — it is part of the discovery process**, so any
method that treats the spec as ground truth mislocates where the learning happens. He explicitly
declines the waterfall framing others reach for: *"Not due to waterfall thinking — many SDD
practitioners evolve their systems iteratively — but rather due to the nature of problem solving."*

## Key points

- **The MDA / Executable UML / RUP flashback, from someone who shipped with them.** At his first
  employer a lightweight UML-plus-review process worked and the diagrams paid off for onboarding and
  extension. Then tool vendors closed the loop with an "action language" so all code could be
  generated. Two failures followed: *"the first victim was the documented design. The executable
  diagrams turned so bloated and verbose that they became literally incomprehensible. After all, the
  new audience was a compiler, not humans."* And the tooling regressed — no pipelines, CLIs, IDEs or
  linters: *"Imagine coding in a Microsoft Word document. That's how it felt."*
- **The line the whole piece turns on:** *"The moment a model becomes the implementation, it ceases to
  be a good model."*
- **Requirements explosion — the load-bearing mechanism.** He invokes **Robert Glass**: *"for every
  10-percent increase in problem complexity, there is a 100-percent increase in the software solution's
  complexity."* Therefore *"each requirement in the spec will lead to tens of implicit design
  requirements that need to be resolved. We cannot leave that as guesswork for an agent to figure
  out."* **Treat the ratio as Glass's assertion as relayed here** — Tornhill names no specific work and
  makes no measurement of his own.
- **Three obstacles to answering that with a fuller spec:** (1) *"Free text lacks precision … Even
  structured prose and checklists leave room for ambiguity. That's why we have programming
  languages."* (2) *"We cannot know the solution requirements up-front"* — and if agents decide them
  for us, recovering them is *"like reverse engineering a legacy codebase. That's the position we'd be
  in. Constantly."* (3) Extending a requirements spec with implementation details and contracts
  **blurs the model** and destroys its value as a different level of abstraction.
- **Learning by doing is not compressible.** *"Human problem solving is inherently iterative and driven
  by reflection in action … We just cannot short-circuit that."* But he is not anti-document: *"we
  should write stuff down to make it more concrete and invite a conversation. That helps thinking, too.
  But we need to treat that document as an imperfect starting point rather than the finished product."*
- **The manager's-dream framing.** *"Have your skilled seniors specify what to build, then pass it on
  to the seemingly simpler 'implementation' while pretending that step is predictable and somehow less
  important. In the 1990s, 'implementation' meant a team of coders kept in the dark. Today, it's
  obviously agents."*
- **Stochasticity is not the objection either.** *"We also know that GenAI is stochastic. But so too is
  a group of humans collaborating on software. And if history taught us anything, the solution isn't
  just better input but also faster feedback loops."*
- **His alternative, stated as capability rather than process:** *"Predictable progress rests on domain
  expertise, intention-revealing software design, automated safeguards for our code and its behavior,
  and rapid visual feedback, all amplified by a highly skilled team. Those capabilities are harder to
  grow than a spec. But they are also far more valuable. With or without SDD."* Position on SDD itself:
  *"something I'll continue to observe but sit out on for now."*

## Limits

- **No measurement of any kind.** Two unnamed employers, personal recollection, one relayed ratio. The
  MDA experience is real and first-hand but decades old and about deterministic code generators, which
  is the disanalogy he acknowledges (*"I acknowledge that 'this time it might be different'"*).
- **NOT INDEPENDENT** for the prescription (above). The piece is unusually free of CodeScene product
  claims, but "automated safeguards for our code and its behavior" is his product's category.
- The Glass ratio is uncited to a work and unverified here — it must not be promoted to "research
  shows".
- One image (an MDA flashback) is noted inline in the raw, not reproduced.

## Connections / contrast

- **This is the strongest form of the objection to [[spec-driven-development]]'s central premise**, and
  it is *not* the waterfall argument the KB has been filing it under. It is: **the spec cannot contain
  the implicit design requirements, and only building surfaces them.** Dilger's answer would have to be
  that an [[event-modeling|event model]] plus [[given-when-then|GWT]] scenarios *does* pin those down —
  a claim the KB has no evidence for, and one Tornhill's obstacle (3) attacks directly: enrich the model
  enough to resolve implicit requirements and you have turned it into the implementation.
- **It collides head-on with [[dilger-is-code-still-the-source-of-truth]]** ("code is a lagging
  indicator", "almost disposable") and with the model-as-rubric evidence in
  [[dilger-one-million-tokens-self-training-modeling-agent]]. Tornhill's claim that a model that becomes
  the implementation stops being a good model is the sharpest external test
  [[model-as-code-vs-model-as-language]] has, and it lands on **both** camps: the model-as-language pole
  by the MDA precedent, and the model-as-code pole not at all — Miller's derived-visualisation design is
  arguably what Tornhill's first employer had and liked.
- **Independent convergence with [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]]:** both
  reach for MDD/MDA as the precedent, both note the executable model's audience shifts from human to
  machine, and both identify the loss of a *readable* abstraction level. Böckeler adds the point
  Tornhill does not: MDD's parseable structure at least bought tool support for validity.
- **With [[comprehension-debt]]:** requirements explosion is the *upstream* form of the same debt —
  the unresolved implicit design decisions accumulate whether or not anyone reads the diff. His
  companion piece [[tornhill-compressed-cognition-cost-of-faster-coding]] supplies the cognitive-load
  half.
- **Sceptic cluster, and the one who declines the waterfall label:**
  [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] (also not a waterfall claim) ·
  [[zaninotto-spec-driven-development-waterfall-strikes-back]] (is) ·
  [[eberhardt-putting-spec-kit-through-its-paces]] (is) ·
  [[ng-spec-driven-development-is-waterfall-in-markdown]] (is).
- Same-author thread: [[ai-readable-code]] · [[tornhill-clear-design-principles-agentic-age]] ·
  [[tornhill-cannot-trust-agent-codescene-mcp]] (the deterministic-external-sensor instinct that his
  "automated safeguards" line here restates).

_Related: [[adam-tornhill]] · [[spec-driven-development]] · [[model-as-code-vs-model-as-language]] ·
[[ai-readable-code]] · [[comprehension-debt]] · [[agentic-coding]] · [[event-modeling]]._
