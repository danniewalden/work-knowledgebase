---
title: "Tornhill — Why Human-Level AI Won't Be Enough"
type: source
created: 2026-07-10
updated: 2026-07-10
sources: [tornhill-why-human-level-ai-wont-be-enough]
raw_file: [raw/articles/tornhill-why-human-level-ai-wont-be-enough.md]
tags: [ai-readable-code, code-health, harness-engineering, loop-engineering, agentic-coding, focus]
---

# Tornhill — "Why Human-Level AI Won't Be Enough"

Source: [[adam-tornhill]], *Code for Humans and Machines* (Substack), 2026-06-30. Raw:
`raw/articles/tornhill-why-human-level-ai-wont-be-enough.md`. (Search-indexing lag missed it in the
07-10 headless run; surfaced via his LinkedIn share and read via live Chrome since Substack is
client-rendered.)

## Summary

The industry's benchmark has been to make AI produce code **at the level of today's best human
experts**. Tornhill's argument: **even if we hit that bar, it still won't be enough** — because AI
itself *changes the quality threshold* required to keep systems stable.

Two evolutionary pressures raise the bar. **Scale:** every past productivity jump let us take on larger,
more complex problems, and **Lehman's laws** say useful software keeps growing and accumulating
complexity unless actively fought — so tomorrow's systems will be far more complex than today's.
**Speed:** an agent generates code orders of magnitude faster than a human, and that speed already
causes problems; future systems will evolve far faster than today's manually-checkpointed pipelines
allow. Combine the two and you get codebases *"few — if any — of today's experts could stay on top of."*

## Why human-expert level is the wrong bar

- **Defect opportunities scale with code volume and change volume** — larger modules, larger changes,
  and higher churn have been linked to fault risk for decades. A human-expert-level AI generating at
  breakneck speed, *without a matching breakthrough in verification and validation*, becomes "a fertile
  breeding ground for bugs" — you get to "truly experience what it means to be **wrong at scale**."
- **The stochastic core doesn't go away** — LLMs are prediction machines; even at a six-sigma defect
  rate, the potential for error is always there. "A one-in-a-million mistake sounds impressive... until
  you start making millions of decisions. All the time." Rare errors stop being rare at the system level.

## The prescription — embrace imperfection

Tornhill rejects the **"superhuman code quality"** path: there's no obvious source of training data or
feedback signal for it (the hardest software decisions are contextual and don't come labeled), and
"AGI has been 'just a few years away' for the better part of fifty years." More importantly,
human-level coding "may not even be the problem we need to solve." His approach to taming agents has
been to **accept their unreliability** — and he thinks that's the key to the future too: instead of
chasing perfect code, **"double down on creating environments where unreliable agents reliably produce
acceptable outcomes."** *"The future might belong to those organizations that embrace that imperfection
today."*

## Connections

The sharpest statement yet of the KB's **environment-over-model** through-line: it puts a *theoretical
floor* under [[harness-engineering]] and [[loop-engineering]] (the value is in the surrounding system,
not in a better model) and under the code-health thread — [[ai-readable-code]],
[[tornhill-codescene-unhealthy-code-agentic-token-cost]], and the empirics of
[[borg-tornhill-code-for-machines-not-just-humans]] (defect risk scales with code/change volume). It
converges with [[dilger-harness-is-20-percent-requirements-are-80|Dilger's "harness is 20%"]] and the
verification-burden / maker≠checker seam in [[langchain-the-art-of-loop-engineering]] — "unreliable
agents, reliable outcomes" is exactly what the verification loop is *for*. Extends his running
[[tornhill-ai-readable-code-series]].

## Caveat

A reflective/opinion essay (no new data of its own) — but it rests on his own peer-reviewed empirics
([[borg-tornhill-code-for-machines-not-just-humans]]) and long-standing fault-risk research, and states
a design stance (accept imperfection, engineer the environment) rather than a testable claim.
