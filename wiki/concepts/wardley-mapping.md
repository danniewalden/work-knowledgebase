---
title: Wardley Mapping
type: concept
created: 2026-06-14
updated: 2026-06-15
sources: [wardley-maps-value-chains-and-evolution, daniel-event-modeling-wardley-mapping]
tags: [strategy, wardley-mapping, business-capabilities, event-modeling, focus]
---

# Wardley Mapping

A strategy technique from **[[simon-wardley]]** ([[wardley-maps-value-chains-and-evolution]]): plot the
components a business needs to serve a **user need** on a map with two axes — **value chain /
visibility to the user** (vertical) and **evolution** (horizontal). The map exposes *where* each
component sits and *how it is evolving*, which drives strategic plays. Grounded 2026-06-15 on the
Wardley primary (Ch.2 Value Chains, Ch.3 Evolution), hosted and expanded by [[chris-daniel]].

## The method

- **Value chain — start from the user need, work backwards.** Anchor on what the customer wants to
  achieve ("help teams collaborate," not "sell software"), then trace the components required to deliver
  it (user → channel → value proposition → key activities/resources/partners → cost). Components depend
  on and influence each other; a change in one ripples through the chain.
- **Evolution — four stages, left to right.** Every component evolves **Genesis → Custom Built →
  Product → Commodity**: from novel / uncertain / rapidly-changing, through growing / scarce / more
  defined, to stable / widely available, to ubiquitous / standardized / utility-like.
- **Evolution → action (the strategic payoff).** Invest in and **differentiate** on Genesis &
  Custom-Built components (advantage lives there); **optimize, or outsource/buy** Product & Commodity
  ones. Watch components drift rightward to anticipate openings and threats. Context is everything —
  the same component can be strategic in one setting and commoditized in another.

## Relation to the focus — the capabilities × strategy × design trio

Pairs with [[business-capabilities]] and [[event-modeling]]: capabilities (Homann,
[[homann-business-capabilities]]) name the **stable "what"** (a capability is a value-chain component);
a Wardley map shows how each capability is **evolving** and therefore how to treat it strategically; and
[[event-modeling]] renders the chosen direction as a concrete, deterministic system design. **[[chris-daniel]]**'s
series ([[daniel-event-modeling-wardley-mapping]]) states the sequence: **Wardley = *where to go and
why*; Event Modeling = *what to build*.** His worked example (observed from the video,
raw note `raw/notes/daniel-em-wardley-video-observations.md`) maps a **software consultancy's time-tracking product**: a
"Strategy Level Wardley Map" on a value-chain × maturity axis to decide build-vs-buy, then an Event
Model with capability swimlanes (Time Management, User registration, Client management, Project
management). [[adam-dymitruk]] has also referenced the EM × Wardley connection. **Agent angle:** the build-vs-buy-by-evolution rule applies to agent investment too —
bespoke agent work pays off on differentiating (Genesis/Custom) capabilities, while commodity ones
should lean on utilities; cf. capability-as-agent-ownership-boundary in
[[autonomous-domain-capabilities]] / [[event-modeled-agent-design]].

## To source next

The captured primary covers only two chapters; **doctrine, climatic patterns, gameplay, and the
pioneers/settlers/town-planners (PST) model** are not yet captured — worth picking up if the Wardley
angle becomes load-bearing.

**Verbatim-transcript gap — dropped (2026-08-04, Dannie-directed).** A word-for-word transcript of the
Daniel EM × Wardley series was previously wanted, but the series is YouTube-only and its caption backend
wouldn't load even via live logged-in Chrome (2026-06-15 and confirmed again 2026-08-03), leaving audio
transcription as the only route — out of scope and not worth the cost for the value returned. Part 1
stays captured as **video observations** (raw note `raw/notes/daniel-em-wardley-video-observations.md`),
which is treated as sufficient. Future watch/sweep runs should **not** re-chase this transcript.
Dymitruk's EM × Wardley talk likewise remains uncaptured and is not being pursued.

_Sources: [[wardley-maps-value-chains-and-evolution]] · [[daniel-event-modeling-wardley-mapping]]._
