---
title: "ESDM — Event-Sourced Domain Modeling (thenativeweb)"
type: source
created: 2026-07-18
updated: 2026-07-18
sources: [esdm-event-sourced-domain-modeling]
raw_file: [raw/articles/esdm-event-sourced-domain-modeling.md]
tags: [event-sourcing, domain-driven-design, cqrs, dynamic-consistency-boundaries, given-when-then, domain-storytelling, spec-driven-development, agentic-ai, tool, focus]
---

# ESDM — Event-Sourced Domain Modeling (thenativeweb)

Official documentation for **ESDM**, the *Event-Sourced Domain Modeling* language, published by
**[[thenativeweb]]** (Golo Roden's company — see [[golo-roden]]). Captured 2026-07-18 from the
Home, "What is ESDM", "Design Principles", and "Use Cases" pages (client-rendered mkdocs-material;
pulled via logged-in Chrome). Source file: `raw/articles/esdm-event-sourced-domain-modeling.md`.
On the [[event-modeled-agent-design]] / [[spec-driven-development]] focus.

## What it is

ESDM describes **event-sourced domains as a set of YAML files** (`.esdm.yaml`), plus a built-in
toolchain. It captures the vocabulary of [[domain-driven-design]], [[cqrs]], and [[event-sourcing]]
— Domains, Subdomains, Bounded Contexts, Aggregates, **Dynamic Consistency Boundaries**, Process
Managers, Read Models, Commands, Events, Queries, Entities, Value Objects, Policies, Event Handlers,
Domain Services, Actors, External Systems, Context Mappings — as a fixed **core schema**. A binary
ships for macOS/Linux/Windows; today it provides `esdm lint` (structural + modeling-rule checks),
`esdm view` (a hierarchical summary of the model), and `esdm glossary`/schema helpers for editor
support. **MIT-licensed**, repo `thenativeweb/esdm`.

Deliberately scoped: *"ESDM is **not** an event store, not a runtime, not a code generator, not a
framework."* It is a **static, descriptive layer** that lives next to the code — the model as
version-controlled files, reviewed in pull requests.

## Key points

- **A standard file format is the whole thesis.** DDD/ES vocabulary is shared but the *artifacts*
  aren't — models rot in slide decks, whiteboard photos, READMEs. ESDM gives the model "a first-class
  home": files next to code, so *"every tool – yours, ours, third-party – speaks the same language
  about your domain."* Fixing the format is what lets linters/validators/generators/IDE-integrations/
  **AI-assisted modelers** be built against it. This is the [[dilger-event-modeling-knowledge-hub-emlang|EmLang]]
  ambition, *shipped and specified* — see comparison below.
- **The schema is the contract.** Each document declares an `apiVersion` pinned to an embedded schema;
  non-breaking changes bump a revision, breaking changes bump the major and old docs keep validating —
  explicitly "the same versioning discipline you find in Kubernetes API groups." No server, no
  registry, fully **offline** ("model is files, not a service"). Rhymes with
  [[dudycz-strictland-contract-testing|schema/compatibility contract testing]].
- **Rules are fixed, not configurable.** One catalog of linter rules, no severity knobs, no per-project
  override file — opinionated by design ("a linter that ships with knobs ends up describing a hundred
  dialects"). This is a **deterministic sensor** in the [[feedforward-and-feedback-controls]] /
  [[harness-engineering]] sense, and the anti-configuration stance is a direct cousin of
  [[tornhill-cannot-trust-agent-codescene-mcp|"give the agent a deterministic external sensor, not
  a 'follow SOLID' prompt"]]. Diagnostics are file/line/column "locations, not stack traces," phrased
  in the user's domain vocabulary.
- **Modeling with AI is a first-class use case.** *"ESDM's YAML is plain enough that LLMs read and
  write it directly, and the fixed schema plus named vocabulary give them precisely the constraints
  they need to produce something coherent."* Point an LLM at the Concepts chapter → it has the full
  vocabulary in context; feed it code → it extracts candidate Aggregates/Events/Commands; feed it an
  interview transcript → it drafts a model. Output is editable YAML checked into version control. This
  is the **agent-authors-the-model** direction of [[event-modeled-agent-design]] — but via a
  plain-text file + lint loop rather than an MCP-on-a-board ([[fraktalio-event-modeler-connect-ai-agents-mcp]],
  [[proophboard-skills-ai-agent-event-modeling]]).
- **Model↔code drift is the enemy; CI is the fix.** The headline failure mode is the model and code
  drifting apart; keeping ESDM YAML beside the code makes drift *fail a PR check* (rename an Aggregate
  → update the model or the linter fails). This operationalizes [[dilger-is-code-still-the-source-of-truth|"the
  model is the source of truth"]] and [[dilger-planning-like-excel-legible-to-human-and-ai|structure
  that keeps a spec legible to human and AI]] as an enforceable gate.
- **DCB is a first-class kind.** Dynamic Consistency Boundary sits alongside Aggregate as a
  "consistency unit" in both the schema and the "documenting an existing system" guidance — a vendor
  siding with the [[dynamic-consistency-boundaries]] line (Pellegrini/[[dilger-dcb-is-what-event-sourcing-should-have-been|Dilger]]/[[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb|Fritzsche]])
  rather than aggregate-only.
- **Two extensions map onto hot KB themes.** **[[given-when-then|Given-When-Then]]** (preceding events
  → triggering action → expected outcomes) and **Domain Storytelling** (Actors, Work Objects,
  Sentences, Groups) ship as *separate* schemas validated by the same toolchain. Extensions never
  inject kinds into the core (asymmetry keeps the core lean). GWT-as-machine-readable-artifact is the
  verification-rubric seam of [[event-modeled-agent-design]]; Domain Storytelling ties to
  [[domain-discovery]] / [[event-storming]].
- **Built to be built on.** Explicit "Building Tools on Top of ESDM" use case: an interoperable
  substrate for CQRS/ES/DDD tooling — "your tool emits ESDM, another consumes it, a third transforms
  it. The format is the contract; the toolchain is open."

## Why it matters here

ESDM is the **file-format + linter rung** the [[event-modeled-agent-design]] focus area was missing.
The KB already had the *vision* of a model that is a spec legible to humans and agents
([[dilger-planning-like-excel-legible-to-human-and-ai]], [[dilger-is-code-still-the-source-of-truth]]),
agents that *author* models ([[fraktalio-event-modeler-connect-ai-agents-mcp]],
[[proophboard-skills-ai-agent-event-modeling]]), and a YAML dialect for it
([[dilger-event-modeling-knowledge-hub-emlang|EmLang]]) — but no open, specified, tool-backed format.
ESDM is that: an MIT-licensed schema + linter that turns "model as source of truth" into an
enforceable CI gate and hands an LLM a constrained vocabulary to model within.

It also extends **[[thenativeweb]] / [[golo-roden]]** from an event *store* (EventSourcingDB,
[[roden-event-sourcing-meets-mcp-whole-story-for-llms]]) to a *modeling language* — the same vendor
now spans "store the events" and "describe the domain that produces them," both aimed at making
event-sourced systems legible to LLMs.

## Relationship to EmLang and the visual-tool camp

- **vs [[dilger-event-modeling-knowledge-hub-emlang|EmLang]]:** both are YAML dialects for
  event-sourced systems. EmLang is a format Dilger *adopts as an import* into the visual
  [[eventmodelers-ai]] platform; ESDM is a *specified core schema + offline linter/CLI* with its own
  versioning contract and extensions. ESDM is the more complete "format is the product" bet.
- **vs [[fraktalio-event-modeler-connect-ai-agents-mcp|Fraktalio]] / [[proophboard-skills-ai-agent-event-modeling|prooph board]]:**
  those expose an **MCP endpoint** so an agent authors the model on a hosted board; ESDM keeps the
  model as **local files** and lets any LLM read/write the YAML directly, with a linter as the gate.
  File-first + offline vs board-first + MCP. (Whether ESDM gains an MCP server — as EventSourcingDB
  did — is an open watch item.)
- **vs [[event-modeling]] the method:** ESDM models ES/DDD/CQRS *structure*, not the Dymitruk
  **timeline/swimlane** method — there is no timeline construct in the core schema. It sits closer to
  Roden/EventSourcingDB and the [[event-sourcing]] substrate than to Event Modeling proper.

## Caveats

Vendor-authored documentation ([[thenativeweb]] makes ESDM), so "a standard format is the point" is
motivated — though the format is MIT-open and the argument is tool-neutral. Docs are undated; several
sub-pages (Concepts detail, Recipes, Modeling Guides) render only client-side and were not all
captured. Maturity is early ("today the binary ships with a linter… more tools may follow"); no
adoption or independent review captured yet.

## Touches

[[thenativeweb]] · [[golo-roden]] · [[event-sourcing]] · [[domain-driven-design]] · [[cqrs]] ·
[[dynamic-consistency-boundaries]] · [[given-when-then]] · [[domain-discovery]] · [[event-storming]] ·
[[spec-driven-development]] · [[event-modeled-agent-design]] · [[dilger-event-modeling-knowledge-hub-emlang]] ·
[[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[harness-engineering]] · [[ai-readable-code]] ·
[[roden-event-sourcing-meets-mcp-whole-story-for-llms]]

_Source: `raw/articles/esdm-event-sourced-domain-modeling.md`._
