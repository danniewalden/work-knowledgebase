---
title: "Dilger — A Flexible, Agent-Enabled Architecture That Keeps Systems Maintainable over years (the Triplet)"
type: source
created: 2026-07-27
updated: 2026-07-27
sources: [dilger-triplet-flexible-agent-enabled-architecture]
raw_file: [raw/articles/dilger-triplet-flexible-agent-enabled-architecture.md]
tags: [event-modeling, event-sourcing, vertical-slice-architecture, coupling, agentic-coding, focus]
---

# Dilger — The Triplet: a flexible, agent-enabled architecture

The definitive naming and write-up of what [[martin-dilger|Dilger]] calls **"the Triplet"** — a
**flexible, agent-enabled architecture** that keeps systems maintainable for years instead of months by
using three building blocks *in union*: **[[event-modeling|Event Modeling]] (plan) +
[[vertical-slice-architecture|Vertical Slices]] (structure) + [[event-sourcing|Event Sourcing]] (store)**.
LinkedIn newsletter *Event Modeling applied*, 2026-07-26 — the full version of the long-stubbed
[[dilger-hold-my-beer-engineer|"Event Modeling applied" teaser]], and the dedicated primary for the
"triplet" prior captures only named in passing ([[dilger-local-llm-distributed-agent-setup-event-modeling]]
"triplet of flexible architectures", [[dilger-dcb-is-what-event-sourcing-should-have-been]]). Explicitly
"heavily inspired by the work of [[adam-dymitruk]]".

## The argument

**The root problem is coupling, and it compounds.** Hexagonal/onion/layered architectures assume you
*already know your boundaries* — they give you a tidy place to put a boundary once someone decides it, but
don't help you *find* it. Agile covers the process side and says nothing about the technology underneath.
Nobody stands in the gap producing the boundaries the technical architecture assumes. So the boundary gets
decided implicitly "by whoever was loudest or most senior that day" (his recurring image: the architect who
comes back from vacation and vetoes a boundary) — the "dreaded module discussion" where three developers
give three different answers because *module* is a blurry word. That rework never shows up as rework; it
shows up as a project that's always a bit behind. Coupling is what makes a single change expensive and every
later change more expensive — the exponential cost curve (the same [[open-closed-principle|OCP]]/flat-cost
argument that underlies Event Modeling).

**Architecture is the whole thing, not just the code.** Requirements are *part of* the architecture — not a
softer discipline that happens before the "real" work. If the shared understanding underneath is wrong,
clean code just gives you "a well-organized version of a mistake." So the Triplet **starts with
requirements** built visually and collaboratively in the room (Event Modeling), detailed enough to serve as
the blueprint that generates most of the code.

## The three pieces, used together

- **Event Modeling comes first** — builds the shared understanding with stakeholders in the room, turning
  "the requirement" from a document into a visual timeline everyone reads the same way; the boundary isn't
  decided by whoever was in the meeting.
- **Vertical slices come next** — a *natural result* of the modeling step. Structure code around the real
  flows the model surfaced, not shared layers (controllers/services/repositories) that force every change
  across the system. A change to one flow stays inside it — "even stronger, a change typically affects only
  one step in a flow," limiting the blast radius.
- **Event sourcing runs underneath both** — keep the full history of what happened; "the ledger of facts
  allows us to decouple the slices," so nobody reconstructs the "why" from memory or Slack six months later.

None is new alone; the insistence is on **all three connected** — the same boundaries discovered in modeling
built into the slices, the same events modeled are the events sourced. "I've watched teams do hexagonal
beautifully with no modeling underneath it… model beautifully and then structure the code in a way that
undid all of it." The value is "married to having all three building blocks filled — a planning block, a
structural block, a storage block — filled in a way that actually connects," and each block must support
**decoupling the slice**. You can swap any block, but then you own re-solving the problems it solved.

## Agent-enabled (the focus seam)

The reason it matters here: **low coupling doesn't just help humans, it makes the system cheap for AI agents
to work inside.** "An agent working on one slice only needs that slice's context, the event log, and a
precise model instead of half the codebase — which is exactly what keeps the overhead and token cost down"
you'd otherwise pay in a highly coupled system. An agent works one slice, doesn't need to understand what's
left or right of it → minimal context, and *less code produced and reviewed*. Changing one slice has no
ripple effect, so slices can be built in isolation → **adding more agents (or engineers) makes the system
done faster, not slower.** This is the [[locality-of-reference|"codebase is the prompt"]] / one-slice-context
thesis stated as an architecture principle, and the structural precondition for
[[dilger-event-modeling-agent-harness|the Event Modeling Agent Harness]]'s collision-free parallel builds.

## Also notable

- **Estimation via Slice-Cycle-Time.** Slices are roughly equal in size, so measure the average time to
  build one ("velocity/performance"); the more you build, the more accurate the "when are we done" guess —
  a concrete alternative to story points / T-shirt sizes he openly disdains.
- **The platform.** [[eventmodelers-ai|app.eventmodelers.ai]] is built around the Triplet: plan (EM) / build
  (ES) / structure (slices), with agents via provided skills + an [[model-context-protocol|MCP]] server, and
  the "nasty problems" solved — Version Control (Git-backed), Backup/Restore (JSON import/export), Code
  Generation (Build Kits).
- **On naming:** "My goal is not to coin a new term… 'Triplet' is just a name I've landed on… if the
  language is useful to you too, take it."

## Connections

Extends [[event-modeled-agent-design]] (the design method for agent systems), [[vertical-slice-architecture]]
(slice = unit of decoupling and of agent work), [[event-sourcing]] + [[event-modeling]]; the coupling thesis
ties to [[balanced-coupling]] / [[business-capabilities]] and [[rico-fritzsche-rpu-reactor-vocabulary]]
(capability/slice as the boundary the agent era needs); the agent-per-slice economics tie to
[[locality-of-reference]], [[ai-readable-code]], and [[dilger-event-modeling-agent-harness]]. Caveat:
vendor-authored (promotes his book/workshop/platform), self-reported, no external quality data — but the
clearest single statement of the EM+ES+VSA "triplet" the KB tracks.

_Source: [[dilger-triplet-flexible-agent-enabled-architecture]] (raw/articles)._
