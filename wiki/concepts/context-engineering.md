---
title: Context Engineering
type: concept
created: 2026-06-11
updated: 2026-08-31
sources: [sadalage-chandrasekaran-making-data-ready-for-agentic-ai, bockeler-context-engineering-coding-agents, fowler-bockeler-harness-engineering, langchain-anatomy-of-an-agent-harness, firecrawl-what-is-an-agent-harness, nick-tune-graphs-memory-skills-agents, roden-event-sourcing-meets-mcp-whole-story-for-llms, martinfowler-prince-building-reliable-agentic-ai-systems, ng-spec-driven-development-is-waterfall-in-markdown]
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

## The substrate view (Tune)

[[nick-tune]] ([[nick-tune-graphs-memory-skills-agents]]) restates this from the build side: *"the model
is the commodity, the context is the product."* He decomposes what sits **underneath** an agent into
**Graph** (a queryable world model — what exists and how it connects), **Memory** (continuity: what was
true at a past instant and what changed), and **Skills** (encoded judgment), with the **Agent** loop on
top. Two of these are the KB's own threads in other clothes: **Memory** as a point-in-time-queryable
history is [[event-sourcing]], and the **Graph** is [[agent-legibility]] delivered as structure rather
than ad-hoc grepping (so the agent can reason about state and a change's blast radius).

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

[[token-budget-quality-cliff]]

_Sources: [[fowler-bockeler-harness-engineering]] · [[langchain-anatomy-of-an-agent-harness]] · [[firecrawl-what-is-an-agent-harness]] · [[nick-tune-graphs-memory-skills-agents]] · [[roden-event-sourcing-meets-mcp-whole-story-for-llms]] · [[martinfowler-prince-building-reliable-agentic-ai-systems]] · [[ng-spec-driven-development-is-waterfall-in-markdown]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]]._
