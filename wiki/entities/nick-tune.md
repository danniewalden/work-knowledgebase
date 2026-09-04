---
title: Nick Tune
type: entity
created: 2026-06-14
updated: 2026-09-02
sources: [nick-tune-graphs-memory-skills-agents, nick-tune-enforced-application-architecture-agents-humans]
tags: [person, context-engineering, ddd, agentic-ai, fitness-functions, focus]
---

# Nick Tune

Software architect / staff engineer and a well-known **domain-driven-design** ([[domain-driven-design]])
author and speaker. In this KB he appears as a watch-listed practitioner voice on **agent substrate /
[[context-engineering]]**: his post [[nick-tune-graphs-memory-skills-agents]] frames **Graph + Memory +
Skills + Agent** as the building blocks underneath any agent and argues for a **queryable system graph**
over agents grepping around (to reason about state and the blast radius of a change). Added to
`watch-config.json`; most of his other recent feed is reposts of AI-sovereignty news (off-thread).

His **queryable-graph** substrate is the same instinct [[jeremiah-lowin]] argues at the orchestration
level in [[prefect-loops-vs-graphs]] — both hold that an **explicit, traversable graph beats agents
making it up as they go** — so he sits adjacent to the [[graph-engineering]] concept (Tune models the
*system/state* graph agents reason over; Lowin models the *control-flow* graph agents run inside).

## The enforcement turn (2026-08, ingested 2026-09-02)

His second contribution here is sharper and more consequential than the first, because it is a **worked
mechanism rather than a framing**: [[nick-tune-enforced-application-architecture-agents-humans]]
(2026-08-13) starts from the flat premise that agents ignore architectural guidance written in *"skill
files, ADRs, and various other places in the repo"* — *"AI does dumb stuff like that all the time even
with a million lines of markdown screaming at it not to do that"* — and answers it by making violations
**fail the build**, via his own DSL (**Rivière**) in three tiers: package classification, layer import
rules, and role-based rules with per-role shape constraints.

That puts him in a position neither side of [[model-as-code-vs-model-as-language]] occupies: the
authoritative artifact is neither a model file nor the code's content, but the **constraint the code
must satisfy**. It also extends [[fitness-functions]] past the limit
[[fowler-bockeler-maintainability-sensors|Böckeler's field report]] identified (that such rules can
only express what imports, file names and folders allow), and makes
[[vertical-slice-architecture]] a build-enforced invariant rather than a convention.

Note the interested-party marker: Rivière is **his own tool**, the post is a series instalment ending
"get in touch," and it carries no before/after measurement — precise mechanism, asserted payoff. He is
also candid that the deepest tier is unmeasured — *"still playing around with that. Come back in 6
months. I feel confident it's the right approach"* — i.e. unsure of the payoff, not the direction.

## Related

[[fitness-functions]] · [[model-as-code-vs-model-as-language]] · [[vertical-slice-architecture]] ·
[[slice]] · [[adr]] · [[business-capabilities]] · [[domain-driven-design]] · [[context-engineering]] ·
[[graph-engineering]]

_Source pages: [[nick-tune-graphs-memory-skills-agents]] ·
[[nick-tune-enforced-application-architecture-agents-humans]]._
