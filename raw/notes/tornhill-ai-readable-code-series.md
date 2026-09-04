---
source_url: https://adamtornhill.substack.com/archive
title: "Code for Humans and Machines — AI-Readable Code series (backlog index)"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-04-19/2026-06-16
retrieved: 2026-06-17
type: note
---

> Provenance note — compiler index of the series from the public archive (post titles + subtitles).
> Personal Substack; full posts not reproduced. The two in-window posts and CLEAR have their own
> detailed notes/pages; this indexes the rest of the "AI-Readable Code" series for context.

Tornhill's Substack "Code for Humans and Machines" is a running series on designing/refactoring code so
that AI agents can read, reason about, and safely modify it. The arc (newest→oldest) per the archive:

- **Hidden Design Decisions: Refactoring Control Coupling** (Jun 16) — boolean flags hide design
  decisions (control coupling); replace with Strategy + a domain type. *(own note/page)*
- **CLEAR: Software Design Principles for the Agentic Age** (Jun 9) — the five named principles.
  *(own page: tornhill-clear-design-principles-agentic-age)*
- **Why Merge Conflicts became the new Agentic Bottleneck** (Jun 2) — merge conflicts as a
  socio-technical signal; behavioral code analysis. *(own note/page)*
- **A Blast from the Past: SDD and the Illusion of Known Scope** (May 28) — "implementation was never
  just typing; it's discovery and learning. Tooling changed, human problem solving didn't." A caution on
  spec-driven development assuming scope is known up front.
- **Make the Domain Explicit: From Procedural Mess to Local Reasoning** (May 21) — breaking apart a
  procedural blob so humans/agents reconstruct less before a safe change. *(the CLEAR "Conceptual
  alignment" worked example)*
- **How Much of my Writing is AI-Generated?** (May 19) — meta/process reflection ("writing is learning;
  LLMs remove that component"). Off the code-design thread.
- **Reveal Intent in Complex Conditions** (May 14) — extraction alone is useless; naming makes the
  difference; refactor complex conditions for agentic coding. *(the CLEAR "Local reasoning" example)*
- **Compressed Cognition: The Cost of Faster Coding** (May 7) — agentic coding *collapses the timeline
  of software decisions*; speed is paid for in **decision density and mental energy**. (Most-shared
  post of the series.)
- **Kill the Conditional Maze: From If-Statements to Rule Pipelines** (May 5) — refactor tangled
  if-chains into composable rules that scale with change.
- **Coding Is Dead (…But It Still Smells Funny)** (Apr 26) — the post-AI developer role/skillset;
  design smells persist even when humans write less code.
- **Refactoring: Express Selections as Tables** (Apr 23) — replace selection logic buried in
  conditionals with table-driven dispatch.
- **How Long Should a Function Be? (And Why It's the Wrong Question)** (Apr 21) — focus on whether code
  communicates intent, not line count.
- **Welcome to Code for Humans and Machines!** (Apr 19) — manifesto: software that stays understandable
  to humans while being machine-legible and transformable by agents.

Common thread: classic design discipline (cohesion, information hiding, naming, intent) re-justified
because agents pay — in tokens, reconstruction work, merge conflicts, and errors — for code that hides
its intent. The refactoring posts (May 14/21, May 5, Apr 23) are the worked examples that CLEAR (Jun 9)
later generalized into named principles.
