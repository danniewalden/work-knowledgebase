---
title: "Osmani — Software Factories, Light and Dark"
type: source
created: 2026-07-27
updated: 2026-07-27
sources: [addyosmani-software-factories-light-and-dark]
raw_file: [raw/articles/addyosmani-software-factories-light-and-dark.md]
tags: [loop-engineering, software-factory, harness-engineering, comprehension-debt, focus]
---

# Osmani — Software Factories, Light and Dark

[[addy-osmani|Osmani]] (addyosmani.com, 2026-07-20) — the first dedicated primary for the **[[software-factory]]**
rung of the loop→harness→factory stack, and the KB's anchor for **light vs dark factories**, **back
pressure**, and the **loops-vs-graphs** question. Leans heavily on [[dex-horthy|Dex Horthy]]'s (HumanLayer)
AI Engineer World's Fair talk *"Harness Engineering is not Enough: Why Software Factories Fail."*

## The stack: loop → harness → factory

"**The loop is the atom. The factory is the loop at scale.**" A **loop** is one agent doing a single job on
repeat (gather context → act → check → repeat until done) — the smallest unit of agentic work; loop
engineering means you design the small system that prompts it instead of prompting turn by turn. A
**[[agent-harness|harness]]** is "the walls around a loop" — sandbox, tools, memory that survives runs, and
the gates that decide what "done" means (the loop is the *behavior*, the harness is the *environment*). A
**[[software-factory|software factory]]** is "many harnessed loops running at once, fed by a queue of work
and drained through a review gate into production, with humans owning the whole thing from above… **not a
bigger agent; it is an org chart made of loops.**" (The term dates to Bob Bemer's 1968 "economics of program
production"; the old dream failed on the difficulty of "stamping out ideas," now worth a fresh look.)

**The factory drawn:** intent (leadership + engineers) and signals (incidents, user requests) feed a queue →
the harness picks an item and builds a change → automated checks (CI, tests, static analysis, scanning) →
**the review gate** → deploy → monitoring feeds back into signals. Every box is near-zero-cost **except the
review gate** — the amber "judgment" box that stubbornly resists scaling. That is the crux.

## Light vs dark

A **dark factory** runs "with the lights off" — code ships that no human has read, verified only by machines
(the manufacturing image: FANUC/Xiaomi lights-out plants; "in software, the floor is the diff"). It's
"surprisingly easy at first" because removing review makes throughput feel like breaking the sound barrier —
but it doesn't pay down **[[comprehension-debt|comprehension debt]]** (the widening gap between how much code
exists and how much any human understands); "it takes it on as fast as it can, with the tests green the whole
way." Horthy ran a fully automated factory ~4 months with no human reading the code; the reckoning "will not
be a dramatic 'it all goes sideways' moment — it will be quiet and late." A **lit factory** is the same
pipeline "with the lights left on where judgment lives" — agents still do most of the building, but the point
of human judgment moves **upstream** to product/design/architecture (review a 200-line plan, not chase 2,000
lines of generated code to find what the decision was). The safety net is "perfectly ordinary architectural
practices we've always known and mostly ignored" — good types/signatures, test seams, legible layout, short
call stacks, well-defined boundaries (small blast radius), DI — now "doing a second job as a cheap and
hard-to-fake safety net." It must live **outside the model**, because the coding agents that feel most capable
(Claude Code, Codex) are RL-trained against their own harness — fluent with tools, not with long-term
maintainability.

## Back pressure — verification is the constraint

"**Back pressure is the rule that you can only hand a loop as much autonomy as you can cheaply and reliably
verify, and not one inch more. Verification, not generation, is the real constraint on a factory.**"
Generation is a wide mouth, verification the narrow neck — speeding up the mouth just deepens the pile at the
neck. Horthy: the problem isn't volume, it's "a surplus of bad PRs." Improving the model won't automatically
close the gap, because architectural excellence has cost functions "measured in months and years" — no tidy
gradients to train on. **What earns a loop the dark:** a check that's cheap, high-frequency, and hard to fake
(green/red oracle, type gates, property tests, review-agent-plus-rubric), answering immediately without
drift; short loops (Horthy's rule of thumb: an agent holds 3–10 steps, loses the thread past ~20). Keep the
lights on where a wrong answer is expensive and only a person can catch it (auth, billing, public API
contracts, year-shaping decisions). "The hard, skilled job is deciding where to put each switch" — all-dark
gets torn down in four months, all-lit is a review bottleneck.

## Loops, graphs, or state machines

Directly answers the "graph engineering" framing circulating since ~07-20. Handing an agent a task, "you're
probably going to build a graph around it" (finite state machine / conditionally-linked calls) — nodes are
explicit steps, edges explicit conditions. Most of that structure was already there (any code is a
control-flow graph); "the genuinely new move was trying to throw the diagram away," leaning on a loop where
the model picks the path tool-call by tool-call — "that felt like liberation, right up until it met a
ten-year-old codebase." So **"owning your control flow is really just walking the graph back around the
loop"** — back pressure drawn as a diagram; you trade some agent freedom for mandatory checks and legible
failure points (point at the node that killed the run). Horthy: most "agents" are "mostly deterministic code,
with LLM steps sprinkled in at just the right points." Seen in LangGraph, LlamaIndex Workflows, Jerry Liu's
hybrid workflow-graph, David Khourshid's "it's state machines and the actor model in new clothes." (Not a
*knowledge* graph — a predefined directed graph of how work should flow.) Ties to
[[nick-tune-graphs-memory-skills-agents]].

## Where the human goes

"The person never left the factory. They moved." Engineers own the **outer loop** (decide the approach,
verify diagnosis+implementation, approve, carry the consequence); agents run the **inner loop** (investigate
→ implement → test → report). The boundary is **evidence** (diffs, tests, logs, a brief why); types/seams/
rubrics make oversight cheap. "You're not down on the line writing changes any more; you're up at the end of
the production line designing it and guarding the gate." "Robots are fine operating in the dark, but humans
need to see what they're doing."

## Connections

Grows [[loop-engineering]] with the [[software-factory]] rung + light/dark + back-pressure + loops-vs-graphs;
builds on [[addyosmani-loop-engineering]], [[addyosmani-own-the-outer-loop]], [[addyosmani-earning-taste-and-judgment]];
[[dex-horthy]] (the factory-failure primary it leans on); ties to [[fowler-agentic-programming]] +
[[stripe-minions-one-shot-coding-agents]] (factory/unattended agents), [[comprehension-debt|comprehension &
cognitive debt]] via [[willison-understand-to-participate]] + [[tornhill-ai-readable-code-series]],
[[langchain-the-art-of-loop-engineering]] (maker≠checker/verification), [[bockeler-context-engineering-coding-agents]],
[[nick-tune-graphs-memory-skills-agents]] (graphs). Caveat: a lead loop-eng voice synthesizing another's
(Horthy's) talk; opinion/field-report, not measured — but the empirical measured cousin is
[[ahe-agentic-harness-engineering]]. Marked 100% human-written by Pangram.

_Source: [[addyosmani-software-factories-light-and-dark]] (raw/articles)._
