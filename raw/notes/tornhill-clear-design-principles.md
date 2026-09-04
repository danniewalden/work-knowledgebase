---
source_url: https://adamtornhill.substack.com/p/clear-software-design-principles
title: "CLEAR: Software Design Principles for the Agentic Age"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-06-09
retrieved: 2026-06-17
type: note
---

> Provenance note — this is a SUMMARY in the compiler's own words (not a verbatim capture; the
> source is a personal Substack publication). Read the original at the URL above.

Adam Tornhill proposes **CLEAR**, a small set of design principles for *AI-readable code* — code
that is safe for agents to evolve and cheap for humans to verify. Framing: SOLID was created for a
different optimization target (human maintainability); agentic development introduces a new
bottleneck he calls **reconstruction work** — an agent must infer structure from local context by
search, tool use, and statistical guesswork, so code can satisfy SOLID yet still be hard for an agent
to reason about when intent, ownership, and change boundaries are implicit. The unifying goal is to
**limit the blast radius** of a change.

The five principles:
- **C — Conceptual alignment:** align behavior with the domain concepts it belongs to.
- **L — Local reasoning:** enable reasoning from local context, for humans and agents.
- **E — Explicit intent:** make the code's purpose visible structurally.
- **A — Avoid search luck:** express similar problems with consistent structures/patterns/extension points.
- **R — Reduce the edit surface:** design to contain change by making boundaries explicit.

He positions CLEAR as a *re-emphasis of classics* (Tell Don't Ask, Law of Demeter, DDD, Parnas's
information hiding) that matter more under agentic coding, not novelty for its own sake; principles,
not rules, because good design must stay mouldable to the domain. Says the series so far covered the
"CLE"; "AR" posts are upcoming. Companion refactoring articles map to each principle (e.g. "Make the
Domain Explicit" → Conceptual alignment; "Reveal Intent in Complex Conditions" → Local reasoning;
"Hidden Design Decisions: Refactoring Control Coupling" → Explicit intent).
