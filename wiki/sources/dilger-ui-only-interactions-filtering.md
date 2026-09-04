---
title: "Source: Dilger — How to Model UI-Only Interactions (A Filtering Example)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-ui-only-interactions-filtering]
raw_file: [raw/articles/dilger-ui-only-interactions-filtering.md]
tags: [event-modeling, given-when-then, event-modeling-anti-patterns, agentic-coding, focus]
---

# Source: Dilger — How to Model UI-Only Interactions (A Filtering Example)

Article by **[[martin-dilger]]** on the eventmodelers.ai blog, **2026-07-31**, ~6 min read. Answers a
Slack question — *"How would you model filtering? As in, you have a table of data of books and you want
to filter it by genre"* — with a worked chapter. Raw capture:
`raw/articles/dilger-ui-only-interactions-filtering.md`.

> **VENDOR SELF-REPORT.** Every mechanism here is a feature of Dilger's own platform
> ([[eventmodelers-ai]] / EM-Studio, [[nebulit]]): Multi-Screen Views, the HTML View editor, built-in
> Query support, the `@eventmodelers/cli`. The piece closes by selling the **priced "Agentic Engineer"
> programme** starting 2026-09-07 (*"only 7 seats left"*) — see
> [[dilger-agentic-engineer-program-stack-agnostic-spec]].

## Summary

The method answer: **most screen interactions are not state changes and should not be modelled as
Commands and Events.** *"Filtering, sorting, expanding a row, switching a tab - these are all views on
data you already have. Model them as Views, not as Commands looking for an Event to justify them."*
The mechanism is **Multi-Screen Views** — two pages (unfiltered list, filtered list) backed by the
**exact same `Books[]` read model** — with behaviour specified in
[[given-when-then|Given/When/Then]] using the read-side **Query** WHEN.

## Key points

- **The honest opening:** *"the honest answer is: it depends - and most of the time, filtering doesn't
  need a Command or an Event at all."* Client-side or an API refetch is an implementation choice the
  model does not need to take a position on.
- **Structure of the worked chapter:** a Chapter is *"a timeline of things that happen - a small,
  self-contained slice of the world you're modeling"* (the [[event-modeling|Element → Slice → Chapter →
  Story → Context]] ladder). Left side: a Command producing a `Book registered` Event on the swimlane.
  Right side: the View.
- **The read-side scenario uses the proposed Query WHEN, now shipped and in ordinary use.** *"Given two
  `Book registered` events - one for Harry Potter, one for Lord of the Rings - When you query by title
  with the key 'Harry Potter', Then the `Books` Read Model returns just that one match."* And the point
  he draws from it: *"Nothing about this Scenario depends on the UI plumbing. It's stated purely in
  terms of the data."* This is the extension proposed in
  [[dilger-extending-event-modeling-query-when]] (2026-06-29) as *optional and not ratified* — here it
  is used as the ordinary way to specify a read side, without restating its status.
- **Screens are authored in the model, in HTML.** *"Give the new HTML View a try - you can write your
  Views with plain HTML, or even better, just generate them very cheaply with your connected agent."*
- **The UI mockup is an agent-readable artifact.** *"Using the UI mockup - which is also accessible for
  a connected agent building from the model - it's quite clear what needs to be done."* This is the
  claim that matters for this KB: **the screen is part of the spec the agent builds from**, not a
  human-only annotation.
- **A 15-second agent onboarding path:** `npx @eventmodelers/cli init-modeling` connects an agent to
  the platform.
- **Enough is enough.** *"This is enough to implement it"* — the completeness bar is the mockup plus
  the GWT scenario, with no Command or Event invented to justify the interaction.

## Limits

- **VENDOR SELF-REPORT** (above), and the article is partly a feature announcement (Multi-Screen
  support, HTML Views, Query support) as well as a method answer.
- **No evidence and no counter-case.** The rule ("model UI-only interactions as Views") is asserted
  from experience — *"I've answered it dozens of times already"* — with no worked example of when
  filtering *should* become an event (e.g. when "which filter a user applied" is itself a business fact
  worth recording, an obvious edge the article does not discuss).
- **Uses the Query WHEN without repeating that it is a proposed, opt-in, unratified extension** to the
  method. Any downstream page must carry that status from
  [[dilger-extending-event-modeling-query-when]].
- Nine inline screenshots are noted in the raw and not reproduced, so the board mechanics are described
  rather than shown.

## Connections / contrast

- **A method clarification for [[event-modeling]] that the KB did not hold:** the "only state changes
  count" rule ("user viewed the calendar" is not an event) restated as *positive* guidance — here is
  what to draw instead, and how to specify it. It is also implicitly an anti-pattern warning
  ([[event-modeling-anti-patterns]]): Commands invented to justify Events for interactions that change
  nothing.
- **The KB's clearest instance of [[screens-as-specification|screens as specification]], and it is
  agent-facing.** Pair with
  [[dilger-ux-as-first-class-in-spec-driven-development]] (UX as a first-class citizen instead of
  markdown-derived), [[dilger-highlighting-markers-give-context-to-agents]] (region-scoped markers
  agents read and build UI from), [[dilger-only-engineers-care-about-consistent-systems]] (Screen
  Preview: hand sketches + HTML mockups + Figma in one storyline) and Dymitruk's *"screens are not a
  distraction"* in [[dilger-podcast-episode-47-agentic-modeling-audit-trails]].
- **It is a partial answer to [[zaninotto-spec-driven-development-waterfall-strikes-back|Zaninotto's]]
  one stated wish** — *"coding agents use text, not visuals … the focus should be on richer visual
  interactions"* — from the camp he was arguing against, with neither aware of the other.
- **And a partial answer to
  [[ng-spec-driven-development-is-waterfall-in-markdown|Ng's authorship objection]]:** a screen is the
  artifact a designer or an end user can actually react to, which is the multi-perspective property Ng
  says a markdown spec destroys. Partial, because nothing here shows a designer in the room — see the
  named gap on [[event-modeled-agent-design]].
- **Tension with [[gojko-adzic]] and [[jeremy-miller]]:** Adzic wants the human-approvable spec to be
  richer than scope-of-work; Miller wants GWT and nothing else authored by hand. Dilger's answer here is
  *screens plus GWT and no more* — closer to Miller on volume, closer to Adzic on reviewability.

_Related: [[martin-dilger]] · [[event-modeling]] · [[given-when-then]] ·
[[dilger-extending-event-modeling-query-when]] · [[event-modeling-anti-patterns]] ·
[[agent-readable-model-artifacts]] · [[spec-driven-development]] · [[eventmodelers-ai]] · [[slice]]._
