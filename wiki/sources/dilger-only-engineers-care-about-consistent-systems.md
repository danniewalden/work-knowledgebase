---
title: "Source: Dilger — Only engineers care about absolutely consistent systems"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-only-engineers-care-about-consistent-systems]
raw_file: [raw/notes/dilger-only-engineers-care-about-consistent-systems.md]
tags: [event-modeling, spec-driven-development, domain-discovery, agentic-coding, focus]
---

# Source: Dilger — Only engineers care about absolutely consistent systems

LinkedIn post by **[[martin-dilger]]**, **2026-09-01** (~330 words). Raw capture:
`raw/notes/dilger-only-engineers-care-about-consistent-systems.md`, retrieved 2026-09-04 in a logged-in
Chrome session; post date derived from LinkedIn's relative age stamp (accurate to the day).

> **VENDOR SELF-REPORT** for the closing product paragraph (EM-Studio's new **Screen Preview**:
> hand-sketched screens, HTML mockups and Figma screens in one storyline). The career anecdote itself is
> personal recollection with no company, date or product named.

**Short-form and the most argumentative of the five notes** — a career story used to make a
methodological point about handovers. No longer primary is referenced.

## Summary

As technical lead on an app for sales agents in physical stores — the capture gives no date — a tight deadline
and budget led the team to **skip the usual chain and talk directly to the agents on the shop floor**.
*"Turns out - What we thought would be useful meant absolutely nothing to them."* The engineering
instinct had been to *"optimize everything, make the system consistent, blocking forms, enforcing the
process. It would have been a desaster."* The lesson: *"Real people care about completely different
things, and they're perfectly fine correcting things manually. Only engineers care about absolutely
consistent systems."*

He then generalises it into a claim about handovers — *"requirements engineers talking to product
owners, product owners talking to business, nobody talking to real clients - everything reshaped a
little at each hop"* — and lands the AI point: *"Now with AI - we are just adding one more hop to the
chain. Engineers talking to AI, writing tons of markdown.. one more handover. I hate it. And I'm
actively working on removing every single one of those handovers."*

## Key points

- **AI as an *additional* handover is the batch's sharpest reframing of the markdown critique.** His
  other posts argue markdown is the wrong *language*
  ([[dilger-communicating-intent-to-an-agent-needs-a-dsl]]) or the wrong *volume*. Here the objection is
  structural: writing a spec for an agent is **one more lossy hop in a chain that was already lossy**,
  regardless of the notation.
- **The prescription is a conversation, then a session, not an artifact.** *"When was the last time you
  were talking to the end user instead of a Jira Ticket? Just give them a call, it might change
  everything. Or even better - just invite them to a short Event Modeling Session. Show them what you
  planned, show them the screens you sketched. Ask the end user for feedback. Turns out - you do not
  have to write a single line of code for that."*
- **Screens are the artifact end users react to** — the mechanism behind
  [[dilger-ux-as-first-class-in-spec-driven-development]] and the reason **Screen Preview** exists
  (sketch + HTML + Figma in one storyline).
- **A substantive concession, easy to miss:** users *"are perfectly fine correcting things manually."*
  That is an argument against over-modelling and against blocking-form enforcement — which cuts against
  the enforcement instinct elsewhere in his own material
  ([[dilger-keep-command-handlers-pure|"enforce, don't just document"]]) and rhymes with the
  Automation-pattern preference for **inspectable to-do lists over rigid process managers**
  ([[process-managers-and-todo-lists]]).

## Limits

- **An anecdote with no verifiable detail and no date** — no employer, product, year or outcome; the
  capture says only that it was "the most important lesson of my career." It is offered as career-shaping
  and read as such, and it is not evidence about agents: the AI claim is appended to the story, not drawn
  from it.
- **The generalisation does not follow from the story.** "Talk to end users" is a classic
  requirements-discovery lesson; "therefore Event Modeling sessions remove the handovers" is a separate
  claim the post asserts without support. **The KB holds no evidence that modelling sessions actually
  achieve multi-stakeholder participation** — the named gap on [[event-modeled-agent-design]].
- **VENDOR SELF-REPORT** for Screen Preview (above).
- *"I'm actively working on removing every single one of those handovers"* is a statement of intent.

## Connections / contrast

- **It is the closest thing in Dilger's corpus to an answer to
  [[ng-spec-driven-development-is-waterfall-in-markdown|Ng's authorship objection]]** — *"the spec is a
  contract between you and the LLM that nobody else signed"* — and it answers it in Ng's own terms:
  the problem is **provenance and hops**, not format. Both men conclude the fix is *"get the people who
  hold the constraints into the room"*; they diverge on what the room produces (Ng: a
  [[decision-trace]] record of conversation; Dilger: a model with screens). **This convergence is worth
  stating on both pages** — it is the second independent instance in this batch of a sceptic and Dilger
  agreeing on a diagnosis and splitting on the remedy.
- **It converges independently with [[larry-constantine]]-era usability thinking and with
  [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto's]] Lean-Startup loop** (identify
  the riskiest assumption, test it cheaply) — both say the expensive artifact is the wrong place to
  resolve uncertainty; Zaninotto resolves it by *building*, Dilger by *asking*.
- **Against [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]]:** Tornhill's claim is
  that implementation *is* the discovery process. Dilger's here is that **user conversation** is, and
  that you *"do not have to write a single line of code for that."* That is the cleanest statement of
  the disagreement in the batch, and it is empirically testable in principle by nobody who has published
  yet.
- **"Only engineers care about absolutely consistent systems"** also bears on
  [[dynamic-consistency-boundaries]] and [[event-sourcing]] advocacy generally: it is a
  practitioner-advocate conceding that strong consistency is often an engineering preference rather
  than a business requirement.

_Related: [[martin-dilger]] · [[event-modeling]] · [[domain-discovery]] ·
[[spec-driven-development]] · [[event-modeled-agent-design]] · [[decision-trace]] ·
[[eventmodelers-ai]] · [[dilger-ux-as-first-class-in-spec-driven-development]]._
