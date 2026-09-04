---
title: Vibe Modeling
type: concept
created: 2026-06-17
updated: 2026-08-31
sources: [event-modeling-event-sourcing-podcast, fowler-agentic-programming, dilger-flea-market-model-to-deploy]
tags: [event-modeling, agentic-coding, ai, vibe-modeling, focus]
---

# Vibe Modeling

A term coined on the podcast (**Ep 19**, "Vibe Modeling, Event Models for the
C-Suite") as the [[event-modeling]] answer to **"vibe coding"** — the practice of building software by
prompting an LLM loosely and accepting what comes out. The hosts' argument: vibe coding lets
non-developers produce apps but is risky precisely because it skips the *shared structure*; **vibe
modeling** is the collaborative front-end — sketch the system as an event model *with* stakeholders and
AI, so the "vibes" are captured as an explicit information-flow blueprint before any code is generated
([[event-modeling-event-sourcing-podcast]]).

The defining property: **the stakeholder never has to learn the method.** The event model is legible
enough — screens across the top, a left-to-right story — that a non-technical person can co-design by
pointing at screens and answering plain questions, while the practitioner (or an agent) captures the
structure underneath. The "vibes" are the stakeholder's intent; modeling is the act of making them
explicit and shared *without* imposing notation on the person who has the domain knowledge.

The concrete demonstration is **Ep 30**: Adam builds a Yahtzee game with LLMs and finds the AI keeps
**breaking scope** — wrecking existing features when asked for a small change — and that the event
model supplies the structure that contains it. This is the podcast's hands-on version of the wider
[[event-modeled-agent-design]] / [[spec-driven-development]] thesis: the model is the guardrail that
keeps loosely-prompted AI from sprawling.

## Worked instance — the flea-market registration (Dilger, 2026-07-01)

The KB's strongest concrete demonstration is [[dilger-flea-market-model-to-deploy|Dilger's flea-market
vignette]]. Asked by his wife to build a flea-market registration form, he opened
[[eventmodelers-ai]] and they **brainstormed by drawing screens** — and, crucially, he **never named or
taught Event Modeling**:

> "She understood exactly what we were doing. Not because I taught her Event Modeling — she has no idea what
> that is. And she doesn't care… Just by drawing the screens as we usually do she could easily follow along."

That is vibe modeling in one line: a non-technical stakeholder **co-models a system by drawing screens
without knowing the method exists.** Ordinary questions ("what happens after someone registers?", "how do
you track who's paid?") elicit the events, commands, and read models; the shared artifact is the model, not
the vocabulary. It connects to [[domain-discovery]] (discovery run live and conversationally, stakeholder's
mental model as source of truth) and lands the podcast's original pitch — the model as the thing
stakeholders *can* inspect and agree on. Dilger's own honest boundary keeps it from over-claiming: for a
trivial app, unstructured vibe *coding* would have been fine; the modeling step "earns its keep" as
complexity grows — i.e. vibe modeling is insurance whose value scales with the system, not a mandate for
every toy app.

## What "vibe coding" means (the term it answers)

[[martin-fowler]] pins down the contrast vibe modeling reacts to ([[fowler-agentic-programming]]): with
**vibe coding** humans *don't look at the code, indeed they forget it exists*; that is what
distinguishes it from **agentic programming**, where humans still review the code in detail. Vibe
modeling targets exactly the gap Fowler's definition exposes — if nobody inspects the code, the
**event model becomes the artifact stakeholders *can* inspect and agree on**, restoring the shared
structure vibe coding discards.

## Related

[[event-modeling]] · [[agentic-coding]] · [[spec-driven-development]] · [[event-modeled-agent-design]] ·
[[given-when-then]] ·
[[model-as-code-vs-model-as-language]]

_Sources: [[event-modeling-event-sourcing-podcast]] · [[fowler-agentic-programming]] · [[dilger-flea-market-model-to-deploy]]._
