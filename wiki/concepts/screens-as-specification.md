---
title: Screens as Specification
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-ux-as-first-class-in-spec-driven-development, dilger-ui-only-interactions-filtering, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-only-engineers-care-about-consistent-systems, dilger-highlighting-markers-give-context-to-agents, zaninotto-spec-driven-development-waterfall-strikes-back, eberhardt-putting-spec-kit-through-its-paces, ng-spec-driven-development-is-waterfall-in-markdown]
tags: [event-modeling, spec-driven-development, given-when-then, agentic-coding, focus]
---

# Screens as Specification

**The claim:** in an agent-facing specification, the **screen is first-class content, not derived
output** — and it is the part of the spec a designer, a product owner or an end user can actually
review. [[martin-dilger]] states it as a workflow property
([[dilger-ux-as-first-class-in-spec-driven-development]], 2026-08-31):

> "Instead of deriving the UX from markdown files ( which become unreadable and impossible to maintain
> from a certain size on ), we focus on the functionality, the UX and the business rules described as
> Given / When / Then ( BDD Style ). **Spec-Driven Development does not need Markdown Files.**"

So the division of labour is **screens carry the interaction, [[given-when-then|GWT]] carries the
rules** — which is narrower and more checkable than the general "use a DSL" claim in
[[model-as-code-vs-model-as-language]].

> **VENDOR SELF-REPORT throughout.** Every mechanism on this page is a feature of Dilger's own
> commercial platform ([[eventmodelers-ai]] / EM-Studio, [[nebulit]]). The fullest primary for the
> workflow is an **uncaptured 60-minute webinar** the LinkedIn note links to; the note itself is
> ~100 words and contains no demonstration. Read the claims here as a stated position with worked
> illustrations, not as evidence that it works.

## Why the method already had room for it

[[event-modeling]] has always put wireframes and mockups in swimlanes across the top of the board, one
lane per actor — screens are original equipment, not an addition. [[adam-dymitruk]] defends this
directly in [[dilger-podcast-episode-47-agentic-modeling-audit-trails]], where a DDD-community post
*"rediscovers"* that showing users' screens carries real information:

> "That's why all the arguments about not having screens and design sessions is just gatekeeping by
> architect wannabes."

*(That episode's **date is unresolved** — see its source page. **Show-notes level, not verified against
audio.**)*

## The mechanism, worked

[[dilger-ui-only-interactions-filtering]] (2026-07-31) is the concrete instance, and its method
content matters independently: **most screen interactions are not state changes and must not be
modelled as Commands and Events.**

> "Filtering, sorting, expanding a row, switching a tab - these are all views on data you already have.
> Model them as Views, not as Commands looking for an Event to justify them."

The filtering example uses **Multi-Screen Views** — an unfiltered page and a filtered page backed by
the *same* `Books[]` read model — with behaviour specified on the read side using the **Query WHEN**
(*"Given two `Book registered` events… When you query by title with the key 'Harry Potter', Then the
`Books` Read Model returns just that one match"*). Note the Query WHEN is used here as ordinary
practice, but its status per [[dilger-extending-event-modeling-query-when]] is **optional, proposed and
not ratified**; that status travels.

The screen is authored *in* the model (plain HTML views, or generated cheaply by a connected agent), and
the agent-facing payoff is stated explicitly: *"Using the UI mockup - which is also accessible for a
connected agent building from the model - it's quite clear what needs to be done."* Two adjacent
surfaces complete the picture: **region-scoped screen markers** an agent reads, validates and builds UI
from ([[dilger-highlighting-markers-give-context-to-agents]]), and a **Screen Preview** placing hand
sketches, HTML mockups and Figma screens in one storyline
([[dilger-only-engineers-care-about-consistent-systems]]).

## The audience argument — and why it matters more than the machine one

The KB's sharpest external objection to spec-first work is about **who can read the artifact**, not
whether an agent can. [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]: a spec flattens a
cross-functional set of mental models into the author's single voice, and no designer, PM or DevOps
engineer will ever open a `.specify` folder — *"a contract between you and the LLM that nobody else
signed."* [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] asks the same thing as *who is the
target user?*, noting SDD tools import product vocabulary while presenting a lone developer as author.
And [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto]] — arguing *against* SDD
entirely — ends with the one wish this page answers:

> "Coding agents use text, not visuals. Sometimes I want to point to a specific zone… if we need new
> tools to make coding agents more powerful, I think the focus should be on richer visual
> interactions."

A sketched screen needs no folder, and it is the artifact an end user reacts to — which is exactly
Dilger's own prescription in [[dilger-only-engineers-care-about-consistent-systems]]: *"invite them to a
short Event Modeling Session. Show them what you planned, show them the screens you sketched… you do
not have to write a single line of code for that."*

**How far this answer goes.** It answers *"nobody will open the artifact."* It does **not** answer
*"nobody else signed it"*: the KB holds **no captured source measuring non-developer participation in a
model that later drove agents**, and every source on this page is one interested party. See the named
gap on [[event-modeled-agent-design]].

## The counter-evidence, which is real

- **Generated UI rationale is where SDD looks worst, and that supports the diagnosis while rejecting
  the cure.** [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt's]] exemplar of AI *"detail that
  fundamentally lacks depth of value"* is invented UX reasoning: *"Karting users need to log data
  trackside on mobile devices, often with gloves or in suboptimal lighting."* Markdown-derived UX doing
  precisely what Dilger says it does — from an author who concludes SDD is not viable at all.
- **Agents can inflate the visual artifact too.** Ep 47's `/wdyt` tuning lesson: an agent flooding a
  slice with hypothetical edge cases *"can make a simple slice look far more complex than it really is,
  since event modeling is visual"* (Dymitruk). The screen's advantage is legibility, and legibility is
  destroyable ([[event-modeling-anti-patterns]]).
- **"BDD Style" is doing loose work.** Screens-plus-GWT is not what specification by example normally
  means by *executable* specification, and [[gojko-adzic]] — who wrote the book — finds SDD tools' GWT
  output *"is not a spec, it lacks a ton of detail"*
  ([[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]]). Dilger's version may be stronger; it
  is not established.
- **No worked case where an authored screen drove agent-built UI end to end** is captured anywhere.

## Related

[[event-modeling]] · [[given-when-then]] · [[agent-readable-model-artifacts]] ·
[[spec-driven-development]] · [[event-modeled-agent-design]] · [[event-modeling-anti-patterns]] ·
[[slice]] · [[decision-trace]] · [[eventmodelers-ai]]

_Sources: [[dilger-ux-as-first-class-in-spec-driven-development]] ·
[[dilger-ui-only-interactions-filtering]] ·
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]] ·
[[dilger-only-engineers-care-about-consistent-systems]] ·
[[dilger-highlighting-markers-give-context-to-agents]] ·
[[zaninotto-spec-driven-development-waterfall-strikes-back]] ·
[[eberhardt-putting-spec-kit-through-its-paces]] ·
[[ng-spec-driven-development-is-waterfall-in-markdown]]._
