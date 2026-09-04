---
title: Long-Running Agents
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, openai-harness-engineering-codex, fowler-fragments-2026-09-01, willison-understanding-chatgpt-work]
tags: [harness-engineering, long-running-agents, coding-agents]
---

# Long-Running Agents

Agents that work on complex tasks spanning many context windows — hours or days. The core
challenge: they work in **discrete sessions, each starting with no memory of the last** — like
"engineers working in shifts" ([[anthropic-effective-harnesses-long-running-agents]]). Compaction
alone is insufficient; bridging the gap is a defining problem of [[harness-engineering]].

## Failure modes without a harness

- **One-shotting:** the agent tries to do too much, runs out of context ([[context-rot]]), and
  leaves a half-implemented, undocumented codebase.
- **Premature victory:** a later session sees prior progress and declares the job done.
- Plus hallucinated tool calls and lost state on failure ([[firecrawl-what-is-an-agent-harness]]).

## The initializer-executor pattern

Anthropic's documented solution (also catalogued by Firecrawl as a standard architecture):

- **Initializer agent** runs once: writes `init.sh`, a progress log (`claude-progress.txt`), an
  initial git commit, and a comprehensive **feature list** in JSON (each `passes: false`). JSON is
  used because the model is less likely to overwrite/reformat it than Markdown.
- **Coding agent** runs each session: gets its bearings (read progress + git log + feature list,
  run `init.sh`, smoke-test), works **one feature at a time**, **self-verifies end-to-end** (e.g.
  browser automation), commits with descriptive messages, and leaves the repo in a clean state.

The "initializer" and "coding" agents differ only in their initial prompt — same system prompt,
tools, and harness. The filesystem + git act as the **shared memory** across sessions
([[langchain-anatomy-of-an-agent-harness]]; cf. [[ralph-loop]]). OpenAI's agent-first build is a
large-scale instance ([[openai-harness-engineering-codex]]).

The "shifts" + on-disk-memory pattern is exactly the **event-driven loop** (level 3) in
[[loop-engineering]]: "the agent forgets, the repo doesn't." Loop engineering names the surrounding
discipline of triggering and stacking such runs.

## Persistent memory + supervision, and a seven-day run (Sept 2026)

**NVIDIA's AVO**, relayed by [[martin-fowler]] in [[fowler-fragments-2026-09-01]], is *"designed to
preserve progress beyond a single model context"* with two mechanisms that name the same problem
initializer-executor solves, differently:

- **Persistent memory** carries forward *"prior implementations, evaluation results, compiler and profiler
  outputs, and accumulated reasoning, allowing the agent to resume from the current state rather than
  repeatedly reconstructing the search."* Note the unit: not a progress *file* but the accumulated
  evaluation record — closer to a search frontier than to a to-do list.
- **A supervisor** that *"monitors the broader trajectory for stagnation or repeated unproductive cycles
  and can redirect the main agent toward alternative strategies"*, while *"the main agent remained
  responsible for deciding what to inspect, change, test, and evaluate."* A separation of *what to try*
  from *whether trying is still working*.

The GPU kernel-optimization run lasted **seven days** — the longest single-task agent run recorded anywhere
in this KB. **Markers: VENDOR SELF-REPORT (NVIDIA on its own harness) and secondhand (Fowler relaying; the
NVIDIA post is not in `raw/`). No methodology, cost or replication.**

**A commercial instance of the state side.** ChatGPT Work gives each session a scratch folder under a
`/workspace` volume that **persists across sessions and is mounted into all concurrently running ones**, so
"file edits from one can be instantly seen by the others" ([[willison-understanding-chatgpt-work]]) —
Willison had 171 such folders. That is the filesystem primitive in its cross-session form, shipped as a
product feature; it is also, as that page notes, a cross-session write surface for a
[[prompt-injection]], which is the cost of the capability.

## Related

[[token-budget-quality-cliff]] · [[agent-harness]] · [[loop-engineering]] · [[agent-coordination-substrates]]

_Sources: [[anthropic-effective-harnesses-long-running-agents]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[openai-harness-engineering-codex]] · [[fowler-fragments-2026-09-01]] · [[willison-understanding-chatgpt-work]]._
