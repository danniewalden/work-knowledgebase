---
title: Yves Goeleven
type: entity
created: 2026-06-14
updated: 2026-06-14
sources: [goeleven-event-sourcing-not-auditing-for-free, goeleven-event-model-to-code-series, coupling-research-note]
tags: [person, event-modeling, event-sourcing, eda, ddd, business-capabilities, focus]
---

# Yves Goeleven

Belgian software architect, Microsoft Azure MVP and **NServiceBus core team** member; creator of
**MessageHandler.net** and **ClubManagement.io**. A strongly on-thread voice for the focus area:
long-form content on **event modeling, event sourcing, event-driven architecture, DDD, coupling /
cohesion**, and designing **around business capabilities** (capability swimlanes as the unit of
design). Blogs at goeleven.com and cloudshaper.wordpress.com; prolific on LinkedIn but in **infrequent
bursts** (so the watch looks back further than 14 days for him).

## In the KB

Sits with the practitioner cluster on the [[event-modeling]] / [[event-sourcing]] substrate
([[adam-dymitruk]], [[martin-dilger]], [[jeremy-miller]]). Distinctive lens: **business-capability
design** (a coupling/cohesion view linking to [[domain-driven-design]] and [[conways-law]]). One
captured source clarifies that [[event-sourcing]] gives an audit *starting point*, not free auditing
([[goeleven-event-sourcing-not-auditing-for-free]]).

His **"translating an Event Model into code" series** ([[goeleven-event-model-to-code-series]]) is the
substantive vein: Event Modeling visualizes *business processes* (even manual ones) with **role** and
**business-capability** swimlanes; decisions→events, intent→commands, state→projections; and the code
mapping command→**Aggregate Root**(decision)→events→**Outbox**→**Projection**→read model. Carries a
sharp coupling lesson — a context's internal events shouldn't double as integration events; a
**contract between capabilities** is required.

## Open thread — unresolved coupling taxonomy

The [[coupling-research-note]] (2026-06-22) tried to verify a **Goeleven coupling-taxonomy series** he
appears to have published on LinkedIn but **could not extract a verified taxonomy** — LinkedIn indexes
poorly for non-logged-in fetches. Surfaced but unconfirmed: his
[profile](https://www.linkedin.com/in/goeleven/), a [post on minimizing data
coupling](https://www.linkedin.com/posts/goeleven_how-to-minimize-data-coupling-data-coupling-activity-7320401061008084993-r5MX),
and a [blog post on low coupling / high cohesion](https://www.goeleven.com/blog/how-to-achieve-low-coupling-and-high-cohesion/).
**To resolve:** Dannie drops direct URLs to the LinkedIn series and the research is re-run. Until then,
treat his coupling taxonomy as a gap in [[coupling-taxonomy]].

_Source pages: [[goeleven-event-sourcing-not-auditing-for-free]] · [[coupling-research-note]]._
