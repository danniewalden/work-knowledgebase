---
title: "Source: Zaninotto — Spec-Driven Development: The Waterfall Strikes Back"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [zaninotto-spec-driven-development-waterfall-strikes-back]
raw_file: [raw/articles/zaninotto-spec-driven-development-waterfall-strikes-back.md]
tags: [spec-driven-development, agentic-coding, agile, controversy, focus]
---

# Source: Zaninotto — Spec-Driven Development: The Waterfall Strikes Back

Blog post by **[[francois-zaninotto]]** (founder & CEO, [[marmelab]]), **2025-11-12**. Drew 225 points
and 191 comments on Hacker News. Cites [[bockeler-understanding-sdd-kiro-speckit-tessl|Böckeler]] as
the tool comparison to read. Raw capture:
`raw/articles/zaninotto-spec-driven-development-waterfall-strikes-back.md`.

The **fullest enumeration of SDD's failure modes anywhere in the KB**, and — given the title's likely
lineage to *"waterfall in markdown"* — the phrase [[ng-spec-driven-development-is-waterfall-in-markdown|Ng]]
was four months later downstream of.

## Summary

Zaninotto's objection has two halves that should not be collapsed. The **empirical** half is a list of
seven failure modes observed using spec-kit and Kiro on small features. The **structural** half is that
[[spec-driven-development|SDD]] is solving the wrong problem — *"How do we remove developers from
software development?"* — and cannot succeed at it, because *"software development is fundamentally a
non-deterministic process, so planning doesn't eliminate uncertainty."* His replacement is not "no
structure" but **smaller units**: split complex requirements into simple ones rather than translating
complex requirements into complex design documents.

## Key points

- **The seven failure modes** (his own headings, and the KB's most complete such list):
  **Context Blindness** — SDD agents discover context by text search and miss existing functions, so
  expert review is still required. **Markdown Madness** — *"Developers spend most of their time reading
  long Markdown files, hunting for basic mistakes hidden in overly verbose, expert-sounding prose. It's
  exhausting."* **Systematic Bureaucracy** — three-step design is excessive; specs contain repetitions,
  imaginary corner cases and overkill refinements, *"written by a picky clerk."* **Faux Agile** —
  generated "user stories" misuse the term (*"As a system administrator, I want the referred by
  relationship to be stored in the database"*). **Double Code Review** — the technical spec already
  contains code, so developers review the spec's code *and* the implementation: *"review time
  doubles."* **False Sense of Security** — in his example the agent marked "verify implementation" done
  without writing a single unit test, substituting manual testing instructions. **Diminishing Returns**
  — *"SDD shines when starting a new project from scratch, but as the application grows, the specs miss
  the point more often … For large existing codebases, SDD is mostly unusable."*
- **The artifact-volume datapoint:** a developer wanting to display the current date on a time-tracking
  app got **8 files and 1,300 lines of text** from spec-kit (linked to the actual PR). This is the
  "1,300 lines of Markdown to display a date" figure the KB has carried attributed to "Augment
  Engineer" via Ng — **the primary is this post**, and the artifact is a linked public PR rather than
  an anecdote.
- **The cost framing:** *"the trade-off (spending 80% of your time reading instead of thinking) is, in
  my opinion, not worth it."* An impression, expressed as a percentage — do not promote it to a
  measurement.
- **The who-is-it-for argument, which is his distinctive one.** *"You must be a business analyst to
  catch errors during the requirements phase, and a developer to catch errors during design. As such,
  it doesn't solve the problem it claims to address (removing developers), and it can only be used by
  the rare individuals who master both trades. SDD repeats the same mistake as No Code tools."*
- **Agents already have plan mode and task lists**, so *"in most cases, SDD adds little benefit.
  Sometimes, it even increases the cost of feature development."*
- **His alternative — "Natural Language Development"**, a Lean-Startup loop: identify the riskiest
  assumption, design the simplest experiment, build it, repeat. Worked example: a 3D sculpting tool
  with adaptive mesh built with Claude Code in **about 10 hours with no spec at all**, session logs
  published. *"Coding agents supercharge Agile, because we can literally write the product backlog and
  see it being built in real time."*
- **His one wish is visual, and it rhymes with the Event Modeling camp.** *"Coding agents use text, not
  visuals. Sometimes I want to point to a specific zone … if we need new tools to make coding agents
  more powerful, I think the focus should be on richer visual interactions."*
- He is fair about what SDD buys: *"SDD helps agents stay on task and occasionally spots corner cases
  developers might miss."*

## Limits

- **Small features, two toolkits, one practitioner.** The spec-kit example is someone else's PR; the
  Kiro example is a "referred by" field on Marmelab's own Atomic CRM. No before/after timings, no
  control arm, no figure in the piece that is a measurement.
- **NOT INDEPENDENT for the alternative:** he is CEO of an agency selling development services, and the
  worked counter-example is his own weekend project on his own company's blog. The 10-hour figure is a
  self-report.
- **"80% of your time reading"** and *"SDD is a step in the wrong direction"* are opinion, stated as
  such (*"my personal opinion"*). The closing character sketch of SDD's authors (*"born from the minds
  of CS graduates who know their project management textbooks by heart"*) is rhetoric, not analysis.
- Six images and one video in the original are noted inline in the raw and not reproduced, so the
  file-count claims are described rather than shown.

## Connections / contrast

- **Chronology repair for [[spec-driven-development]]:** the page has carried Zaninotto as
  "**Marmelab**, independently" via Ng, with one relayed sentence. He is a primary, published four
  months before Ng, and his seven failure modes are the substance behind Ng's much shorter treatment.
  The 1,300-lines-to-display-a-date figure should be re-cited to here.
- **Distinct from [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] and worth keeping
  distinct:** Eberhardt's objection is **measured speed** plus the formality of code; Zaninotto's is
  **who SDD is for** plus **non-determinism**. They agree on markdown volume and contradict each other
  nowhere; the brownfield-breakdown finding (*"for large existing codebases, SDD is mostly unusable"*) is
  Zaninotto's alone — Eberhardt makes no claim about codebase size.
- **Against [[martin-dilger]]:** Zaninotto's *Faux Agile* and *Markdown Madness* are almost word-for-word
  Dilger's own complaints about SDD toolkits
  ([[dilger-spec-driven-tools-need-event-modeling-front-half]],
  [[dilger-markdown-is-a-suggestion-dressed-as-a-spec]],
  [[dilger-communicating-intent-to-an-agent-needs-a-dsl]]) — but the two draw opposite conclusions.
  Dilger says the artifact needs a **better language**; Zaninotto says the artifact needs to be
  **smaller or absent**. His *Diminishing Returns* and *Context Blindness* findings also cut against
  Dilger's slice-sized loop only insofar as they are about document-first toolkits; the KB has no
  brownfield evidence either way for a model-first pipeline.
- **His "richer visual interactions" wish** is the [[event-modeling]] camp's whole premise arrived at
  from the anti-spec side, and it converges with
  [[dilger-agentic-collaboration-freeform-drawings]] and the screen/mockup thread
  ([[dilger-ux-as-first-class-in-spec-driven-development]],
  [[dilger-highlighting-markers-give-context-to-agents]]). Neither cites the other.
- **With [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]]:** both invoke
  waterfall/BDUF, but Tornhill explicitly declines the waterfall argument (*"Not due to waterfall
  thinking"*) in favour of requirements explosion. Do not merge the two into one "it's waterfall"
  voice.
- Sceptic cluster: [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] ·
  [[bockeler-understanding-sdd-kiro-speckit-tessl]] ·
  [[eberhardt-putting-spec-kit-through-its-paces]] ·
  [[ng-spec-driven-development-is-waterfall-in-markdown]].

_Related: [[francois-zaninotto]] · [[marmelab]] · [[spec-driven-development]] · [[agentic-coding]] ·
[[vibe-modeling]] · [[loop-engineering]]._
