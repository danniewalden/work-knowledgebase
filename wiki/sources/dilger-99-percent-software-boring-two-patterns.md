---
title: "Dilger — 99% of software is boring: it's only two patterns (State change / State view), which is why AI fits"
type: source
created: 2026-08-10
updated: 2026-08-10
sources: [dilger-99-percent-software-boring-two-patterns]
raw_file: [raw/notes/dilger-99-percent-software-boring-two-patterns.md]
tags: [event-modeling, event-modeled-agent-design, spec-driven-development, cqrs, vibe-modeling, focus]
---

# Dilger — "99% of Software is boring"

Source: [[martin-dilger]], LinkedIn post, ~2026-08-08 (2d old at capture). Raw:
`raw/notes/dilger-99-percent-software-boring-two-patterns.md`. Hashtags #eventmodeling #eventsourcing.

## Summary

Dilger's reductionist thesis: every system, however unique it looks, breaks down into **two repeating
patterns** — **State change** (how information gets *into* the system) and **State view** (how information
is used and pulled back *out*). He tells workshop groups "four patterns" so it isn't too boring, "but
between us — it's only two." Five years of modeling with [[event-modeling|Event Modeling]] convinced him it
is "always the same thing … Lego bricks, and we effectively only use two colors."

The payoff for agents: **once you accept it's only two patterns, AI becomes dramatically more useful** — no
need to hand-write the repetitive state-change / state-view code ("glorified copy & paste"). "The repetitive
nature of event modeling is exactly what makes it a great fit for AI — it gives AI **tight guardrails and
clear instructions instead of an open-ended blank page**." He closes on the EM↔Spec-Driven-Development
bridge again: EM alone suffices for SDD, but he's making it combine with **Spec-Kit / Kiro / Spec-Kitty** to
"meet companies where they are" on policy — the *creative* part of software is navigating company politics,
not writing code.

## Key points

- **Two-patterns reduction** — State change + State view; the "four patterns" of the standard method
  (Command, View, Translation, Automation) collapse, in his telling, to the [[cqrs|CQRS]] write/read split
  as the irreducible core.
- **Repetition = AI-friendliness** — the argument that the *boring, repetitive* shape of event-modeled code
  is precisely what makes it safe to hand to an agent: tight guardrails beat a blank page (the guardrail
  half of [[vibe-modeling]] and [[spec-driven-development]]).
- **EM as the front half of SDD toolkits** — restates [[dilger-spec-driven-tools-need-event-modeling-front-half]]:
  EM is sufficient but pragmatically bridged into Spec-Kit/Kiro/Spec-Kitty to fit company policy.

## Connections

Deepens [[event-modeling]] (the two-ideas core), [[event-modeled-agent-design]] (repetition→guardrails as
why agents fit), [[cqrs]] (the write/read reduction), [[spec-driven-development]] and [[vibe-modeling]].
Same EM↔SDD-bridge thread as [[dilger-spec-driven-tools-need-event-modeling-front-half]].

## Caveat

LinkedIn marketing for [[eventmodelers-ai]] and the *Spec Driven* book; a deliberately provocative
simplification ("only two patterns") that elides the Translation/Automation integration patterns the method
itself treats as first-class. Framing, not evidence.
