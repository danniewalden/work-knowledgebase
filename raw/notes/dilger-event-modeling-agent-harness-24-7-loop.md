---
source_url: https://www.linkedin.com/in/martindilger/recent-activity/all/
title: "I have agents running 24/7 — the Event Modeling Agent Harness"
author: Martin Dilger
publication: LinkedIn (post)
published: 2026-06-17
retrieved: 2026-06-17
type: note
---

> Captured verbatim from Martin Dilger's LinkedIn post (≈1h old at retrieval, marked "Edited"). The post includes a diagram titled "EVENT MODELING AGENT HARNESS"; the diagram text is transcribed below the post body.

## Post body

I have agents running 24/7 - looking for work and I don´t pay them most of the time.

I'm utilizing local models, my most used model being QWEN3.6:9B which gives good results with acceptable speed.
I run them on Ollama in a ralph-loop.

For modeling, I typically use Claude Code and stronger models - mostly Sonnet, but also local models work well enough for some tasks.

Coding is the easy part. You should be able to work with lightweight and cheap models. If coding requires strong reasoning skills or the "1-million-context"-window - you might revisit the reason for that - typically it´s coupling.

For this I define a Blue-Print-Architecture. Coding becomes like "Painting by the numbers", filling some gaps in the templates and that´s it.

Also for reviews using my "WDYT" (what do you think )-Skill, I typically utilize stronger models with better reasoning, also Sonnet gives good results.

I rarely need Opus, not even mentioning Fable..

Agents need feedback.
The backbone of it all Event Modeling - and especially the Given-When-Then Scenarios provided by the model. Heavily relyong on Behavior-Driven-Development-Principles.

Just asked ChatGTP to visualize my workflow. It did a pretty decent job.

## Diagram (transcribed): "EVENT MODELING AGENT HARNESS"

Subtitle: "24/7 LOOP – ALWAYS WAITING, ALWAYS WORKING"

Three framing notes:
- THE SLICE IS THE UNIT OF WORK — a slice represents a complete unit of work; agents work on slices; humans don't care who made the change.
- AGENTS CAN MODEL TOO — a human or another agent can model a slice; the harness doesn't care who made the change; the next available agent picks it up.
- READY MEANS ACTIONABLE — once a slice is marked Ready, it enters the execution queue; the next available agent picks it up.

Continuous loop steps:
1. MODEL THE SLICE (human or agent) — humans or agents model the slice using Event Modeling; they can create/move slices or update existing ones. (Event modeling rate: human + AI agent.)
2. MARK SLICE AS READY — Draft → Ready, marked done/checked.
3. AGENT PICKS UP READY SLICE — an available agent picks up the slice and works on it.
4. AGENT WORKS ON THE SLICE — the agent reconciles the read model and projects an outcome.
5. MARK SLICE DONE — Ready → In Progress → Done; the slice is complete and ready for downstream use.

Loop behavior: "AGENT HARNESS — Waiting for Changes." Continuously watches for slices; starts work immediately when Ready; runs 24/7.

Key principles (as listed): Slice = Unit of Work; Anyone can model; Ready slices → immediate action; Continuous 24/7 loop; No bottlenecks / No delays.

## Why it matters (capture note, not the author's words)

Names and diagrams a concrete "Event Modeling Agent Harness": an always-on (ralph-loop) agent harness whose unit of work is the Event Modeling *slice*, gated by a Draft→Ready→In Progress→Done state machine, with the model's Given-When-Then scenarios as the feedback/spec backbone (BDD). Bridges the wiki's event-modeling × agent-harness threads: [[event-modeled-agent-design]], [[agent-harness]], [[harness-engineering]], [[ralph-loop]], [[long-running-agents]], [[spec-driven-development]], [[vertical-slice-architecture]] (slice = unit of work), and Dilger's earlier [[dilger-model-is-a-living-spec-always-on-agent]]. Note the "coupling, not context-window" claim and the cheap-local-models-for-coding / stronger-models-for-modeling-and-review split (cf. [[locality-of-reference]], [[context-engineering]]).
