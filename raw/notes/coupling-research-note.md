---
source_url: local upload
title: "Coupling — research note"
author: Claude (deep research run) for Dannie
publication: Internal research output
published: 2026-06-22
retrieved: 2026-06-22
type: note
---

# Coupling — research note
> Status: research input, not a decision (2026-06-22).
> Owner: TBD when boundary-weighting / coupling-cost-score becomes an active feature.
> Scope: weight semantics for dependency edges on user-needs maps, in service of a future feature that scores or suggests boundary configurations.
## Framing — what "boundary" means here
The user-needs-map PRD describes boundaries as **interpretive** — team, system, domain, make/buy, etc. — but the primary intent for this product is **software-model boundaries**: bounded contexts, system seams, module decomposition. Team boundaries (Conway / Team Topologies) are an adjacent application, not the central one. This narrows which literature applies most directly.
- **Khononov's coupling model fits closest** — it is explicitly about software-boundary placement (bounded contexts, services, modules).
- **Stevens/Myers/Constantine 1974** supplies foundational vocabulary but is module-internal and pre-distributed-systems.
- **Team Topologies** supplies partition-side constraints (cognitive load, ISH) that *can* apply if the editor reads a boundary as "a team" — but it offers no edge weights and isn't the default lens.
## 1. Classical taxonomy — Stevens / Myers / Constantine 1974
The original coupling taxonomy. Constantine developed it in the mid-1960s, first presented at the 1968 National Symposium on Modular Programming, widely cited in Stevens, Myers & Constantine, "Structured Design," *IBM Systems Journal* 13(2), May 1974 (DOI 10.1147/sj.132.0115). Yourdon & Constantine, *Structured Design* (1979), formalizes the definition:
> Coupling is "the measure of the strength of interconnection" between modules — "the more we must know of module B to understand module A, the more closely connected A is to B."
Six levels, **strongest** (worst) to **weakest** (best):
| # | Level | Definition |
|---|---|---|
| 1 | Content | One module modifies/references the internals of another (jumps into private code, alters local data). |
| 2 | Common | Modules share a global data region (shared writable globals). |
| 3 | External | Modules share an externally imposed data format / protocol. |
| 4 | Control | One module passes flags/switches that direct another's flow. |
| 5 | Stamp | Modules share a composite data structure but use only a subset. |
| 6 | Data | Modules share only the elementary data they actually need. |
**Fit for the capability-map.** Vocabulary mismatch — this is intra-program module connection, not capability-graph edges. Useful as historical anchor; not a viable edge-weight scheme.
## 2. Khononov — primary recommendation
Vladik Khononov (correct spelling; the earlier "konokhov" was a misspelling). Author of *Learning Domain-Driven Design* (O'Reilly 2021) and *Balancing Coupling in Software Design* (Addison-Wesley 2024, ISBN 9780137353538). The 2024 book is the most directly applicable framework for this product.
### Three orthogonal dimensions
| Dimension | What it measures | Scale | How obtained |
|---|---|---|---|
| **Integration Strength** | How much knowledge two components share via the integration | Four-level ordinal (see below) | Editor judgment |
| **Distance** | Physical/logical separation between coupled components | methods → objects → packages/namespaces → services/microservices → systems | Observable from deployment topology |
| **Volatility** | Likelihood that a component will need to change | High (Core subdomain) / Low (Supporting, Generic subdomain) | Editor judgment via DDD subdomain classification. Khononov **explicitly warns against** using commit history — accidental volatility from poor design skews commit-based assessment. |
These three combine into a numeric balance, with a chapter (Ch. 10) titled "Balancing Coupling on a Numeric Scale" and a formula: `BALANCE = (STRENGTH XOR DISTANCE) OR NOT VOLATILITY`. The formula is defined for individual coupling sites, not for partition-scoring directly — an open question for any algorithm that scores candidate partitions.
### Integration Strength scale (Chapter 7), strongest → weakest
| Level | Name | Definition |
|---|---|---|
| 4 | **Intrusive** | Integration via private interfaces, internal databases, undocumented APIs. "Both fragile and implicit." Maps to classical content coupling. |
| 3 | **Functional** | Components share functional requirements ("what", not "how"). Canonical example: duplicated business logic that forces co-change. |
| 2 | **Model** | Components share knowledge of a (typically business-domain) model. Explicitly tied to DDD bounded contexts. |
| 1 | **Contract** | Integration via an explicit published contract. Weakest, most desirable form. |
Sources verified (3-0 on every claim):
- [Khononov's modularity GitHub skill](https://github.com/vladikk/modularity/blob/main/skills/balanced-coupling/SKILL.md) (primary)
- [coupling.dev — Integration Strength](https://coupling.dev/posts/dimensions-of-coupling/integration-strength/) (Khononov's site)
- [coupling.dev — Balance](https://coupling.dev/posts/core-concepts/balance/)
- [InformIT publisher TOC for "Balancing Coupling"](https://www.informit.com/store/balancing-coupling-in-software-design-successful-software-9780137353538)
- [Tech Lead Journal podcast episode 188](https://techleadjournal.dev/episodes/188/)
- [InfoQ podcast — Balancing Coupling](https://www.infoq.com/podcasts/balancing-coupling-software-design/)
## 3. Yves Goeleven — unresolved
The deep-research workflow could not verify Goeleven's LinkedIn coupling taxonomy series against primary sources. LinkedIn indexes poorly for non-logged-in fetches; the agent surfaced [his profile](https://www.linkedin.com/in/goeleven/), [one LinkedIn post on data coupling](https://www.linkedin.com/posts/goeleven_how-to-minimize-data-coupling-data-coupling-activity-7320401061008084993-r5MX), and [a blog post on low coupling / high cohesion](https://www.goeleven.com/blog/how-to-achieve-low-coupling-and-high-cohesion/), but could not extract a verified taxonomy. The no-paraphrase-from-memory rule blocks inventing one.
**To resolve:** drop direct URLs to the LinkedIn series in a follow-up and re-run.
## 4. Side-by-side
| Dimension | Stevens/Myers/Constantine 1974 | Khononov 2024 | Team Topologies 2019 | Change-coupling (Tornhill / CodeScene) |
|---|---|---|---|---|
| Scale | 6 levels (content / common / external / control / stamp / data) | 4-level Integration Strength + Distance + Volatility | Categorical interaction modes (Collaboration / X-as-a-Service / Facilitation); no edge scale | Continuous (co-change frequency) |
| Scope | Intra-program modules | Components, services, systems | Teams, streams, the architectures they shape | Files / modules in a VCS |
| Distance? | No | Yes | Implicit (handover chains) | No |
| Volatility? | No | Yes (via DDD subdomain) | No | Implicit (co-change rate) |
| Quantitative? | Qualitative ordinal | Yes — numeric balance formula | No (visual + categorical) | Yes (mineable) |
| How obtained | Static analysis (lower levels) + reading internals (upper) | Editor judgment (Strength, Volatility) + observable (Distance) | Likert survey + checklist (ISH) | VCS-mineable: same commit / same author-window / shared ticket ID |
| Fits the capability-map edge model? | Vocabulary mismatch | **Direct fit** | Constraint-side, not edge-side | Wrong shape (telemetry, not judgment) |
**Adjacent measurement frameworks** (context, not edge-weight candidates):
- **Martin's instability metric.** `I = Ce / (Ca + Ce)` where Ca is afferent (in-) coupling and Ce is efferent (out-) coupling. Per-component direction metric. Useful for diagnosis ("which capabilities are most depended-upon"), not for edge weights.
- **Newman/Louvain modularity / conductance.** Graph-partitioning *objective functions*. They tell you HOW to partition a weighted graph; they don't tell you what the weights should mean. Designed for sparse-but-large graphs; on the 10–15-node graphs typical of a single user-needs map, optimal partitions are often visually obvious and the algorithm's confidence is near the noise floor.
- **Conway's homomorphic force** (Allan Kelly). Team-communication structure and software architecture tend to assume the same shape. Implication: edge weights on a software-boundary graph are *also* (implicitly) a model of team-coordination friction, even when the editor is thinking purely about software seams. The interpretive nature of boundaries follows from this.
## 5. Measurable vs subjective
| Coupling type | How obtained | Fits editor-dial UX in this product? |
|---|---|---|
| Change-coupling (Tornhill/CodeScene) | VCS-mineable (no human judgment) | No — automatable; asking editors to estimate it is a category error |
| Stevens/Yourdon — lower levels (data, stamp, control) | Static analysis (call graphs, parameter types) | Partial — observable from code, not judgment |
| Stevens/Yourdon — upper (common, content) | Reading internals | Subjective, judgment-friendly |
| **Khononov Integration Strength** | Subjective ("does A know B's domain model?") | **Yes** — designed as a thinking tool |
| Khononov Distance | Observable (deployment topology) | Falls out of the partition — not an edge property |
| **Khononov Volatility** | Subjective (DDD subdomain) | **Yes** — Khononov explicitly says not commit history |
| Team Topologies cognitive load | Likert survey (Team Cognitive Load Assessment) | Partition-side, not edge |
| ISH boundary fit | Yes/maybe/no checklist | Partition-side validator |
For an editor-judgment-driven product, the dimensions that fit are the ones Khononov himself defines as subjective.
## 6. Provisional recommendation (contingent — not a decision)
If/when the product adds dependency-edge weighting, expose **two** editor-set dimensions:
1. **Integration Strength** (primary) — Khononov 4-level ordinal (intrusive / functional / model / contract). The dimension Khononov's book argues is the right partitioning signal; subjective by design; the four levels are concrete enough that an editor can answer "do these two capabilities share a domain model, or only a contract?" in seconds.
2. **Volatility-coupling** (secondary) — editor's judgment of "when capability A changes, how likely is it that B must also change?" The human analog of change-coupling. Khononov treats volatility via DDD subdomain rather than git history, which is consistent with the no-telemetry constraint of this product.
Treat as **not** edge weights:
- **Distance** — property of the candidate partition, not the edge. Distance only acquires meaning once a boundary is drawn.
- **Cognitive load / domain complexity** — partition-side *constraints* (Team Topologies' "≤1 complex OR ≤1 complicated domain per team" quota), to apply if/when boundaries are interpreted as teams. Not edge weights.
- **Change-coupling itself** — telemetry-derived; doesn't fit editor-judgment UX.
- **Classical Stevens-Myers-Constantine levels** — module-internal vocabulary; not designed for capability-graph edges.
Two dimensions, not three, is also a UX constraint — three dials per edge is too much cognitive load on the editor weighting a dense graph.
## 7. Open questions specific to this product
Before any of the above becomes a decision, the product owes itself answers to:
1. **Per-map vs global edges.** Current PRD: edges are scoped to a single map. Are weights too? If a capability pair has different weights on different maps, what does "global coupling" mean — sum? max? frequency? Affects whether boundary recommendations are per-map or cross-map.
2. **Numeric mapping.** Integration Strength as 1-2-3-4 linear, or exponential? Knowledge-shared compounds; an exponential mapping may better reflect Khononov's intent. The book's BALANCE formula is ordinal; the algorithm needs a cardinal number.
3. **Folding Distance in.** Khononov's per-site BALANCE formula isn't defined for candidate-partition scoring. Does the algorithm sum per-edge BALANCE, or cluster on Strength-only first and apply Distance / Volatility as post-hoc filters?
4. **Score vs suggester.** A live coupling-cost score (editor draws, score updates) keeps the editor in the structural-thinking loop; an auto-suggester takes them out of it. Which serves the user-needs-map's "see the structural shape" JTBD?
5. **Goeleven gap.** Worth resolving before treating the literature as fully canvassed.
## 8. Caveats from verification
- **Khononov's Distance** has a refuted-claim qualifier — one verifier (vote 1-2) pushed back on a definition that overspecified "encapsulation boundaries" vs "physical/network distance." The verified safe reading is the methods → objects → packages → services → systems scale.
- **Team Topologies group-size cutoffs** (Dunbar-style ~5/~15/~50/~150) were claimed as hard upper bounds; refuted 0-3. Treat as heuristics, not constraints.
- **ISH as bounded-cognitive-load criterion** was claimed as the primary boundary lens for ISH; refuted 0-3. ISH's actual anchors are "Could this run as SaaS?" and "Could the team act independently?" — autonomy and self-containment, not cognitive load directly.
- **Martin's instability and Newman/Louvain** are stated here from general knowledge, **not** from the verified-claim pool. Treat as context.
- **Recommendation section is synthesis**, not a verified-source claim — design opinion grounded in verified inputs.
- Khononov 2024 is the most recent and least settled framework here. Stevens/Yourdon (1979) and Team Topologies (2019) are settled.
## 9. Sources
Primary (verified):
- IBM Systems Journal 13(2), 1974, DOI [10.1147/sj.132.0115](https://dl.acm.org/doi/10.1147/sj.132.0115) — Stevens, Myers, Constantine, "Structured Design"
- [IEEE Computer Society — Constantine pioneer biography](https://history.computer.org/pioneers/pdfs/C/Constantine.pdf)
- [Khononov — modularity GitHub skill](https://github.com/vladikk/modularity/blob/main/skills/balanced-coupling/SKILL.md)
- [coupling.dev — Khononov's companion site](https://coupling.dev/posts/dimensions-of-coupling/integration-strength/)
- [InformIT — "Balancing Coupling in Software Design" TOC](https://www.informit.com/store/balancing-coupling-in-software-design-successful-software-9780137353538)
- [CodeScene — Change coupling docs](https://codescene.io/docs/guides/technical/change-coupling.html)
- [Team Topologies — Finding good stream boundaries with ISH](https://teamtopologies.com/key-concepts-content/finding-good-stream-boundaries-with-independent-service-heuristics)
- [Team Topologies — Team interaction modeling](https://teamtopologies.com/key-concepts-content/team-interaction-modeling-with-team-topologies)
- [IT Revolution — "Team Topologies" book excerpt PDF](https://itrevolution.com/wp-content/uploads/2022/06/TTOP_excerpt.pdf)
Secondary (verified for cross-referencing):
- [Yourdon/Constantine "Structured Design" quote repository](https://wstomv.win.tue.nl/quotes/structured-design.html)
- [Tech Lead Journal podcast — Khononov interview](https://techleadjournal.dev/episodes/188/)
- [Software Architecture Guild — Balancing Coupling](https://software-architecture-guild.com/guide/architecture/boundaries/balancing-coupling/)
Unresolved (need direct URLs from user):
- Yves Goeleven LinkedIn coupling taxonomy series
## 10. Research-run stats
5 search angles, 23 sources fetched, 95 claims extracted, 25 adversarially verified (22 confirmed 3-0, 3 killed), 12 findings after synthesis, 105 agent calls.
