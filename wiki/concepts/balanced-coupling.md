---
title: Balanced Coupling
type: concept
created: 2026-06-17
updated: 2026-06-22
sources: [khononov-golden-age-of-modularity, coupling-research-note, khononov-modularity-claude-code-plugin]
tags: [coupling-cohesion, modularity, ddd, business-capabilities, agent-legibility, substrate]
---

# Balanced Coupling

A model from **[[vlad-khononov]]** (book: *Balancing Coupling in Software Design*) for reasoning about
coupling as a thing to **balance**, not blindly minimize. The aim is not "low coupling everywhere" but
the *right* coupling in the right places — strong coupling kept local and away from volatile parts.

## The three dimensions

Khononov judges any coupling between two components along three axes, whose interaction decides whether
it will hurt:

- **Strength** — how much one component must know about the other's internals (from shared
  domain knowledge / intrusive integration down to loose, contract-only messaging). Stronger coupling
  demands more co-change.
- **Distance** — how far apart the coupled components live (same method/class → module → service →
  system). Distance multiplies the cost of co-change.
- **Volatility** — how often the coupled area actually changes. Coupling to stable things is cheap;
  coupling to volatile things is where pain concentrates.

The heuristic: **high strength is fine at short distance** (a tight, cohesive unit), and **distance is
fine when strength and volatility are low** (stable, contract-only integration). Trouble is the
combination of strong coupling *across* large distance *to* volatile components.

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
the same dimensions and balance rule). *Still wanted:* a first-party capture of the book's own text on
the BALANCE formula and the Integration Strength definitions, and a resolution of the **per-site →
per-partition** scoring gap.

_Sources: [[khononov-golden-age-of-modularity]] · [[coupling-research-note]] · [[khononov-modularity-claude-code-plugin]]._
