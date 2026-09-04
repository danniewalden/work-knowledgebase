---
title: "Fritzsche — Microservices are not a maturity level"
type: source
created: 2026-06-29
updated: 2026-06-29
sources: [fritzsche-microservices-not-a-maturity-level]
raw_file: [raw/notes/fritzsche-microservices-not-a-maturity-level.md]
tags: [business-capabilities, microservices, software-architecture, focus]
---

# Fritzsche — Microservices are not a maturity level

LinkedIn post by **[[rico-fritzsche]]** (2026-06-24; captured 2026-06-29 via logged-in Chrome).
Source file: `raw/notes/fritzsche-microservices-not-a-maturity-level.md`. Points back to a critical
article he wrote in 2023 (linked in first comment, not captured). Tagged `#microservices
#softwarearchitecture #modularmonolith`.

## What it says

Pushes back on the common "**you must master a modular monolith before you earn microservices**" line
(he names **Anton Martyniuk** as propagating it). His position:

- **Microservices are not a maturity level**, not a reward for experienced teams, and not something to
  adopt because other companies do. They are an **architectural decision with a concrete cost and a
  concrete purpose**, justified only by a valid reason: independent deployment, different scaling
  characteristics, strong business boundaries, or **organizational autonomy**.
- **Ownership is the underestimated point.** Microservices work only when a team **owns a service end to
  end** — responsibility for change, operation, failures, and the consequences of decisions. Without
  that ownership the result is "an organizational mess rather than technical autonomy." The discussion is
  "much bigger than technology — it's about boundaries, domain knowledge, responsibility and how an
  organization actually works."
- A **modular monolith** can absolutely be the right choice (cheaper to move boundaries inside one
  deployable unit) — but it's *one* option, not a mandatory first step. Sometimes starting with
  microservices is justified up front when business/operational/organizational constraints are already
  known.
- The real questions: *What is the goal? What are the boundaries? Who owns what? What structure can carry
  that responsibility realistically?* "Used for the right reasons they work very well; used as a default
  pattern they become expensive confusion."

## Why it matters here

A [[business-capabilities|capability]]/[[conways-law|ownership]]-first lens on the
monolith-vs-microservices debate: the deciding variable is **who owns a boundary end to end**, not team
seniority. Consistent with Fritzsche's broader claim that the **domain capability is the ownership
boundary** ([[autonomous-domain-capabilities]]) and with [[team-topologies]]' ownership/cognitive-load
framing. Mostly off the AI-agents thread — captured under the people-watch *anything-substantive* rule as
a substrate-design position.

## Caveats

LinkedIn opinion post; the supporting article (2023, first comment) is uncaptured. Off the EM×agents
focus — substrate/architecture-philosophy. One practitioner's view, framed as a rebuttal to a named peer.

## Touches

[[rico-fritzsche]] · [[business-capabilities]] · [[conways-law]] · [[team-topologies]] ·
[[autonomous-domain-capabilities]]

_Source: `raw/notes/fritzsche-microservices-not-a-maturity-level.md`._
