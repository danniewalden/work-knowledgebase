---
source_url: https://adr.github.io/madr/
title: "About MADR — Markdown Architectural Decision Records"
author: The ADR GitHub Organization (Oliver Kopp et al.)
publication: adr.github.io/madr
published: 2024-09-17 (MADR 4.0.0 release; site continuously updated)
retrieved: 2026-08-31
type: article
---

# Markdown Architectural Decision Records (MADR)

> "Markdown Architectural Decision Records" (MADR) `[ˈmæɾɚ]` – decisions that matter `[ˈmæɾɚ]`.

An Architectural Decision (AD) is a justified software design choice that addresses a functional or non-functional requirement of architectural significance. This decision is documented in an Architectural Decision Record (ADR), which details a single AD and its underlying rationale. To capture these records in a lean way, the Markdown Architectural Decision Records (MADRs) have been invented: MADR is a streamlined template for recording architectural significant decisions in a structured manner.

Scientific publication: [Markdown Architectural Decision Records: Format and Tool Support](https://dblp.org/rec/conf/zeus/KoppAZ18.html) (Kopp, Armbruster, Zimmermann, ZEUS 2018).

## News (selected)

- **2024-09-17: Release of MADR 4.0.0.** "bare" and "minimal" templates added.
- 2024-09-02: MADR 4.0.0-beta. "To strengthen the importance for decisions in software architecture work, MADR spells out 'Markdown Architectural Decision Records'. They can still be used to sustain any decision, our focus is on architectural decisions."
- 2022-10-09: MADR 3.0.0. "The most important change is the merge of sections 'Positive Consequences' and 'Negative Consequences' into 'Consequences' to enable similar grammar as in 'Pros and Cons of the Options'."
- 2022-05-17: MADR 3.0.0-beta. "Besides improvement of the template, there was a renaming from 'Markdown Architectural Decision Records' to 'Markdown Any Decision Records' to follow the movement 'ADR = Any Decision Record? Architecture, Design and Beyond'. The acronym is still MADR."
- 2018-04-03: Scientific publication.

## The MADR project's own decisions (site navigation)

0000 Use Markdown Architectural Decision Records · 0001 Dual License the Work · 0002 Do Not Use Numbers in Headings · 0003 Write Own MADR Tooling · 0004 Write Own TOC Tool · 0005 Use Dashes in Filenames · 0006 Use Names as Identifier · 0007 Do Not Emphasize Line Headings · 0008 Add Status Field · 0009 Support Links To Other ADRs Inside an ADR · 0010 Support Categories · 0011 Use Asterisk as List Marker · 0012 Use Curly Braces to Denote Placeholders · 0013 Use YAML front matter for metadata · 0014 Allow "neutral" arguments · **0015 Include "Consulted" and "Informed" of RACI** · 0016 Outcome before Detailed Pros and Cons · 0017 Use Same Format for Outcomes and Options · 0018 Use "Confirmation" as Heading · ADR Template

## Overview

An Architectural Decision (AD) is a software design choice that addresses a functional or non-functional requirement that is architecturally significant. This might, for instance, be a technology choice (e.g., Java vs. JavaScript), a choice of the IDE (e.g., IntelliJ vs. Eclipse IDE), a choice between a library (e.g., SLF4J vs java.util.logging), or a decision on features (e.g., infinite undo vs. limited undo). Do not take the term "architecture" too seriously or interpret it too strongly. As the examples illustrate, any decisions that might have an impact on the architecture somehow are architectural decisions.

It should be as easy as possible to a) write down the decisions and b) to version the decisions.

There are debates about what is an architecturally-significant decision and which decisions are not architecturally significant. Since we believe that any (important) decision should be captured in a structured way, we offer the MADR template to capture any decision.

## Example

```
# Use Plain JUnit5 for advanced test assertions

## Context and Problem Statement

How to write readable test assertions?
How to write readable test assertions for advanced tests?

## Considered Options

* Plain JUnit5
* Hamcrest
* AssertJ

## Decision Outcome

Chosen option: "Plain JUnit5", because it is a standard framework and the features of the other frameworks do not outweigh the drawbrack of adding a new dependency.
```

## Applying MADR to your project

Create folder `docs/decisions` in your project. Copy all files in folder `template` from the MADR project to the folder `docs/decisions` in your project.

```
npm install madr && mkdir -p docs/decisions && cp node_modules/madr/template/* docs/decisions/
```

### Create a new ADR (manual approach)

1. Copy `docs/decisions/adr-template.md` to `docs/decisions/NNNN-title-with-dashes.md`, where `NNNN` indicates the next number in sequence.
2. Edit `NNNN-title-with-dashes.md`.

The filenames follow the pattern `NNNN-title-with-dashes.md` (ADR-0005), where `NNNN` is a consecutive number ("we assume that there won't be more than 9,999 ADRs in one repository"), the title is stored using dashes and lowercase, and the suffix is `.md`. "Decisions are placed in the subfolder `decisions/` to keep them close to the documentation but also separate the decisions from other documentation."

#### Automatic approach

There is currently no tooling supporting MADR 3.0.0.

### Lint ADRs

"ADRs are written using Markdown. Since Markdown allows many styles, formatting can be inconsistent. To notify about inconsistencies, markdownlint has been invented. There is an initial configuration for it at `template/.markdownlint`."

## Using MADR in large projects

"Large projects may accumulate hundreds of decision records over time, and finding them might be hard. MADR does not enforce any repository or directory organization structure."

Categories via subdirectories:

```tree
.
`-- decisions
    |-- backend
    |   |-- 0001-use-quarkus.md
    `-- ui
        `-- 0001-use-vuejs.md
```

"This approach makes all categories explicit because the subdirectory/folder names define the categories. As a consequence, numbers of ADRs are no longer unique throughout the repository, but locally within a category only. Ideally, the ADR categorization [uses] the same organizing principles as other artifacts such as the code… This comes down to a meta-decision to be made rather early on."

## Full template (development version)

```
---
# These are optional elements. Feel free to remove any of them.
# status: "{proposed | rejected | accepted | deprecated | … | superseded by ADR-0123"
# date: {YYYY-MM-DD when the decision was last updated}
# decision-makers: {list everyone involved in the decision}
# consulted: {list everyone whose opinions are sought (typically subject-matter experts); and with whom there is a two-way communication}
# informed: {list everyone who is kept up-to-date on progress; and with whom there is a one-way communication}
---
# {short title, representative of solved problem and found solution}

## Context and Problem Statement

{Describe the context and problem statement, e.g., in free form using two to three sentences or in the form of an illustrative story. You may want to articulate the problem in form of a question and add links to collaboration boards or issue management systems.}

<!-- This is an optional element. Feel free to remove. -->
## Decision Drivers

* {decision driver 1, e.g., a force, facing concern, …}
* {decision driver 2, e.g., a force, facing concern, …}

## Considered Options

* {title of option 1}
* {title of option 2}
* {title of option 3}

## Decision Outcome

Chosen option: "{title of option 1}", because {justification. e.g., only option, which meets k.o. criterion decision driver | which resolves force {force} | … | comes out best (see below)}.

<!-- This is an optional element. Feel free to remove. -->
### Consequences

* Good, because {positive consequence, e.g., improvement of one or more desired qualities, …}
* Bad, because {negative consequence, e.g., compromising one or more desired qualities, …}

<!-- This is an optional element. Feel free to remove. -->
### Confirmation

{Describe how the implementation of/compliance with the ADR can/will be confirmed. Is the chosen design and its implementation in line with the decision? E.g., a design/code review or a test with a library such as ArchUnit can help validate this. Note that although we classify this element as optional, it is included in many ADRs.}

<!-- This is an optional element. Feel free to remove. -->
## Pros and Cons of the Options

### {title of option 1}

{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
<!-- use "neutral" if the given argument weights neither for good nor bad -->
* Neutral, because {argument c}
* Bad, because {argument d}

### {title of other option}

{example | description | pointer to more information | …}

* Good, because {argument a}
* Good, because {argument b}
* Neutral, because {argument c}
* Bad, because {argument d}

<!-- This is an optional element. Feel free to remove. -->
## More Information

{You might want to provide additional evidence/confidence for the decision outcome here and/or document the team agreement on the decision and/or define when/how this decision the decision should be realized and if/when it should be re-visited. Links to other decisions and resources might appear here as well.}
```

## Template variants (4.0.0)

`adr-template.md` (all sections + explanations) · `adr-template-minimal.md` (mandatory sections only) · `adr-template-bare.md` (all sections, no explanations) · `adr-template-bare-minimal.md` (mandatory only, no explanations).

## License

Dual-licensed under MIT and CC0: `SPDX-License-Identifier: MIT OR CC0-1.0`.

---

*Capture note (2026-08-31, amended same day — the first pass over-stripped the page and removed two things the wiki then cited, the 'Automatic approach' line and the project's own ADR list; both restored above from the same fetch): captured to ground the `[[adr]]` wikilink, which had been dangling from [[decision-trace]] since the 2026-08-30 lint with no source behind it — the lint's own note said it "was deliberately NOT written rather than fabricated." This is the canonical MADR site (the format Dannie's own ADR tooling targets, at version 4.0). Note the naming history, which matters for the wiki's vocabulary: MADR was renamed "Markdown **Any** Decision Records" in 3.0.0-beta (2022) and renamed **back** to "Architectural" in 4.0.0-beta (2024) — "to strengthen the importance for decisions in software architecture work… They can still be used to sustain any decision, our focus is on architectural decisions." Site nav, edit links and the older-versions table stripped; the full template and example are preserved verbatim in code fences as published. Content is MIT OR CC0.*
