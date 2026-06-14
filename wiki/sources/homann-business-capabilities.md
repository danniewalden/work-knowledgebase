---
title: "Homann — A Business-Oriented Foundation for Service Orientation"
type: source
created: 2026-06-14
updated: 2026-06-14
sources: [homann-business-oriented-foundation-service-orientation]
tags: [business-capabilities, business-architecture, ddd, coupling-cohesion, primary, focus]
---

# Homann — A Business-Oriented Foundation for Service Orientation

The **seminal primary** on business-capability mapping: **[[ulrich-homann]]** (Microsoft, Feb 2006),
widely cited (incl. the BIZBOK Guide) as the origin of treating a business as a network of
capabilities. Captured 2026-06-14 to ground [[business-capabilities]] (a focus area flagged important
by Dannie). Raw (summary, copyright-trimmed): `raw/papers/homann-business-oriented-foundation-service-orientation.md`.

## Key points

- **Capability = what, not how.** "A particular ability or capacity that a business may possess or
  exchange to achieve a specific purpose or outcome" — a **black box** with defined inputs/outputs and
  a contracted **service-level expectation**, encapsulating people/process/technology/information.
  Examples: Pay Employees, Ship Product.
- **Stability argument.** *What* a business does is stable; *how* (processes, tech, org) is volatile.
  Architecting around capabilities yields a "firm, longer-lasting base" and "enduring assets" — the
  grocery self-checkout example: same capabilities, different process.
- **Capability connectors.** Links carrying rich semantics (I/O + control/policy); discovering the
  connections "may be as valuable as defining the capabilities" — you manage change through
  connections while the black boxes stay put. (This is the coupling/cohesion crux.)
- **Capability map = nested taxonomy.** L1 Foundation (Operations vs Environmental) → L2 Capability
  Groups → L3…n Business Capabilities. Spans the whole value network, not one legal entity.
- **Process ≠ capability.** Process is the *implementation* of the capability blueprint at a point in
  time.

## Why it matters

Supplies the authoritative definition and structure behind [[business-capabilities]], independent of
any one practitioner. Grounds [[yves-goeleven]]'s capability-swimlane practice
([[goeleven-event-model-to-code-series]]) and connects to [[domain-driven-design]] (bounded contexts),
[[conways-law]] (ownership), and the "contract between capabilities" coupling rule. The black-box +
connectors framing also prefigures service/agent boundaries ([[event-modeled-agent-design]]).

## Caveats

2006, written to justify SOA/Web services; the SOA framing is dated, but the capability concepts are
the durable contribution. Microsoft-authored.

## Links

Entities: [[ulrich-homann]]. Concepts: [[business-capabilities]], [[domain-driven-design]],
[[conways-law]], [[wardley-mapping]], [[event-modeling]]. Related:
[[goeleven-event-model-to-code-series]], [[daniel-event-modeling-wardley-mapping]].
