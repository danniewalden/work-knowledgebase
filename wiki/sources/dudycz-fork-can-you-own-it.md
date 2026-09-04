---
title: "Oskar Dudycz — You Can Fork a Package, but Can You Own It?"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [dudycz-fork-can-you-own-it]
raw_file: [raw/articles/dudycz-fork-a-package-can-you-own-it.md]
tags: [software-architecture, dependencies, supply-chain, agentic-coding, off-thread]
---

# Oskar Dudycz — You Can Fork a Package, but Can You Own It?

Blog post by **[[oskar-dudycz]]** (Event-Driven.io, 2026-06-08, CC BY-SA 4.0). Source:
`raw/articles/dudycz-fork-a-package-can-you-own-it.md`. **Largely off-thread** for this KB (dependency
posture / supply-chain ownership) — captured under the people-watch *anything-substantive* rule; filed
mainly for the **"LLM as a fork"** hook.

## The argument

Responding to **[[mitchell-hashimoto]]** ("fork your dependencies, trim them, don't update unless it
breaks"), Dudycz agrees but reframes: the real issue **isn't forking, it's ownership** — "we don't
*decide* to take a dependency, we just install one." Supply-chain attacks, license dramas, half-finished
SBOMs all trace to taking on a dependency without deciding to. Forking React isn't realistic; the advice
holds for small libs and breaks for big ones ("the small stuff we can hold; the big stuff stays a bet").
He argues for an explicit **dependency posture**: inventory (SBOM, e.g. `npm sbom`), criticality,
lifecycle/upgrade strategy, **bus factor**, mitigation (often *paying the maintainer* is cheaper than
rebuilding and lowers bus factor), and response time. "Architecture… is about choosing which liabilities
we are willing to own."

## The on-thread hook — "LLM as a fork"

Dudycz rejects the claim that LLMs dissolve the dependency question: **"I don't see how LLMs can change
the cost of *owning* code. They can (maybe) change the cost of *producing* it."** Writing the small thing
was never the hard part — *owning, understanding, maintaining, being on the hook at 2 a.m.* is, "and no
model takes that off our plate." The old move was "install and move on"; the new move is **"vibe it and
move on"** — "same missing decision, new flavour." He frames LLM-built, unowned tools as a new strain of
**Shadow IT**.

## Why it matters here

Off the core focus, but the "LLM as a fork" point is a useful **ownership/responsibility caveat** for the
[[agentic-coding]] / [[unattended-coding-agents]] thread: cheap *production* of code does not reduce the
cost of *owning* it — a counter-weight to "vibe coding" optimism that complements
[[tornhill-cannot-trust-agent-codescene-mcp|Tornhill's]] "you're still on the hook for quality." Caveat:
opinion essay; the bulk (SBOM, bus factor, .NET license dramas) is general software-supply-chain
commentary, not on-thread.

## Touches

[[oskar-dudycz]] · [[agentic-coding]] · [[unattended-coding-agents]] · [[mitchell-hashimoto]]

_Source: `raw/articles/dudycz-fork-a-package-can-you-own-it.md`._
