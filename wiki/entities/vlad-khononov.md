---
title: Vlad Khononov
type: entity
created: 2026-06-17
updated: 2026-07-31
sources: [khononov-golden-age-of-modularity, coupling-research-note, khononov-modularity-claude-code-plugin, khononov-microservices-hype-to-ai-sloop]
tags: [person, domain-driven-design, coupling, business-capabilities, modularity, substrate, skeptic]
---

# Vlad Khononov

Software-design author and speaker. First name properly **Vladik** (also written Vladimir/Vlad — and
note the [[coupling-research-note]] flags "konokhov" as a prior misspelling to avoid). Author of
O'Reilly's **"Learning Domain-Driven Design"** (2021) and Addison-Wesley's **"Balancing Coupling in
Software Design"** (2024, ISBN 9780137353538), and creator of the **[[balanced-coupling|Balanced
Coupling]]** model — assessing coupling along three dimensions (**strength × distance × volatility**) so
teams can reason about *which* couplings actually hurt rather than chasing "low coupling" everywhere.
Blogs at **"Rants on Software Design"** (vladikk.com), maintains a companion site **[coupling.dev]
(https://coupling.dev)**, ships a **Claude Code plugin** "Modularity Skills"
([[khononov-modularity-claude-code-plugin]], github.com/vladikk/modularity) that operationalizes
Balanced Coupling as two agent skills, and runs O'Reilly *Software Architecture Superstream* sessions
(e.g. "Optimizing AI Architecture Capabilities").

The 2024 book is the substantive primary behind Balanced Coupling: it defines a four-level **Integration
Strength** scale (intrusive → functional → model → contract), the methods→…→systems **Distance** scale,
subdomain-based **Volatility** (explicitly *not* commit history), and a numeric balance formula
`BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY` (Ch. 10). The [[coupling-research-note]] judges his
model the **direct fit** for software-boundary placement and the basis for dependency-edge weighting in
the user-needs-map product.

## Position — boundaries are the thing AI depends on

His 2026 angle relevant to this KB: **modularity and good boundaries are what make a codebase
tractable for AI agents**, not just for humans. In [[khononov-golden-age-of-modularity|"The Golden Age
of Modularity"]] he defines modular design by two tests — *localized change* (few components touched,
ideally one) and *predictable effect* — and argues the AI/"vibe coding" wave only pays off on modular
code. On LinkedIn he posts on **context engineering for coding agents** and the broader AI-economy
("proprietary knowledge as a company's most valuable asset"), though that feed is largely event
promotion and reshares — the substance is in the blog and books.

## The skeptic voice on the loop hype

He is also the KB's **only contrarian on the [[loop-engineering]] thread**. In
[[khononov-microservices-hype-to-ai-sloop|"Remember the microservices hype 12 years ago?"]] (2026-06-30)
he frames the **AI "(s)loop"** — *loop* spelled with a nod to *slop* — as the new Holy Grail that rhymes
with the microservices hype: "a crowd chasing something most of them can't quite define," where the
metric shifted from "thousands of services" to "thousands of deploys per day," and asks what we'll reach
for "to cope with the hangover this time" (as microservices reached for the modular monolith and the
monorepo). It's the hype-cycle face of his standing thesis — the loop wave pays off only on the same
modular substrate — and the skeptics' counterweight the otherwise advocate-heavy [[loop-engineering]]
page now carries.

## In the KB

Khononov supplies the **design-theory spine** under the coupling/cohesion axis of
[[business-capabilities]], complementing the seminal [[ulrich-homann|Homann]] capability primary. His
modularity tests are [[agent-legibility]] / [[locality-of-reference]] stated from first principles, and
they converge with the practitioner voices on the agentic-coding thread —
[[adam-tornhill|Tornhill's]] [[tornhill-clear-design-principles-agentic-age|CLEAR]],
[[rico-fritzsche|Fritzsche]], [[jeremy-miller|Miller]], and [[martin-dilger|Dilger's]] "coupling, not
context-window." Watched in `watch-config.json` (blog + LinkedIn). His taxonomy sits at the modern end of
the [[coupling-taxonomy]] landscape, descending from [[larry-constantine]]'s 1974 levels.

_Source pages: [[khononov-golden-age-of-modularity]] · [[coupling-research-note]] · [[khononov-modularity-claude-code-plugin]] · [[khononov-microservices-hype-to-ai-sloop]]._
