---
title: Software Factory
type: concept
created: 2026-07-27
updated: 2026-08-31
sources: [dilger-lights-off-software-factory-dead-end, dilger-trust-needs-to-be-engineered, addyosmani-software-factories-light-and-dark, stripe-minions-one-shot-coding-agents, fowler-agentic-programming, prefect-loops-vs-graphs, jwilger-agent-skills-factory-pipeline]
tags: [loop-engineering, software-factory, harness-engineering, comprehension-debt, focus]
---

# Software Factory

**The top rung of the loop → harness → factory stack.** A software factory is **many harnessed
[[loop-engineering|loops]] running at once, fed by a queue of work and drained through a review gate into
production, with humans owning it from above** ([[addyosmani-software-factories-light-and-dark|Osmani]]).
"The loop is the atom; the factory is the loop at scale" — and crucially it is **"not a bigger agent; it is
an org chart made of loops."** The paradigm shift is from writing code to **building and running the factory
that writes it** — the unit of work moves up from the diff to the loop, the [[agent-harness|harness]], and
the flow between them. (The dream is old — Bob Bemer's 1968 "economics of program production" — and mostly
failed on "the difficulty of stamping out ideas"; the last two years made it worth a fresh look.)

## The wiring diagram

Intent (leadership + engineers) and signals (incidents, user requests) feed a **queue** → the harness picks
an item and builds a change → **automated checks** (CI, tests, static analysis, scanning) → the **review
gate** → deploy → monitoring feeds back into signals. Every box is near-zero-cost **except the review gate** —
the "judgment" box that stubbornly resists scaling. That gate is the whole argument.

## Light vs dark

- **Dark factory:** code ships that **no human has read**, verified only by machines (the lights-out
  manufacturing image — FANUC/Xiaomi; "in software, the floor is the diff"). Easy at first — removing review
  makes throughput feel like breaking the sound barrier — but it doesn't pay down
  [[comprehension-debt|comprehension debt]], it "takes it on as fast as it can, with the tests green the
  whole way." The reckoning is "quiet and late." [[dex-horthy|Dex Horthy]] ran one ~4 months (no human
  reading the code) and needed painstaking manual debugging to recover.
- **Lit factory:** the *same* pipeline "with the lights left on where judgment lives" — agents build, but a
  human reads what ships **and** the point of judgment moves **upstream** to product/design/architecture
  (review a 200-line plan, not 2,000 lines after the fact). The safety net is ordinary architecture doing a
  second job (types, test seams, legible layout, short call stacks, small blast radius, DI) — and it must
  live **outside the model**, because capable coding agents are RL-trained for tool fluency, not long-term
  maintainability.

## Back pressure — the governing rule

**"You can only hand a loop as much autonomy as you can cheaply and reliably verify, and not one inch more.
Verification, not generation, is the real constraint."** Generation is a wide mouth, verification the narrow
neck; speeding the mouth just deepens the pile at the neck. **What earns a loop the dark:** a check that's
cheap, high-frequency, and hard to fake (green/red oracle, type gates, property tests, review-agent + rubric),
immediate and non-drifting; short loops (Horthy: an agent holds 3–10 steps, loses the thread past ~20). Keep
the lights on where a wrong answer is expensive and only a person can catch it. "The hard, skilled job is
deciding where to put each switch" — all-dark self-destructs in months, all-lit is a review bottleneck.

## Loops vs graphs

"Owning your control flow is really just walking the graph back around the loop" — a predefined directed
graph (nodes = steps, edges = conditions) is **back pressure drawn as a diagram**: trade agent freedom for
mandatory checks and legible failure points. The "throw the diagram away, let the model pick the path
tool-call by tool-call" move "felt like liberation right up until it met a ten-year-old codebase." Seen in
LangGraph, LlamaIndex Workflows, David Khourshid's "state machines in new clothes"; adjacent to
[[nick-tune-graphs-memory-skills-agents|Nick Tune's graph substrate]].

This is the same move [[jeremiah-lowin|Lowin]]/[[prefect|Prefect]] ([[prefect-loops-vs-graphs]]) name as
**[[graph-engineering|directed agentic graphs]]** — macro orchestration across many agents, one node per
full agentic invocation, control returning to the orchestrator at each edge. A factory's "org chart made
of loops" *is* such a graph; Osmani's back-pressure and Lowin's node-level capability scoping ("don't
hand your agent a bazooka") are the same governing instinct drawn at different altitudes. See
[[graph-engineering]] for the full treatment.

## Relationship to neighbours

- **[[loop-engineering]]:** the factory is loop engineering's largest unit; back-pressure and the
  inner/outer-loop split ([[addyosmani-own-the-outer-loop]]) are its governing rules.
- **[[harness-engineering]]:** "harness engineering is not enough" ([[dex-horthy|Horthy]]) — a good harness
  makes one loop reliable but doesn't decide *which* loops earn autonomy; that's the factory-level judgment.
- **[[unattended-coding-agents]] / [[stripe-minions-one-shot-coding-agents]]:** Stripe's minions (*Stripe's own figure*, 1,000+
  merged PRs/week behind deterministic shift-left gates) are a lit-leaning factory in production.
- **[[ahe-agentic-harness-engineering]]:** the measured cousin — an agent evolving the harness inside the
  factory's improvement loop.
- **vs. [[event-modeled-agent-design]]:** the EM seam is now partly *worked* —
  [[john-wilger|Wilger's]] factory pipeline ([[jwilger-agent-skills-factory-pipeline]]) is a
  software factory whose **work-items are event-model slices and whose review-gate oracle is each
  slice's [[given-when-then|GWT]]** (rejected unless it hits an external boundary), with the event model
  as the upstream human-authored spec driving the whole line ([[dilger-event-modeling-agent-harness]] is
  the harness-side counterpart).

## The named dissent — "the lights-off factory is a dead end" (Dilger, 2026-08-16)

The dark-factory section above had no practitioner arguing against it by name. It has one now, and from
someone otherwise maximally bullish on agentic engineering
([[dilger-lights-off-software-factory-dead-end]]):

> "Every single team I know who went down that route circled back. I don't practice it either, even
> though I'm all in on agentic engineering."

His failure mode is specifically an **incident** failure mode — "production burning and no one there to
navigate the code base ( as no one has ever seen it )" — i.e. [[comprehension-debt]] coming due at the
worst moment. And he states the bind this page circles: *"you can't do full code reviews - it'll not be
sustainable with the increased output - you just moved the bottleneck. But you can't do no code-reviews
either."*

His answer is **layers of trust** rather than more review: model-as-spec with GWT guard rails →
executable specs written before any code → static gates with defined consequences (*files changed outside
the Slice Under Development = immediate fail*) → a **2–3 minute structural** review that is explicitly
not functional, "at this point we already know it works." Failures are disposed of, not repaired — the
slice goes back to "planned" and a learning is recorded.

Two things this contributes that the page lacked:

- **The reason to keep a human in the loop is comprehension, not correctness.** "I keep connected to the
  code base… If something goes wrong, I roughly know where to look." That is a different justification
  from back-pressure, and a stronger one against the dark factory.
- **A stated asymmetry about what is reversible.** He does not much care how a slice is implemented
  internally — "any bad implementation can be easily replaced" — but cares a great deal about system
  structure and *the shape of the persisted events*. Compare the reversibility axis on
  [[autonomy-ladder]]: the irreversible decision here is the event schema.

The paired post two days earlier ([[dilger-trust-needs-to-be-engineered]]) gives the general form:
constrain what the agent may decide, and there is less to verify — *"not by doing more reviews, but by
making most of them obsolete."*

*Caveat: "every single team I know" is unattributed hearsay, and the pipeline described is the one his
own platform supports.*

_Sources: [[addyosmani-software-factories-light-and-dark]] · [[stripe-minions-one-shot-coding-agents]] · [[fowler-agentic-programming]] · [[prefect-loops-vs-graphs]] · [[jwilger-agent-skills-factory-pipeline]]._
