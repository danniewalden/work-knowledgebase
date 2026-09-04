---
title: "Source: Bogard — Vertical Slice Architecture Webinar Recording, and What's Next"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [bogard-vertical-slice-architecture-webinar-recording-whats-next]
raw_file: [raw/articles/bogard-vertical-slice-architecture-webinar-recording-whats-next.md]
tags: [vertical-slice-architecture, agentic-coding, ai-readable-code, substrate, focus]
---

# Source: Bogard — Vertical Slice Architecture Webinar Recording, and What's Next

Short post (a "1 min read" announcement) by **[[jimmy-bogard]]** on jimmybogard.com, 2026-09-01. Raw
capture: `raw/articles/bogard-vertical-slice-architecture-webinar-recording-whats-next.md`.

This is the **first time the KB has Bogard himself — the originator of
[[vertical-slice-architecture|VSA]] — connecting his own pattern to AI-assisted development.** Everything
the VSA page carries on the agent argument to date comes from other people
([[jeremy-miller]], [[rico-fritzsche]], [[martin-dilger]], [[nick-tune]]).

## Summary

Announcement of the recording of a Codeartify webinar ("Vertical Slice Architecture: Effective Guardrails
for AI Development", 700+ registrations), plus a two-part six-hour follow-up course and a Zurich workshop
(17–18 November). The substance is three sentences of argument, which the KB's VSA page had already
noticed and flagged as un-ingested:

> "In short, we've made **writing** code nearly free and left the cost of **verifying and changing** it
> exactly where it was. **An agent doesn't read your architecture diagram. It reads your repo and copies
> what it finds.** That's why structure matters more now, not less. Slices hold up under an agent because
> a change fits in one context window, the blast radius stops at the slice boundary, and the tests still
> mean something after a refactor."

## Key points

- **The economics claim:** writing code is nearly free; **verifying and changing** it costs what it
  always did. Structure therefore "matters more now, not less" — a direct inversion of the "AI makes
  architecture matter less" line.
- **The mechanism claim, and the KB's best one-line statement of it:** *"An agent doesn't read your
  architecture diagram. It reads your repo and copies what it finds."* This is the reason an advisory
  boundary is insufficient and a **structural** one is not.
- **Three named properties of a slice under an agent:** (1) a change **fits in one context window**;
  (2) the **blast radius stops at the slice boundary**; (3) **tests still mean something after a
  refactor**.
- **Framing as "guardrails."** The webinar title positions VSA as *guardrails for AI development* — i.e.
  the pattern is being taught as an agent-safety measure, not only as a code-organisation preference.
- **Commercial context:** the post sells training (Codeartify sessions, a paid workshop). It is an
  announcement, not an argument developed at length.

## Connections / contrast

- **Closes an explicit gap on [[vertical-slice-architecture]].** That page already quotes this raw file
  in a parenthetical, noting it was the sharpest available statement of *why* an advisory boundary fails
  and marking it un-ingested. It is now ingested; the parenthetical should cite this page.
- **The originator now agrees with the borrowers — which is not corroboration.** [[jeremy-miller]] called
  Wolverine's VSA emphasis "accidentally prescient" and was explicit that the token claim is **unproven**
  ("it's incumbent upon people like me to prove that out over time",
  [[miller-jasperfx-critterstack-ai-event-modeling-strategy]]). Bogard states the same three properties
  as fact, with **no measurement whatsoever** — so the page's token/blast-radius argument still rests
  entirely on assertion - one more asserting voice, the same evidentiary standing. (Not a headcount:
  [[fritzsche-vsa-does-not-fix-entity-centered-thinking|Fritzsche]] disputes the blast-radius claim, so
  he is not among its asserters.)
- **Supplies the missing rationale for [[nick-tune-enforced-application-architecture-agents-humans|Tune's
  build-time enforcement]].** Tune reports that agents violate written guidance and therefore fails the
  build on cross-feature imports; Bogard says *why* that happens (the agent reads the repo, not the
  doc). Read together they form the argument for enforcement rather than convention.
- **Contrast with [[rico-fritzsche]]'s objection.** Bogard's "the blast radius stops at the slice
  boundary" is exactly what [[fritzsche-vsa-does-not-fix-entity-centered-thinking|Fritzsche disputes]] —
  a CRUD-shaped slice still radiates through the shared entity model, so slice-shaped folders do not by
  themselves bound blast radius. Bogard's claim is conditional on the slice having been cut along a
  business operation, which he does not restate here. The two should be read as a pair.
- Adjacent: [[slice]] (the model-unit vs code-unit disambiguation) · [[locality-of-reference]] ·
  [[agent-legibility]] · [[ai-readable-code]] · [[token-budget-quality-cliff]] ·
  [[dudycz-vertical-slices-ownership-and-external-dependencies]] (the same closing argument, worked out
  in far more detail) · [[cqrs]].

## Limits

- **A promotional announcement, ~220 words including headings.** The argument is three sentences; the reasoning behind it is
  in a webinar recording and paid courses that **are not captured** — the recording and Q&A are the
  primary, and this page is only its trailer.
- **No measurement, no example, no caveats.** "A change fits in one context window" is asserted without a
  codebase, a model, or a token count. IMPRESSION NOT MEASUREMENT applies to all three slice properties.
- **Commercially interested**: Bogard sells VSA training, and the post exists to sell it.
- Says nothing about *how to cut* a slice — the question [[fritzsche-vsa-does-not-fix-entity-centered-thinking]]
  and [[dudycz-vertical-slices-ownership-and-external-dependencies]] both argue is the one that decides
  whether any of the claimed properties hold.

_Source: `raw/articles/bogard-vertical-slice-architecture-webinar-recording-whats-next.md`._
