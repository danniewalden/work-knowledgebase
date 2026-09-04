---
title: "Willison — sqlite-utils 4.0rc2, mostly written by Claude Fable ($149.25)"
type: source
created: 2026-07-18
updated: 2026-07-18
sources: [willison-sqlite-utils-4-mostly-written-by-fable]
raw_file: [raw/articles/willison-sqlite-utils-4-mostly-written-by-fable.md]
tags: [agentic-coding, loop-engineering, maker-checker, llm-pricing, focus]
---

# Willison — sqlite-utils 4.0rc2, mostly written by Claude Fable ($149.25)

Source: [[simon-willison]], *"sqlite-utils 4.0rc2, mostly written by Claude Fable (for about $149.25)"*,
simonwillison.net, **2026-07-05** (annotated-release-notes entry). Raw capture:
`raw/articles/willison-sqlite-utils-4-mostly-written-by-fable.md`. A worked, real-world instance of the
**maker≠checker verification loop** on his own OSS project.

## Summary

Willison drives a coding agent (Claude Fable, via Claude Code for web) to take `sqlite-utils` from 4.0rc1
to a release he "felt truly comfortable about," and documents the loop mechanics and the cost. The
story's value is the **layered verification**: the model reviews its own release, then a *different*
model reviews that work, and the surviving bugs feed a fresh session.

## Key points

- **The agent as its own first reviewer.** A single prompt — "final review before shipping a stable 4.0…
  spot any last-minute breaking changes" — produced a report flagging **5 "release blockers,"** the worst
  a `delete_where()` bug that never committed and **poisoned the connection (silent data loss)**. Clearing
  the feedback took **37 prompts, 34 commits, +1,321 / −190 across 30 files.**
- **Cross-model review really works.** Willison then had **Codex / GPT-5.5 (xhigh)** review Fable's work —
  "I used to think having one model review another was superstitious… the problem is *it really does
  work*." It surfaced **2 more P1 transaction-semantics bugs** (a `db.query("update…")` that raised
  `ValueError` *after* already committing; an `INSERT … RETURNING` that only committed if the generator
  was exhausted). These were pasted into a **fresh Fable session** that reproduced and fixed them — a
  concrete **maker≠checker** (and cross-vendor checker) loop in the wild.
- **Review the docs first.** "Reviewing the documentation edits first is an *excellent* way to build an
  initial understanding of what has changed" — reading the doc diff before the code diff is his method for
  regaining comprehension (ties to [[willison-understand-to-participate]]).
- **Release notes are ideal agent-outsourceable work.** "Release notes are a great example of writing I'm
  OK to outsource to agents because they need to be boring, predictable and accurate" — and having the
  agent append to an "Unreleased" changelog section as each change lands makes the changelog's commit
  history a running summary.
- **Harder tasks parallelize the human.** Because the agent needs 10–15 min to churn, harder tasks give
  *more* room to do other things (he prompted next steps from his phone at a July-4th parade).
- **A rare concrete cost datapoint.** Itemized via **AgentsView** run inside the session: **$149.25** total
  (main Fable session $141.02 + four Fable subagents ~$1.4–2.4 each + an Opus prompt-counting agent
  $0.32). He notes he "should have leaned more heavily into subagents with cheaper models."

## Why it matters

The cleanest worked example the KB has of the **verification / maker≠checker loop**
([[langchain-the-art-of-loop-engineering]], grader loop) applied to real OSS maintenance — and it extends
it to **cross-model review** (one vendor's model checking another's) as a habit that catches P1 bugs a
single model misses. Reinforces the "independent check decides done" principle of
[[addyosmani-own-the-outer-loop]] and [[willison-directly-responsible-individuals]] (Willison stays the
reviewer/DRI: he did the final GitHub PR review himself). Also a rare itemized **agentic-coding cost**
datapoint for the token-economics thread ([[tornhill-codescene-unhealthy-code-agentic-token-cost]],
[[willison-rewriting-bun-in-rust]] ≈$165k). Caveat: single project, single author, promotional-adjacent to
the Fable subscription; costs are estimated unsubsidized.

## Links

[[simon-willison]] · [[agentic-coding]] · [[loop-engineering]] · [[langchain-the-art-of-loop-engineering]] ·
[[addyosmani-own-the-outer-loop]] · [[willison-directly-responsible-individuals]] ·
[[willison-rewriting-bun-in-rust]] · [[tornhill-codescene-unhealthy-code-agentic-token-cost]]

_Source: [[willison-sqlite-utils-4-mostly-written-by-fable]] (raw: `raw/articles/willison-sqlite-utils-4-mostly-written-by-fable.md`)._
