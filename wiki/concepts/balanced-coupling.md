---
title: Balanced Coupling
type: concept
created: 2026-06-17
updated: 2026-09-04
sources: [khononov-golden-age-of-modularity, coupling-research-note, khononov-modularity-claude-code-plugin, khononov-ai-doesnt-fix-your-real-bottleneck, khononov-coupling-should-be-weighed-not-counted]
tags: [coupling-cohesion, modularity, ddd, business-capabilities, agent-legibility, substrate]
---

# Balanced Coupling

A model from **[[vlad-khononov]]** (book: *Balancing Coupling in Software Design*) for reasoning about
coupling as a thing to **balance**, not blindly minimize. The aim is not "low coupling everywhere" but
the *right* coupling in the right places — strong coupling kept local and away from volatile parts.

## The three dimensions

Khononov judges any coupling between two components along three axes, whose interaction decides whether
it will hurt:

- **Shared knowledge** — how much one component must know about the other's internals (from shared
  domain knowledge / intrusive integration down to loose, contract-only messaging). More shared
  knowledge demands more co-change. *(**Terminology corrected 2026-09-04:** this page previously named
  this axis "**Strength**". Khononov's own current wording for the triad is **"shared knowledge"** —
  see the first-party statement below. Same axis, and the book's four-level **Integration Strength**
  scale is how it is graded; "strength" is the scale's name, not the axis's.)*
- **Distance** — how far apart the coupled components live (same method/class → module → service →
  system). Distance multiplies the cost of co-change. Khononov's own gloss makes it wider than geometry:
  distance is "physical **and organizational**."
- **Volatility** — how often the coupled area actually changes. Coupling to stable things is cheap;
  coupling to volatile things is where pain concentrates.

The heuristic: **a lot of shared knowledge is fine at short distance** (a tight, cohesive unit), and
**distance is fine when shared knowledge and volatility are low** (stable, contract-only integration).
Trouble is the combination of strongly-knowledge-coupled components *across* large distance *to*
volatile components.

**First-party statement of the triad (2026-02).** The three dimensions above were sourced to the book and
the [[coupling-research-note]]; [[khononov-ai-doesnt-fix-your-real-bottleneck]] states them in the
author's own current words, and names the first axis **"shared knowledge"** rather than *strength*: "the
knowledge components share about each other. The more knowledge is shared, the higher the likelihood that
a change in one will trigger cascading changes in others." Distance is "physical **and
organizational**"; volatility is "the probability that a component will need to change in the first
place. High volatility amplifies design problems; low volatility neutralizes them." His balance rule, in
prose: components that change together are located close; components that don't are spread apart; and
"ultimately, **volatility multiplies** the effects of complexity." Same model, and the terminology drift
(shared knowledge ≈ Integration Strength) is worth knowing when reading him. **Cite the triad to this
piece**, not to [[khononov-coupling-should-be-weighed-not-counted]] — that companion post covers **only**
the Integration Strength scale. **NOT INDEPENDENT** — the model's own author, closing with his own book
via an affiliate link. **No data in either post.**

## The dimensions in detail (from the 2024 book)

The [[coupling-research-note|2026-06-22 research note]] pins down the scales from the book
*Balancing Coupling in Software Design* (Addison-Wesley 2024, ISBN 9780137353538) and Khononov's
companion site [coupling.dev](https://coupling.dev):

**Integration Strength** (Ch. 7) — a four-level ordinal, strongest → weakest:

| Level | Name | Definition |
|---|---|---|
| 4 | **Intrusive** | Integration via private interfaces, internal databases, undocumented APIs — "both fragile and implicit." Maps to classical [[coupling-taxonomy\|content coupling]]. |
| 3 | **Functional** | Components share functional requirements (the "what", not the "how"). Canonical case: duplicated business logic that forces co-change. |
| 2 | **Model** | Components share knowledge of a (typically business-domain) model. Explicitly tied to DDD bounded contexts. |
| 1 | **Contract** | Integration via an explicit published contract. Weakest, most desirable. |

**Why weigh rather than count (2026-02, first-party prose).**
[[khononov-coupling-should-be-weighed-not-counted]] gives the four levels in his own words and the
argument for the scale's existence: each level down "removes an *entire category* of shared reasons for
change," which is why "a single intrusive dependency can cause more cascading changes than a hundred
contract-based ones." His illustration: a component with 1 outgoing and 100 incoming dependencies scores
~0.01 on `I = Ce / (Ce + Ca)` — "textbook stability" — while its one outgoing dependency reaches into
another component's internals (a service reading another service's database) and the 100 incoming ones go
through stable contracts. "The metric says: rock-solid stability. Reality says: ticking time bomb." Each
level restated: **intrusive** = "you have to assume that *all* knowledge is shared… reasons for cascading
changes are essentially unbounded"; **functional** = "switches from 'how?' to 'what'" (the same rule
implemented twice); **model** = "shifts from logic to structure… entities, relationships, and concepts";
**contract** = "the contract encapsulates everything behind it… only modifications to the contract itself
propagate."

The generalisable warning: "Static analysis tools count because counting is easy to automate. But easy to
automate and useful are not the same thing. A metric that treats use of reflection to modify a private
field and an API call as equivalent is likely to point you in the wrong direction." Worth reading against
the KB's measurement-based sources — [[tornhill-codescene-unhealthy-code-agentic-token-cost]] (**VENDOR
SELF-REPORT** figures), [[fitness-functions]], [[fowler-bockeler-maintainability-sensors]] — as the
sharpest sceptical frame on automatable design metrics the KB has. Caveats: **NOT INDEPENDENT**; the
100-dependency component is a **constructed illustration**; "in my experience, chasing those metrics never
really made the design more modular" is a **practitioner self-report**; and the post never addresses the
obvious rejoinder that direct DB access *is* automatically detectable. **This post does not state the
triad** — only this axis; the triad is in [[khononov-ai-doesnt-fix-your-real-bottleneck]].

**Distance** — physical/logical separation: methods → objects → packages/namespaces →
services/microservices → systems. *Observable* from deployment topology rather than judged. (A verifier
in the research run pushed back on over-specifying this as "encapsulation boundaries"; the safe reading
is the methods→…→systems scale.)

**Volatility** — likelihood the area changes, judged via **DDD subdomain** (High = Core; Low =
Supporting / Generic). Khononov **explicitly warns against using commit history** — accidental
volatility from poor design skews any commit-based estimate.

**The numeric balance.** Ch. 10 ("Balancing Coupling on a Numeric Scale") gives a formula —
`BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY` — i.e. strong-and-close or weak-and-far is
balanced, and coupling to stable things is always fine. Note it is defined for an **individual coupling
site**, not for scoring a whole candidate partition; turning it into a partition score is an open
problem (see the research note's open questions).

## Application — edge weights for a user-needs map

The [[coupling-research-note]] evaluates this model as the basis for **dependency-edge weights** on a
capability/user-needs map. Conclusion: of the three dimensions, the two that suit an editor-judgment dial
are the *subjective* ones — **Integration Strength** (primary) and **Volatility-coupling** (secondary,
the judgment-based analog of change-coupling). **Distance is not an edge property** — it falls out of
the partition once a boundary is drawn. Two dials, not three, is also a cognitive-load constraint on the
editor. Contrast with the other frameworks in [[coupling-taxonomy]] and the partition-side constraints
in [[team-topologies]].

## The modularity test

In ["The Golden Age of Modularity"]([[khononov-golden-age-of-modularity]]) Khononov gives the practical
payoff as a two-part test for a modular design: (1) **localized change** — when you change the system
it's clear which (few, ideally one) components are affected; and (2) **predictable effect** — you can
predict the change's effect on behavior. Good coupling choices are what make both true.

## Operationalized as an agent skill

Khononov has turned the model into a **Claude Code plugin**
([[khononov-modularity-claude-code-plugin|"Modularity Skills"]]) — two agent skills that *apply* the
three dimensions rather than just describe them: `/modularity:review` audits an existing codebase for
imbalances (mapping each integration on strength/distance/volatility, applying the balance rule, emitting
a review with coupling.dev links), and `/modularity:high-level-design` designs a modular architecture
from requirements and self-reviews until clean. His pitch is explicitly the AI-coding era: most AI tools
give *code-level* feedback, "but that's not where the costly mistakes hide" — generated code accumulates
architectural debt faster, so the leverage is at the boundary. This makes Balanced Coupling the
coupling-substrate analogue of the Event-Modeling-as-agent-skill pattern
([[jwilger-agent-skills-event-modeling]], [[proophboard-skills-ai-agent-event-modeling]]).

## Where it sits in the KB

- The **design-theory spine** under [[business-capabilities]] — it puts mechanics behind the
  capability boundary intuition ("*how* changes often, *what* is stable"): a capability boundary is a
  bet about strength/distance/volatility. Pairs with the [[ulrich-homann]] capability primary (the
  *what-not-how* black box) as the two anchors of that concept.
- A first-principles statement of [[agent-legibility]] / [[locality-of-reference]]: "localized change +
  predictable effect" is exactly what makes a codebase cheap and safe for an agent to evolve, which is
  why Khononov frames modularity as the thing **AI agents depend on**. Converges with
  [[tornhill-clear-design-principles-agentic-age|Tornhill's CLEAR]] ("reduce the edit surface", "local
  reasoning") and is part of the [[ai-readable-code]] thread.
- Related substrate: [[vertical-slice-architecture]] (couple inside a slice), [[domain-driven-design]]
  (bounded contexts), [[dynamic-consistency-boundaries]] (which boundary a decision really needs),
  [[open-closed-principle]].

## To capture next

The primary book is now grounded second-hand via the [[coupling-research-note]] (book TOC,
coupling.dev) and the [[khononov-modularity-claude-code-plugin|Modularity Skills plugin]] (which encodes
the same dimensions and balance rule). *Partly closed (2026-09-04):*
[[khononov-coupling-should-be-weighed-not-counted]] gives the Integration Strength definitions in the
author's own prose, and [[khononov-ai-doesnt-fix-your-real-bottleneck]] the triad and balance rule.
*Still wanted:* the book's own text on the **BALANCE formula** (neither post states it), and a resolution
of the **per-site → per-partition** scoring gap.

_Sources: [[khononov-golden-age-of-modularity]] · [[coupling-research-note]] · [[khononov-modularity-claude-code-plugin]] · [[khononov-ai-doesnt-fix-your-real-bottleneck]] · [[khononov-coupling-should-be-weighed-not-counted]]._
