---
title: Long-Running Agents
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [anthropic-effective-harnesses-long-running-agents, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, openai-harness-engineering-codex]
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

## Related

[[token-budget-quality-cliff]]

_Sources: [[anthropic-effective-harnesses-long-running-agents]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[openai-harness-engineering-codex]]._
