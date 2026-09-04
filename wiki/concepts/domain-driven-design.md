---
title: Domain-Driven Design (DDD)
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [semaphore-dymitruk-event-modeling, tune-no-rapport-with-a-model-you-didnt-code]
tags: [ddd, software-design, methodology, agentic-ai]
---

# Domain-Driven Design (DDD)

A software development approach that **matches code components to the business/application
domain** and unifies the language of domain experts and developers so terminology stays
consistent within each area.

## Relationship to Event Modeling

Per [[adam-dymitruk]] ([[semaphore-dymitruk-event-modeling]]), [[event-modeling]] represents
DDD on the blueprint through **swimlanes** — arranged to separate physical systems and
logical subsystems while preserving each area's subject-matter language (e.g. inventory vs.
invoicing). This connects to the step in event modeling where [[conways-law|Conway's Law]] is
applied to give teams ownership of autonomous parts of the system.

## Can you model with an agent? The rapport problem (Tune, 2026-08-28)

The open question DDD faces in the agent era, stated by [[nick-tune]]
([[tune-no-rapport-with-a-model-you-didnt-code]]): agents are *"not that good at [domain modelling] by
default,"* and — the claim that outlives that — *"discussing and refining a domain model is not the same
as writing the lines of code yourself. I don't feel as connected, I don't feel that the model is as
deeply embedded in my mind as it would be if I wrote the code. **And that means the domain model is
going to be worse** because I'm clearly missing some nuances that could lead to big modelling
breakthroughs."* His conclusion: *"I'm struggling to see how to get the same level of rapport with the
model without actually writing the code. **Maybe it's not even possible.**"*

The implicit premise is worth naming: **writing the code was a mode of thinking about the domain**, not
a transcription step — which is precisely what [[spec-driven-development]] assumes away, and what
[[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill's "SDD and the Illusion of Known
Scope"]] attacks from the implementation side ("implementation is an essential part of the discovery
process itself").

Two counter-considerations the post does not raise. **DDD already had this problem**: [[event-storming]]
and [[domain-discovery]] exist because a *group* must reach rapport with a model no single member typed,
and ubiquitous language is the mechanism for transferring it. Whether those formats extend to a
human/agent pair is the open question — and the KB's candidate answer is to keep the modelling act and
delegate only the typing ([[event-modeling]], [[model-as-code-vs-model-as-language]],
[[event-modeled-agent-design]]). Second, [[tornhill-beyond-lambdas-raising-the-abstraction-level|naming
the domain into the code]] is the mechanism for encoding whatever insight you do have into code an agent
typed; it does not manufacture the insight. **Thin capture** — a short LinkedIn post; a quality claim
inferred from a stated feeling, and unobservable by construction (a missed breakthrough leaves no
trace). See [[comprehension-debt]] and [[verification-burden]].

## Related

[[event-modeling]] · [[event-sourcing]] · [[business-capabilities]] (capabilities as stable
boundaries — a sibling lens to bounded contexts) · [[open-closed-principle]] · [[event-storming]] ·
[[conways-law]] · [[vibe-modeling]] · [[comprehension-debt]] · [[verification-burden]] ·
[[nick-tune]] · [[domain-discovery]] · [[entity-centric-thinking]]

_Source pages: [[semaphore-dymitruk-event-modeling]] · [[tune-no-rapport-with-a-model-you-didnt-code]]._
