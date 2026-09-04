---
title: Event Sourcing
type: concept
created: 2026-06-11
updated: 2026-08-03
sources: [semaphore-dymitruk-event-modeling, eventmodeling-what-is-event-modeling, akka-event-sourcing-backbone-agentic-ai, akka-agentic-systems-are-distributed-systems, atomicobject-cqrs-event-sourcing-production-walkthrough, event-modeling-event-sourcing-podcast, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember, roden-event-sourcing-meets-mcp-whole-story-for-llms, enzler-event-sourcing-aggregates-dcb-or-what, adaptech-workflow-not-inside-giant-process-manager, fritzsche-choosing-storage-is-choosing-what-your-system-forgets]
tags: [event-sourcing, pattern, cqrs, agentic-ai, architecture]
---

# Event Sourcing

A design pattern that stores state as an **append-only log of immutable events** rather
than overwriting rows in a database. [[adam-dymitruk]]'s analogy: like accounting,
**"no erasers are allowed"** — you only ever add events; current state is derived by
replaying them. The store is an **event store**: a database built to recall events in a
guaranteed order.

## Properties

- **Full history / audit** — every change is retained, so you can see how information
  evolved and who/what caused it.
- **No "downhill effect"** — changing state means appending one event, not carefully
  updating many interdependent queries.
- **Multiple projections** — the same events feed many read models / views, each isolated
  from the others.
- Per Dymitruk, adopting it is a modest change: ~80% of the work is the same UI-on-a-model
  app; the addition is the ordered, replayable ledger.

## Two domains this KB connects

1. **Information systems** — the partner pattern to [[event-modeling]]: the blueprint
   defines the contract for what each workflow step leaves on the ledger vs. projects to a
   screen. Lineage runs through [[cqrs]] and [[greg-young]].
2. **Agentic AI** — [[kevin-hoffman]] / [[akka]] argue event sourcing is the **"backbone"**
   of [[agentic-ai]]: because LLMs are nondeterministic, an immutable event log gives
   **perfect recall** (reproduce any agent's state and know *why*), **auditability**,
   durable inter-agent communication, and **agent/event versioning via replay**. Storing
   agent memory as replicated events also yields a distributed backbone
   ([[akka-agentic-systems-are-distributed-systems]]). For how this substrate maps onto
   [[anthropic]]'s concrete [[agentic-workflow-patterns]], see [[event-sourced-agentic-patterns]].

## Related

[[event-modeling]] · [[cqrs]] · [[dynamic-consistency-boundaries]] · [[vertical-slice-architecture]] ·
[[business-capabilities]] · [[autonomous-domain-capabilities]] · [[agentic-ai]] ·
[[event-sourced-agentic-patterns]] · [[event-driven-architecture]] · [[agentic-event-driven-systems]] ·
[[open-closed-principle]] · [[domain-driven-design]]

**Substrate note (2026-06-14):** the focus now explicitly includes the event-sourcing design
substrate around Event Modeling — see [[dynamic-consistency-boundaries]] (per-decision consistency
scopes replacing the fixed aggregate) and [[vertical-slice-architecture]] (feature-slice organization
that yields [[cqrs]] and maps to Event Modeling slices).

**Update (2026-06-15):** [[martin-dilger]] argues DCB *is* event sourcing "what it always should have
been," recasting the aggregate as a *static* consistency boundary
([[dilger-dcb-is-what-event-sourcing-should-have-been]]). [[rico-fritzsche]] treats recorded events as
the **Application State** that capabilities (RPUs) interpret to form the domain
([[autonomous-domain-capabilities]]).

**Update (2026-06-19):** Fritzsche makes the "no aggregates" claim explicit —
**Event Sourcing does not require aggregates** ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]):
ES is *defined* by the event history as source of truth, and the "rebuild aggregate → call method →
append at expected version" pattern is one implementation the DDD community conflated with the
definition. The same post separates the consistency layer from ES itself — [[autonomous-domain-capabilities|CCC]]
is the representation-agnostic principle, [[dynamic-consistency-boundaries|DCB]] a tag-based store
contract, **neither a synonym for Event Sourcing.**

**Production reference (2026-06-17):**
[[atomicobject-cqrs-event-sourcing-production-walkthrough|Atomic Object's production walkthrough]]
grounds the pattern in a real stack (NestJS + KurrentDB + PostgreSQL/Drizzle): commands-as-intent,
aggregate-as-state-machine with type-level exhaustiveness, **snapshots as a non-authoritative
optimization**, **upcasters/event-versioning from day one**, at-least-once **idempotent projections**,
and a split between transactional read-model projections and async side-effect projections. Its advice
to **keep aggregates small** (solve cross-aggregate work with async projections, not bigger aggregates)
is the conventional counterpoint to the [[dynamic-consistency-boundaries|DCB]] "kill the aggregate" line.

**Event store as agent memory — two payoffs (2026-06-21):** two new ES-vendor sources sharpen *why*
the immutable log matters for agents. [[axoniq]] ([[allard-buijze]]) argues **agent
[[agent-explainability|explainability]] is an infrastructure problem, not a model problem**:
state-based stores overwrite the causal history regulators now require (EU AI Act, SR 11-7, GDPR
Art. 22), and only an event store captures *why* a decision was made
([[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]]). It also draws a crisp
**event store vs. event stream** line — a store records *why* (full causal context, replayable); a
stream (Kafka) only moves *what*. [[golo-roden]] takes the *context-quality* angle: CRUD is "only the
last chapter," an event store gives an LLM "the whole story," and **events are the natural language for
LLMs**, reachable via [[model-context-protocol|MCP]]
([[roden-event-sourcing-meets-mcp-whole-story-for-llms]], [[context-engineering]]). Same backbone, two
payoffs: *explainability* (why it decided) and *context* (what it needs to decide well). See
[[agent-explainability]].

**Third-way substrate note (2026-06-23):** [[urs-enzler]]
([[enzler-event-sourcing-aggregates-dcb-or-what]], part 11 of his ES series) argues the cheapest
consistency boundary is often **no concurrency at all** — "small data" + a task-based UI
(command-per-task, no unit-of-work) and, where possible, replacing a concurrent design with a
non-concurrent one (draft-intent + single-threaded batch), serialising only where genuinely needed via
infrastructure (Azure Service Bus sessions). A pragmatic "you might not need aggregates *or* DCBs"
counterweight; see [[dynamic-consistency-boundaries]].

**Long-running workflows note (2026-07-29):** [[adaptech-group]]
([[adaptech-workflow-not-inside-giant-process-manager]]) argues the event log is the **durable
evidence** that makes long-running processes recoverable: rather than a large saga/process manager
holding hidden in-memory state, model progress as a **projected to-do list** read by focused
processors, so after a restart a processor can **verify rather than repeat** a possibly-completed
action. See [[process-managers-and-todo-lists]].

**Note (2026-06-12):** event sourcing is a pattern *within* the broader
[[event-driven-architecture]] family. Three external 2026 sources now apply it to agents directly:
[[confluent-agentic-event-driven-systems-architecture]] lists immutability, exactly-once, and
**deterministic replay** as production design principles for agent decisions, and
[[atlan-event-driven-architecture-for-ai-agents]] names event sourcing as a core agent-coordination
pattern — externally corroborating the Akka "backbone" thesis above. See [[agentic-event-driven-systems]].

**Practitioner commentary (2026-06-17):** the [[event-modeling-event-sourcing-podcast]] (Dymitruk &
[[martin-dilger]], 46 eps) is the running conversational source for this pattern — recurring hard parts
captured there include [[event-versioning-and-upcasting|schema migration / upcasting]] (Eps 5, 37, 46),
replay times and metrics (Ep 17), Git-as-event-store (Eps 26, 40), "SQL is an anti-pattern" (Ep 22),
and the historical framing "event sourcing predates anything in computing" + the accounting analogy
(Ep 39). Show-notes-level only (transcripts were blocked).

## Event Sourcing is a *storage decision*, not "thinking in events" (Fritzsche, 2026-07)

[[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]] gives the concept its clearest
conceptual grounding by holding four words apart — **state** (what holds), **event** (a change at one
moment, whose *type* carries what the before/after pair loses), **fact** (a true statement bound to its
moment — "you cannot update a fact"), and **record** (a fact written to a store). The dividing line is
**the discipline of the record, nothing else**: an append-only relational table *keeps facts*; an event
log edited in place *keeps state under a misleading name*. "Overwritten records keep state; appended
records keep facts." So current state is **derived** (Greg Young: "a Left Fold of previous behaviours"),
and **Event Sourcing is the decision to make event records authoritative — one storage choice; "thinking
in events" does not depend on it.** This separates the *method* from the *store* (the same split Fritzsche
draws for [[agent-explainability]] and [[command-context-consistency]]).

_Source pages: [[eventmodeling-what-is-event-modeling]] · [[semaphore-dymitruk-event-modeling]] · [[akka-event-sourcing-backbone-agentic-ai]] · [[akka-agentic-systems-are-distributed-systems]] · [[atomicobject-cqrs-event-sourcing-production-walkthrough]] · [[event-modeling-event-sourcing-podcast]] · [[fritzsche-choosing-storage-is-choosing-what-your-system-forgets]]._
