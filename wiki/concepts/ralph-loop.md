---
title: Ralph Loop
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [langchain-anatomy-of-an-agent-harness, openai-harness-engineering-codex, addyosmani-code-agent-orchestra, voss-what-the-hell-is-a-loop-anyway, morris-humans-and-agents-in-software-engineering-loops, addyosmani-practical-loop-engineering]
tags: [harness-engineering, pattern, long-running-agents, focus]
---

# Ralph Loop

A [[agent-harness|harness]] pattern (after Geoffrey Huntley's "Ralph Wiggum" loop) for continuing
work across context windows: a **hook intercepts the model's attempt to exit and reinjects the
original prompt into a clean context window**, forcing the agent to keep working against a
completion goal ([[langchain-anatomy-of-an-agent-harness]]).

The filesystem makes it work — each iteration starts fresh but reads state (progress files, git
history) left by the previous one, so it complements the [[long-running-agents]]
initializer-executor pattern. [[openai-harness-engineering-codex]] uses a Ralph-style loop to
drive a PR to completion: the agent reviews its own changes, requests agent reviews, responds to
feedback, and iterates until all reviewers are satisfied.

In [[loop-engineering]] terms the Ralph loop is the **agent loop** (level 1) made persistent — the
innermost primitive that loop engineering composes with verification, event-driven, and hill-climbing
loops, rather than the whole stack. *(That placement is not universal — see the correction below.)*

## The five-step cycle, and the four memory channels ([[addyosmani-code-agent-orchestra|Osmani, 2026-03]])

The clearest operational description in the KB. *"Popularized by Geoffrey Huntley **and Ryan Carson**"* —
Carson's standalone `ralph` tool implements the core loop and his Antfarm project layers multi-agent
orchestration on top of it; **the Carson attribution is new to this KB.** The cycle: **pick** (next task
from `tasks.json`) → **implement** → **validate** (tests, types, lint) → **commit** (if checks pass, and
update task status) → **reset** (clear context, start fresh).

*"The key insight is **stateless-but-iterative**. By resetting each iteration, the agent avoids
accumulating confusion. Small bounded tasks produce cleaner code with fewer hallucinations than one
enormous prompt."* **Four channels of memory persist across resets: git commit history, a progress log,
the task state file, and `AGENTS.md` as long-term semantic memory** — which is the concrete form of this
page's "the filesystem makes it work."

Safeguards: feed errors back for auto-retry but **kill and reassign after 3+ stuck iterations**; always
work on feature branches; **hard limits on iterations, time and tokens**; the agent opens a PR and a human
reviews before merge. *"Start with one loop overnight. Graduate to ten loops on ten branches."*

*(**IMPRESSION NOT MEASUREMENT** for every quantity in the orchestra piece, and **NOT INDEPENDENT** — the
author is a Director at Google Cloud AI promoting his own book and citing his own prior posts. See
[[loop-engineering]] and the batch-C do-not-promote list.)*

## Where it sits, and a correction to how the KB uses the term

[[voss-what-the-hell-is-a-loop-anyway|Voss]] classifies the Ralph loop as **the task loop** — the second
of his four loop architectures, *"the first loop to get a name."* It iterates on **a single artifact** and
ends on **spec compliance plus passing tests**; *"A Ralph loop restarts a coding agent against the same
specification over and over, allocating a completely fresh context window every iteration and doing
exactly one task per loop. **The apparent waste is the point:** refeeding the full spec each time prevents
the [[context-rot]] and compaction events that quietly degrade long-running sessions."* Note this does not
match the KB's placement of the Ralph loop as LangChain's *agent loop* (level 1) made persistent — for
Voss it is a distinct architecture with its own exit condition, not a persistent version of the innermost
one. Both readings are now on the page; the KB does not pick.

**And the human is not optional.** Both new sources correct the colloquial usage. Voss, relaying Huntley:
the human writes the spec, judges doneness, and has one more job — *"watching the loop, spotting failure
patterns, and fixing them so they never recur,"* which Huntley compared to *"a locomotive engineer,
someone whose whole job is keeping the train on the rails."*
[[morris-humans-and-agents-in-software-engineering-loops|Morris]] puts it in a footnote: *"These days
'ralph loop' is often used colloquially to mean just firing up a bunch of agents and leaving them to keep
looping until (hopefully) they finish their task. **But as originally described the operator plays an
important role in steering agents as they ralph.**"* [[jeremiah-lowin|Lowin's]] worry that loop
engineering *"got boiled down to the dumbest version of itself"* (on [[graph-engineering]]) is about
exactly this drift. *(Morris is **NOT INDEPENDENT** on harness engineering — Thoughtworks author,
Thoughtworks series, Thoughtworks-coined term.)*

For where the pattern sits in current practice, note that
[[addyosmani-practical-loop-engineering|Osmani, 2026-08]] describes hand-rolled Ralph experiments as the
*early-2026* stage of the discipline, run *"largely on some of our personal projects where, if we ran into
a wall, it didn't really have a big cost"* — since narrowed to the `/goal` and `/loop` primitives.

_Sources: [[langchain-anatomy-of-an-agent-harness]] · [[openai-harness-engineering-codex]] · [[addyosmani-code-agent-orchestra]] · [[voss-what-the-hell-is-a-loop-anyway]] · [[morris-humans-and-agents-in-software-engineering-loops]] · [[addyosmani-practical-loop-engineering]]._
