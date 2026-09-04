---
title: Jimmy Bogard
type: entity
created: 2026-06-14
updated: 2026-09-04
sources: [bogard-vertical-slice-architecture, bogard-vertical-slice-architecture-webinar-recording-whats-next]
tags: [person, architecture, cqrs, ddd, dotnet, agentic-coding]
---

# Jimmy Bogard

.NET architect and OSS author (creator of **AutoMapper** and **MediatR**); originator of the term
[[vertical-slice-architecture|Vertical Slice Architecture]] ([[bogard-vertical-slice-architecture]],
2018). He arrived at VSA by moving a long-term project off onion architecture toward [[cqrs]] and
organizing code by feature slices rather than layers, and has taught DDD-with-VSA training since. Still
shipping AutoMapper/MediatR on a quarterly cadence (as of early 2026).

In the KB he anchors the [[vertical-slice-architecture]] concept — the architecture that
[[event-modeling]]'s vertical slices (and the agent "slice" task unit in
[[jwilger-agent-skills-event-modeling]] / [[dilger-model-is-a-living-spec-always-on-agent]]) map onto.

## Now teaching VSA as AI guardrails (2026-09)

[[bogard-vertical-slice-architecture-webinar-recording-whats-next]] (2026-09-01) is the first time the
KB has **the pattern's originator** connecting it to agentic development: a Codeartify webinar with 700+
registrations titled *"Vertical Slice Architecture: Effective Guardrails for AI Development"*, plus a
six-hour two-part course and a Zurich workshop (17–18 Nov). His argument in three sentences: "we've made
**writing** code nearly free and left the cost of **verifying and changing** it exactly where it was…
**An agent doesn't read your architecture diagram. It reads your repo and copies what it finds.** That's
why structure matters more now, not less. Slices hold up under an agent because a change fits in one
context window, the blast radius stops at the slice boundary, and the tests still mean something after a
refactor."

That middle sentence is the KB's best one-line statement of why an advisory boundary fails and a
structural one doesn't — the missing rationale under
[[nick-tune-enforced-application-architecture-agents-humans|Tune's build-time enforcement]]. Caveats: a
~350-word promotional post selling training, **no measurement**, and the substance is in an uncaptured
recording. The condition it omits is [[fritzsche-vsa-does-not-fix-entity-centered-thinking|Fritzsche's]]:
a CRUD-shaped slice bounds nothing.

## Related

[[slice]] · [[model-as-code-vs-model-as-language]]

_Source pages: [[bogard-vertical-slice-architecture]] ·
[[bogard-vertical-slice-architecture-webinar-recording-whats-next]]._
