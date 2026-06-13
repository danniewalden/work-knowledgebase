---
title: Ralph Loop
type: concept
created: 2026-06-11
updated: 2026-06-11
sources: [langchain-anatomy-of-an-agent-harness, openai-harness-engineering-codex]
tags: [harness-engineering, pattern, long-running-agents]
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

_Sources: [[langchain-anatomy-of-an-agent-harness]] · [[openai-harness-engineering-codex]]._
