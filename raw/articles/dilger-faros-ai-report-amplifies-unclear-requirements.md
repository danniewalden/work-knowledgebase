---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7471428116150849537/
title: "On the Faros AI Report: AI amplifies unclear requirements"
author: Martin Dilger
publication: LinkedIn
published: 2026-06-13
retrieved: 2026-06-13
type: article
---

# On the Faros AI Report: AI amplifies unclear requirements

**Martin Dilger** — *LinkedIn feed post, 14h ago*

---

I just read the Faros AI Report - 22,000 developers across 4,000 teams - and the numbers look awful (not that I'm surprised...)

I've been saying the same thing in every workshop: AI doesn't fix unclear requirements, it amplifies them. Now there's a 22,000-developer dataset backing that up.

On a first sight, the throughput numbers look like a dream:
task completion +33.7%, epics completed per developer +66.2%, AI-generated code now 60% of what's accepted (up from 20%).

That´s just one side of the coin.

→ Bugs per developer: +54%
→ Incidents per PR: +242.7% - more than triple
→ PRs merged with zero review: +31.3%
→ Median review time: +441.5%

The most uncomfortable finding: this happens even to teams with strong engineering practices. Good process alone doesn't absorb what AI is now producing.

AI writes code that looks correct - idiomatic, well-named, consistent style. But looking right and being right are different things, and the gaps are invisible on the surface.

Reviewers have to read every line carefully to catch them. That's slow, expensive, senior-engineer work - and it's exactly the bottleneck forming.

The report's own conclusion: more reviewers and stricter gates treat the symptom. The fix has to happen upstream - give AI (and humans) richer context and a clear spec before a single line of code is written.

And this is the part that made me sit up, because it's the exact thing I've been talking about for four years straight.

Event Modeling solve exactly this for teams: get business and engineering aligned on a visual, validated model of how the system behaves - nobody writes code - not even AI - before this is clear.

No surprise that the same artifact is what's missing from AI-assisted development too. An Event Model gives an AI agent (and the humans reviewing its output) a shared source of truth: which events exist, what triggers them, how the pieces fit. Instead of guessing intent from a messy codebase, the AI gets pointed at a model that already encodes that intent.

Smaller PRs. Reviewers who know what a change is supposed to do. An AI that's no longer guessing.

If "throughput up, confidence down" sounds familiar, happy to chat about where the gaps in your process probably are and how to fix them.

---
I´m Martin, I´m building the agentic modeling plattform on eventmodelers.ai - bringing business, engineering and ai together.

#eventmodeling #eventsourcing
