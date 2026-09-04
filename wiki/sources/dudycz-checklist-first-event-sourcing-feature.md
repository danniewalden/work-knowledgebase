---
title: "Source: Dudycz — A checklist for picking your first Event Sourcing feature (LinkedIn)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-checklist-first-event-sourcing-feature]
raw_file: [raw/notes/dudycz-checklist-first-event-sourcing-feature.md]
tags: [event-sourcing, adoption, substrate, focus]
---

# Source: Dudycz — A checklist for picking your first Event Sourcing feature (LinkedIn)

LinkedIn post by **[[oskar-dudycz]]**, 2026-09-01, part of his **#EventDrivenDiary** series. Raw
capture: `raw/notes/dudycz-checklist-first-event-sourcing-feature.md` — captured verbatim via **live
logged-in Chrome**; only edit is collapsing LinkedIn's `hashtag\n#x` markup. **Date accurate to the day,
not the hour.**

**Register, and the author's own disclaimer.** This is a **PRACTITIONER HEURISTIC — 14 questions he
proposes, not a validated instrument** — and he disclaims it in the post itself: *"if this checklist
lacks the depth and nuance for you, then I agree; that's why I don't like checklists! And hey, are you
looking for nuance and in-depth analysis on LinkedIn? Sweet summer child!"* The nuance lives in a linked
article (`https://lnkd.in/dAurDQ4B`, shortened, **not resolved at capture**) — so **the fuller primary is
NOT in the KB**; capturing it is a named gap in the batch deltas.

## Summary

The question is adoption, not theory: *"How to start with #EventSourcing? How to pick a first feature for
it?"* — answered as fourteen questions to ask about a candidate feature. Reproduced as posted:

1. Who owns the process lifecycle?
2. Do we produce our own events, or only consume other people's?
3. Can a command be rejected for a business reason?
4. Is the decision a business rule or a retry policy?
5. Could we run an EventStorming session on it with a non-technical colleague?
6. Does the stream end?
7. Is it off the critical path?
8. What happens if it's wrong for a day?
9. Could we walk it back in a week?
10. Is it small enough to do slightly rogue?
11. Can the event store we choose run on storage we already operate?
12. Does it fit inside a single module?
13. Is any part of it asynchronous?
14. Is it real?

He closes by inviting disagreement ("What would you add to this (check)list? Or maybe you disagree with
it?").

## Key points

- **The list is not one list.** Read against the KB's other substrate material it separates into four
  groups, which is what makes it useful rather than arbitrary:
  - **Is this a decision-shaped domain at all?** (1, 2, 3, 4, 5, 13) — ownership of the lifecycle,
    producing rather than only consuming facts, **commands that can be rejected for a business reason**,
    and the business-rule-vs-retry-policy distinction. Question 3 is the tell that a decision exists to
    record; question 4 separates domain logic from infrastructure concerns.
  - **Does the data have a shape you can live with?** (6, 12) — "**Does the stream end?**" is the
    lifetime question he develops in [[dudycz-archiving-events-stream-lifetime-slicing]]; "does it fit
    inside a single module?" is the boundary question from
    [[dudycz-vertical-slices-ownership-and-external-dependencies]].
  - **Is the blast radius survivable while you learn?** (7, 8, 9, 10) — off the critical path, tolerable
    if wrong for a day, reversible in a week, small enough to do "slightly rogue." This is the group that
    makes it an *adoption* checklist rather than a design one, and question 10 is unusually candid about
    how such things actually start in organisations.
  - **Can you operate it, and does it matter?** (11, 14) — run the store on storage you already operate;
    and "**is it real?**" as the final filter against demo-shaped pilots.
- **Question 5 is a method dependency:** if you cannot run an [[event-storming]] session on it with a
  non-technical colleague, the domain probably is not understood well enough to record facts about.
- **He does not claim the list is sufficient** — the explicit anti-checklist framing is part of the
  content, and any downstream page should carry it.

## Connections / contrast

- **The KB's first adoption-selection guidance for event sourcing.** [[event-sourcing]] carries *why* and
  *how*, and [[axoniq-government-ai-explainability-requirements]] carries a vendor's "adopt incrementally,
  start where auditability matters most." Dudycz's list is finer-grained and, notably, **selects on
  reversibility and low stakes rather than on business value** — the opposite of the vendor's
  start-where-it-matters-most advice. That is a genuine difference in adoption strategy worth recording:
  learn cheaply first (Dudycz) vs. prove value where the pain is (AxonIQ, an interested party).
- **Questions 3 and 4 encode the [[command-context-consistency]]/[[dynamic-consistency-boundaries]]
  premise**: a feature is worth event-sourcing when there is a *decision with rejectable outcomes*, which
  is precisely what a consistency boundary protects. [[enzler-event-sourcing-aggregates-dcb-or-what]]
  reaches the same place from the other end (if commands rarely conflict, you may need no boundary
  mechanism at all).
- **Compatible with [[fritzsche-event-sourcing-is-not-an-audit-feature|Fritzsche's]] motivation
  argument** — note that **"do we need a history?" is not on the list.** Whether by design or not, the
  checklist selects on decisions, ownership and reversibility, exactly as Fritzsche says one should.
- Adjacent: [[event-modeling]] · [[business-capabilities]] · [[slice]] ·
  [[dilger-99-percent-software-boring-two-patterns]] (where ES is and isn't worth it) ·
  [[dudycz-fixing-bugs-in-event-sourcing]] (question 8, "what happens if it's wrong for a day?", is that
  article in one line).

## Limits

- **A social-post checklist the author himself disclaims** (see above). Not validated, not weighted, no
  scoring, no guidance on what to do when answers conflict — and the questions are unexplained one-liners
  whose reading depends on knowing his other work.
- **The fuller article is uncaptured**, so the nuance he says exists is not in the KB.
- **No evidence of any kind**: no adoption outcomes, no reports of teams using it.
- Several questions are **ambiguous as posted** — "Is it real?", "slightly rogue", "Is the decision a
  business rule or a retry policy?" — and cannot be applied without interpretation.
- Day-accurate date only; series context uncaptured.

_Source: `raw/notes/dudycz-checklist-first-event-sourcing-feature.md`._
