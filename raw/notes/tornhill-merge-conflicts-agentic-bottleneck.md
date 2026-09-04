---
source_url: https://adamtornhill.substack.com/p/why-merge-conflicts-became-the-new
title: "Why Merge Conflicts became the new Agentic Bottleneck"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-06-02
retrieved: 2026-06-17
type: note
---

> Provenance note — SUMMARY in the compiler's own words (personal Substack; not a verbatim capture).
> Read the original at the URL above.

Thesis: **agentic coding reinforces software-engineering fundamentals** — the less humans hand-code,
the more design/architecture and a **socio-technical fit** matter, because coordinating multiple agents
in one codebase puts pressure on the architecture. **Recurring merge conflicts are a socio-technical
signal**, and it doesn't matter that the "social agent" is now an AI agent. The industry reaction —
stacked PRs, PR queues, intelligent conflict resolution — patches symptoms rather than the root cause,
which is usually *technical*: "no org chart can dig you out of an architectural blob."

The mechanism (Brooks, *The Mythical Man-Month*): coordination cost grows quadratically (n(n-1)/2);
work parallelizes only when tasks are **independent at the level of the problem domain** — and that
independence must also exist **in the code**. Separate features/workflows/capabilities need separate
*homes* in the design (domain-aligned), or two "independent" tasks collide in the same code. Recurring
merge conflicts are "the canary" telling you the work you do is misaligned with the work your
architecture supports. He cites the leaked Claude Code repo as architectural convergence — an
`extractToolStats()` accreting git analytics, diffs, telemetry, UX timing — so unrelated changes (human
or agent) collide in the same function. GenAI "delivered on the 10x promise" for merge conflicts via
sheer speed.

Tool: **behavioral code analysis** (from *Your Code as a Crime Scene* / *Software Design X-Rays*) makes
coordination cost visible — **hotspots** (change-pressure areas), **coordination analysis** (many
contributors competing for the same area), **change coupling** (boundaries that fail to support
independent evolution). It gives evidence/priorities, not fixes. Typical remedies: break an
author-congested hotspot along domain boundaries; consolidate a local change-coupling cluster into one
package (low package cohesion); and the bad one — change coupling across architectural elements,
usually caused by **technical** separation of concerns (MVC/MVP-thin layering) rather than building
blocks that communicate domain concepts. None are quick fixes, but without them parallel agents stop
adding speed and become a serial bottleneck.
