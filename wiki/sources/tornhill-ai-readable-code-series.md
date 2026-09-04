---
title: "Adam Tornhill — Code for Humans and Machines (AI-Readable Code series)"
type: source
created: 2026-06-17
updated: 2026-06-17
sources: [tornhill-ai-readable-code-series]
raw_file: [raw/notes/tornhill-ai-readable-code-series.md]
tags: [ai-readable-code, agentic-coding, refactoring, focus]
---

# Adam Tornhill — Code for Humans and Machines (AI-Readable Code series)

Consolidated index/summary of **[[adam-tornhill]]**'s Substack series "Code for Humans and Machines"
(Apr–Jun 2026), beyond the three posts with their own pages
([[tornhill-clear-design-principles-agentic-age|CLEAR]],
[[tornhill-hidden-design-decisions-control-coupling|Hidden Design Decisions]],
[[tornhill-merge-conflicts-agentic-bottleneck|Merge Conflicts]]). Index at
`raw/notes/tornhill-ai-readable-code-series.md` (post titles/subtitles; personal Substack, not
reproduced).

## The series in brief

A running body of work on designing and refactoring code so agents can read, reason about, and safely
change it — classic design discipline (cohesion, information hiding, naming, intent) re-justified for
the agent era. The **refactoring walkthroughs** are the worked examples that
[[tornhill-clear-design-principles-agentic-age|CLEAR]] later generalized into named principles:

- **Make the Domain Explicit: From Procedural Mess to Local Reasoning** (May 21) — the CLEAR
  *Conceptual alignment* example; reduce what humans/agents must reconstruct before a safe change.
- **Reveal Intent in Complex Conditions** (May 14) — the CLEAR *Local reasoning* example; "extraction
  alone is useless — naming makes the difference."
- **Kill the Conditional Maze: From If-Statements to Rule Pipelines** (May 5) — refactor tangled
  conditionals into composable rules.
- **Refactoring: Express Selections as Tables** (Apr 23) — table-driven dispatch over buried selection
  logic.
- **How Long Should a Function Be?** (Apr 21) — the wrong question; what matters is whether code
  communicates intent.
- **An Opinionated (and Mainly Correct) Guide to Naming** (Jun 23 — now its own page,
  [[tornhill-opinionated-guide-to-naming]]) — naming as cognitive compression; name for the call site,
  Wishful Thinking, domain types over primitives, drop `I`-prefix/get-set/dumpster names; cites an LLM
  study finding identifier-name improvements "yielded the largest returns."

The **thesis / reflection** posts:

- **Compressed Cognition: The Cost of Faster Coding** (May 7, the series' most-shared) — agentic coding
  *collapses the timeline of software decisions*; speed is paid for in **decision density and mental
  energy**. A counter-weight to naive "faster is better" framing.
- **A Blast from the Past: SDD and the Illusion of Known Scope** (May 28) — a caution on
  [[spec-driven-development]]: "implementation was never just typing — it's discovery and learning";
  tooling changed, human problem-solving didn't.
- **Coding Is Dead (…But It Still Smells Funny)** (Apr 26) — the post-AI developer role; design smells
  persist when humans write less code.
- **Welcome to Code for Humans and Machines!** (Apr 19) — the manifesto: software legible to humans *and*
  machine-transformable by agents.
- (Off-thread: **How Much of my Writing is AI-Generated?**, May 19 — a writing-process reflection.)

## Why it matters here

The body of evidence behind [[ai-readable-code]] and [[adam-tornhill]]'s entity page: shows CLEAR was
distilled from concrete refactorings, and adds two notable cross-thread points — **Compressed Cognition**
(a wellbeing/decision-density caution that complements the speed-vs-quality story in
[[agentic-coding]]) and **SDD and the Illusion of Known Scope** (a pragmatic challenge to the
[[spec-driven-development]] "spec-first" optimism of [[martin-dilger]] et al., worth holding alongside
it). Reinforces [[agent-legibility]], [[locality-of-reference]], and [[balanced-coupling]].

## Caveats

Index-level summary from public titles/subtitles (+ the two full in-window posts); individual
walkthroughs not read in full. Personal Substack.
