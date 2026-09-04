---
title: "Source: Anthropic — Effective Harnesses for Long-Running Agents"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [anthropic-effective-harnesses-long-running-agents]
raw_file: [raw/articles/anthropic-effective-harnesses-long-running-agents.md]
tags: [harness-engineering, long-running-agents, claude-agent-sdk, anthropic]
---

# Source: Anthropic — Effective Harnesses for Long-Running Agents

Engineering post by Justin Young, [[anthropic]], published 2025-11-26. The most concrete recipe
for a [[long-running-agents]] harness, with an accompanying autonomous-coding quickstart. Raw
capture: `raw/articles/anthropic-effective-harnesses-long-running-agents.md`.

## Summary

The core challenge: agents work in discrete sessions, each starting with **no memory of the last**
— "engineers working in shifts." Compaction alone isn't enough; even Opus 4.5 looping on the
[[claude-agent-sdk]] fails to build a production web app from a high-level prompt. The fix is a
**two-agent structure**: an *initializer* that sets up a durable environment once, and a *coding
agent* that makes incremental, well-documented progress each session.

## Key points

- **Two observed failure modes:** (1) the agent one-shots the app, runs out of context mid-build,
  and leaves a half-implemented, undocumented mess; (2) a later session sees prior progress and
  **prematurely declares the job done**.
- **Initializer agent** (different first-context-window prompt) writes: an `init.sh` to run the
  dev server, a `claude-progress.txt` log, an initial git commit, and a comprehensive **feature
  list** (200+ items for the claude.ai clone), each marked `passes: false`.
- **JSON beats Markdown** for the feature-tracking file — the model is less likely to overwrite or
  reformat it. Coding agents may only flip the `passes` field; "unacceptable to remove/edit tests."
- **Incremental progress:** work *one feature at a time*; commit with descriptive messages; write
  progress summaries; leave the repo in a "clean state" (mergeable to main). Git enables recovery.
- **End-to-end testing:** Claude marks features done without true verification unless explicitly
  prompted to test as a human user would (browser automation / Puppeteer MCP screenshots). Vision
  and browser-automation limits remain (e.g. can't see native alert modals).
- **Getting up to speed:** every session runs `pwd`, reads progress + git log, reads the feature
  list, runs `init.sh`, and does a basic end-to-end smoke test before starting new work.
- **Failure-mode → solution table** maps each failure to an initializer behaviour + coding-agent
  behaviour. Note: "initializer" and "coding" agents differ only in initial prompt — same system
  prompt, tools, and harness.
- **Open question:** single general-purpose agent vs. specialised testing/QA/cleanup agents; and
  generalising beyond web apps (e.g. scientific research, financial modeling).

## Connections / contrast

Defines the **initializer-executor** harness pattern that [[firecrawl-what-is-an-agent-harness]]
later catalogues as a standard architecture. The `claude-progress.txt` + feature-list + git
approach is a concrete instance of [[fowler-bockeler-harness-engineering]]'s feedforward guides
(feature spec) and feedback sensors (tests, smoke checks). Directly addresses [[context-rot]] and
extends the KB's [[anthropic]] / [[agent-engineering]] thread. The [[claude-agent-sdk]] is named
elsewhere as the canonical general-purpose [[agent-harness]].

_Source page: [[anthropic-effective-harnesses-long-running-agents]]._
