---
title: "Martin Fowler — Agentic Programming (bliki)"
type: source
created: 2026-06-30
updated: 2026-06-30
sources: [fowler-agentic-programming]
raw_file: [raw/articles/fowler-agentic-programming.md]
tags: [agentic-coding, harness-engineering, vibe-coding, definitions, focus]
---

# Martin Fowler — Agentic Programming

Bliki entry by **[[martin-fowler]]** on martinfowler.com (2026-05-21), captured verbatim.
Source: `raw/articles/fowler-agentic-programming.md`. The crisp canonical definition the KB had
been citing without a dedicated page.

## The definition

A "profound change to the nature of programming": developers increasingly **prompt an LLM to write
code, then review the results**, rather than typing it themselves. Humans remain responsible for what
the software does and how it works, but **use different skills** to create their products. Fowler
settles on **"agentic programming"** as the name (over "agentic coding / engineering").

## Two distinctions that pin the term down

- **vs. [[vibe-modeling|vibe coding]]** — with vibe coding humans *don't look at the code* and forget
  it exists; with agentic programming they *are concerned with the code, often giving it detailed
  review*. (This is the clean line the KB's [[agentic-coding]] page needed.)
- **vs. LLM autocomplete** — agentic programming is also distinct from using an LLM as sophisticated
  in-IDE code completion. Agentic tools work in a **terminal environment**: the programmer issues
  prompts (often incorporating saved guideline documents), the LLM **manipulates the source tree
  directly** — creating/modifying files, running code, evaluating tests, continuing for extended
  periods — then humans review the code, tests, and **outputs from other sensors**.

## What it implies for skills

The shift raises the question of what programmers do next. Fowler names **[[harness-engineering]]
("working on the guides and sensors around the LLM") as central** — an explicit endorsement of the
Böckeler/Thoughtworks vocabulary the KB tracks ([[fowler-bockeler-harness-engineering]],
[[feedforward-and-feedback-controls]]) — and elevates the importance of **programmers understanding
their domain** and collaborating with users to iteratively define the product. The latter rhymes
directly with [[dilger-harness-is-20-percent-requirements-are-80|Dilger's 80% claim]] and
[[spec-driven-development]].

## Why it matters here

A short, authoritative, vendor-neutral definition that anchors [[agentic-coding]] and draws the
agentic-programming / vibe-coding / autocomplete boundaries the KB uses informally. Its "guides and
sensors" line is Fowler co-signing the harness-engineering frame, and its "understand the domain"
close is the Thread-1/Thread-4 seam in miniature.

## Touches

[[martin-fowler]] · [[agentic-coding]] · [[harness-engineering]] · [[feedforward-and-feedback-controls]] ·
[[vibe-modeling]] · [[spec-driven-development]] · [[dilger-harness-is-20-percent-requirements-are-80]] ·
[[fowler-bockeler-harness-engineering]]

_Source: `raw/articles/fowler-agentic-programming.md`._
