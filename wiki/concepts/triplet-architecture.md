---
title: Triplet Architecture
type: concept
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-triplet-flexible-agent-enabled-architecture, dilger-slicing-keeps-the-cost-curve-flat, dilger-local-llm-distributed-agent-setup-event-modeling, dilger-dcb-is-what-event-sourcing-should-have-been, dilger-event-modeling-agent-harness, dilger-hold-my-beer-engineer]
tags: [event-modeling, event-sourcing, vertical-slice-architecture, architecture, agentic-coding, focus]
---

# Triplet Architecture

**[[martin-dilger]]'s name for using three things *in union* rather than separately:
[[event-modeling]] to plan, [[vertical-slice-architecture|vertical slices]] to structure,
[[event-sourcing]] to store.** Named in his *Event Modeling applied* newsletter
([[dilger-triplet-flexible-agent-enabled-architecture]], 2026-07-26), explicitly "heavily inspired by the
work of [[adam-dymitruk]]", and now hashtagged as `#tripletarchitecture` on most of his posts.

| Block | Role | What it contributes |
| --- | --- | --- |
| **[[event-modeling]]** | plan | The blueprint, built collaboratively, detailed enough to generate most of the code |
| **[[vertical-slice-architecture]]** | structure | The decomposition the blueprint lands in — one [[slice]] per step |
| **[[event-sourcing]]** | store | The record that keeps the *why*, and makes state a replay rather than an overwrite |

The claim is not that any of the three is new. It is that **each one fails to deliver on its own**, and
the combination is what produces a flexible, agent-enabled system.

## The argument

**The root problem is coupling, and it compounds.** Hexagonal, onion and layered architectures assume you
already know your boundaries — they give you a tidy place to *put* a boundary once someone decides it,
but no help *finding* it. Agile addresses the process and says nothing about the technology underneath.
Nobody stands in that gap, so the boundary gets decided implicitly "by whoever was loudest or most senior
that day." That rework never appears as rework; it appears as a project that is always slightly behind.

**Requirements are part of the architecture.** Not a softer discipline that happens first. If the shared
understanding is wrong, clean code just gives you *"a well-organized version of a mistake."*

**The payoff is a flat cost curve**, stated as the point of architecture at all
([[dilger-slicing-keeps-the-cost-curve-flat]], 2026-08-29):

> "Building a feature in 5 years costs exactly as much or less as today. That's the only purpose of
> architecture… Every feature added adds friction. The reason is coupling that slowly accumulates."

## Why it matters to the agent thread

This is the page's real reason to exist: the Triplet is the **structural precondition** under most of
what [[event-modeled-agent-design]] claims, and it is usually cited in passing rather than explained.

- **The agent seam.** An agent works one [[slice]], needing only that slice's context plus the event log
  and the model — so *adding agents makes delivery faster rather than slower*. That property is what
  makes [[dilger-event-modeling-agent-harness|his 24/7 harness]] possible at all, and it is why the
  board-level claim-lock works without code-level coordination
  ([[dilger-local-llm-distributed-agent-setup-event-modeling]]).
- **Slicing is a specification-time activity, not a refactoring one.** *"This must happen while
  specifying already."* Slicing after the fact does not produce the property.
- **The AI-specific stake.** *"This is what makes working with AI so hard in grown code bases. Attempting
  Spec-Driven-Development without having a solution to this is like playing russian roulette. Play it
  long enough and you'll inevitably loose."* (sic) That is the sharpest version in the KB of why
  [[spec-driven-development]] is not sufficient on its own — the spec has nowhere clean to land.
- **"Slices are like Candy for AI."** The token-economics claim, which [[jeremy-miller]] arrives at
  independently from the other side of [[model-as-code-vs-model-as-language]] — and which neither of them
  has measured.

## Relationship to the substrate pages

The Triplet is a **packaging**, and each block has its own page with its own evidence and its own
disputes; this page should not restate them:

- Event sourcing's consistency model is itself contested — Dilger holds that
  [[dynamic-consistency-boundaries|DCB]] "is what event sourcing should have been"
  ([[dilger-dcb-is-what-event-sourcing-should-have-been]]), which changes the *store* block's shape.
- [[rico-fritzsche]]'s [[autonomous-domain-capabilities|RPU]] / [[command-context-consistency|CCC]] work
  reaches a similar destination — an explicit decide-path owning its own context — from a different
  direction and without the Event Modeling front half. Whether the Triplet and CCC are the same
  architecture under two vocabularies is genuinely open, and worth settling.
- The flat-cost-curve claim is the same [[open-closed-principle]] argument that underlies Event Modeling
  generally: new features *add* code rather than modify shared code. See [[slice]].

## Evidential status

**Vendor framing, coherent, unmeasured.** Every capture is Dilger's own, most of them LinkedIn marketing
for [[eventmodelers-ai]] and the *Spec Driven* book. What raises it above assertion is the running
instance — 3× on-prem machines, 6–10 agents in [[ralph-loop|ralph-loops]] 24/7, slices claim-locked on a
board — which is a real system doing real work, described in enough mechanical detail to be checked by
anyone willing to build it. What is missing is any comparison: no team has reported building the same
thing twice, once with the Triplet and once without, and the cost-curve claim is by construction a
five-year claim that nobody has held still long enough to test.

## Open questions

- **Is the union necessary, or is slicing doing the work?** He claims the three only pay off together,
  but the agent-parallelism evidence is entirely about slices, and the event log's role in it is
  audit-and-replay rather than decomposition. A slices-plus-event-sourcing system without the Event
  Modeling front half would be the natural control.
- **What breaks first at scale?** All captured instances are small teams or one person with many agents.
  Nothing describes the Triplet in an organisation with several teams sharing a context.
- **Is the detailed Triplet article captured?** The 2026-08-29 post links one behind an `lnkd.in`
  shortlink that has never resolved. [[dilger-triplet-flexible-agent-enabled-architecture]] is the
  newsletter version; whether there is a fuller article behind that link is still open.

## Related

[[event-modeling]] · [[vertical-slice-architecture]] · [[event-sourcing]] · [[slice]] ·
[[event-modeled-agent-design]] · [[dynamic-consistency-boundaries]] · [[autonomous-domain-capabilities]] ·
[[spec-driven-development]] · [[open-closed-principle]] · [[martin-dilger]] · [[eventmodelers-ai]] ·
[[agent-harness]]

_Sources: [[dilger-triplet-flexible-agent-enabled-architecture]] ·
[[dilger-slicing-keeps-the-cost-curve-flat]] ·
[[dilger-local-llm-distributed-agent-setup-event-modeling]] ·
[[dilger-dcb-is-what-event-sourcing-should-have-been]] · [[dilger-event-modeling-agent-harness]] ·
[[dilger-hold-my-beer-engineer]]._
