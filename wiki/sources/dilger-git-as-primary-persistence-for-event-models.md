---
title: "Source: Dilger — Git as primary persistence for Event Models (BYODS in EM-Studio)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dilger-git-as-primary-persistence-for-event-models]
raw_file: [raw/notes/dilger-git-as-primary-persistence-for-event-models.md]
tags: [event-modeling, agent-readable-model-artifacts, agent-governance, event-sourcing, focus]
---

# Source: Dilger — Git as primary persistence for Event Models (BYODS in EM-Studio)

LinkedIn post by **[[martin-dilger]]**, **2026-09-02** (~230 words). Raw capture:
`raw/notes/dilger-git-as-primary-persistence-for-event-models.md`, retrieved 2026-09-04 in a logged-in
Chrome session; post date derived from LinkedIn's relative age stamp (accurate to the day).

> **VENDOR SELF-REPORT and a product announcement.** EM-Studio is Dilger's own commercial platform
> ([[eventmodelers-ai]], [[nebulit]]); the post also launches a LinkedIn group, *"Solving the hard parts
> of Spec Driven Development"*. Nothing here is a report of use — the git backend is announced as being
> added (*"Now I'll add Git as a primary persistence as well"*), not demonstrated.

**Short-form, and the only primary the KB has for this mechanism.** No longer article or webinar is
referenced.

## Summary

EM-Studio's storage layer becomes pluggable, with **git as a first-class primary store rather than a
backup extension**. The progression he gives: Supabase/Postgres first (*"technically it's only one
table for the source data (of course it's all event sourced)"*), then SQLite as a lightweight
alternative (*"Both are live and used heavily"*), now **git with no relational database at all** —
*"All data lives in Git."* Shape: **one repository per board**, configurable, **with branching
supported**. The design principle is **"BYODS" — bring your own datastore** (Redis, S3, YAML,
SharePoint all named as possible), and the governance pay-off he names is *"You can store your models
in a Worm-Drive for auditability."*

## Key points

- **Git as primary, not as an export.** The platform already tracked and versioned every change *"but
  only as an extension. Like a backup."* The change is that the model's authoritative home becomes the
  repo — which makes the model a **versioned, diffable, branchable artifact by construction** rather
  than by export.
- **One repo per board, branching supported.** Branching a *specification* is the load-bearing detail:
  it makes speculative or parallel model change a first-class operation, and it is the natural pairing
  for a fleet of agents claiming slices off that board
  ([[dilger-loop-engineering-never-argue-with-agent]]).
- **BYODS as an enterprise-flexibility argument.** *"The system was designed from the start for
  'BYODS'"*; the framing throughout is *"Solving Event Modeling for the Enterprise."*
- **WORM-drive storage for auditability** — write-once-read-many media as the model's substrate. This is
  a **governance** claim, not a modelling one, and it is the first time the KB holds a proposal to make
  the *specification itself* tamper-evident rather than just the event log.
- **The model store is itself event-sourced** — *"of course it's all event sourced"* — so the platform
  applies [[event-sourcing]] to the modelling activity, one level above the domain.

## Limits

- **VENDOR SELF-REPORT · announcement, not experience.** The git backend is stated as being added. There
  is no report of anyone running it, no performance or merge-behaviour detail, and no worked example of
  a model merge or a branch reconciliation — which is precisely where a git-backed *graph* artifact gets
  hard.
- **Unaddressed by the post:** how a two-dimensional board serialises so that diffs and merges are
  meaningful; what happens when two agents (or two humans) branch and diverge on the same slice; and how
  branching interacts with the claim-lock mechanism that keeps parallel agents from colliding.
- **No auditability requirement is cited** — no regulation, standard, auditor or customer is named for
  the WORM claim. Compare [[axoniq-government-ai-explainability-requirements]], where the KB does hold a
  sourced requirements argument.
- "Used heavily" (of Postgres and SQLite) is unquantified.

## Connections / contrast

- **It is the proposed *implementation* for [[adam-dymitruk]]'s "agents need an audit trail, not a
  snapshot"** ([[dilger-podcast-episode-47-agentic-modeling-audit-trails]]) — applied one level up.
  Dymitruk's argument is about the *system's* events; this makes the **model's own history** the
  audit trail: every change to the specification versioned, attributable and, on WORM media,
  tamper-evident. So the audit-trail-vs-snapshot argument now has an answer for the spec layer, a
  separate answer for the domain layer (the event log itself), and an independently built answer for the
  **agent loop** ([[nick-tune-event-sourced-claude-code-workflows]]). Three layers, one instinct.
- **It adds a rung to [[agent-readable-model-artifacts]]' ladder** — or rather completes one. The
  ladder ran freeform whiteboard → raw XML in git → grid coordinates → board-via-MCP → linted file
  format → export-on-demand. Git-as-primary collapses the board/file split the page used to draw: the
  board *is* files, so an agent can read the model with `git` and `grep` and see its history, and
  **model↔code drift becomes a diff between two repos rather than a bespoke check**. Compare
  [[dilger-drawio-model-in-code]], where model-in-git was right but raw XML gave the agent *"no
  framework to follow"* — this is that idea with a schema and a platform behind it, and
  [[esdm-event-sourced-domain-modeling|ESDM]]'s file-first-plus-linter position arrived at from the
  hosted-board side.
- **For [[agent-governance]]:** a versioned, WORM-able specification is a **feedforward** control on the
  spec ([[feedforward-and-feedback-controls]]) — you can prove what the agent was told to build, not
  only what it did. The KB's governance sources have so far only argued for audit trails of agent
  *actions*.
- **The sceptics' angle:** [[eberhardt-putting-spec-kit-through-its-paces|Eberhardt]] argues specs are
  *point-in-time* and rarely revisited once a feature ships, so versioning them is cost without return;
  [[tornhill-blast-from-the-past-sdd-illusion-of-known-scope|Tornhill]] notes the MDA tooling regression
  — no pipelines, no CLIs, no linters, *"imagine coding in a Microsoft Word document."* Git-as-primary is
  a direct answer to Tornhill's tooling objection (the model gets the whole git toolchain) and no answer
  at all to Eberhardt's.
- **[[decision-trace]] contrast:** Ng's proposal keeps multi-perspective input as a *record of
  conversation*; git-versioning keeps a record of the *artifact*. A commit history says what the spec
  became and when, not who agreed to it — so this does not touch Ng's authorship objection.

_Related: [[martin-dilger]] · [[agent-readable-model-artifacts]] · [[event-modeling]] ·
[[agent-governance]] · [[event-sourcing]] · [[decision-trace]] · [[eventmodelers-ai]] ·
[[esdm-event-sourced-domain-modeling]] · [[spec-driven-development]]._
