---
title: Yves Goeleven
type: entity
created: 2026-06-14
updated: 2026-06-14
sources: [goeleven-event-sourcing-not-auditing-for-free, goeleven-event-modeling-visualize-business-processes, goeleven-interaction-design-aggregate-outbox-projection, goeleven-event-model-to-code-projection]
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

_Source pages: [[goeleven-event-sourcing-not-auditing-for-free]]._
