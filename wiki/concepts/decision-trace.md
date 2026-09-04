---
title: Decision Trace
type: concept
created: 2026-08-16
updated: 2026-09-04
sources: [ng-spec-driven-development-is-waterfall-in-markdown, dilger-describing-without-solving-burns-you-out, bockeler-tdd-inside-the-agent-loop, dudycz-fixing-bugs-in-event-sourcing]
tags: [spec-driven-development, agentic-coding, provenance, decision-records, focus]
---

# Decision Trace

A **retrievable chain of provenance from a decision to the code that implements it** — meeting →
structured notes → ticket → prompt → in-flight decision log — proposed by [[alvis-ng]] as the replacement
for the up-front specification as an agent's source of structure
([[ng-spec-driven-development-is-waterfall-in-markdown]], 2026-03).

The distinguishing property is **direction**: a spec is written *before* the work and describes what
should happen; a trace accumulates *during* the work and records what actually did, including the pivots.
Ng's contrast: "And when things change mid-iteration, as they always do, the trace captures the pivot.
The spec would have just been wrong."

## The shape of it

1. **Recorded cross-functional syncs** — the raw material. The constraints that decide a feature
   ("that flow breaks for screen readers", "we can't deploy that behind the canary setup") are surfaced by
   people who wouldn't have been asked to review a spec.
2. **LLM-structured notes** — decisions made, constraints identified, agreed acceptance criteria, open
   questions flagged; committed alongside the code. "Not as a spec. As a structured record of what the
   team actually aligned on."
3. **Tickets** carrying those criteria into "the natural unit of work that engineers already read" —
   the documentation isn't removed, it's moved to where people actually look.
4. **A human-written prompt per ticket** — "The prompt is the spec, scoped to one task, written by
   someone who was in the room when the decisions were made."
5. **A decision log the agent maintains as it builds** — every trade-off chosen, every alternative
   rejected.

## Why it's a distinct idea, not just "write ADRs"

An [[adr|ADR]]-style record documents an architectural choice; a decision trace is a **debugging
instrument**. Ng's argument for it is diagnostic: today, "You open the spec. You compare it to the
implementation. You try to figure out where they diverged." — which he characterises as comparing "a
fantasy document to reality and wondering which one lied." With a trace you walk backwards to *the exact
assumption that broke* (his words) and find
the conversation where it was made. Where a stale spec fails **silently**, a trace fails **legibly**.

It is also the KB's clearest statement of a **constructive role for AI in the alignment step itself**:
not the reader of the spec but "the structurer of your conversations, the scribe of your decisions, the
tracer of your reasoning" — making the output of human alignment "retrievable, structured, and permanent."

## Where it sits against the rest of the KB

- **Against [[spec-driven-development]]:** it is the direct counter-proposal. Note the two are not
  fully opposed on substance — [[dilger-describing-without-solving-burns-you-out|Dilger's]] "describing ≠
  designing" and Ng's "you're a reviewer, not a builder" are the *same worry* about the human checking
  out, reached from advocacy and from critique respectively.
- **Alongside [[given-when-then]]:** Ng doesn't drop acceptance criteria, he **relocates their
  authorship** — they come out of the sync, not out of one person's document. A GWT scenario agreed in
  the room and a GWT scenario authored at a desk are the same artifact with very different standing.
- **Alongside [[comprehension-debt]]:** comprehension debt is unread *code*; the gap a trace addresses is
  unrecorded *reasoning*. Both are paid at incident time, and both are made worse by speed.
- **Alongside [[context-engineering]]:** a trace is a bet about *which* context is high-value — the
  provenance of a decision beats a fuller statement of the decision itself.
- **Tension with [[event-modeled-agent-design]]:** an event model is also built collaboratively in the
  room and is also a living artifact, so it satisfies much of Ng's requirement — but it is still a
  *model of intended behaviour*, not a record of deliberation. Whether a maintained model plus its edit
  history *is* a decision trace is an open question this page can't settle from one source.

## Open questions

- **No evaluation exists.** The trace workflow is asserted, not measured — the same standard of evidence
  Ng faults SDD advocates for. Nothing in the KB tests whether teams sustain a decision log any better
  than they sustained Confluence.
- **Who maintains it?** Ng's step 5 delegates the decision log to the model, which reintroduces the
  self-reporting problem [[bockeler-tdd-inside-the-agent-loop|Böckeler]] raises about agents grading
  their own process: an agent's account of why it chose an approach is not evidence that it chose it for
  that reason.
- **Does it survive scale?** A trace per ticket across a large team is a large corpus with no stated
  retrieval story beyond "follow the trail."

## A cheap primitive: stamp the build that made the decision (Dudycz, 2026-07)

[[dudycz-fixing-bugs-in-event-sourcing]] adds one field to event metadata and gets a decision trace for
free: **`buildSha`**, "the commit the service was running when it appended the event… an environment
variable and a few lines in whatever builds our metadata." Then "which decisions did *that* version of
the system make?" is a query, not an archaeology exercise — his case returns exactly the events the broken
binary produced, and excludes records merely touched in the same window. Alongside it,
**`correlationId`** groups everything from one user action and **`causationId`** chains back to the
triggering command: "when the bad value comes out of a handler three hops from the request, that chain is
how we find which request it was."

**Why it matters beyond event sourcing.** This is the "which version of the system decided this" question
that [[agent-explainability]] and [[agent-governance]] ask of agents, answered at the cheapest possible
layer — and it transfers directly to agent-written records (which agent, which model, which prompt or
skill version stamped on the fact it produced). Contrast the heavier instruments on this page: it is
detection-grade metadata rather than a narrative trace, and it is **advice, not a reported practice** —
offered inside an invented scenario, and it assumes one deployable per stream and immutable build tags.

_Sources: [[ng-spec-driven-development-is-waterfall-in-markdown]] ·
[[dilger-describing-without-solving-burns-you-out]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[dudycz-fixing-bugs-in-event-sourcing]]._
