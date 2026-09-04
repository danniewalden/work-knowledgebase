---
title: "Borg, Hagatulah, Tornhill & Söderberg — Code for Machines, Not Just Humans"
type: source
created: 2026-06-21
updated: 2026-06-21
sources: [borg-tornhill-code-for-machines-not-just-humans]
raw_file: [raw/papers/borg-tornhill-code-for-machines-not-just-humans.md]
tags: [agentic-coding, code-health, ai-readable-code, harness, research, focus]
---

# Borg, Hagatulah, Tornhill & Söderberg — Code for Machines, Not Just Humans: Quantifying AI-Friendliness with Code Health Metrics

Peer-reviewed paper (arXiv 2601.02200; **accepted for FORGE 2026** — the 3rd ACM Int'l Conference on
AI Foundation Models and Software Engineering), submitted 2026-01-05. Authors: **[[markus-borg]]**,
Nadim Hagatulah, **[[adam-tornhill]]**, Emma Söderberg. Capture is verbatim of the abstract +
Introduction + Background + Method (§1–3.2); Results/Discussion not transcribed. Raw:
`raw/papers/borg-tornhill-code-for-machines-not-just-humans.md`.

## What it studies

Whether **code quality predicts "AI-friendliness."** Quality is measured with CodeScene's **CodeHealth
(CH)** metric (1–10, calibrated to human comprehension; ≥9 = Healthy, 4–9 = Warning, <4 = Alert;
Warning+Alert grouped as Unhealthy). AI-friendliness is proxied by the **success rate of LLM-driven
refactoring** on 5,000 Python files from competitive programming (CodeContests): a refactoring is
*correct* if the unit tests still pass (the oracle) and *beneficial* if CH increases. Six LLMs are
tested (five open-weight 20–30B models run locally + one SotA model via Anthropic's API). Three RQs:
how perplexity (PPL) differs by health; how the **break rate** differs by health; and how well CH
*predicts* break rate vs. PPL and SLOC.

## Headline findings

- **Human-friendly code is also machine-friendly.** LLMs have significantly **lower break rates on
  Healthy code (CH ≥ 9)**, with corresponding **risk reductions of 15–30%**.
- **CodeHealth is the better predictor** of refactoring correctness than **perplexity (PPL)** (the
  LLM-intrinsic confidence baseline) or **Source Lines of Code (SLOC)**.
- **Practical takeaway:** organizations can use CH to **route AI work** — flag Healthy code as
  lower-risk for AI processing and reserve human oversight for Unhealthy code. "Investing in
  maintainability not only helps humans; it also prepares for large-scale AI adoption" — quality is "a
  prerequisite for safe and effective use of AI."

## Why it matters here

This is the **peer-reviewed primary** grounding the KB's code-health × agentic thread, which until now
rested on [[adam-tornhill|Tornhill's]] vendor LinkedIn reshare
([[tornhill-codescene-unhealthy-code-agentic-token-cost]]). Note the precise relationship: the **35–45%
token-spend** figure is from a *separate* CodeScene study; **this** paper contributes the **15–30%
refactoring-risk reduction** and the **CH > PPL/SLOC** predictor result. It upgrades [[agentic-coding]]
("bad code degrades the agent") and [[ai-readable-code]] (Tornhill's CLEAR) from claim-level to a
citable, test-oracle-backed result, and gives [[harness-engineering]] / [[fowler-bockeler-maintainability-sensors|maintainability
sensors]] an empirical reason to gate AI on code health. The "use CH to decide where AI is low-risk"
recommendation is a concrete [[feedforward-and-feedback-controls|sensor-driven]] routing policy.

## Caveats

- **Domain & language:** 5,000 *Python competitive-programming* files (60–120 SLOC, ≥1 code smell),
  chosen because they ship with test cases — not industrial code; generalization to large legacy
  codebases is assumed, not shown here.
- **Task proxy:** "AI-friendliness" = refactoring success specifically; other agent tasks may differ.
- **Conflict of interest:** CH is CodeScene's commercial metric and two authors (Borg, Tornhill) are
  affiliated — though this is a peer-reviewed venue with an objective test-pass oracle, which is much
  stronger evidence than the marketing posts.
- Only §1–3.2 captured; the quantitative Results tables live in the full paper at the source URL.

## Touches

[[markus-borg]] · [[adam-tornhill]] · [[agentic-coding]] · [[ai-readable-code]] · [[harness-engineering]] ·
[[fowler-bockeler-maintainability-sensors]] · [[feedforward-and-feedback-controls]] ·
[[mutation-testing]] · [[tornhill-codescene-unhealthy-code-agentic-token-cost]] · [[agent-legibility]]

_Source: `raw/papers/borg-tornhill-code-for-machines-not-just-humans.md`._
