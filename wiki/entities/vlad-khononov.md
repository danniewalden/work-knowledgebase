---
title: Vlad Khononov
type: entity
created: 2026-06-17
updated: 2026-09-04
sources: [khononov-golden-age-of-modularity, coupling-research-note, khononov-modularity-claude-code-plugin, khononov-microservices-hype-to-ai-sloop, khononov-ai-doesnt-fix-your-real-bottleneck, khononov-coupling-should-be-weighed-not-counted, khononov-value-of-90-percent-done-never-lower]
tags: [person, domain-driven-design, coupling, business-capabilities, modularity, comprehension-debt, substrate, skeptic]
---

# Vlad Khononov

Software-design author and speaker. First name properly **Vladik** (also written Vladimir/Vlad — and
note the [[coupling-research-note]] flags "konokhov" as a prior misspelling to avoid). Author of
O'Reilly's **"Learning Domain-Driven Design"** (2021) and Addison-Wesley's **"Balancing Coupling in
Software Design"** (2024, ISBN 9780137353538), and creator of the **[[balanced-coupling|Balanced
Coupling]]** model — assessing coupling along three dimensions (**shared knowledge × distance × volatility** — "strength" is the scale's name and the label the book and this KB have used, but his own first-party statement of the triad names the first axis *shared knowledge*) so
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

## Position — comprehension is the bottleneck (Theory of Constraints, 2026-02)

His strongest formulation, and the one to cite ([[khononov-ai-doesnt-fix-your-real-bottleneck]]): a
system's throughput is set by its bottleneck, so speeding up anything else "doesn't improve the system;
you produce more work-in-progress that piles up in front of the bottleneck." In software the bottleneck
is not typing — "if you have a clear understanding of the business domain and requirements, is it that
hard to codify the domain knowledge? Not really. Writing new code is the easy part." It is **"our
ability to comprehend systems,"** capped by working memory (he cites 4±1 / 7±2 as "studies" with **no
reference given on the page**). Complexity is therefore operational, not aesthetic: not "this is a hard
problem" but **"we don't know what will happen when we touch something."**

So AI accelerates a **non-bottleneck**, and "the Theory of Constraints predicts exactly what happens
next: the system degrades." He extends it to the agents ("the larger the codebase an LLM has to work
with, the faster its context fills up and the less effective it becomes") and reframes the question:
not "how do we write code faster?" but **"how do we keep systems understandable as they grow?"**

The P.S. is a claim the KB did not have from him: "Generating code that *looks* modular and designing a
system that *is* modular are two very different things. Modularity is a system-level property. It requires
understanding the business domain, the organizational structure, and the trade-offs between them.
**That's not a prompting problem.**"

**Markers.** **NOT INDEPENDENT** (the post concludes with his own model and book, via an affiliate link)
and **IMPRESSION NOT MEASUREMENT** (the TOC mapping is analytical; nothing here is measured, and the
working-memory figures are unreferenced). This is the theoretical spine under [[comprehension-debt]] —
see that page. His companion post three days later
([[khononov-coupling-should-be-weighed-not-counted]]) covers **only the Integration Strength axis** and
states those four levels in his own prose; the triad above belongs to this post, not that one. Both are
**out-of-window backfills** (2026-02), not new developments.

## An aphorism on the last mile (2026-08-28)

One line, posted on LinkedIn, and the whole of the post:
*"The value of being 90% done, or even 99% done, has never been lower than in the AI era"*
([[khononov-value-of-90-percent-done-never-lower]]). **86 characters, no argument, no evidence, no
elaboration — a slogan, not a finding**, and it must never be counted as a corroborating voice for
another claim. The plausible last-mile reading (when the first 90% is nearly free, all the value sits in
finishing, hardening and verification) is *the KB's inference, not his words*; for the argued version
cite [[khononov-ai-doesnt-fix-your-real-bottleneck]] instead. Filed as a crisp position on the
[[verification-burden]] strand, and as a **liveness datum**: his own channels have been quiet since
2026-05-01, so LinkedIn is currently where he posts — relevant to `watch-config.json`.

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

_Source pages: [[khononov-golden-age-of-modularity]] · [[coupling-research-note]] ·
[[khononov-modularity-claude-code-plugin]] · [[khononov-microservices-hype-to-ai-sloop]] ·
[[khononov-ai-doesnt-fix-your-real-bottleneck]] (2026-02, the argued version) ·
[[khononov-coupling-should-be-weighed-not-counted]] (2026-02, Integration Strength in his own prose) ·
[[khononov-value-of-90-percent-done-never-lower]] (2026-08-28, an 86-character slogan — **not a
finding**)._
