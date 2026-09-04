---
title: "Fritzsche — Functional Core / Imperative Shell for Agentic Coding"
type: source
created: 2026-06-16
updated: 2026-06-16
sources: [fritzsche-functional-core-imperative-shell-agentic-coding]
raw_file: [raw/articles/fritzsche-functional-core-imperative-shell-agentic-coding.md]
tags: [agentic-coding, vertical-slice-architecture, locality-of-reference, agent-legibility, harness-engineering, business-capabilities, focus]
---

# Fritzsche — Functional Core / Imperative Shell for Agentic Coding

**Source:** Rico Fritzsche, *"Functional Core / Imperative Shell for Agentic Coding — How
Repository Structure, Feature Slices, and Project-Level Skills Guide Coding Agents Toward
Self-Contained Features"*, ricofritzsche.me (also Medium), 2026-04-14.
Raw capture: [[fritzsche-functional-core-imperative-shell-agentic-coding]] (raw/articles/).

## What it argues

The repository teaches the agent its structure **before the prompt does**. If the codebase
exposes services, controllers, repositories, managers, helpers, `common`/`shared` folders, and
generic file names, those are exactly the shapes the agent reproduces — "the problem starts long
before the prompt." So the lever for reliable agent output is not better prompting but a codebase
(plus skill files and review rules) that makes the desired shape the path of least resistance.

The desired shape is a **self-contained [[vertical-slice-architecture|feature slice]]** given an
internal form by **Functional Core / Imperative Shell**:

- **Shell** = entry, loading, and external effects (HTTP, DB, external systems). May load data and
  persist results.
- **Core** = pure, deterministic decision logic. Must not perform IO.
- Naming carries the design: inside `register_client/`, files are `load_registration_context`,
  `decide_registration`, `append_registration` — names that describe *behavior/execution*, not
  technical categories (`service.rs`, `manager.rs`, `repository.rs`, `util.rs`). Generic technical
  names "pull the structure back toward technical categories instead of behavior."

## Three rules that make it stick

1. **Share nothing that carries domain meaning.** A slice may use bootstrapped infrastructure (DB
   pool, HTTP client, logger, config) but its *meaningful behavior* must not live in a shared
   service/model/helper. Treating data as explicit input/output removes the pull toward a central
   mutable object that "carries the current meaning of the system."
2. **Project-level skills define the generation environment.** A `SKILL.md` sits one level *above*
   the feature (e.g. `.codex/skills/feature-slice-rust/`) and encodes the non-negotiables: feature
   isolation, no imports from other features, no `common/shared/utils`, no classes/services/
   managers/repositories, explicit IO boundaries. "The feature is the generated result; the skill
   defines the generation environment."
3. **Cross-feature dependencies are a structural exception, not an optimization.** The default is
   *no* cross-feature dependency. Two features both validating an address does **not** justify a
   shared abstraction — the real test is "do they need to change together for the same reason?"
   The practical test for a slice: *can it be changed, regenerated, or replaced from its own slice
   without pulling domain-specific behavior in from elsewhere?* If no, the dependency has gone too far.

## Why it matters for the KB

This is the **practitioner "how-to" that operationalizes [[locality-of-reference]]**. Where
[[miller-codebase-is-the-prompt-vertical-slices-ai|Miller]] argues *the codebase is part of the
prompt* and Fritzsche's own [[rico-fritzsche-autonomous-domain-capabilities-ccc|CCC/RPU post]]
argues capabilities need a "home," this article gives the concrete repo recipe: FC/IS *inside* the
slice, behavior-describing file names, share-nothing defaults, and skills as the enforcement layer.
It strengthens three existing threads at once:

- **[[vertical-slice-architecture]]** — adds the *internal* shape of a slice (FC/IS) and an explicit
  cross-feature-dependency rule, complementing Bogard's "couple in a slice" and Miller's "small
  slices win."
- **[[agent-legibility]] / [[harness-engineering]]** — skills + review rules + naming are the
  "guides" that keep generated code from drifting back to OOP defaults; an agent's narrow working
  surface makes shared abstractions especially costly.
- **[[business-capabilities]] / [[autonomous-domain-capabilities]]** — "feature slice as boundary of
  ownership"; share-nothing keeps a capability's behavior local.

## Notable verbatim points

- "People talk about prompting, model quality, or tool choice, while the code repository keeps
  teaching the agent the wrong structure."
- "At that point the instruction stops being a feature request and starts becoming a structural
  constraint."
- "A human can jump across the codebase … An agent has a much narrower working surface."
- "This is not only a prompting topic. It is an engineering topic."
- Companion skill templates: `github.com/ricofritzsche/agentic-feature-slice-templates`. Builds on a
  prior article ("Agentic coding reveals what self-contained feature slices actually are").

_Source: [[fritzsche-functional-core-imperative-shell-agentic-coding]]._
