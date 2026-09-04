---
title: "Khononov — the AI '(s)loop' as the new Holy Grail (microservices-hype rhyme)"
type: source
created: 2026-07-31
updated: 2026-07-31
sources: [khononov-microservices-hype-to-ai-sloop]
raw_file: [raw/notes/khononov-microservices-hype-to-ai-sloop.md]
tags: [loop-engineering, skeptic, contrarian, hype-cycle, microservices, modularity]
---

# Khononov — the AI "(s)loop" as the new Holy Grail

A short **LinkedIn post** by **[[vlad-khononov]]** (2026-06-30) — the KB's **only skeptic / contrarian
voice on the [[loop-engineering]] thread**. Source file:
`raw/notes/khononov-microservices-hype-to-ai-sloop.md` (a note; apostrophes reconstructed from a live
Chrome scrape). Read for its framing, not new technical content.

## The argument (a historical rhyme, not a refutation)

**"Remember the microservices hype 12 years ago?"** The cool kids couldn't stop talking about
microservices as the Holy Grail of software engineering — "ironically, most of them couldn't tell you
what a microservice actually was. Like a bunch of blind men describing an elephant." How it turned out:

1. the **comeback of the modular monolith**, as "half the crowd quietly admitted they never needed the
   network calls in the first place";
2. the microservices heroes "mostly ended up with **distributed monoliths**"; and
3. to cope with the dependency web across poorly-drawn boundaries, they reached for **the monorepo**.

Then the pivot: *"Nowadays, the cool kids discovered the new Holy Grail: the **AI (s)loop**. New
protagonist, same plot: a crowd chasing something most of them can't quite define. 10 years ago it was
about thousands of services, today it's thousands of deploys per day. Let's see what we'll reach for to
cope with the hangover this time."*

The **"(s)loop"** spelling is the whole editorial: *loop* + *slop*. The claim is not that loops don't
work — it's that a genuinely useful idea is being inflated into an ill-defined Holy Grail by people who
can't define it, and that a corrective (the microservices era's modular-monolith/monorepo hangover cure)
will follow.

## Why it matters here

- **The contrarian counterweight the thread lacked.** [[loop-engineering]] is built mostly from
  advocate/practitioner primaries (Osmani, swyx, Willison, Cherny, Steinberger, Anthropic). This is the
  first captured voice saying *the discourse itself is a hype cycle* — filed as the skeptics' note on
  that page. It doesn't dispute the mechanics; it disputes the froth and predicts a reckoning.
- **Consistent with Khononov's own line.** It's the hype-cycle face of his standing thesis that
  **boundaries/modularity are the thing that actually pays off** ([[khononov-golden-age-of-modularity]]):
  microservices failed where boundaries were badly drawn; by implication the loop wave pays off only on
  the same modular substrate ([[business-capabilities]], [[balanced-coupling]]). The predicted "cope"
  this time is left open — an invitation, and a rhyme with the modular-monolith correction.
- **Adjacent framings.** Rhymes with the "dumbest version becomes representative" worry Lowin voices
  about the [[ralph-loop|Ralph loop]] in [[prefect-loops-vs-graphs]] ("a new round of slop"), and with
  the "stay the engineer" caveats of [[loop-engineering]] and
  [[dudycz-fork-can-you-own-it|Dudycz on owning vs producing code]] — but Khononov is the only one
  framing the whole trend as a repeat of a named prior hype cycle.
- Caveat: a short, deliberately provocative social post — rhetoric and analogy, no data.

## Links

Entities: [[vlad-khononov]]. Concepts: [[loop-engineering]], [[business-capabilities]],
[[balanced-coupling]], [[ralph-loop]].
Related sources: [[khononov-golden-age-of-modularity]], [[khononov-modularity-claude-code-plugin]],
[[prefect-loops-vs-graphs]], [[dudycz-fork-can-you-own-it]], [[addyosmani-loop-engineering]].

_Raw source: `raw/notes/khononov-microservices-hype-to-ai-sloop.md`._
