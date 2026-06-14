---
title: Birgitta Böckeler
type: entity
created: 2026-06-11
updated: 2026-06-14
sources: [fowler-bockeler-harness-engineering, fowler-bockeler-maintainability-sensors]
tags: [person, thoughtworks, harness-engineering, generative-ai]
---

# Birgitta Böckeler

Distinguished Engineer and AI-assisted delivery expert at [[thoughtworks]], with 20+ years as a
developer, architect, and technical leader. Author of the KB's anchor [[harness-engineering]]
article ([[fowler-bockeler-harness-engineering]], 2026-04-02, published on [[martin-fowler]]'s
site), which supersedes her February 2026 memo.

Her contributions: the **guides (feedforward) vs. sensors (feedback)** and **computational vs.
inferential** taxonomy ([[feedforward-and-feedback-controls]]); the harness as a cybernetic
**governor**; the **steering loop**; three **regulation categories** (maintainability /
architecture fitness / behaviour); and **harnessability** / "ambient affordances." She frames a
coding-agent user harness as a specific form of [[context-engineering]].

She then put the model into practice in **Maintainability Sensors for Coding Agents**
([[fowler-bockeler-maintainability-sensors]], May 2026) — a field report rebuilding an app with
agents using *sensors only, almost no guides*. Findings: computational sensors (ESLint,
`dependency-cruiser`) shine at the file/function level, especially with **custom lint messages as
self-correction guidance** and **threshold-raising** instead of binary suppression; raw coupling data
is too noisy for AI alone; an **inferential AI modularity review** ("garbage collection") was the most
valuable; and **[[mutation-testing]]** is crucial once you leave testing to AI (coverage ≠
effectiveness).

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-bockeler-maintainability-sensors]]._
