---
title: "LangChain — The Art of Loop Engineering"
type: source
created: 2026-06-28
updated: 2026-06-28
sources: [langchain-the-art-of-loop-engineering]
raw_file: [raw/articles/langchain-the-art-of-loop-engineering.md]
tags: [loop-engineering, harness-engineering, agent-observability-and-evals, unattended-coding-agents, focus]
---

# LangChain — The Art of Loop Engineering

Blog post by **Sydney Runkle** ([[langchain|LangChain]], 2026-06-16).
Source file: `raw/articles/langchain-the-art-of-loop-engineering.md`. The vendor-side companion to
[[addyosmani-loop-engineering|Osmani]] and [[swyx-loopcraft-art-of-stacking-loops|swyx]] — it turns the
"stack loops" idea into a concrete, instrument-it-today taxonomy mapped onto LangChain primitives (read
the product pitch in, but the four-loop model is tool-agnostic). Running example: LangChain's internal
docs-writing agent.

## The four stacked loops

Each loop wraps the one below; the defining move is that an outer loop's feedback **reaches inside and
rewrites the inner loop**, so every cycle makes the inner loops more effective.

1. **Agent loop** — a model calls tools in a loop until the task is done (`create_agent`). *Automates
   work.*
2. **Verification loop** — a **grader** (deterministic *or* LLM-as-judge) scores output against a
   rubric and, on failure, sends it back with feedback. The **maker≠checker** principle. For the docs
   agent: run tests, check links resolve, check the diff is scoped to what was requested — no manual
   review for those error classes. Tradeoff: more latency/cost per run, "worth it when quality matters
   more than speed, which is most production use cases." (`RubricMiddleware` / `after_agent` hook.)
   *Ensures quality.*
3. **Event-driven loop** — an event (new doc, schedule, webhook) fires and the agent runs; "it's a
   component running continuously inside a larger system," not something you invoke manually. Cites
   **openclaw "heartbeats"** as the always-on proactive-assistant pattern. (LangSmith Deployment crons
   / webhooks; Fleet channels.) *Automates work at scale.*
4. **Hill-climbing loop** — "the fourth (and arguably most important) automates *improvement*." Every
   run produces a **trace**; an analysis agent reads the traces and **rewrites the harness config**
   (prompt/tool/grader tweaks; for open-weight models, RL fine-tuning on trace/eval outcomes; memory
   and retrieved skills can be improved the same way). "The return arrow doesn't just loop back to the
   top — it reaches inside and updates the agent loop directly." (LangSmith **Engine**.)

## Human-in-the-loop at every level

Automation ≠ removing humans. Natural oversight points: require human input before sensitive tool
calls (loop 1); a human grader for sensitive workflows (loop 2); human approval of outputs (loop 3);
harness improvements through human review before deploy (loop 4). "An automated grader can check
whether links resolve; it takes a human to notice the framing is wrong for the audience."

## The strategic claim

"AI leaders like Steipete, Boris, and Andrej have all arrived at the same conclusion: the potential in
agents is in the loops you build around them." LangChain argues focus should pivot from loops 1–2 (well
understood) to **loops 3–4, where value compounds** — embedding agents in your ecosystem so they
continuously improve against your criteria. Satya framing: companies that build learning loops early,
"where human judgment and token capital compound together," gain a hard-to-replicate advantage.

## Why it matters here

Gives [[loop-engineering]] its concrete taxonomy, and **loop 4 closes a gap the KB had only implied**:
[[agent-observability-and-evals|traces/evals]] fed back into an automatic harness rewrite — the missing
return path from observability into [[harness-engineering]]. Loops 1–2 restate [[react-loop]] +
[[feedforward-and-feedback-controls|sensors]]; loop 3 is [[long-running-agents]] /
[[unattended-coding-agents]].

## Touches

[[loop-engineering]] · [[langchain]] · [[harness-engineering]] · [[react-loop]] ·
[[feedforward-and-feedback-controls]] · [[agent-observability-and-evals]] · [[long-running-agents]] ·
[[unattended-coding-agents]] · [[context-engineering]]

_Source: `raw/articles/langchain-the-art-of-loop-engineering.md`._
