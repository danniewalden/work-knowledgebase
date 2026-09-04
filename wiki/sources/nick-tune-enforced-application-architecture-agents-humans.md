---
title: "Nick Tune — Enforced Application Architecture for Agents and Humans"
type: source
created: 2026-09-02
updated: 2026-09-02
sources: [nick-tune-enforced-application-architecture-agents-humans]
raw_file: [raw/articles/nick-tune-enforced-application-architecture-agents-humans.md]
tags: [software-architecture, fitness-functions, agentic-coding, vertical-slice-architecture, domain-driven-design, ddd, focus]
---

# Nick Tune — Enforced Application Architecture for Agents and Humans

Blog post by **[[nick-tune]]** at nick-tune.me, **2026-08-13**, subtitled *"Enforcing application
architecture instead of relying on markdown files."* Raw capture:
`raw/articles/nick-tune-enforced-application-architecture-agents-humans.md`. A follow-up to an earlier
post on "a deterministic solution I had been working on"; this one is a self-described brain-dump
snapshot of a richer mental model. TypeScript/NX monorepos, using his own DSL (**Rivière**).

## The premise it starts from

The post does not argue that written architectural guidance is insufficient — it **assumes** it, in the
first sentence:

> "One of the most frustrating parts of AI-generated code is that it does not follow architectural
> guidelines that are written in skill files, ADRs, and various other places in the repo."

And later, more bluntly: *"AI does dumb stuff like that all the time even with a million lines of
markdown screaming at it not to do that."* The response is not better prose. It is to make the wrong
thing **fail the build**.

## The enforcement tiers

His summary of the key things, in his own ordering:

1. **Classify packages** — different package types need different rules (domain model vs CLI app).
2. **Prefer broad, generic rules at the layer level** (folder A cannot import from folder B).
3. **Use fine-grained role-based rules as a last resort.**
4. **Enforce domain boundaries.**

**Package classification.** A package matching `packages/{subdomain}/domain-model` must have — and can
only have — one root folder, `/domain`, which cannot import from other subdomains' domain models or
use-cases packages. Inside `/domain`, any sub-folder is allowed: *"domain models should express the
business however necessary."* The one permitted outward dependency is a **published language** — pure,
usually versioned contracts (in his project a JSON Schema exposed as a TypeScript library). His verdict
on this tier: *"If you're only going to add one convention in your codebase, enforcing domain isolation
is probably the best one."*

**Layer rules, and the deliberate asymmetry.** The `use-cases` package is treated in the opposite
spirit from the domain model: *"Contrary to the domain model, I do want things to be highly standardised
and boring. All the plumbing and orchestration should be similar for each use case."* All feature code
lives in `/features/{feature}` — he glosses this parenthetically as **"(i.e. vertical slices)"** — with
no sharing between feature folders (`importRules: { allow: {} }`), and each feature folder must provide
its own `/commands`, `/queries`, `/data-access` and `/adapters`. Packages must live inside a subdomain,
so a `use-cases` command can import `domain` only from `ownSubdomain`, and a misplaced domain-model
package fails the build outright.

**Role rules, for what layers cannot express.** Code is annotated (`/** @riviere-role value-object */`)
and rules filter on layer *plus* role. An `/adapters` folder may import from `/domain` — but only
things typed `domain-port`, nothing else, so domain logic cannot accumulate there. `/data-access` may
import `aggregate` and `value-object` but **never** `domain-service`, "because that type of coupling
should never happen." He anticipates the obvious gaming — *"You might think that AI will just put all
the logic in a domain-port but that role is highly constrained so it can't."*

**Role constraints, the tightest tier.** A role's *shape* can be constrained: his `value-object` requires
a private constructor, a branded private member, `parse`-prefixed static methods and data members, and
forbids callable data members, `Error` supertypes, and dependencies on `aggregate` or `domain-service`.
The stated trade is explicit — *"Even if that means some code is not as elegant as I would like,
consistency makes things easier to navigate and, more importantly, enforce. So I optimise for that."*
The mechanism is structural rather than admonitory: *"AI cannot implement an aggregate inside
value-object because an aggregate-repository must return an aggregate. So it wouldn't be able to load
it."*

## What he is honest about

He does not claim the whole stack pays off. Package, domain and layer rules he would not skip —
*"If you can't set codebase standards at that level, I don't think you'll get far with agentic AI."*
Annotating every file with a role and writing role-level rules is unresolved: *"Yeah, still playing
around with that. Come back in 6 months. I feel confident it's the right approach."* Read the third
sentence with the second: his uncertainty is about the **payoff**, not the direction. He also notes the maintenance loop this creates — every time
the agent finds a new way to write bad code, he can add a constraint — and immediately qualifies it:
*"that is not always as easy as I'm making out, and requires trading off optimal code vs consistent
boring code."*

A closing observation that is not about enforcement at all: with the role vocabulary in place, feature
planning can discuss **which new roles are needed and where solution parts will live**, which he says
gets to the right outcome faster — *"Not big up-front design, but getting the rough shape right and
identifying tricky decisions early."*

## Interested-party note

**Rivière is Tune's own tool**, the post is the second in a series developing it, and it ends *"If you
want help adding this to your codebase, get in touch."* Per this wiki's vendor-claim convention, the
effectiveness claims here are **author self-report about his own tool** and travel with that marker.
Note also what is *absent*: no before/after measurement, no token or defect numbers, no comparison
against a markdown-guidance baseline. The mechanism is plausible and precisely described; the payoff is
asserted.

## In the KB

- **A third position in [[model-as-code-vs-model-as-language]].** Neither camp holds this ground: the
  authoritative artifact is not a model file and not the code's content but the **build constraint** the
  code must satisfy. Markdown's failure is his premise rather than his thesis.
- **[[fitness-functions]] at a finer grain than the KB had.** [[birgitta-bockeler]]'s field report
  ([[fowler-bockeler-maintainability-sensors]]) cautions that such rules "can only express what imports,
  file names, and folder structure allow" and that deeper coupling judgment needs inferential review.
  Tune's role and role-constraint tiers are a direct attempt to push the computational sensor past that
  line — the same objection, answered with more machinery.
- **[[vertical-slice-architecture]] made mandatory.** `/features/{feature}` with zero cross-feature
  imports is VSA as an enforced invariant rather than a convention, and it supplies a mechanism for the
  blast-radius-stops-at-the-slice-boundary claim that page already makes. (That phrasing is the wiki's,
  not Tune's — he never discusses blast radius here.)
- **An [[adr]] kept aligned by hand.** *"ADR-002 describes the same architecture for humans. The ADR and
  executable Rivière configuration are kept aligned."* This is MADR's optional **Confirmation** section
  actually wired up — and the alignment is manual, which is a maintenance cost the post does not cost out.
- **[[business-capabilities]] at the code boundary.** Subdomain isolation enforced at build time is a
  capability boundary with teeth; contrast [[rachel-laycock]]'s org-level rung and
  [[autonomous-domain-capabilities]]'s runtime one.

## Links

Entities: [[nick-tune]] · [[birgitta-bockeler]]. Concepts: [[fitness-functions]] ·
[[model-as-code-vs-model-as-language]] · [[vertical-slice-architecture]] · [[slice]] · [[adr]] ·
[[business-capabilities]] · [[domain-driven-design]] · [[agentic-coding]] · [[harness-engineering]] ·
[[balanced-coupling]]. Related: [[nick-tune-graphs-memory-skills-agents]] ·
[[fowler-bockeler-maintainability-sensors]] · [[miller-jasperfx-critterstack-ai-event-modeling-strategy]] ·
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec]].
