---
title: Context Engineering
type: concept
created: 2026-06-11
updated: 2026-09-04
sources: [sadalage-chandrasekaran-making-data-ready-for-agentic-ai, bockeler-context-engineering-coding-agents, fowler-bockeler-harness-engineering, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, nick-tune-graphs-memory-skills-agents, roden-event-sourcing-meets-mcp-whole-story-for-llms, martinfowler-prince-building-reliable-agentic-ai-systems, ng-spec-driven-development-is-waterfall-in-markdown, guo-survey-question-answering-to-task-completion-harness-design, mcateer-evolution-of-the-agent-harness, macmanus-pocock-wayfinder-skill-fog-of-war, miracle-my-loop-engineering-workflow, addyosmani-code-agent-orchestra, wong-graph-engineering-wiring-agents-into-an-organization]
tags: [context-engineering, harness-engineering, agent-engineering]
---

# Context Engineering

The practice of deciding **what information enters the model's context window at each step** —
and what to compress, retrieve, or leave out. It optimises the *input* to the model. The crispest
definition comes from [[bockeler-context-engineering-coding-agents|Böckeler]] (quoting Bharani
Subramaniam): **"curating what the model sees so that you get a better result."**

## The taxonomy (Böckeler, 2026-02-05)

[[birgitta-bockeler]]'s [[bockeler-context-engineering-coding-agents|primer]] gives the concept its
vocabulary. Context configuration splits into **reusable prompts** — **Instructions** ("do this") vs
**Guidance** (rules/guardrails) — and **context interfaces**, descriptions telling the LLM *how to
fetch more if it decides to*: **Tools**, **[[model-context-protocol|MCP]] servers**, and **Skills**
(load-on-demand). Files in the workspace are the most powerful interface, so [[ai-readable-code|how
well your code reads as context]] matters. Two axes organise the rest: **who loads it** (LLM /
human / agent-software at deterministic lifecycle points) and **how much** (balance — bigger windows
don't justify dumping; build rules up gradually; transparency about what fills the window is a key
tool feature). Her **Instructions vs Guidance** split prefigures the harness-engineering **guides vs
sensors** distinction below. The honest caveat — **"illusion of control"**: "in spite of the name,
this is not *really* engineering," execution still depends on LLM interpretation, so think in
probabilities, not "ensure it does X."

Techniques drawn from the sources: **compaction** (summarise older history when the window fills),
**tool-call offloading** (keep head/tail tokens, write the full output to the filesystem),
**retrieval** ([[retrieval-augmented-generation]]) of only the relevant docs per step, **Skills /
progressive disclosure** to avoid loading everything up front, and positioning the most important
content at prompt boundaries to counter "Lost in the Middle." All are responses to [[context-rot]].

## Relationship to harness engineering

The two are distinct but nested:

- **Context engineering** controls *what the model sees*.
- **[[harness-engineering]]** controls *the environment the agent operates in* — what it can
  access, what gets verified, what forces a retry.

Per [[fowler-bockeler-harness-engineering]], context engineering supplies the *means* to make
guides and sensors available to the agent, so engineering a coding-agent user harness is "a
specific form of context engineering." [[langchain-anatomy-of-an-agent-harness]] frames harnesses
as "largely delivery mechanisms for good context engineering." Both sit inside [[agent-engineering]].

An external, non-practitioner statement of the same boundary arrived in 2026-06:
[[guo-survey-question-answering-to-task-completion-harness-design|Guo et al. (arXiv:2606.20683)]] make
"workflows and context engineering" paradigm 2 of four and harness engineering paradigm 3, with the dividing
line stated in one word — **context engineering "remains fundamentally feedforward"**, whereas the harness
"**closes the loop**: the model acts, observes environment responses, and reasons over observations to decide
its next step." *(arXiv preprint — not peer-reviewed.)* That is [[feedforward-and-feedback-controls]]'s
guides-vs-sensors distinction reached independently by an academic group, and it is the crispest available
formulation of why these are two pages. In the same survey's decomposition, context engineering owns exactly
one of six harness responsibilities — the **context manager**, which "determines what information enters the
model context, when and in form" (see [[agent-harness]]). One further wrinkle from
[[mcateer-evolution-of-the-agent-harness|McAteer]]: context management is the clearest case of
[[harness-absorption]] — compaction has begun migrating from harness code into model weights, moving a
context-engineering concern inside the model.

## The substrate view (Tune)

[[nick-tune]] ([[nick-tune-graphs-memory-skills-agents]]) restates this from the build side: *"the model
is the commodity, the context is the product."* He decomposes what sits **underneath** an agent into
**Graph** (a queryable world model — what exists and how it connects), **Memory** (continuity: what was
true at a past instant and what changed), and **Skills** (encoded judgment), with the **Agent** loop on
top. Two of these are the KB's own threads in other clothes: **Memory** as a point-in-time-queryable
history is [[event-sourcing]], and the **Graph** is [[agent-legibility]] delivered as structure rather
than ad-hoc grepping (so the agent can reason about state and a change's blast radius).

## A skill *is* context management — and what a child agent needs ([[macmanus-pocock-wayfinder-skill-fog-of-war|Pocock, 2026-08-20]])

The best one-line definition of a skill in the KB, and it belongs on *this* page rather than under
tooling: *"Whenever you're thinking about context management — **because that's really what a skill is,
you're managing the context of the agent you're working in** — you need to think about the information
flow."* A knowledge file is about the domain; **a skill is about what enters the window, and when.**

Pocock's `/wayfinder` skill derives its whole design from one question — *"what does the **child** need in
that situation?"* — and the answer is two artifacts: **the map** (everything else: all the decisions
already made) and **the ticket** (the specific task that goes into the session).

**Four sources independently converge on the same parent→child contract**, which is arguably this batch's
most robust practitioner consensus: **one authoritative shared artifact + one scoped assignment.**

| Source | The shared artifact | The scoped assignment |
| --- | --- | --- |
| [[macmanus-pocock-wayfinder-skill-fog-of-war]] | the **map** | the **ticket** |
| [[miracle-my-loop-engineering-workflow]] | the contract document — *"It is the contract; **do not re-derive what it settles**"* | the written **commission** |
| [[addyosmani-code-agent-orchestra]] | upstream report files (`DATA.md`, `LOGIC.md`) the child must read first | the subagent brief + explicit file ownership |
| [[wong-graph-engineering-wiring-agents-into-an-organization]] | **authoritative** state (the actual diff, the actual test output) | per-node work, with convenience summaries kept separate |

Wong states the failure mode the contract exists to prevent: if every node keeps private context and
passes a one-line summary, you get *"the multi-agent version of a game of telephone — the reviewer agent
approving something the writer agent never actually did."*

**And naming is treated as load-bearing engineering, not flavour.** *"If you just call everything a
ticket, or if you just refer to it in different ways in different places, then it's going to be really
confused and you're going to get strange behavior. Whereas if you use these very specific, what I call
**leading words**, to lead the agent to understand exactly what each part is… then you've got your
skill."* He built an (unreleased) **AI coding dictionary** and made all his skills and courses conform to
it, and he names what he is doing: *"**I realized that I needed a ubiquitous language between me and the
agent.** Between me and the agent, there is a communication barrier."* That is
[[domain-driven-design|Evans's]] ubiquitous language with a new second party, arrived at from pure
agent-mechanics reasoning with no DDD framing — directly relevant to this KB's
[[event-modeling]] thread, and note his aside that **agents are *"really good at domain modeling,
actually."*** *(An unevidenced aside in an interview — convergent framing, not support for any claim about
how well agents model domains.)*

**The fog of war is the honest middle between "write the spec" and "just prompt."** *"You can't quite
decide everything right at the start… You can make certain decisions, and those certain decisions sort of
lead you there and push further out into the fog of war."* So: **plan iteratively, but keep a durable map
of what has been decided.** His selection rule between his two skills is clean — *"Use 'grill me' in cases
where you feel like you can plan the whole thing in a single session… For stuff where you don't know the
path ahead… use wayfinder"* (session-sized vs multi-session uncertainty) — and his ticket taxonomy
(grilling / prototype / research / **task**, where task is *"basically, just anything the human needs to
do that the agent can't do"*) gives the plan **first-class slots for human work.** Compare
[[dilger-spec-driven-development-needs-four-phases]] and
[[ng-spec-driven-development-is-waterfall-in-markdown]].

*(A ~1,450-word promotional interview on release week: **no measurement, no comparison, no outcome data**
— not even a self-reported before/after on planning time. Its only quantities are audience metrics
(220,000 GitHub stars, 347,000 subscribers), which say nothing about efficacy. The dictionary underpinning
the terminology claim is **unreleased and unexaminable**, and the skill's actual contents are images not
transcribed in the capture.)*

## Events as context (Roden, 2026-06-21)

[[golo-roden]] ([[roden-event-sourcing-meets-mcp-whole-story-for-llms]]) makes a data-side context
argument: *"an average model with excellent context beats a top model lacking context,"* where context
means above all the **data** the model can reach. He claims **events are the natural language for
LLMs** — business-named (semantics in the data, not status codes), chronological (readable as a
narrative, closer to text than a table), and self-contained — so an [[event-sourcing|event store]]
delivers the richest context "without requiring additional preparation." This is the same instinct as
Tune's **Memory** below: a point-in-time-queryable history is the highest-quality context source. The
flip-side payoff of the same log is [[agent-explainability]].

## Context discipline in production (PRINCE, 2026-06)

[[martinfowler-prince-building-reliable-agentic-ai-systems|Bayer's PRINCE]] supplies a regulated worked
example of the core principle: *"larger context windows did not remove the need to be selective about
what each agent sees."* It deliberately **does not treat the prompt as one container** — planning context
goes to Think&Plan, retrieval context to the Researcher, evidence context to the Reflection agent,
synthesis context to the Writer — reducing **context pollution** and making each agent independently
evaluable. Concrete moves: Text-to-SQL injects only the *relevant schema subset*, not the full schema;
the Reflection agent gets the question + collected evidence, not the whole history. Reliability "comes
from engineering both the context the model sees and the harness within which it acts."

## The missing context is social, not textual (Ng, 2026-03)

Every source above treats context as *material that exists somewhere and must be selected, compressed and
routed*. [[ng-spec-driven-development-is-waterfall-in-markdown]] adds the case where the context **does
not exist in written form at all** and no retrieval strategy can reach it: the designer's "that flow
breaks for screen readers," the DevOps lead's "we can't deploy that behind the canary setup," the scope
change that happened in a Slack thread forty minutes after the spec was committed. His observation:
"None of it would have been in a spec, because the person writing it wouldn't have known to include it" —
an *unknown-unknowns* argument rather than a selection argument.

The practical consequence is a different acquisition step upstream of the usual pipeline: record the
cross-functional sync, have an LLM structure it into decisions/constraints/criteria/open questions, and
treat that as the high-value context ([[decision-trace]]). It also gives the field a second failure mode
beside context rot and pollution — call it **context that was never captured** — for which the fix is
convening people, not engineering the window.

## Declared once, not re-derived per request (Sadalage/Chandrasekaran, 2026-08)

The data-architecture statement of this page's discipline, and a useful compression of it. A
**context layer** of three versioned models — domain (what exists), semantic (how numbers are computed),
capability (what may be done) — where the unifying property is not meaning but *place*:

> "Each one is a place where a guarantee is declared once, in version control, instead of being worked
> out afresh by the model on every request."

([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]].) Their prescription against context sprawl is the same one Böckeler's
taxonomy implies: **route the agent through the layer, never the raw schema**, and treat every
hallucination as a *missing definition* — "fix the definition, not the prompt." The supporting datum they
cite is AtScale's: text-to-SQL accuracy under 20% against a raw schema versus over 92.5% with a semantic
layer, **same model**. That is the strongest quantitative claim in the KB for context structure beating
model capability, though it is a vendor's own benchmark.

Also relevant to the retrieval side of this page: their freshness SLA for a vector index is keyed to
*when the index was last successfully rebuilt*, not when content last changed — which catches both the
updated-but-unindexed document and the silently-failed indexer.

## Related

[[token-budget-quality-cliff]] · [[harness-absorption]] · [[agent-harness]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[nick-tune-graphs-memory-skills-agents]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] · [[martinfowler-prince-building-reliable-agentic-ai-systems]] · [[ng-spec-driven-development-is-waterfall-in-markdown]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[guo-survey-question-answering-to-task-completion-harness-design]] · [[mcateer-evolution-of-the-agent-harness]] · [[macmanus-pocock-wayfinder-skill-fog-of-war]]._
