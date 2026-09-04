---
title: Gojko Adzic
type: entity
created: 2026-08-16
updated: 2026-09-04
sources: [adzic-spec-driven-development-revenge-of-waterfall-or-bdd, ng-spec-driven-development-is-waterfall-in-markdown]
tags: [person, bdd, given-when-then, specifications, spec-driven-development, focus]
---

# Gojko Adzic

Author of **Specification by Example**, **Impact Mapping**, **Lizard Optimization** and others; partner
at Neuri Consulting LLP; working on Narakeet and Votito. The BDD/specification tradition that produced
the [[given-when-then]] format this wiki leans on throughout the [[event-modeling]] thread is largely
his and Dan North's.

> **Primary ingested 2026-09-04.** [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] —
> *"Spec Driven Development - revenge of Waterfall or BDD taken to new level?"*, LinkedIn Pulse,
> **2025-09-29** — is now a source page, and this page cites it directly rather than reaching him
> through [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]. It is the **earliest primary in
> the KB's SDD critique cluster**: three weeks after GitHub's Spec Kit launched and five months before
> Ng's synthesis.

## ⚠ Repaired: he is not the hostile anti-SDD voice this KB cited him as

For a period this wiki carried Adzic only as a secondhand judgment via
[[ng-spec-driven-development-is-waterfall-in-markdown]] — that he called
[[spec-driven-development|SDD]] *"the revenge of waterfall or BDD taken to a new level."* **That
attribution was wrong, and the primary now settles it.** Four corrections, all checkable against
[[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]]:

1. **The phrase is his title, posed as a question — not his verdict.**
2. **He never calls SDD waterfall in the body.** Not once.
3. **He answers the BDD half of his own title directly: *"It does not, really."***
4. **He is the warmest of the KB's SDD critics**, not the most hostile — see the quotation below. Filing
   him as a hostile voice, or counting him toward an "anti-SDD front," misrepresents him.

Ng deployed the headline as an "even the BDD pioneer says so" move, and this wiki amplified it. The
generalisable caution: **a rhetorical question in a title is not a position**, and a secondhand quote
with no link is worth exactly as much as the link it doesn't have. Any page still citing Adzic as an
anti-SDD or waterfall-accusation voice is carrying the repaired error and should be corrected to this
page.

His overall posture is markedly **warmer** than any of the other three SDD critics the KB holds:

> "This so far looks interesting, and definitely something to keep an eye on, especially as it's still
> early days. Teams looking for more structure in their AI code generation workflows might find it useful
> now."

He also lists things he *likes*: the flow "mimics a lot of what I am currently doing when using Claude
Code, and makes it more systematic," and exposing the tool's conclusions as editable text files is "a
great way to keep a human in the loop."

## What he actually argues

Three objections — and both of the first two are **first-party**, since he wrote *Specification by
Example* and *Impact Mapping*. The first is sharper for this wiki than the misattributed one:

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
just in code." **That test — detailed enough to approve or complain about, but not just in code — is the
most checkable criterion for a spec artifact anywhere in the KB.**

**The scoping complaint converges independently with [[martin-dilger]]'s phase 1**
([[dilger-spec-driven-development-needs-four-phases]]), neither citing the other — an advocate and a
sceptic of the same wave locating the same missing step. See [[spec-driven-development]],
[[given-when-then]].

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
critiques the KB holds** — ahead of [[birgitta-bockeler]] (2025-10-15),
[[francois-zaninotto|Zaninotto]]/[[marmelab]] (2025-11-12) and
[[colin-eberhardt|Eberhardt]]/[[scott-logic]] (2025-11-26), and roughly five months ahead of Ng
(2026-03).

**Where he sits among them, since the KB has flattened this before.** The four are not one anti-SDD
front: Adzic is the warmest and never argues against specification at all (his complaint is that the
generated artifact isn't one); Böckeler practises spec-first and recommends it; Eberhardt rejects the
*purest* form while defending the debate; [[adam-tornhill|Tornhill]] scopes himself to the strong form
and explicitly declines the waterfall argument; only Zaninotto calls SDD *"a step in the wrong
direction"* outright.

## Related

[[given-when-then]] · [[spec-driven-development]] · [[event-modeling]] ·
[[model-as-code-vs-model-as-language]] · [[alvis-ng]] · [[birgitta-bockeler]] ·
[[colin-eberhardt]] · [[francois-zaninotto]] · [[martin-dilger]]

_Sources: [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] (the primary — cite this) ·
[[ng-spec-driven-development-is-waterfall-in-markdown]] (secondhand, and shown above to be unreliable on
this point — do not cite it for Adzic's position)._
