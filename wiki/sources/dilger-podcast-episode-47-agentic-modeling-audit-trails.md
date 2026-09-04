---
title: "Source: EM Podcast Ep 47 — Agentic Modeling, Audit Trails, and the Fish Shell Effect"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-podcast-episode-47-agentic-modeling-audit-trails]
raw_file: [raw/articles/dilger-podcast-episode-47-agentic-modeling-audit-trails.md]
tags: [event-modeling, event-sourcing, agentic-ai, podcast, event-modeling-anti-patterns, focus]
---

# Source: EM Podcast Ep 47 — Agentic Modeling, Audit Trails, and the Fish Shell Effect

Show notes for **Episode 47** of the [[event-modeling-event-sourcing-podcast|Event Modeling & Event
Sourcing podcast]] with **[[martin-dilger]]** and **[[adam-dymitruk]]**, published on
`eventmodelers.ai/docs/podcast/episode-47/`. Raw capture:
`raw/articles/dilger-podcast-episode-47-agentic-modeling-audit-trails.md`.

> **⚠ DATE UNRESOLVED — do not assign one.** The page carries no publication date in its HTML, its
> metadata or its visible text, so the capture is filed `published: unknown` and **the wiki must treat
> the date as unresolved too**. What is known: Ep 47 is **absent from the podcast RSS feed and from
> podcast.eventmodeling.org**, both of which still end at **Ep 46 (2026-04-26/27)**, so it post-dates
> 2026-04-27. Internal dating signals: it announces [[golo-roden]] as a confirmed speaker for the
> *"already sold-out"* Event Modeling Conference (the 2027 Munich edition, Roden having already spoken
> at the 2026 edition on 2026-06-26), and the site banner reads *"Agentic Engineer Course — September
> cohort sold out"* (cf. [[dilger-agentic-engineer-program-stack-agnostic-spec]], 2026-09-03).
> **And it may not be a new item at all:** `eventmodelers.ai/docs/podcast` is a channel prior sweeps
> never polled — a separate, more current episode index than the `.org` one — so this is at least as
> likely a *missed-channel discovery* as a fresh publication.

> **VENDOR SELF-REPORT** for everything about the tooling: eventmodelers.ai / EM-Studio is Dilger's own
> commercial platform ([[eventmodelers-ai]]), and the `/wdyt` skill discussed here ships on it.

**Show-notes level only.** As with [[event-modeling-event-sourcing-podcast]], this page is built on
published notes and quoted pull-outs, **not verified against the audio**
(<https://www.youtube.com/watch?v=p7w38COHTZM>).

## Summary

Two threads matter for this KB. **Dilger** ran two AI agents modelling alongside him on a live board and
demoed the *"what do you think"* gap-finding skill, with a tuning lesson about over-specification.
**Dymitruk** states the counterpoint the rest of the batch answers: *agents need an audit trail, not a
snapshot.* The remainder is community commentary (the industry rediscovering old ideas; screens are not
a distraction; fish-shell-vs-bash as a metaphor for tooling resistance).

## Key points

- **Two agents modelling concurrently, and the claim about it.** A Claude Code instance and a **Hermes**
  agent added slices and comments alongside him simultaneously; *"he says it was indistinguishable from
  modeling with humans."* **IMPRESSION NOT MEASUREMENT**, and the strongest form of the KB's
  agent-authors-the-model rung ([[event-modeled-agent-design]]) — but a felt comparison, not an
  evaluation.
- **The `/wdyt` skill in action.** The agent reads through slices and **posts comments asking
  clarifying questions**: *"He commented on the slice and asked: well, what happens if a user clicks
  this twice? What should be the behavior? … And this is perfectly valid — a perfectly valid
  question."* This is the [[event-modeling-anti-patterns|/wdyt]] skill already in the KB, now with a
  worked interaction.
- **The tuning lesson, which is the transferable finding.** The first version *"flooded the model with
  100 comments inventing hypothetical gaps."* The fix: *"don't just look at what is there — don't
  comment on something because it's not specified. Just look at what is there and make sense of it,
  then give me comments. And then it got significantly better."* A **restriction to what is present,
  with invention forbidden**, is what turned a noisy reviewer into a useful one. The counts (100 → "genuinely
  useful") are impressions.
- **Dymitruk's counter-pressure on the same skill:** an over-eager agent flooding a
  [[given-when-then|given-when-then]] list with edge cases *"can make a simple slice look far more
  complex than it really is, since event modeling is visual."* So the anti-pattern is not just noise —
  it degrades the artifact's primary affordance.
- **Specification by example as the pre-existing answer.** *"Event modeling already solves the
  'infinite possibility tree' problem: draw a few representative example paths and trust the
  implementer to infer the rest, rather than trying to specify everything."* Framed as *"the insight
  spec-driven development is still catching up to."*
- **"Agents need an audit trail, not a snapshot" — Dymitruk, verbatim:** *"Events are the truth, the
  full story, not just the current state. Read models are derived and disposable. If an agent goes
  sideways, follow the event trail, find the divergence, fix it, replay. No mystery, no data surgery."*
  Note the provenance: the hosts are **relaying a LinkedIn post by Svet Angelov**, which is not
  captured in `raw/` — so the origin of the framing is uncaptured and Dymitruk's endorsement is the
  citable part.
- **Screens are not a distraction.** A DDD-community post *"rediscovers"* that showing users' screens
  carries real information; Event Modeling has always treated screens as legitimate,
  information-only artifacts. Dymitruk, sharply: *"all the arguments about not having screens and
  design sessions is just gatekeeping by architect wannabes."*
- **Shared vocabulary as the durable payoff:** *"event modeling gives teams an industry-wide shared
  vocabulary — command handlers, event handlers — instead of one-off, in-house conventions that don't
  scale across companies"* ([[em-standardization-foundation]]).
- **[[golo-roden]] confirmed** for the sold-out conference with an assumed-knowledge talk.
- **Fish shell vs bash** as Dymitruk's metaphor: resistance to a better tool is never about the tool —
  it is *"that's not how we work here"*, the same resistance [[event-sourcing]] and [[event-modeling]]
  meet.

## Limits

- **Date unresolved** (above) — the single most important caveat on this page. Any downstream page
  citing it must not imply a date, and must not treat it as "the newest thing" without saying the
  channel was previously unpolled.
- **Show notes, not transcript.** Quotes are the site's own pull-outs; nothing is verified against
  audio, and the KB's standing podcast caveat applies.
- **VENDOR SELF-REPORT** for the platform and skill; **IMPRESSION NOT MEASUREMENT** for
  "indistinguishable from modeling with humans" and for the comment counts.
- The audit-trail framing originates in an **uncaptured third-party LinkedIn post** (Svet Angelov);
  treat Dymitruk as endorsing, not originating.

## Connections / contrast

- **The audit-trail-vs-snapshot argument now has a proposed implementation *and* an instrumented
  instance.** Dymitruk states the requirement here; **[[dilger-git-as-primary-persistence-for-event-models]]**
  proposes the storage answer for the *model* (one git repo per board, branching, WORM-drive
  auditability); and **[[nick-tune-event-sourced-claude-code-workflows]]** independently builds the
  answer for the *loop* (only events persisted, state by replay, per-state timings and hook-denial
  counts). Three sources, three layers, none citing the others — the strongest triangulation in this
  batch. See [[event-sourced-agentic-patterns]], [[agent-governance]].
- **The over-specification finding is a new [[event-modeling-anti-patterns|anti-pattern]] of a
  different kind** from "The Shapes": not a bad model shape a human drew, but **a bad shape an agent
  reviewer induces**. It also puts a real limit on the KB's model-as-rubric optimism
  ([[dilger-one-million-tokens-self-training-modeling-agent]]) — an agent grading a spec can make the
  spec worse.
- **It converges with [[bockeler-tdd-inside-the-agent-loop]] from the model side:** her finding is that
  agent-invented micro-tests suppress design; his is that agent-invented edge cases bloat the model.
  Same mechanism — **an agent inventing its own acceptance criteria** — at two altitudes.
- **"Specification by example already solves the infinite tree"** is the Event Modeling camp's direct
  answer to [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd|Adzic's]] complaint that Spec
  Kit's spec *"lacks a ton of detail"* — and note they answer it in **opposite directions**: Adzic wants
  more detail in a human-readable place, Dymitruk says representative paths plus a competent implementer
  is the right amount. Both are inside the BDD/[[given-when-then]] tradition.
- **Screens-as-legitimate** is the podcast-side statement of
  [[dilger-ux-as-first-class-in-spec-driven-development]] and
  [[dilger-ui-only-interactions-filtering]], and of the KB's existing screen-markers datapoint
  ([[dilger-highlighting-markers-give-context-to-agents]]).

_Related: [[event-modeling-event-sourcing-podcast]] · [[martin-dilger]] · [[adam-dymitruk]] ·
[[event-modeled-agent-design]] · [[event-modeling-anti-patterns]] · [[event-sourced-agentic-patterns]] ·
[[given-when-then]] · [[agent-governance]] · [[golo-roden]] · [[eventmodelers-ai]]._
