---
title: Dynamic Consistency Boundaries (DCB)
type: concept
created: 2026-06-14
updated: 2026-06-14
sources: [pellegrini-dynamic-consistency-boundary]
tags: [event-sourcing, dcb, ddd, consistency, focus]
---

# Dynamic Consistency Boundaries (DCB)

**Concept stub** (added 2026-06-14 when Dannie broadened the focus to the Event Modeling design
substrate). A **Dynamic Consistency Boundary** defines a transactional consistency scope *at runtime,
per decision*, rather than fixing it up front in an aggregate. Origin: **[[sara-pellegrini]]**'s "Kill
Aggregate" series and her naming post ([[pellegrini-dynamic-consistency-boundary]], 2023); the idea is
also associated with **[[adam-dymitruk]]**.

## The idea

A decision in an event-sourced system is a function: **input** = the ordered stream of *relevant* past
events (the "given"); **output** = new events (the consequence). DCB is an **optimistic lock** for
that: append the output **iff** the relevant input stream is unchanged between load and append. The
event store needs two capabilities — **dynamic query** (select events by criteria, e.g. tags) and
**conditional append** (write only if the query result still matches). Immutability makes the check
cheap (compare the last event).

The payoff is escaping the **aggregate** as the mandatory consistency unit: consistency boundaries
become per-operation "temporary bubbles" that include just the events a decision needs, so the model
can evolve without re-architecting around early aggregate choices ("Aggregates introduce rigidity").

## Where it sits / why it's in the focus

DCB is part of the [[event-sourcing]] / [[cqrs]] design substrate around [[event-modeling]] (the
focus broadened to include it). It connects to several existing threads:

- **Event Modeling fit.** EM models decisions as command→event on a timeline; DCB is a principled
  answer to "which events must I read, and how do I append safely" for those decisions — boundaries
  drawn from the timeline rather than from aggregates.
- **Tooling adoption (out-of-window, foundational — not filed as new):** Axon Framework 5 shipped
  experimental DCB support (AxonIQ, Steven van Beelen, Jun 2025) using tag-based multi-stream
  queries; the Critter Stack's **Marten 9.0** added a higher-performance DCB option via PostgreSQL
  HSTORE ([[martin-dilger|—]] reported by [[jeremy-miller]] via *The Shade Tree Developer*, May 2026).
  *These are the canonical current implementations to capture if/when an in-window development lands.*
- **Agent angle (claimed).** Vendor framing argues DCB "reduces AI hallucinations" and lets the
  architecture evolve safely under agent-driven change — a possible bridge to
  [[event-modeled-agent-design]] worth watching, currently assertion-level.

## What's open / to capture next

A primary write-up tying DCB to *agent* design (vs. plain event sourcing); the Pellegrini/Savić
conference talk; and the Axon AF5 / Marten 9.0 implementation docs as proper sources if they re-surface
in-window. This stub should grow into a full concept page as on-topic sources are ingested.

_Sources: [[pellegrini-dynamic-consistency-boundary]]._
