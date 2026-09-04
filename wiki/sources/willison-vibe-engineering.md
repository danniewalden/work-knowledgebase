---
title: "Willison — Vibe engineering (the origin of the term)"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [willison-vibe-engineering]
raw_file: [raw/articles/willison-vibe-engineering.md]
tags: [agentic-coding, coding-agents, loop-engineering, definitions, vibe-coding, agentic-engineering, term-lineage]
---

# Willison — Vibe engineering

Blog post by **[[simon-willison]]** (simonwillison.net, **2025-10-07**), part of his "How I use LLMs
and ChatGPT" series. The **origin/coinage post** for the term **"vibe engineering"** — the accountable
counterpart to [[vibe-modeling|vibe coding]]. Source file: `raw/articles/willison-vibe-engineering.md`.
This is the dated precursor to his later living guide [[willison-agentic-engineering-patterns|Agentic
Engineering Patterns]]; kept as its own page because it is the term's naming primary and carries the
lineage note below.

## Core thesis

Vibe coding is now well-established as "the fast, loose and irresponsible way of building software with
AI — entirely prompt-driven, with no attention paid to how the code actually works." That leaves a
**terminology gap** for the opposite end: "seasoned professionals accelerate their work with LLMs while
staying **proudly and confidently accountable** for the software they produce." Willison proposes
**vibe engineering** for it, "with my tongue only partially in my cheek" — the self-contradictory
"vibes"+"engineering" mismatch is deliberate, meant to be sticky and to do a little productive
gatekeeping. He explicitly frames this as harder, not easier, than vibe coding.

## The term-lineage note (why this page exists standalone)

An inline **update dated 2026-02-23** records that the field **settled on "Agentic Engineering"**
instead: *"It looks like the term 'Agentic Engineering' is coming out on top for this now. I have a new
tag for that and I'm working on a not-quite-a-book."* So the naming trail the KB tracks is:
**Willison "vibe engineering" (Oct 2025) → the ecosystem's "agentic engineering" (by Feb 2026)** — the
same tag under which his [[willison-agentic-engineering-patterns|patterns guide]] (started 2026-02-23,
i.e. the same week) now lives, and the practitioner counterpart to [[martin-fowler]]'s "agentic
programming" ([[fowler-agentic-programming]]). This post is where the "vibe" strand of that vocabulary
starts. See [[agentic-coding]] for the settled boundary.

## LLMs reward top-tier engineering practice

The post's substantive claim: coding agents (Claude Code, Codex CLI, Gemini CLI — tools that "iterate
on code, actively testing and modifying it until it achieves a specified goal") **amplify existing
senior-engineer skill**. The practices they reward are exactly the ones seniors already have:

- **Automated testing** — a robust, stable suite lets agents "fly"; **test-first is particularly
  effective with agents that can iterate in a loop** (the verify-and-iterate seam of [[loop-engineering]]).
- **Planning in advance** — iterate on a high-level plan first, then hand it to the agent.
- **Comprehensive documentation** — feed it in so the model uses APIs without reading the code first;
  "write good documentation first and the model may build the matching implementation from that alone."
- **Good version control** — LLMs are "fiercely competent at Git," better than most at `git bisect`.
- **Effective automation** — CI, formatting, linting, preview-env CD all benefit the agent too.
- **A culture of code review**, **a very weird form of management** ("weird digital interns who will
  absolutely cheat if you give them a chance"), **manual QA**, **research skills**, **shipping to a
  preview environment**, an instinct for **what can be outsourced**, and an updated **sense of estimation**.

The punchline: "If you're going to really exploit these tools, you need to be operating at the top of
your game… AI tools **amplify existing expertise**." Almost all of these are senior-engineer traits
already — the same "the human job shifts up, not away" line running through
[[dilger-harness-is-20-percent-requirements-are-80]], [[spec-driven-development]], and the
"stay the engineer" caveats of [[loop-engineering]].

## Why it matters here

- **Term primary.** This is the naming origin for the accountable-end vocabulary the KB uses on the
  [[agentic-coding]] / [[loop-engineering]] threads, plus the documented pivot to "agentic engineering."
- **Accountability lineage.** "Proudly and confidently **accountable** for the software they produce"
  is the seed of Willison's later, sharper [[willison-directly-responsible-individuals|DRI]] argument
  (an agent must never be the accountable party) and rhymes with [[addyosmani-own-the-outer-loop|Osmani's
  Answerability]]. The accountable/reckless split here is the human-ownership boundary of the whole thread.
- **Practitioner anchor.** Reinforces [[simon-willison]] as the hands-on "what actually works with
  coding agents" voice; not an [[event-modeling]] source.

## Links

Entities: [[simon-willison]], [[martin-fowler]]. Concepts: [[agentic-coding]], [[loop-engineering]],
[[vibe-modeling]], [[harness-engineering]], [[spec-driven-development]].
Related sources: [[willison-agentic-engineering-patterns]] (the successor guide),
[[willison-designing-agentic-loops]], [[willison-directly-responsible-individuals]],
[[fowler-agentic-programming]], [[addyosmani-own-the-outer-loop]].

_Raw source: `raw/articles/willison-vibe-engineering.md`._
