# Why Topic-3 has drawn fifteen blanks — a watch diagnosis

**Question.** Topic-3 of `watch-config.json` ("Event sourcing, DCB, CQRS, vertical slice architecture &
business capabilities") has reported "nothing new in window" for **fifteen consecutive sweeps**. Is the
field quiet, or is the watch pointed at the wrong thing?

**Answer: neither, quite. The field is busy, the watch is mis-pointed, and the "fifteen blanks" is
mostly a reporting artifact.** The substrate material has been arriving the whole time — through the
*people* axis, roughly twice a week — while the *topic* axis reported silence and the report format made
it look like a dead thread.

---

## The evidence

Substrate captures filed between 2026-06-04 and 2026-08-26 — the exact window in which Topic-3 reported
fifteen blanks:

| Author | Captures | Span |
| --- | --- | --- |
| Rico Fritzsche | 13 | 06-08 → 08-26 |
| Oskar Dudycz | 4 | 06-08 → 08-10 |
| Vlad Khononov | 2 | 06-30, plus the plugin capture |
| Enzler, AtomicObject, AxonIQ, Goeleven | 4 | 04-14 → 06-23 |
| **Total** | **~22** | **~12 weeks** |

That is a capture roughly every four days on the declared substrate topics — event sourcing, DCB, CQRS,
vertical slices, capability-based design. **Every single one arrived via the people watch.** Not one was
attributed to a Topic-3 query in any log entry.

So the thread is not dead. It is the second most productive thread in the KB after Event Modeling ×
agents — and most of it **has** been compiled: only four of those captures are still outstanding
(Batch I of `outputs/ingest-plan-2026-08-30.md`). Which sharpens the point rather than softening it.
The substrate has been arriving *and* being absorbed for three months, while the sweep report said
"nothing new in window" fifteen times running.

---

## Four structural faults in Topic-3

### 1. The queries have no recency mechanism
Topic-3's eleven queries are generic architecture terms plus a year:

> `"event sourcing" 2026 new` · `CQRS pattern 2026` · `"vertical slice architecture" 2026` ·
> `capability-based design bounded context business architecture`

Web search ranks these by authority, not recency, so they return the highest-authority *evergreen* pages
on each term — and those never change. This is precisely what the log records, verbatim, fifteen times:
eventsourcing.readthedocs, AxonIQ, Baeldung, JAVAPRO (Oct-2025), Ingebrigtsen (Mar-10), eventsourcing.dev,
dotnetconsult (Feb-2026). The query set is structurally incapable of surfacing a two-day-old post. It
isn't failing to find new material; it is asking a question whose answer cannot change.

Contrast Topics 1 and 2, which name **channels** (`eventmodeling.org new posts`, `eventmodelers.ai new post`)
alongside their keyword terms. Topic-3 names no channel at all.

### 2. Topic-3 is redundant with the people watch for everyone who matters
All six of the substrate's active voices are already `people` entries with URLs: Fritzsche, Dudycz, Miller,
Goeleven, Khononov, Tune. Anything they publish is caught by the people axis before Topic-3 could
plausibly see it. What's left for Topic-3 to add uniquely is **new voices** — and see fault 1 for why it
can't find those either.

### 3. The people list is missing the substrate's own originators
The wiki has entity pages for people the watch does not follow:

- **Sara Pellegrini** — the originator of Dynamic Consistency Boundaries, named in Topic-3's own
  description ("the 'kill the aggregate' line of work"). No `people` entry, no channel.
- **Jimmy Bogard** — named in Topic-3's description as the vertical-slice lineage. No `people` entry.
- **Allard Buijze / AxonIQ** — AxonIQ surfaces in the evergreen tier of *every single sweep*, which means
  the watch keeps bumping into the channel without ever polling it properly.

If DCB is a declared sub-area and the person who named DCB isn't on the watch list, the fifteen blanks
stop being surprising.

### 4. The "business capability" social query is a confirmed homonym trap
The 08-26 sweep established this directly: on X and LinkedIn, "business capability" returns HR/marketing/ESG
usage ("responsible data handling is becoming a core business capability"), not architecture. Since business
capabilities is your **flagged-important** priority, this is the most costly of the four faults — the
highest-priority sub-topic has the least functional query in the config.

---

## Recommended config changes

Ranked by expected yield. None of these have been applied — say the word and I'll edit `watch-config.json`.

1. **Add the missing substrate people** (highest yield, lowest effort): Sara Pellegrini, Jimmy Bogard, and
   AxonIQ/Allard Buijze as a company-level channel. All three already have wiki entity pages, so the
   grounding exists; the URLs need verifying on a live sweep before they go in.
2. **Replace Topic-3's generic queries with channel polls.** Drop `"event sourcing" 2026 new`,
   `CQRS pattern 2026`, `"vertical slice architecture" 2026` and the rest of the bare-term set outright —
   fifteen sweeps is a sufficient sample. Replace with named-site checks (eventsourcing.dev, AxonIQ blog,
   event-driven.io, the DCB spec site if one exists) polled for new dated posts, which is how Topics 1 and 2
   actually work.
3. **Fix the business-capability query** by requiring an architecture co-term — `"business capability" AND
   (bounded context OR capability map OR decomposition OR coupling)` — or drop the social variant entirely
   and rely on Goeleven, Fritzsche and Khononov, who are where all the capability material has come from
   anyway.
4. **Change how Topic-3 is reported.** The current format reports the topic axis in isolation, so a week
   with three Fritzsche substrate captures still prints "Topic-3: nothing new in window." Report the
   substrate by *thread*, crediting whichever axis found it. This one change would have prevented the
   false impression that produced this investigation.
5. **Consider retiring Topic-3 as a keyword axis entirely** and keeping only a small new-voice-hunting query
   set. Its real function — following the substrate — is already the people watch's job, and doing it in two
   places produces exactly this kind of contradictory reporting.

---

## The honest caveat

I have not verified that the recommended channels (a DCB spec site, Pellegrini's and Bogard's current
publishing homes) are live and worth polling — that needs a sweep, and this was a read-only analysis of the
config and the log. Treat items 1 and 2 as "verify, then add" rather than settled.

There is also a possibility this diagnosis under-weights: the substrate *authors* may be busy while the
substrate *field* is genuinely quiet on new ideas. Fritzsche's 13 captures are largely restatements of one
position (entity-vs-event, CCC vs DCB) rather than 13 developments. If so, the right response is not more
channels but a decision that the substrate is adequately covered by six people and the topic axis can go.
That is a judgment call about focus scope, and it is yours.
