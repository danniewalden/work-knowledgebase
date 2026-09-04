---
title: "Prieto — Code Is The Ultimate Diagram"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [yordis-prieto-code-is-the-ultimate-diagram]
raw_file: [raw/articles/yordis-prieto-code-is-the-ultimate-diagram.md]
tags: [event-sourcing, agentic-coding, source-of-truth, focus]
---

# Prieto — Code Is The Ultimate Diagram

Raw: `raw/articles/yordis-prieto-code-is-the-ultimate-diagram.md` — [[yordis-prieto]],
yordisprieto.com, 2026-07-02. The first captured source *authored by* Prieto (previously
a watch-list stub named by [[adam-dymitruk]]), establishing his actual position.

## Summary

Prieto argues diagrams are **discovery tools, not the design**: draw them at the whiteboard
to find the shape of a problem, then throw them away, because the moment code is written the
diagram starts to drift and no sync process can hold. **The code is the source of truth**;
every diagram is just a *view* of it, and if the picture and the code disagree, the code
wins. The right move is to **regenerate the picture from the code** on demand rather than
drag code back to a stale picture — "code is the ultimate diagram."

## Key points

- **Diagrams are for discovery, early/cheap/throwaway.** Their value is the shared
  understanding built in the room; "nothing ships from a picture. The software is the
  software." Anchoring on a diagram too soon means defending the picture instead of
  interrogating the problem.
- **Diagrams decay structurally, not through sloppiness.** Design keeps happening *in the
  code* — every commit is a decision (a name, a boundary, a retry). "A six month old diagram
  is a story about a system that does not exist anymore."
- **So flip the direction:** let the picture come from the code. The code already encodes
  which modules call which, which events get published, which boundaries are real vs merely
  aspirational. "If the picture and the code disagree, the code wins. Always."
- **The catch is tooling.** The flip only works if a fresh picture is cheap to regenerate;
  hand-redrawing is "a tooling gap, not a law of nature."

## Connections — a genuine tension with the EM/model-first camp

This is the **counter-position** to the Event-Modeling "the model is the living spec / source
of truth" thesis. It directly contradicts [[dilger-is-code-still-the-source-of-truth]]
([[martin-dilger]]: *code is a lagging indicator of intent; the model/spec is the source of
truth; AI makes code almost disposable, regeneratable from the spec*) and sits opposite
[[dilger-model-is-a-living-spec-always-on-agent]] and the [[event-modeled-agent-design]] premise.
The KB now holds **both directions of the arrow**: Dilger regenerates *code from the model*;
Prieto regenerates *the diagram from the code*. Both agree the stale hand-maintained artifact
is the enemy and that regeneration is the fix — they disagree on which artifact is primary.
Note that Prieto's framing predates encountering EM's "model-in-code + validating framework"
answer ([[dilger-drawio-model-in-code]]), which is partly a response to exactly his "tooling
gap." Prieto's own stack is [[event-sourcing]] / [[cqrs]] / [[event-driven-architecture]]
(recent writing: the Outbox and Claim-Check patterns).

_Sources: [[yordis-prieto-code-is-the-ultimate-diagram]]._
