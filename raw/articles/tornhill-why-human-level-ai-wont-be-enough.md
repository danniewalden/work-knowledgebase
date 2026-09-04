---
source_url: https://adamtornhill.substack.com/p/why-human-level-ai-wont-be-enough
title: Why Human-Level AI Won't Be Enough
author: Adam Tornhill
publication: Code for Humans and Machines (Substack)
published: 2026-06-30
retrieved: 2026-07-10
type: article
---

# Why Human-Level AI Won't Be Enough

*What if today's best engineers aren't enough for tomorrow's systems? By following today's trends, we may discover that human-level code quality was never the problem we needed to solve.*

ADAM TORNHILL — JUN 30, 2026 — section: TRENDS & REFLECTIONS

Having an AI produce code at the quality of a human expert has been the dream and definitive benchmark for years now. Recent progress on both foundation models and, perhaps more important, the agentic harnesses have made this dream seem less distant.

Let’s assume we (or BigTech) succeed: tomorrow’s coding agents perform at the level of today’s best software engineers. My argument is that this still wouldn’t be enough.

## AI Raises the Quality Bar

A popular claim these days is that coding agents already write better code than many programmers. That’s probably true. And the bar keeps getting pushed.

So why would a coding agent performing at the level of a human expert still be inadequate?

The reason is that AI itself changes the quality threshold required to keep systems stable.

The most obvious change is that tomorrow’s systems will be much more complex than today’s. We just need to look back at our history. Each major productivity increase in software history has made us take on larger and more complex problems. Improved capabilities let us automate tasks we couldn’t automate before. Lehman’s laws of software evolution captured that force decades ago: useful software keeps changing, growing, and accumulating complexity unless we actively fight it.

> Software systems keep changing, growing, and accumulating complexity.

Another change is that an agent is orders of magnitude faster than a human in terms of raw code generation. That speed causes problems already today. And still: future systems are likely to evolve at a pace that is significantly higher than today where we still have plenty of constraints and manual checkpoints in our delivery pipelines.

Combine these two evolutionary pressure points, and you get codebases that few — if any — of today’s experts could stay on top of.

## Scale Changes the Problem

These pressure points also explain why human expert level is the wrong bar.

The first challenge is that defect opportunities scale with code volume and change volume. It’s a safe bet to claim that future systems will have that relationship, too. Larger modules, larger changes, and higher code churn have been linked to fault risk for decades.

Without a corresponding breakthrough in verification and validation techniques, a more ambitious and larger system developed at that breakneck speed by a future human-expert-level AI would be a fertile breeding ground for bugs and quality risks. We’d get to truly experience what it means to be wrong at scale.

Second, coding agents are based on a stochastic core. At their very heart, LLMs are prediction machines. Even if we manage to reduce their defect rate to something like the magical six sigma, lessons from industrial production still tell us that the potential for error will always be there.

A tiny failure rate is manageable at human throughput. But generate enough code, and rare errors stop being rare at the system level. A one-in-a-million mistake sounds impressive...until you start making millions of decisions. All the time. That’s one consequence of scale.

So today’s bar is too low for tomorrow’s AI. AI changes the scale of the problem.

## Embrace Imperfection

If human-expert code is insufficient, then quality, correctness, and fit need to be addressed with a different approach, too.

One possible response is to aim for superhuman code quality. Personally, I don’t think that’s a realistic path. Where would we even get the training data and feedback signal? Synthetic data, but from what and whom? The hardest software decisions are contextual, and rarely come labeled and packaged as reusable training examples. And yes, AGI has been “just a few years away” for the better part of fifty years. I wouldn’t hold my breath.

More importantly, human-level coding may not even be the problem we need to solve.

Today, my approach to taming agents has been to accept their unreliability. I suspect that direction holds the keys to the future of software quality, too.

So, perhaps, instead of aiming to generate perfect code, we’d need to double down on creating environments where unreliable agents reliably produce acceptable outcomes. The future might belong to those organizations that embrace that imperfection today.
