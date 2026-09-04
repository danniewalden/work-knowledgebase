---
title: Architectural Decision Record (ADR)
type: concept
created: 2026-08-31
updated: 2026-09-02
sources: [madr-markdown-architectural-decision-records, nick-tune-enforced-application-architecture-agents-humans]
tags: [documentation, decision-records, architecture, madr]
---

# Architectural Decision Record (ADR)

**A short markdown document recording one design decision and the reasoning behind it** — the context
and problem, the options considered, the option chosen, and why. Version-controlled next to the code, one
file per decision, numbered `NNNN-title-with-dashes.md` in a `docs/decisions/` folder.

Written 2026-08-31 to ground a wikilink that had been dangling from [[decision-trace]] since the 08-30
lint. The KB's source is the canonical **MADR** site
([[madr-markdown-architectural-decision-records]], MADR 4.0.0), the template Dannie's own ADR tooling
targets.

## The definition, and its deliberate looseness

> "An Architectural Decision (AD) is a software design choice that addresses a functional or
> non-functional requirement that is architecturally significant… **Do not take the term 'architecture'
> too seriously or interpret it too strongly.** As the examples illustrate, any decisions that might have
> an impact on the architecture somehow are architectural decisions."

The MADR authors are explicit that they are sidestepping the "is this architecturally significant?"
argument rather than settling it: *"Since we believe that any (important) decision should be captured in
a structured way, we offer the MADR template to capture any decision."* The naming history records the
same ambivalence — MADR was renamed **Markdown *Any* Decision Records** in 2022 and renamed **back** to
*Architectural* in 2024, "to strengthen the importance for decisions in software architecture work…
They can still be used to sustain any decision, our focus is on architectural decisions."

## The MADR 4.0 shape

Mandatory: **Context and Problem Statement** → **Considered Options** → **Decision Outcome** ("Chosen
option: X, because …"). Optional but common: **Decision Drivers**, **Consequences** (good/bad in one
list, merged in 3.0), **Confirmation** (how compliance will be checked — "although we classify this
element as optional, it is included in many ADRs"), **Pros and Cons of the Options** (good/neutral/bad),
**More Information**. YAML frontmatter carries `status`, `date`, `decision-makers`, `consulted`,
`informed` — the last three being RACI roles.

Four template variants ship: full, minimal, bare (no explanations), bare-minimal. Dual-licensed MIT or
CC0. Backed by a 2018 paper (Kopp, Armbruster & Zimmermann, ZEUS).

## Relation to the rest of this KB

**ADR ≠ [[decision-trace]].** The distinction that page draws is the right one and now has a grounded
source on the other side: an ADR records *a human's* architectural choice, deliberated before the fact,
in a form meant to be read years later. A decision trace records *an agent's* run-time reasoning, emitted
during execution, for debugging and audit. Same word, different artifact, different reader.

Three connections worth noting:

- **"Confirmation" is the ADR's given/when/then.** MADR asks how compliance with the decision *will be
  checked* — "a design/code review or a test with a library such as ArchUnit can help validate this."
  That is the same instinct as [[given-when-then]] on a [[slice]]: a decision that cannot be checked has
  not been fully specified. MADR treats it as optional; Event Modeling does not.
- **ADRs are the "why" that code cannot carry** — the argument
  [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] makes while rejecting SDD: *"I'm not against
  all documentation, on the contrary, capturing architectural details and design decisions is very
  valuable. Code can give you the 'what', but cannot tell you the 'why'."* An ADR is his counter-example
  to his own critique — the documentation that survives because it records something the code cannot.
- **Categorisation is a meta-decision.** For large repositories MADR suggests subdirectories as
  categories, and notes the organising principle "ideally uses the same organizing principles as other
  artifacts such as the code." In a [[slice]]-organised or capability-organised codebase that would mean
  decisions filed by [[business-capabilities|capability]] — which the source raises as an option and does
  not pursue.

## What the KB does not hold

No evidence on whether ADRs work — no study of adoption, decay, or whether anyone reads them later. The
source is a format specification and its own project's ADRs, not a field report.

**The agent-facing question now has one practitioner's report, and it is not encouraging** (added
2026-09-02). [[nick-tune]] opens [[nick-tune-enforced-application-architecture-agents-humans]] by naming
ADRs among the artifacts agents ignore: *"One of the most frustrating parts of AI-generated code is that
it does not follow architectural guidelines that are written in skill files, ADRs, and various other
places in the repo."* His response is not to write better ADRs but to move the decision's *force* out of
prose and into a build-enforced DSL — while keeping the ADR for humans: *"ADR-002 describes the same
architecture for humans. The ADR and executable Rivière configuration are kept aligned."*
*(Author self-report: **Rivière is Tune's own tool**, and the post offers no measurement of either the
problem or the fix.)*

Two things follow for this page. First, it is the KB's first concrete instance of **Confirmation
actually wired up** — MADR asks how compliance "can/will be confirmed… a test with a library such as
ArchUnit," and Tune's config is that test, for a decision that has an ADR number. Second, **the post
does not say what keeps the two aligned** — the sentence is passive ("are kept aligned") and names no
mechanism, so two artifacts state one architecture with nothing visible enforcing the correspondence.
Whether that is a person, a script or a convention is exactly the interesting question, and it is
unanswered. That is a drift risk MADR does not address either — and it sharpens this page's open
question rather than settling it. One practitioner's complaint that agents ignore ADRs is not a study;
what he offers is a *worked alternative* to relying on them.

## Related

[[decision-trace]] · [[given-when-then]] · [[spec-driven-development]] · [[context-engineering]] ·
[[comprehension-debt]] · [[business-capabilities]] · [[agent-explainability]] · [[fitness-functions]] ·
[[nick-tune]]

_Sources: [[madr-markdown-architectural-decision-records]] ·
[[nick-tune-enforced-application-architecture-agents-humans]]._
