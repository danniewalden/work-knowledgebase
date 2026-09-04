---
title: Dex Horthy
type: entity
created: 2026-07-27
updated: 2026-07-27
sources: [addyosmani-software-factories-light-and-dark]
tags: [person, loop-engineering, software-factory, harness-engineering, focus]
---

# Dex Horthy

Co-founder of **HumanLayer** and author of the **"12-factor-agents"** framing. Named in the KB via
[[addyosmani-software-factories-light-and-dark|Osmani's "Software Factories, Light and Dark"]], which leans
heavily on Horthy's AI Engineer World's Fair talk **"Harness Engineering is not Enough: Why Software Factories
Fail"** (youtu.be/htM02KMNZnk).

## Positions attributed (via Osmani)

- **"Harness engineering is not enough."** A good [[agent-harness|harness]] makes one loop reliable but
  doesn't decide *which* loops can safely run unattended — that judgment is the [[software-factory|factory]]
  level, and getting it wrong is why software factories fail.
- **The dark-factory failure, from experience.** Ran a fully automated code factory ~4 months with no human
  reading the code; the failure was severe and required painstaking manual debugging to pinpoint — the
  concrete evidence behind [[comprehension-debt|comprehension debt]] as "quiet and late."
- **Short-loop rule of thumb:** an agent holds up for **3–10 steps**, then starts losing the thread past
  ~20 (context accumulation → wandering) — the practical basis for [[software-factory|back pressure]] and
  "what earns a loop the dark."
- **"Most agents aren't very agentic"** — "mostly deterministic code, with LLM steps sprinkled in at just
  the right points"; the loops-vs-graphs point that owning your control flow beats letting the model pick
  every path.
- The nightly **one-anti-pattern cron** (a GitHub Action that fixes exactly one lint/optional-prop issue,
  commits, opens one small readable PR) as an example of a tight, low-risk unattended loop.

## Status

**Watch-list candidate** flagged during the 2026-07-27 ingest — a factory-failure/loop-engineering primary
voice worth its own watch entry (HumanLayer; 12-factor-agents). Only referenced second-hand so far (via
Osmani); his talk and 12-factor-agents writing are the primaries to capture directly.

## Connections

[[software-factory]] · [[loop-engineering]] · [[harness-engineering]] · [[addyosmani-software-factories-light-and-dark]]
(the source that surfaced him) · [[addy-osmani]].
