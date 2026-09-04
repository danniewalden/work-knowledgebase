---
title: "Source: Adzic — Spec Driven Development: revenge of Waterfall or BDD taken to a new level?"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [adzic-spec-driven-development-revenge-of-waterfall-or-bdd]
raw_file: [raw/articles/adzic-spec-driven-development-revenge-of-waterfall-or-bdd.md]
tags: [spec-driven-development, given-when-then, agentic-coding, controversy, bdd, focus]
---

# Source: Adzic — Spec Driven Development: revenge of Waterfall or BDD taken to a new level?

LinkedIn Pulse article by **[[gojko-adzic]]**, **2025-09-29** — three weeks after GitHub's Spec Kit
launched, and **the earliest of the four primaries behind the KB's SDD critique cluster** by a wide
margin (Böckeler 2025-10-15, Zaninotto 2025-11-12, Eberhardt 2025-11-26, Ng 2026-03). Written from a
Citcon session where he and others ran Spec Kit with Claude Code on a conference-voting system. Raw
capture: `raw/articles/adzic-spec-driven-development-revenge-of-waterfall-or-bdd.md`.

Adzic is the author of *Specification by Example* and *Impact Mapping*, so the BDD comparison in the
title is **first-party**, not an outsider's analogy.

## Summary

Adzic reads [[spec-driven-development|SDD]] as *"an attempt to formalize a workflow around AI agent
coding, extracting and codifying successful patterns … into a process that can be standardized, and
can be enforced by a tool across different people and teams."* He likes that the tool's conclusions
land in **editable text files committed to version control** — a real human-in-the-loop mechanism —
and says the flow "mimics a lot of what I am currently doing when using Claude Code, and makes it
more systematic." His objections are about **what the generated artifact is** and **what phase is
missing**, not about specification as such.

## Key points

- **Correcting a misattribution the KB carried since 2026-08-16.** The actual title is *"Spec Driven
  Development - revenge of Waterfall or BDD taken to new level?"* — **posed as a question**, not his
  verdict. (The wiki's version, *"the revenge of waterfall or BDD taken to a new level"*, is Ng's
  paraphrase of it, not Adzic's wording.)
  [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]] relayed it as a judgment and the wiki
  repeated it. Adzic answers the BDD half **"It does not, really"** and **never calls SDD waterfall
  anywhere in the body**.
- **His actual verdict is the warmest of the four critics:** *"definitely something to keep an eye
  on, especially as it's still early days. Teams looking for more structure in their AI code
  generation workflows might find it useful now."* Filing him as an anti-SDD voice is wrong.
- **Scope-of-work, not specification.** The generated "spec" carries [[given-when-then|Given-When-Then]]
  acceptance scenarios plus MUST/SHOULD functional requirements, but *"this is on such a high level
  that it fits more the scope of work than a specification … This is not a spec, it lacks a ton of
  detail."* The raw preserves the twelve-FR sample verbatim.
- **The real spec migrates into the tests — and that is the missed opportunity.** *"The real 'spec'
  then ends up being in unit and integration tests that are generated based on these requirements"*,
  which are *"readable only for developers."* Hence the answer to his own title: SDD is **not** BDD
  taken further, because the executable specification stops being human-readable. He wants *"a source
  of truth that's detailed enough for people to approve/complain about, but not just in code."*
- **The missing scoping phase.** With a spec at that granularity *"the tool tried to do too much and
  kind of went off the rails. We generated a ton of tests and code, but it was so overwhelming that
  the whole 'human in the loop' idea was no longer feasible."* His fix is an explicit scoping phase
  enforcing iterative delivery and progressive enhancement.
- **Documentation nobody reads.** *"Walls of text that are difficult to parse. Most of it seems to be
  for the tool to track its own progress"* — the same finding Böckeler, Zaninotto and Eberhardt each
  report independently.
- **Bad technical defaults are cheap to fix and worth the friction.** Spec Kit picked an outdated
  Node.js version; editing the generated file was easy, and *"making such choices explicit at least
  forces people to think harder about what they want to do."*
- He notes Kiro takes the IDE-fork route where Spec Kit generates agent slash-commands, and scopes his
  conclusions to Spec Kit only.

## Limits

- **One session, one greenfield toy problem** (a conference voting system) at a conference workshop,
  September 2025 — three weeks into Spec Kit's life, and he says so repeatedly ("first impressions",
  "still early days"). No figures of any kind appear in the piece.
- **Interested in the comparison he is making:** he authored *Specification by Example*, so "is this
  BDD?" is a question about his own tradition's claim to the ground. That cuts both ways — first-party
  expertise, first-party stake.
- Kiro is assessed second-hand ("from what I understand") and he explicitly asks for corrections.

## Connections / contrast

- **This is the primary the KB was missing on the [[spec-driven-development]] page**, which since
  2026-08-16 quoted him only through Ng and carried a correction block flagging the misattribution.
  The page's Adzic material should now be rewritten from here.
- **His "missing scoping phase" is independently the same complaint as
  [[dilger-spec-driven-development-needs-four-phases|Dilger's phase 1 (Idea → Intent)]]** — two people
  arriving at *"the tools implement the easy middle"* from the BDD tradition and the
  [[event-modeling]] tradition respectively, **neither citing the other**. That convergence is worth
  more than either claim alone, and it is now grounded in both primaries.
- **Against [[jeremy-miller]]:** Miller's position in [[model-as-code-vs-model-as-language]] is that
  going *straight to BDD specifications* is right and the intermediate model is waste. Adzic's finding
  is that Spec Kit already does effectively that — and the result is a spec only developers can read.
  The two are not in agreement despite both invoking BDD; Adzic wants the human-reviewable layer that
  Miller's design deliberately derives rather than authors.
- **With [[given-when-then]]:** GWT scenarios *appear* in the generated Spec Kit spec, which is why
  the artifact looks like specification by example and isn't. Adzic's test is whether a non-developer
  can approve or complain about it — the same provenance-style test [[decision-trace]] applies from a
  different angle.
- Sceptic cluster: [[bockeler-understanding-sdd-kiro-speckit-tessl]] ·
  [[zaninotto-spec-driven-development-waterfall-strikes-back]] ·
  [[eberhardt-putting-spec-kit-through-its-paces]] ·
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope]] ·
  [[ng-spec-driven-development-is-waterfall-in-markdown]].

_Related: [[gojko-adzic]] · [[spec-driven-development]] · [[given-when-then]] ·
[[model-as-code-vs-model-as-language]] · [[agentic-coding]]._
