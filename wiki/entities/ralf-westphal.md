---
title: Ralf Westphal
type: entity
created: 2026-08-03
updated: 2026-08-03
sources: [fritzsche-command-context-consistency-principle]
tags: [person, command-context-consistency, event-sourcing, substrate]
---

# Ralf Westphal

Software architect and long-time .NET author/trainer (co-founder of the "Clean Code Developer"
initiative). In this KB he appears as the **coiner of [[command-context-consistency|Command Context
Consistency]] (CCC)** — described against an event store as "the context is all the events relevant for a
command during the consistency check," with a command's events recorded only after the same query
confirms no new context events arrived.

[[rico-fritzsche]] credits Westphal with the name and generalizes the rule to be **store-agnostic**
([[fritzsche-command-context-consistency-principle]]); it is the same commit-time condition
[[sara-pellegrini|Pellegrini]] expresses for event stores as the
[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]].

## Where he appears

- [[fritzsche-command-context-consistency-principle]] — credited as CCC's coiner; the canonical CCC page.
- [[fritzsche-why-your-software-cannot-explain-business-decisions]] — CCC stated jointly ("as described by
  Ralf Westphal and me").

_Original source: Ralf Westphal, "Command Context Consistency" (ralfwestphal.substack.com), cited in
[[fritzsche-command-context-consistency-principle]]; not separately captured in `raw/`._
