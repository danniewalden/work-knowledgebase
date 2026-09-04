---
title: "Dymitruk — Event Modeling is the map into the system, so the LLM barely matters; AI melts the barrier to good defaults"
type: source
created: 2026-08-10
updated: 2026-08-10
sources: [dymitruk-ai-melts-barrier-event-modeling-is-the-map]
raw_file: [raw/notes/dymitruk-ai-melts-barrier-event-modeling-is-the-map.md]
tags: [event-modeling, event-modeled-agent-design, event-sourcing, agentic-ai, focus]
---

# Dymitruk — "The model is the map; the LLM is pennies before a steamroller"

Source: [[adam-dymitruk]], two same-day LinkedIn posts, ~2026-08-09. Raw:
`raw/notes/dymitruk-ai-melts-barrier-event-modeling-is-the-map.md`
(urns 7492280951054487552 + 7492295097636515840). Hashtags #EventModeling #EventSourcing #Linux.

## Summary

Two compact theses from the method's creator.

**(1) "Only fundamentally sound and critical ideas will survive the AI disruption."** Code artifacts and
current patterns are "a black box" — you have to run the software to see if it works, and there is "no
standard way to see what's going on inside your solution," which gets time-consuming and error-prone as a
system grows. With **[[event-modeling|Event Modeling]] you have a map for how everything works**, giving
control "that no AI tooling gives you." His sharp corollary: **which LLM you use "doesn't matter that
much"** — the way you *see into* the system matters far more, "we're at the point that choosing an LLM is
like picking up pennies in front of a steamroller."

**(2) "AI is melting the barrier to entry"** for learning anything that isn't the (possibly dysfunctional)
default — he analogizes to two years of rising **Linux** adoption (freedom, customizability, moral high
ground) and applies it to **[[event-sourcing|Event Sourcing]]**: "Why would you not want 100% accountability
built into every system by default?" Leaning the right way from the start "isn't going to cost you time and
effort as before." He's "never been more optimistic."

## Key points

- **Model-is-the-map / LLM-agnostic** — the value is in the *visibility* the model gives, not the model
  weights; a strong statement that the spec, not the LLM, is the durable asset. The steamroller line is the
  quotable form of [[dilger-is-code-still-the-source-of-truth|Dilger's "model is the source of truth"]] and
  the counter to [[yordis-prieto-code-is-the-ultimate-diagram|Prieto's "code is the source of truth"]].
- **AI lowers the cost of choosing good defaults** — the adoption argument for Event Sourcing / Event
  Modeling: AI removes the historical time/effort penalty for not taking the standardized-but-dysfunctional
  default (accountability-by-default becomes cheap to adopt).
- **Optimistic framing** — a rare upbeat-adoption take to set against the KB's skeptics
  ([[khononov-microservices-hype-to-ai-sloop]]) and cost-realists
  ([[dilger-real-cost-of-ai-is-second-order]]).

## Connections

Extends [[adam-dymitruk]]'s position and [[event-modeled-agent-design]] (the model as the durable,
LLM-agnostic asset). Touches [[event-sourcing]] (accountability-by-default as the adoption pitch), the
model-vs-code source-of-truth tension ([[dilger-is-code-still-the-source-of-truth]] vs
[[yordis-prieto-code-is-the-ultimate-diagram]]), and [[dymitruk-ai-trained-on-dysfunction-agents-are-a-must]]
(the "trained on dysfunction" companion thesis).

## Caveat

Two short LinkedIn posts — aphoristic and promotional, no worked evidence. "The LLM barely matters" is a
deliberately provocative overstatement (model capability plainly still affects codegen quality); read as
emphasis on where the *durable* value sits, not a literal claim.
