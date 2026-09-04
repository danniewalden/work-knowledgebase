---
title: Harness Absorption
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [mcateer-evolution-of-the-agent-harness, guo-survey-question-answering-to-task-completion-harness-design, harnessx-composable-adaptive-evolvable-agent-harness-foundry, harnessforge-joint-harness-and-policy-evolution, langchain-anatomy-of-an-agent-harness, willison-fireside-chat-claude-code-team, breunig-harnesses-are-situated-agents, graph-engineering-era-of-llm-agents-system-intelligence]
tags: [harness-engineering, agent-harness, harness-absorption, contested, focus]
---

# Harness Absorption

**Harness capabilities migrating into model weights, after which the harness deletes the scaffold:
train → absorb → shed → repeat.** Named and argued by
[[mcateer-evolution-of-the-agent-harness|Dan McAteer (Latent.Space, 2026-08-22)]]. It is the frame that
decides whether [[harness-engineering|harness work]] is a durable investment or temporary scaffolding, so
it belongs beside every "build more harness" argument in the KB.

## The two curves

McAteer's framing device: the harness and the model improve on **two separate curves** — "what the harness
asks of the model, and what the model can deliver in practice" — and the **gap between them is agent
effectiveness**. On that reading the 2025–26 jump in agent usefulness was **the two curves crossing**, not
either one leaping, which is why the same harness ideas failed in 2023 and worked in 2026.

His four eras: **ReAct** (harness ahead of model, so the loop thrashed) → **AutoGPT's premature autonomy**
(the harness asked for far more than the model could deliver) → **the IDE retreat** (asking much less, and
therefore working) → **Claude Code** (the curves crossing, so a demanding harness finally pays). The
supporting argument is the compounding one: *"a loop amplifies the capability a model has"* — at 95%
reliability per step, twenty steps is ≈36%, so small per-step gains change what a loop can be asked to do
at all.

*(A practitioner essay. The two-curves device is **narrative rather than measured** — neither curve is
plotted, and no metric is offered for "what the harness asks."*)

## The metric

**Progress = how much of the harness you get to delete at equal capability.** His words: *"the measure of
the pace of agent harness evolution is how much of the harness you get to delete, while retaining the same
capability level."* That is a genuinely usable instrument — it turns "the models got better" into a
countable property of your own repo — and it is the inverse of every "our harness grew to 512k LOC" boast.

## Evidence, every item marked

None of it is independent measurement, and the markers travel with the numbers:

- **Compaction into weights.** The GPT-5.1-Codex-Max launch line — "The first model natively trained to
  operate across multiple context windows through compaction" — i.e. auto-compaction migrating out of
  harness code and into the model. **[[openai]] vendor self-report**, relayed.
- **Claude Code's system prompt cut by ~80%.** **[[anthropic]] self-report about its own product**, though
  corroborated first-hand in [[willison-fireside-chat-claude-code-team]] — and *per frontier model*, not
  globally.
- **codex-1 RL'd inside its own environment.** **Vendor self-report**, relayed.
- **Harness-Bench: 52.4 → 76.2 across harnesses on 106 tasks with zero model change** (a 23.8-point
  spread), glossed "half the agent is the harness". **SECONDHAND, unlinked, and there is no primary
  capture of Harness-Bench anywhere in this KB** — flag it as secondhand at every use. It is the most
  quoted harness number in the KB and the weakest sourced.
- **ARC-AGI-3 13.3% → 38.3% (GPT-5.6 Sol) from retained reasoning + compaction.** **[[openai]] self-report
  about its own model, relayed.** The same two mechanisms reappear one generation later with a named
  harness and a benchmark-maintainer post attached — see the harness-leverage section on
  [[agent-harness]] — which makes the claim *traceable*, not independent.

## The academic form

[[guo-survey-question-answering-to-task-completion-harness-design|Guo et al. (arXiv:2606.20683)]] make this
the fourth rung of their paradigm ladder: "**internalization**; agentic behaviors are increasingly trained
into model parameters", plus co-evolution *(arXiv **preprint**, not peer-reviewed)*. So absorption is not
only a practitioner's essay — a 17-author survey names the same direction from the research side.

The **mechanism as engineering** already exists in two method papers:
[[harnessx-composable-adaptive-evolvable-agent-harness-foundry|HarnessX]] "closes the harness-model loop by
turning trajectories into both harness updates and model training signal", and
[[harnessforge-joint-harness-and-policy-evolution|HarnessForge]] co-evolves the harness–policy pair rather
than freezing the model. *(Both preprints, and **their reported gains are contested** — see
[[harness-evolution]].)*

## The counter-claim, given equal weight

[[langchain-anatomy-of-an-agent-harness|LangChain's Harrison Chase]] argues the opposite trend: better
models **expand** what harnesses must do rather than shrinking them, with Claude Code at 512k+ LOC and
growing. **The wiki does not pick.** Both can be true at once — the *prompt* shrinks while the *codebase*
grows — and note that the two claims are not even measured in the same unit: McAteer counts deleted
scaffold, Chase counts lines of harness. Until someone measures both on one product over one period, this
is two plausible directions rather than a resolved trend.

A second complication, from [[breunig-harnesses-are-situated-agents|Breunig]]: model–harness **co-training
may be routine and undisclosed** (his aside on Meta training Muse Spark to know its harness — *"much like
others, they just don't write about it"*). If so, absorption is happening faster than any published record
shows, *and* every benchmark claiming to isolate harness quality from base-model strength is harder to
trust. An unevidenced aside; carry it as an open question.

## What absorption leaves

The useful half of the thesis is the residue. A model cannot absorb **permissions, identity, trust or
[[agent-legibility|legibility]]** — "a model that absorbs permissions into itself has dissolved
permissions" — so on this reading those are the durable part of harness work and much of the rest is
scaffolding with a shelf life. Where the surviving harness turns around and becomes a surface aimed at the
*human* rather than the model, see [[attention-interface]].

## Open questions

- **Which layers absorb, and in what order?** Compaction and long-context operation went first. Nothing
  says whether tool use, verification or coordination follow, or whether they can.
- **Does the deletion metric hold up in practice?** No one has published a harness diff over time. It is
  cheap to instrument on your own repo and would be the first real datum here.
- **Is orchestration next?** McAteer expects [[multi-agent-orchestration]] to be absorbed into weights;
  [[graph-engineering-era-of-llm-agents-system-intelligence|Feng et al.]], the same month, argue
  coordination is a *system*-level property that a single agent's capabilities "cannot resolve". Two
  2026-08 claims about the same near future pointing in opposite directions — see [[graph-engineering]].

## Related

[[agent-harness]] · [[harness-engineering]] · [[harness-evolution]] · [[attention-interface]] ·
[[context-engineering]] · [[token-budget-quality-cliff]] · [[agent-legibility]]

_Sources: [[mcateer-evolution-of-the-agent-harness]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[harnessx-composable-adaptive-evolvable-agent-harness-foundry]] · [[harnessforge-joint-harness-and-policy-evolution]] · [[langchain-anatomy-of-an-agent-harness]] · [[willison-fireside-chat-claude-code-team]]._
