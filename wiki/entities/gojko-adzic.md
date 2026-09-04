---
title: Gojko Adzic
type: entity
created: 2026-08-16
updated: 2026-08-31
sources: [ng-spec-driven-development-is-waterfall-in-markdown]
tags: [person, bdd, given-when-then, specifications, spec-driven-development, focus]
---

# Gojko Adzic

Author of **Specification by Example**, **Impact Mapping**, **Lizard Optimization** and others; partner
at Neuri Consulting LLP; working on Narakeet and Votito. The BDD/specification tradition that produced
the [[given-when-then]] format this wiki leans on throughout the [[event-modeling]] thread is largely
his and Dan North's.

> **Primary captured 2026-08-31, awaiting ingest.**
> `raw/articles/adzic-spec-driven-development-revenge-of-waterfall-or-bdd.md` — *"Spec Driven Development
> - revenge of Waterfall or BDD taken to new level?"*, LinkedIn Pulse, **2025-09-29**. This page still
> describes what the KB held *before* that capture; it should be rewritten when Batch G runs. The
> correction below is applied now because the page was actively wrong.

## ⚠ The quote this KB has been repeating is a misattribution

Until today Adzic appeared here only as a secondhand judgment via
[[ng-spec-driven-development-is-waterfall-in-markdown]]: that he called
[[spec-driven-development|SDD]] *"the revenge of waterfall or BDD taken to a new level."*

**That is the title of his post, posed as a question — not his verdict.** The body answers the BDD half
directly: *"It does not, really."* He never calls SDD waterfall anywhere in the text. And his overall
posture is markedly **warmer** than any of the other three SDD critics the KB now holds:

> "This so far looks interesting, and definitely something to keep an eye on, especially as it's still
> early days. Teams looking for more structure in their AI code generation workflows might find it useful
> now."

He also lists things he *likes*: the flow "mimics a lot of what I am currently doing when using Claude
Code, and makes it more systematic," and exposing the tool's conclusions as editable text files is "a
great way to keep a human in the loop."

Ng deployed the headline as an "even the BDD pioneer says so" move, and the KB amplified it. Worth
recording as a caution: **a rhetorical question in a title is not a position**, and a secondhand quote
with no link is worth exactly as much as the link it doesn't have.

## What he actually argues

Three objections, and the first is sharper for this wiki than the misattributed one:

1. **The generated "spec" is scope-of-work, not specification.** Spec Kit's given/when/then acceptance
   criteria and MUST/SHOULD/COULD requirements sit "on such a high level that it fits more the scope of
   work than a specification." His verdict on the sample it produced: *"This is not a spec, it lacks a
   ton of detail."* The real specification then migrates into unit and integration tests "readable only
   for developers" — *"a missed opportunity to create human-readable specs and drive the work from that."*
2. **There is no scoping phase**, and that is why it fails: with a spec that vague "the tool tried to do
   too much and kind of went off the rails. We generated a ton of tests and code, but it was so
   overwhelming that the whole 'human in the loop' idea was no longer feasible."
3. **Walls of tool-progress documentation** that are for the tool, not for people, and get skimmed.

His closing ask is a design brief rather than a rejection: an explicit scoping phase promoting iterative
delivery, and "a source of truth that's detailed enough for people to approve/complain about, but not
just in code."

## Why it matters here

That last line is, almost word for word, the [[event-modeling]] claim — a specification precise enough
to be authoritative and legible enough for the business to argue with, which is neither prose nor code.
It arrives from the tradition that invented [[given-when-then]], from someone who is **not** an Event
Modeling advocate, and it lands on the same target as [[martin-dilger]]'s "Markdown is a suggestion
dressed up as a spec" from a different direction: Dilger says prose is the wrong *language*, Adzic says
the generated artifact is at the wrong *altitude*. See [[model-as-code-vs-model-as-language]].

Note also what he does **not** say, since the wiki previously assumed it: he makes no
collaboratively-derived-vs-desk-authored argument. That reading was this wiki's own — see
[[given-when-then]], where it has now been marked as such.

## Chronology

His post is **2025-09-29**, three weeks after Spec Kit's launch and the **earliest of the four SDD
critiques the KB holds** — ahead of [[birgitta-bockeler]] (2025-10-15), Zaninotto/Marmelab (2025-11-12)
and Eberhardt/Scott Logic (2025-11-26), and roughly five months ahead of Ng (2026-03).

## Related

[[given-when-then]] · [[spec-driven-development]] · [[event-modeling]] ·
[[model-as-code-vs-model-as-language]] · [[alvis-ng]] · [[birgitta-bockeler]]

_Sources: [[ng-spec-driven-development-is-waterfall-in-markdown]] (secondhand, and shown above to be
unreliable on this point). Primary in `raw/`, awaiting ingest._
