---
title: "Source: Dudycz — Fixing bugs in Event Sourcing is hard, for real?"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-fixing-bugs-in-event-sourcing]
raw_file: [raw/articles/dudycz-fixing-bugs-in-event-sourcing.md]
tags: [event-sourcing, event-versioning-and-upcasting, decision-trace, operations, substrate, focus]
---

# Source: Dudycz — Fixing bugs in Event Sourcing is hard, for real?

Article by **[[oskar-dudycz]]** (Architecture Weekly / event-driven.io, 2026-07-27). Raw capture:
`raw/articles/dudycz-fixing-bugs-in-event-sourcing.md`.

**Everything numeric in this article is an invented scenario, not data.** It opens "Imagine we're
working on a hotel reservations system" and every figure — the 4.50→7.00 tourist tax, the 1,240 matched
rows, the ~900 from the broken build, the 340 wrongly caught, the 180.00→205.00 rate revision, the ~400
repriced reservations, the 98.00-vs-73.00 city tax — is **illustrative arithmetic within that scenario**.
The experience claims around it ("I've been on both ends of this", the night-audit horror story, "I've
done all of those") are **IMPRESSION NOT MEASUREMENT**. Cite the mechanism, never the numbers.

## Summary

The article answers the standard objection to [[event-sourcing]] ("you can't fix bad data in an immutable
log") by running the same incident twice — once against a mutable row, once against an event stream — and
comparing what material is left to work with afterwards.

**The bug:** a tourist-tax rate change adds validity periods; the lookup resolves the rate once per
reservation from the **check-out date** and applies it to every night, so a stay crossing the boundary is
charged the new rate for old nights. Shipped 12 March, reported 19 March, fixed 16:02 the same day.

**State-based recovery fails in a specific, traceable way.** The row records `total_amount` and
`updated_at` and nothing about how the number was produced — no breakdown, no record of which nights got
which rate, no rate-plan version. So the corrective migration must **recompute**, and recomputing reads
today's rate plan (revised on 15 March for the season), which reprices rooms that were never wrong. The
`WHERE` clause also catches reservations merely *touched* during the window, "and there's nothing in the
row that separates 'this changed' from 'this changed because of the bug'." Then migration two must be
written against the data migration one produced: `updated_at` is now uniform, `total_amount` holds the
migration's value, and booking dates have to be reconstructed from confirmation emails. **"If we get that
wrong, the input to migration three is the output of migration two."**

**Event-sourced recovery differs because the inputs survive.** `RatePlanApplied` still says v4 at
180.00/night; `ReservationPriceCalculated` still carries the per-night breakdown; the wrong `cityTax` is
"sitting there in plain sight" next to the numbers that produced it. So the correct total is a
calculation, not a reconstruction — "The 14 March event still says what it said on 14 March, whatever was
appended later."

## Key points

- **`buildSha` in event metadata is the article's most portable, most concrete idea.** Record the commit
  the service was running when it appended the event ("an environment variable and a few lines in
  whatever builds our metadata"), and the blast-radius query becomes exact:
  `WHERE type = 'ReservationPriceCalculated' AND metadata->>'buildSha' = 'a4f9c2e'` — returning the events
  the broken binary produced, and **not** the ones merely touched in the same week. `correlationId`
  groups one user action, `causationId` chains back to the triggering command. "Without the SHA, we're
  still ahead, because the position and timestamp of an appended event don't move once it's written.
  Still, I recommend to add the sha."
- **Fix forward; do not rewrite.** "Events are immutable, and, surprising as it sounds, having precise
  history, bugs included, is a valid scenario. It's often the only way to see later what really went
  wrong." Quoting his own earlier post: *"you should not change the past… even including bugs, is a valid
  scenario."* The move is an **accountant's correcting entry** — append `ReservationPriceCorrected`
  (`previousTotal`, `correctedTotal`, `reason`), then rebuild read models and fix the bug.
- **The correction is itself an event, and that has a UX consequence:** "the next person to open this
  stream sees that a bug happened, when it was corrected and why. Nobody has to remember, and if we
  surface it in the UI, the front desk sees it too."
- **Recursion is bounded.** If the correction is *also* wrong, "the recovery is the same operation as
  before, because the 14 March events are still there… attempt three is calculated from the booking, not
  from attempt two." This is the precise statement of what the mutable version loses: **fixing data
  overwrites the evidence you'd need to check whether the fix worked.**
- **The best argument in the piece is the "customer already fixed it" case.** A front-office agent had
  already corrected one reservation by hand, taking 42.00 off the rooms as goodwill agreed with her
  manager. A blind bulk recalculation is *arithmetically correct* and **undoes a deliberate human
  decision** — third number, third email, and a support note describing a value that no longer exists.
  With a stream you can branch on it (skip if a `ReservationPriceCorrected`, or any price-affecting
  event, follows the bad one), and everything skipped goes on a list for a person. **"In the mutable
  model, a bug and a deliberate correction look identical: a number in a column. There's nothing to
  branch on."**
- **Make the correction a feature.** Ask the business "how do you fix this today?" — there is almost
  always an existing answer (a form, a manager's approval, a note in the folder). Model it:
  `CorrectReservationPrice` with permissions, validation and a **mandatory reason**, producing
  `ReservationPriceCorrected`. The bulk fix then runs through the same command as the front desk, and
  "nobody connects to the production database at 23:00." His follow-up question when the business says
  something can never happen: **"fine, how often?"**
- **The honest concession on partial adoption:** you *can* prepare a state-based system (JSON breakdown
  column, rate-plan version, a `price_history` table, a `corrected_by` marker) — "I've done all of
  those" — but each is added *after* the incident that taught you to, on the table where that incident
  happened. "What we're building at that point is a **partial event log, decided per column, under time
  pressure.**"
- **"But now the history contains a bug" — yes.** "The wrong price was real. It was shown to the guest…
  it may have reached the invoice and the tax report. A log that shows only the corrected price can't
  explain why the guest called." If a clean stream is needed for a regulator or a migration, **copy and
  transform into a new stream and keep the original.**
- **What it does not promise:** "None of this stops us shipping the bug, makes repricing 900 reservations
  free, or spares us the conversations with guests whose total changed twice. What we get is **better
  material to work with.**"

## Connections / contrast

- **Answers an objection the KB had no answer to.** [[event-sourcing]] and
  [[event-versioning-and-upcasting]] cover *schema* change; this is the first source on **bad data and
  incident recovery**, which is the objection practitioners actually raise. The two are complementary and
  should stay distinct: upcasting is about an event's *shape* changing; this is about an event's *value*
  being wrong.
- **A corrective-event vocabulary the KB lacked.** `ReservationPriceCorrected` as a first-class,
  permissioned, reason-carrying command sits naturally beside
  [[fritzsche-how-event-sourcing-grows-with-the-business|Fritzsche's additive-schema argument]] (new
  capability = new event type + new function) — correction as *just another capability* rather than an
  out-of-band operation. It is also the operational form of
  [[dilger-done-is-done-open-closed-new-slice|"done is done"]]: don't edit the past, add a slice.
- **The strongest evidence-preservation argument in the KB, and it is not about audit compliance.**
  Where [[axoniq-government-ai-explainability-requirements|AxonIQ]] argues the log satisfies regulators
  and [[fritzsche-event-sourcing-is-not-an-audit-feature|Fritzsche]] argues audit is the wrong
  motivation, Dudycz shows a third payoff neither names: the log is what lets you **check your own
  fix**. That is an *engineering* argument for the same property, and it partly reconciles the two — the
  history matters, but for recovery rather than for reporting.
- **`buildSha` is a [[decision-trace]] primitive.** It links a stored fact to the exact code that
  produced it — the same "which version of the system decided this" question
  [[agent-explainability]] asks of agents, answered at the event-metadata level. Directly reusable for
  agent-written events (which agent, which prompt version, which build).
- **Fritzsche's row critique, with a bill attached.**
  [[fritzsche-why-the-entity-model-is-an-illusion]] argues the row "says nothing about how they got
  there" and that audit/history tables are workarounds; this article prices exactly that gap in an
  incident. The two make an unusually complete case, one conceptual and one operational.
- Adjacent: [[cqrs]] (read-model rebuild after correction) · [[given-when-then]] (the `needsCorrection`
  predicate is a testable rule) · [[oskar-dudycz]] · [[dudycz-checklist-first-event-sourcing-feature]]
  ("What happens if it's wrong for a day?" is this article compressed to one question).

## Limits

- **A constructed scenario, start to finish.** No client, no incident report, no measured outcome. The
  comparison is between two accounts the same author wrote, and the state-based version is written to
  fail (though the failure mode — recompute-with-today's-config — is a familiar one).
- **Costs are acknowledged but not quantified**: read-model rebuild time, the bulk-append path ("we could
  optimise it by loading multiple reservations at once… the rest is mostly performance optimisation"),
  and the operational load of a human review list.
- **`buildSha` is offered as advice, not as a validated practice** — no report of it being used in anger,
  and it silently assumes one deployable per event stream and immutable build tags.
- **Presumes projections can be rebuilt cheaply** and that downstream consumers (invoices, tax reports,
  emails already sent) can absorb a correction — the article names those side effects but does not solve
  them.
- **The "copy and transform into a new stream" escape hatch for regulators is one sentence**, with no
  treatment of identity, references, or the GDPR-style erasure case (see
  [[dudycz-archiving-events-stream-lifetime-slicing]] for his adjacent thinking on stream lifetime).
- Author is a commercial trainer/consultant on event sourcing - an interested party for "event sourcing
  handles this better," though the argument is mechanical and checkable. Note that **this** post carries
  no sales pitch and closes only "Cheers! Oskar"; the consulting p.s. is on
  [[dudycz-vertical-slices-ownership-and-external-dependencies]], not here.

_Source: `raw/articles/dudycz-fixing-bugs-in-event-sourcing.md`._
