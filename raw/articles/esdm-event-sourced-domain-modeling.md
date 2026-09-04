---
source_url: https://www.esdm.io/
title: "ESDM — Event-Sourced Domain Modeling (documentation: Home, What is ESDM, Design Principles, Use Cases)"
author: the native web GmbH (thenativeweb)
publication: esdm.io (official ESDM documentation)
published: 2026 (undated docs; retrieved version)
retrieved: 2026-07-18
type: article
---

# Event-Sourced Domain Modeling (Home)

Welcome to the official documentation for **ESDM** – the Event-Sourced Domain Modeling language.

**ESDM** describes event-sourced domains as YAML and ships with the tools to manage them. The language captures the building blocks of **Domain-Driven Design**, **CQRS**, and **Event Sourcing** – Aggregates, Events, Commands, Process Managers, Read Models, Context Mappings, and the rest – along with the artifacts that surround modeling work, such as **Domain Storytelling** discoveries and **Given-When-Then** specifications.

Whether you model by hand, build tools that consume domain models, lean on AI to model or to analyze code, or simply want a written record of an event-sourced system you already built, this documentation is the starting point.

ESDM ships as pre-built binaries for **macOS**, **Linux**, and **Windows**.

## Pick your path

Different visitors want different things.

- **Modeling for the first time** — You're learning Domain-Driven Design or Event Sourcing, or you want to capture a model from scratch. (Getting Started; Modeling Guides.)
- **Modeling with AI** — You want an LLM to help you draft a model, or to extract one from existing code. ESDM's YAML is plain enough that LLMs can read and write it directly, and the Concepts pages give the model exactly the vocabulary it needs. (Your First Model with AI; Concepts; Recipes.)
- **Documenting an existing system** — You already have an event-sourced system and want to capture it as a model. (Concepts; Reference.)
- **Building tools that consume ESDM** — You're building tooling – validators, generators, transformers, IDE plugins – that interoperates with ESDM. The schema reference is the contract you build against. (Reference: Core Schema; Extensions.)
- **Already know ESDM, just need a lookup** — CLI Reference; Core Schema Reference; Extensions.

## Licensing

ESDM is **open source** under the **MIT license**.

## Need Support?

If you or your team need help designing, integrating, or scaling an event-sourced system, we're happy to assist. Just reach out to hello@thenativeweb.io.

Repository: thenativeweb/esdm (GitHub). Legal: the native web GmbH.

Core Schema kinds (from navigation): actor, aggregate, bounded-context, command, context-mapping, domain, domain-service, dynamic-consistency-boundary, entity, event, event-handler, external-system, policy, process-manager, query, read-model, subdomain, value-object.

Extensions: Domain Storytelling (Actor, Work Object, Sentence, Group; domain-story reference) and Given-When-Then (Feature, Scenario).

CLI commands referenced: `esdm lint`, `esdm view`, `esdm glossary`.

---

# What is ESDM

ESDM is the Event-Sourced Domain Modeling language. It describes event-sourced domains – Domains, Bounded Contexts, Aggregates, Events, Commands, Process Managers, Read Models, and the relationships between them – as a set of YAML files.

ESDM is a YAML language plus a built-in toolchain. The schema defines what an ESDM document may contain. The toolchain reads, validates, and renders those documents. Today the binary ships with a linter that catches structural and modeling errors, a command that renders a hierarchical summary of a model, and helpers that materialize the schemas locally for editor support. More tools may follow.

## Why a Standard Format

Event Sourcing and Domain-Driven Design come with a lot of vocabulary – Aggregates, Bounded Contexts, Process Managers, Dynamic Consistency Boundaries, Read Models, Context Mappings. In practice, the language is shared, but the artifacts are not. Teams capture their models in slide decks, whiteboard photos, README.md files, or scattered code comments, and the model drifts the moment it leaves the room.

ESDM gives the model a first-class home. The model is files, the files live next to the code, the files are reviewed in pull requests, and a shared format means every tool – yours, ours, third-party – speaks the same language about your domain.

The standardization is the point. When the format is fixed, you can build tooling against it: linters, validators, generators, transformers, IDE integrations, AI-assisted modelers. ESDM provides the schema and a starting toolchain; the format is open enough that more tools, internal or external, can grow around it.

## Extensions

Beyond the core vocabulary, ESDM ships extension schemas for artifacts that surround the modeling work. Domain Storytelling captures discovery stories – Actors, Work Objects, and the activities that connect them – as their own kind of document. Given-When-Then captures behavioral specifications – preceding Events, a triggering action, expected outcomes – on top of the core kinds.

Each extension follows the same format conventions as the core and is validated by the same toolchain. Extensions never inject kinds into the core, and core documents never validate against an extension – the asymmetry keeps the core lean while letting the surface grow.

## What ESDM Is Not

ESDM is not an event store, not a runtime, not a code generator, not a framework. It does not execute your domain. It does not know about your database, your message bus, or your deployment pipeline. It is a static, descriptive layer that lives alongside your code and helps you keep the model honest.

That separation is deliberate. A modeling language that tries to also be a framework forces you into specific runtime choices, and a runtime that tries to also be a modeling language buries the model under implementation detail. ESDM keeps the two apart so you can mix it freely with whatever you actually run in production.

---

# Design Principles

ESDM is shaped by a small number of decisions that we made deliberately and that we expect to keep, even as the language grows.

## The Model Is Files, Not a Service

ESDM models live as .esdm.yaml files in your repository. There is no central server, no registry, no online lookup. When you run the linter, it reads your files, parses them against an embedded schema, and reports findings. That is the entire pipeline.

This keeps ESDM completely offline. It works in air-gapped environments, in CI runners without outbound network access, and on the train. It also makes the tool trivial to reason about – nothing happens that you cannot reproduce from the source.

## The Schema Is the Contract

Every ESDM document declares an apiVersion, and that version pins the document to a specific schema. The schema is embedded in the binary – the very same schema every tool in the toolchain validates against. There is no version negotiation, no schema migration, no surprise.

When the schema changes in a non-breaking way, the schema revision goes up but the apiVersion stays the same. When a breaking change ever happens, the apiVersion moves to a new major, and old documents continue to validate against the old schema. This is the same versioning discipline you find in Kubernetes API groups, and it has the same property: stability is the default, change is opt-in.

## Extensions Sit Alongside the Core, Not Inside It

Beyond the core vocabulary, ESDM defines extensions – independent schemas that describe artifacts the core leaves out. The Given-When-Then extension models behavioral scenarios. The Domain Storytelling extension captures discovery stories.

Crucially, extensions do not inject kinds into the core. A core document validates against the core schema and only the core schema; an extension document validates against its own. That asymmetry is what lets us add new extensions over time without ever touching the core.

## Rules Are Fixed, Not Configurable

ESDM has a single, fixed catalog of linter rules. You cannot disable them, you cannot change their severity, and there is no project-level configuration file that overrides any of this. A rule either applies or it doesn't, and that decision is made by us, not by a YAML file in your repository.

This is opinionated by design. A linter that ships with knobs ends up describing a hundred different dialects of the same language, and the value of a shared model collapses with it. We pick the rules carefully, we remove rules that turn out to be wrong, and we trust the result.

The trade-off is that some rules will occasionally feel too strict for a specific situation. When that happens, the right move is usually to revisit the model – the rule is almost always pointing at something real.

## Diagnostics Are Locations, Not Stack Traces

Every diagnostic ESDM emits points at a file, a line, and a column. There are no stack traces, no internal error frames, no error codes that require a lookup table. The message reads as a sentence, the location is a place you can navigate to, and the fix is in your editor.

The principle is that the toolchain reports problems in the user's vocabulary, not in its own.

---

# Use Cases

ESDM was built for teams who are serious about Event Sourcing and Domain-Driven Design and want their model to stay coherent as the system grows.

## Capturing a Model During Discovery

When a team runs Event Storming, Domain Storytelling, or any similar discovery format, the artifacts at the end of the day are usually photos and sticky notes. ESDM gives you a place to put those discoveries that survives the workshop.

You can write the Events you discovered, the Commands that produce them, the Actors that issue those Commands, and the Bounded Contexts that hold them, and you get immediate feedback on whether the model is internally consistent. An Aggregate that owns no Events, a Command that nobody issues, or a Process Manager without a starting condition – ESDM flags those before they harden into assumptions.

For Domain Storytelling specifically, ESDM ships an extension that captures stories as their own kind of document and validates them under the same toolchain.

## Documenting an Existing System

You already have code. The model exists, but only in the heads of the people who built it, in scattered comments, and in the names of types and methods. Writing the model down – in ESDM YAML, on disk, next to the code – turns that implicit knowledge into a first-class artifact the rest of the team can read.

Start with the consistency units: every Aggregate, Dynamic Consistency Boundary (DCB), Process Manager, and Read Model the system has. List the Events each one publishes, the Commands each one accepts. The exercise alone surfaces gaps: an Event nobody listens to, a Command without an Actor, a Read Model fed by no projection. Once written, the model can grow with the code instead of trailing behind it.

## Keeping the Model and the Code in Sync

The most common failure mode for a domain model is not that the model is wrong, but that the model and the code drift apart. The team makes a refactoring decision in a sprint, the diagram on the wiki stays untouched, and six months later nobody trusts either source.

When the model lives in version-controlled YAML next to the code, drift becomes visible. A pull request that renames an Aggregate has to update the model in the same change set, or the linter fails the check. A new Event has to declare its publisher and its consumers, or the linter fails the check. The pressure of code review keeps the model honest.

This is the use case that benefits most from running the linter in CI. The check is fast, the failures are precise, and the cost of fixing a drift inline is much smaller than the cost of recovering a wrong model later.

## Communicating with Stakeholders

A model expressed as YAML is also a model expressed in domain language. The names of Aggregates, Events, and Commands are the same names the domain experts use. When you sit down with a product owner or a subject-matter expert, the model is a document you can read together, paragraph by paragraph.

The view command renders an ESDM model as a hierarchical summary – Domain, Subdomains, Bounded Contexts, Consistency Units, the Events and Commands they own. It is the closest thing to a model overview that you can produce on demand and trust to match the source. For more depth, the Given-When-Then extension lets you capture concrete behavioral scenarios alongside the model, in the format domain experts already recognize from BDD.

## Governing a Multi-Team System

In a single-team system, the rules of Event Sourcing tend to be implicit – everyone knows them, and they don't need to be written down. In a system with multiple teams and shared Bounded Contexts, what one team assumes about another's Events becomes load-bearing, and assumptions diverge fast.

ESDM makes those contracts explicit. A Context Mapping declares the relationship between two Bounded Contexts. A cross-context Event reference is a fact, not a guess. When two teams agree on a contract and write it down in the model, the toolchain holds them to it.

## Modeling with AI Assistance

Large language models can help with both ends of modeling work: drafting a fresh model from a domain conversation, and extracting an implicit model out of an existing code base. ESDM's YAML is plain enough that LLMs read and write it directly, and the fixed schema plus named vocabulary give them precisely the constraints they need to produce something coherent.

Point an LLM at the Concepts chapter and it has the full ESDM vocabulary in its context. Feed it source code, and it can extract candidate Aggregates, Events, and Commands. Feed it a transcript of a domain expert interview, and it can sketch the first draft of a model. The output is editable YAML that you check into version control and refine like any other model.

## Building Tools on Top of ESDM

ESDM is a format, and a format is something tools can be built against. Validators, generators, transformers, IDE plugins, dashboards, AI assistants, code generators that target a specific runtime – all of them can read and write ESDM YAML, and all of them speak the same vocabulary about your domain because the schema is fixed.

If you build CQRS, Event Sourcing, or DDD tooling, ESDM gives you an interoperable substrate to build on. Your tool emits ESDM, another tool consumes it, a third tool transforms it. The format is the contract; the toolchain is open.
