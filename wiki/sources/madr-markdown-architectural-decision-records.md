---
title: "MADR — Markdown Architectural Decision Records"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [madr-markdown-architectural-decision-records]
raw_file: [raw/articles/madr-markdown-architectural-decision-records.md]
tags: [documentation, decision-records, architecture, madr, specifications]
---

# MADR — Markdown Architectural Decision Records

The canonical MADR site (adr.github.io/madr), captured 2026-08-31 at **MADR 4.0.0**. Raw capture:
`raw/articles/madr-markdown-architectural-decision-records.md`. Dual-licensed MIT or CC0. Backed by a
2018 peer-reviewed paper (Kopp, Armbruster & Zimmermann, *Markdown Architectural Decision Records:
Format and Tool Support*, ZEUS 2018) — one of the few genuinely peer-reviewed sources in this KB.

Captured to ground the `[[adr]]` wikilink, which had dangled from [[decision-trace]] since the 08-30
lint. See [[adr]] for the compiled concept.

## What it specifies

One decision per markdown file, `NNNN-title-with-dashes.md`, in `docs/decisions/`, version-controlled
alongside the code. The 4.0 template:

- **Mandatory:** Context and Problem Statement → Considered Options → Decision Outcome
  ("Chosen option: X, because …").
- **Optional:** Decision Drivers · Consequences (good/bad merged into one list in 3.0) ·
  **Confirmation** ("how the implementation of/compliance with the ADR can/will be confirmed… a
  design/code review or a test with a library such as ArchUnit") · Pros and Cons of the Options
  (good/**neutral**/bad) · More Information.
- **YAML frontmatter:** `status` (proposed | rejected | accepted | deprecated | superseded by ADR-NNNN),
  `date`, `decision-makers`, `consulted`, `informed` — the last three being RACI roles, added by the project's own **ADR-0015**, "Include
  'Consulted' and 'Informed' of RACI".
- Four variants ship: full, minimal, bare, bare-minimal.

## The two things worth carrying into the wiki

**1. The scope question is dodged on purpose.** *"Do not take the term 'architecture' too seriously or
interpret it too strongly… Since we believe that any (important) decision should be captured in a
structured way, we offer the MADR template to capture any decision."* The naming history is the artifact
of that ambivalence: renamed to "Markdown **Any** Decision Records" in 3.0.0-beta (2022), renamed back to
"**Architectural**" in 4.0.0-beta (2024) — "to strengthen the importance for decisions in software
architecture work… They can still be used to sustain any decision, our focus is on architectural
decisions." The acronym never changed.

**2. "Confirmation" is an acceptance criterion in all but name.** The template asks how compliance will
be *checked*, and notes that "although we classify this element as optional, it is included in many
ADRs." That is [[given-when-then]]'s move applied to a design decision rather than a behaviour — and the
fact that it is optional here and mandatory on a [[slice]] is a real difference between the two
traditions, worth stating rather than eliding.

## Caveats

- **A format specification, not evidence.** Nothing here reports whether ADRs get read, stay current, or
  change outcomes. The only worked examples are the MADR project's own ADRs about MADR.
- Living site, continuously edited; captured at one moment. The "full template" shown is the
  *development* version, which may differ from the 4.0.0 release.
- Tooling is thin by the authors' own admission — "There is currently no tooling supporting MADR 3.0.0"
  still appears under the automatic-approach heading.

## Related

[[adr]] · [[decision-trace]] · [[given-when-then]] · [[spec-driven-development]] ·
[[context-engineering]] · [[comprehension-debt]]
