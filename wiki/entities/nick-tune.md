---
title: Nick Tune
type: entity
created: 2026-06-14
updated: 2026-09-04
sources: [nick-tune-graphs-memory-skills-agents, nick-tune-enforced-application-architecture-agents-humans, tune-no-rapport-with-a-model-you-didnt-code, nick-tune-event-sourced-claude-code-workflows]
tags: [person, context-engineering, ddd, agentic-ai, fitness-functions, comprehension-debt, focus]
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

## Event-sourced agent loops (2026-03-04)

[[nick-tune-event-sourced-claude-code-workflows]] is the third of a series (workflows as state machines
→ declarative DSLs → fully event-sourced, the last suggested to him by **Yves Reynhout**) and the KB's
only source that applies [[event-sourcing]] to the **agent loop** rather than to the domain: persist
only events, derive state by replay, and read per-state dwell time, rejection counts and hook-denial
counts off the log — then feed the events back to Claude to rewrite the harness. Code in his
`autonomous-claude-agent-team` repo. **NOT INDEPENDENT · IMPRESSION NOT MEASUREMENT** — his own harness,
personal projects, and the *"15 minutes in RESPAWN vs 2 minutes DEVELOPING"* reading is from one
session, which he states himself; the *"I've seen great results on real projects"* claim carries no
number.

## The rapport problem — a stated open problem, not a mechanism (2026-08-28)

His third written contribution is unlike the other two: no DSL, no substrate, no proposal.
[[tune-no-rapport-with-a-model-you-didnt-code]] reports that agents are *"not that good at [domain
modelling] by default (that's the nice way of putting it)"* — and then makes the sharper claim, which
survives the agents getting better: *"discussing and refining a domain model is not the same as writing
the lines of code yourself. I don't feel as connected… **And that means the domain model is going to be
worse** because I'm clearly missing some nuances that could lead to big modelling breakthroughs."*
Ending: *"I'm struggling to see how to get the same level of rapport with the model without actually
writing the code. **Maybe it's not even possible.**"*

This relocates the [[verification-burden]] from review to **modelling**: the loss happens before there
is code to read, so no review regime, test boundary or agent reviewer addresses it — and it is
**unobservable**, since a modelling breakthrough that didn't happen leaves no trace. It is the KB's only
suggestion that [[comprehension-debt]] may be **unpayable** rather than merely unpaid. **Thin capture**:
a short LinkedIn post, no evidence, and a quality claim inferred from a stated feeling — a hypothesis
with a named mechanism, not a finding.

### Hold his positions together; the pair is the interesting thing

He instruments and automates the **loop** to the point of having an agent optimise its own harness, and
he makes violations of architecture **fail the build** — while doubting he can build rapport with a
**domain model** he did not hand-code. That is a **boundary claim: delegate the process, author the
model**, and it is the most fully articulated third voice in
[[model-as-code-vs-model-as-language]]. Two consequences worth stating:

- It cuts against the [[martin-dilger]] / [[eventmodelers-ai]] thesis that a sufficiently good spec DSL
  lets agents do the modelling.
- It sits in tension with his own [[nick-tune-enforced-application-architecture-agents-humans|Rivière]]
  work: build enforcement guarantees the *shape* of code nobody wrote, and **nothing in a build enforces
  modelling insight.**

## Related

[[fitness-functions]] · [[model-as-code-vs-model-as-language]] · [[vertical-slice-architecture]] ·
[[slice]] · [[adr]] · [[business-capabilities]] · [[domain-driven-design]] · [[context-engineering]] ·
[[graph-engineering]] · [[verification-burden]] · [[comprehension-debt]] · [[vibe-modeling]]

_Source pages: [[nick-tune-graphs-memory-skills-agents]] ·
[[nick-tune-enforced-application-architecture-agents-humans]] ·
[[nick-tune-event-sourced-claude-code-workflows]] (2026-03-04) ·
[[tune-no-rapport-with-a-model-you-didnt-code]] (2026-08-28)._
