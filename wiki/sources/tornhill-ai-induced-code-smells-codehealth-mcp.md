---
title: "Source: Adam Tornhill — AI-induced code smells (CodeHealth MCP feature post)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-ai-induced-code-smells-codehealth-mcp]
raw_file: [raw/notes/tornhill-ai-induced-code-smells-codehealth-mcp.md]
tags: [verification-burden, codescene, vendor-claim, ai-readable-code, focus]
---

# Source: Adam Tornhill — AI-induced code smells (CodeHealth MCP feature post)

LinkedIn post by **[[adam-tornhill]]** (**2026-09-03**), captured verbatim at
`raw/notes/tornhill-ai-induced-code-smells-codehealth-mcp.md` via logged-in Chrome. A **product
announcement** for a new feature in **CodeScene's CodeHealth MCP**. Filed for the position it states,
not for evidence: **this capture contains no figures at all.**

## Summary

He asks two questions — "a) What are the most common AI-induced code smells? b) How often do the
safeguards kick in on AI-generated code?" — says the new CodeHealth MCP feature answers them, and
reports that the resulting stats are "really interesting." Then the sentence that matters for the
verification thread:

> "As evident from the screenshot, there are plenty of complexity-inducing code smells that **I — as
> the human in the loop — never need to see** thanks to the CodeScene MCP. Pretty cool."

## Key points

- **The clearest statement of the *enforce what you don't inspect* bargain**, and of what it buys: not
  "the smells don't happen" but "**I never need to see them**." Detection and remediation are moved
  below the human's attention line entirely.
- **It presupposes a measurable category — "AI-induced code smells"** — i.e. that agent-written code
  has a characteristic defect profile distinct from human code, and that a tool can count it. If
  substantiated, that would be materially new for [[ai-readable-code]]; it is not substantiated here.
- **"How often do the safeguards kick in"** is the interesting metric nobody in this batch reports: the
  intervention *rate* on agent output. It is the missing quantity in the whole
  [[verification-burden]] dispute — how much would you actually have caught by reading?
- Completes the pattern of his August–September position: triage what you read
  ([[tornhill-task-uncertainty-decides-what-code-you-read]]), enforce the rest deterministically
  ([[tornhill-controlling-the-uncertainty-machine]]), and here, ship the enforcement as a product
  feature.

## Limits

- **VENDOR SELF-REPORT, at full strength.** A CodeScene product post about CodeScene's own MCP, written
  by CodeScene's founder/CTO. It is marketing for the exact remedy his essays prescribe, and the
  marker travels with any use of it.
- **NO NUMBERS EXIST IN THIS CAPTURE.** The statistics he refers to are in an **attached screenshot
  image**, not in the post text. The capture therefore carries the *claim that such stats exist* and
  nothing more. **Do not cite a figure from this page — there is none**, and no page in this KB may
  attribute a smell frequency, smell ranking or safeguard-trigger rate to it.
- No methodology, sample, corpus, definition of "AI-induced," or baseline against human-written code.
  "AI-induced" as a causal label is unsupported by anything in the capture.
- LinkedIn-derived date (accurate to the day).

## Connections / contrast

- **[[verification-burden]]** — the vendor-tooling end of the triage position, and the crispest
  formulation of its promise ("never need to see"). Also the page's best illustration of why the
  position needs an interested-party marker: the person telling you not to read the code sells the
  tool that reads it.
- **[[tornhill-cannot-trust-agent-codescene-mcp]]** — the prior claim this depends on: an LLM cannot
  reliably self-assess code health, so the sensor must be deterministic and external. Same product,
  same argument, now with an AI-specific smell taxonomy layered on.
- **[[fowler-bockeler-maintainability-sensors]] / [[fitness-functions]]** — the sensor-vs-prevention
  strand; this is a sensor that also *hides* its findings from the human, which is a step further than
  a sensor that reports them.
- **Against [[osmani-agentic-code-review-skill-five-axes|Osmani]]**: both automate the inspection, but
  Osmani's judge is an LLM producing a review a human reads, Tornhill's is a deterministic checker
  whose findings the human never sees. Judgement vs. enforcement, and visibility vs. suppression.
- **[[borg-tornhill-code-for-machines-not-just-humans]] / [[tornhill-codescene-unhealthy-code-agentic-token-cost]]**
  — where his actual evidence lives (a peer-reviewed FORGE 2026 study, and earlier CodeScene research).
  Cite those for numbers; cite this only for the position.
- Also: [[comprehension-debt]], [[ai-readable-code]], [[agent-governance]], [[guardian-agents]].

## Links

Entities: [[adam-tornhill]] · [[markus-borg]] · [[addy-osmani]]. Concepts:
[[verification-burden]] · [[ai-readable-code]] · [[fitness-functions]] · [[comprehension-debt]] ·
[[agent-governance]] · [[guardian-agents]]. Related sources:
[[tornhill-cannot-trust-agent-codescene-mcp]] · [[tornhill-controlling-the-uncertainty-machine]] ·
[[tornhill-task-uncertainty-decides-what-code-you-read]] ·
[[borg-tornhill-code-for-machines-not-just-humans]] ·
[[tornhill-codescene-unhealthy-code-agentic-token-cost]] ·
[[osmani-agentic-code-review-skill-five-axes]].

_Raw source: `raw/notes/tornhill-ai-induced-code-smells-codehealth-mcp.md`._
