---
title: Business Capabilities
type: concept
created: 2026-06-14
updated: 2026-09-04
sources: [laycock-citizens-build-agents-execute-experts-govern, nick-tune-enforced-application-architecture-agents-humans, homann-business-capabilities, goeleven-event-model-to-code-series, goeleven-event-sourcing-not-auditing-for-free, daniel-event-modeling-wardley-mapping, rico-fritzsche-autonomous-domain-capabilities-ccc, khononov-golden-age-of-modularity, rico-fritzsche-rpu-reactor-vocabulary, devadoss-cead-capability-aligned-agent-design, skelton-team-topologies-foundation-ai-roi, dora-roi-ai-assisted-software-development-2026, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-why-the-entity-model-is-an-illusion]
tags: [business-capabilities, coupling-cohesion, ddd, event-modeling, architecture, focus]
---

# Business Capabilities

A **business capability** is *what* an organization is able to do — a stable, outcome-oriented ability
(e.g. "Booking", "Payments", "Catalog Management") — independent of *how* it's currently realized
(the process, org chart, or technology). Capability-based design uses these as the **long-term-stable
boundaries** around which you organize processes, teams, and software. A focus-area concept for Dannie
(flagged important, 2026-06-14).

## Primary definition (Homann, 2006)

The seminal source is **[[ulrich-homann]]**'s *A Business-Oriented Foundation for Service Orientation*
([[homann-business-capabilities]]), the most-cited origin of capability mapping (referenced by the
BIZBOK Guide):

- A **business capability** is "a particular ability or capacity that a business may possess or
  exchange to achieve a specific purpose or outcome" — it describes *what* the business does (outcomes
  + service levels) and **encapsulates** people, process, technology and information.
- A capability is a **"black box"**: external, observable, measurable behavior with defined
  inputs/outputs and a contracted **service-level expectation**; the internal "how" is irrelevant at
  this level. (This is why capabilities map onto services — and onto agent boundaries.)
- **Capability connectors** link capabilities and carry rich semantics (information exchange +
  control/policy). Homann's striking claim: discovering the *connections* "may be as valuable as
  defining the capabilities" — you manage change through connectors while the black boxes stay stable.
- A **business capability map** is a **nested taxonomy** (L1 Foundation: Operations vs Environmental →
  L2 Capability Groups → L3…n Business Capabilities), spanning the whole value network. **Process ≠
  capability:** process is the implementation of the capability blueprint at a point in time.

## Why capabilities make good boundaries

The core argument is **coupling and cohesion**: *how* a business does something changes often (process
tweaks, reorgs, new tech), but *what* it does is far more stable. Drawing boundaries around the stable
"what" means change tends to stay **inside** one capability instead of rippling across many — high
cohesion within, low coupling between. This is the same instinct behind [[domain-driven-design]]'s
**bounded contexts**, [[conways-law]] (teams own capabilities, so the architecture mirrors a sensible
org structure), the [[open-closed-principle]] (extend a capability without modifying others), and
[[vertical-slice-architecture]] (features cut vertically through a capability, not across layers).

**[[vlad-khononov]]** supplies the design-theory spine here: his **[[balanced-coupling|Balanced
Coupling]]** model judges a coupling by its *shared knowledge × distance × volatility* (his own wording; "strength" names the scale, not the axis — see [[balanced-coupling]]) (so the aim is not "no coupling" but keeping strong
coupling at short distance and away from volatile parts), and his
[[khononov-golden-age-of-modularity|modularity test]] — change is *localized* and its *effect is
predictable* — is exactly the property a good capability boundary buys. It also reframes capabilities as
an **agent-era** concern: modular, low-blast-radius boundaries are what make a codebase tractable for AI
agents (cf. [[agent-legibility]], [[tornhill-clear-design-principles-agentic-age|CLEAR]]).

## In this KB — Goeleven's capability-centric Event Modeling

[[yves-goeleven]] is the KB's clearest practitioner of capability-based design
([[goeleven-event-model-to-code-series]]):

- In an [[event-modeling|Event Model]], the **bottom swimlanes are business capabilities** (top
  swimlanes are roles). Capabilities are "the long-term stable boundaries within which part of the
  business process gets performed."
- **Decisions are owned by the capability, not the individual** — a business decision is recorded as
  an event inside the capability swimlane "even when the decision is taken in the mind of an authorized
  person." Different roles may be *authorized* to take it, but ownership belongs to the capability.
- Humans send **intent (commands)** to a capability; the capability reports back **state (read
  models/projections)** derived from its own decisions. Each capability is realized differently per
  org.
- **Contract between capabilities is required:** a capability's *internal* events should not double as
  integration events with other capabilities — otherwise you couple them as tightly as a shared
  database (the Dragan Stepanović exchange). Integration needs an explicit, owned contract (event,
  state, or UI). This is the crisp coupling/cohesion rule of the approach.
- Each capability's event stream also gives a per-process **audit** when enriched with
  who/when/where/what/why ([[goeleven-event-sourcing-not-auditing-for-free]]).

## Giving a capability a "home" — Fritzsche's Autonomous Domain Capabilities

**[[rico-fritzsche]]** sharpens the boundary argument for the agent era
([[rico-fritzsche-autonomous-domain-capabilities-ccc]]): most architectures give a capability *no clear
home* — layered approaches smear it across handlers/repositories/shared models, and even
[[vertical-slice-architecture]] leaks ownership when the handler still depends on a shared object model
or aggregate. His fix ([[autonomous-domain-capabilities]]): each capability is a **Request Processing
Unit** that, via **Command Context Consistency (CCC)**, builds a *local* context from recorded events,
decides, and emits consequences — so *domain = recorded state + the capabilities that interpret it*.
This restates Goeleven's "decisions are owned by the capability" and "contract between capabilities"
rules as an executable pattern, and is closely parallel to [[dynamic-consistency-boundaries|DCB]]
(build a decision's scope from the relevant events, not a fixed aggregate).

His 2026-06-17 follow-ups ([[rico-fritzsche-rpu-reactor-vocabulary]]) name the pattern's vocabulary
(RPU / Reactor / Interaction / Delivery Mechanism / Providers) and add a sharp diagnosis of why
capabilities make better boundaries than object models: layered architecture is **"distributed technical
ownership"** — one capability fragmented across controller/service/repo/entity/mapper, so independent
capabilities are forced to evolve together through shared structures (coordination pressure). Making the
*capability* the ownership boundary keeps change additive and local — the same coupling/cohesion claim as
Homann's black box and [[balanced-coupling|Khononov's]] localized-change test, stated as a code-structure
rule. He also insists **user interaction ≠ domain capability** (they evolve for different reasons).

### What a capability is, operationally — and why capabilities grow additively (2026-08)

Two Aug-2026 articles reduce the capability to something you can point at in a repo.
**A capability is one action the domain can take, named in pairs with the fact it produces** —
"the capability *InfleetVehicle* produces the *VehicleInfleeted* event, and the *InspectVehicle*
capability produces the *VehicleInspected* event… **Every action that leads to an event is a domain
capability**" ([[fritzsche-how-event-sourcing-grows-with-the-business]]). They are "autonomous,
self-contained, and coherent. **They share only the Application State** — in this implementation, an
Event Store and the event definitions. However, they know nothing about each other"
([[fritzsche-why-the-entity-model-is-an-illusion]]).

The consequence is the strongest boundary argument on this page: because each capability derives its own
state by folding only the events its rules read, **adding a capability changes nothing else**, and adding
a *fact* changes only the capabilities that need it. "Events are additive, since no reader needs to know
the big picture. Functions remain small because they derive their specific perspective precisely from the
events." Where an entity-centred design makes a new process step "a change to a shared structure, because
the database represents a global, shared, mutable state," here there is no shared structure to change —
so **no schema migration and no data migration** (his worked case: `AcquireVehicle` and `ReceiveVehicle`
untouched; `InfleetVehicle` gains one fold case and one rule). Cost does land on new **projections**,
which he says explicitly.

*One authored vehicle-rental example, no measurement; and see [[entity-centric-thinking]] for the
counter-position that keeps business rules on the entity ([[oskar-dudycz]]).*

## Relation to the focus (agents)

Stable capability boundaries are a natural unit for **agent ownership and autonomy**: an agent (or
multi-agent group) can own a capability, act through its commands, and emit/consume its events — the
same "agent as user/processor on a swimlane" mapping as [[event-modeled-agent-design]]
([[dymitruk-event-modeling-future-proof-agents]]). Capabilities give agents a contracted blast-radius;
cf. the legibility/contract themes in [[harness-engineering]] and the [[agentic-event-driven-systems]]
"agents subscribe→reason→publish, never call each other directly" pattern. Fritzsche's RPU makes this
literal: a capability that owns its context/decision/consequences *is* the agent's home.

## The agent-era extension — deVadoss's CEAD and the Agent Capability Contract

**[[john-devadoss]]** carries the capability-boundary argument furthest into multi-agent architecture
([[devadoss-cead-capability-aligned-agent-design]], arXiv, 2026-05-07). His **CEAD** (Capability-Aligned
Enterprise Agent Design) makes the durable business capability — not a role, prompt, or agent count —
the primary design object, with the first two design principles being **"capability before agent"** and
**"boundary before topology."** This is the same coupling/cohesion instinct as Homann's black box and
Fritzsche's RPU, now stated as a rule for *how many agents to build and where each one lives*: decompose
into separate agents **only** where there is a durable reason — separate business ownership, materially
different tool authority, distinct data classification, specialized evaluation, or independent release
cadence.

The keystone is the **Agent Capability Contract (ACC)** — deVadoss's explicit descendant of the **SOA
service contract/SLA**, which is itself the operationalization of Homann's *"contracted black box with a
service-level expectation."* The ACC is Homann's black box for the agent era: a contracted capability
boundary that now additionally carries **autonomy level (L0–L4), tool scopes, memory/state design,
verification design, escalation triggers, evaluation evidence, and a retirement path.** Where a service
contract described inputs/outputs/SLA, the ACC adds everything that makes a *probabilistic, stateful,
goal-directed* actor accountable — while keeping the capability's internal "how" a black box. CEAD's
four planes even preserve the SOA lineage literally: existing services, microservices, and data products
sit in an **Enterprise Capability Plane** that agents consume through contracts and least-privilege
adapters — *"agents do not own enterprise capabilities by default."*

CEAD corroborates this page's whole spine from the agent side. It restates Goeleven's **"decisions are
owned by the capability, not the individual"** (the ACC names the capability's owner and the decisions
the agent may make) and the **"contract between capabilities"** rule (agents interact through explicit
contracts, "never through hidden prompt dependencies"). It independently lands on Fritzsche's
**capability-as-home** (the ACC records "the design decision that justifies an agent's existence"). And
its simulation over 10,000 tasks supplies the missing *evidence*: a **governance-first but design-poor**
agent grid — strong policy, audit, and least-privilege but weak capability alignment — scored 50.8% safe
success versus **CEAD's 70.6%**, i.e. **governance cannot compensate for bad capability boundaries.**
Removing the capability map + ACCs was the ablation that hurt functional success and auditability most.
The failure mode when you ignore all this is **micro-agent proliferation = a distributed monolith of
agents** (see [[coupling-taxonomy]]).

On the organization side, **[[matthew-skelton]]** makes the mirror-image claim
([[skelton-team-topologies-foundation-ai-roi]]): the **value-flow-aligned team boundary is the boundary
that makes an autonomous agent effective**, and **data should be a curated product digestible for both
humans and agents** — a capability/team stewarding its own contracted data. Together the two 2026 sources
bracket the thesis: deVadoss on the *architecture* boundary, Skelton on the *organization* boundary, both
insisting the durable capability/value boundary comes before the tooling.

## The data-architecture arrival — Sadalage & Chandrasekaran's capability model

A third 2026 source reaches this boundary from a direction none of the above do: **data architecture**.
[[pramod-sadalage]] and [[prem-chandrasekaran]] ([[thoughtworks]]) propose a three-part *context layer*
for agents — a **domain model** (what exists; consulted, never executed), a **semantic model** (how the
numbers are computed), and a **capability model** (what the agent may do)
([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]], 2026-08-27). Their capability model is a
curated set of operations where each one declares **permissions** (who may invoke it, acting as whom)
and an **owner** (accountable when it misbehaves), and each *acting* one additionally declares
**preconditions** and a **reversibility class**.

This is deVadoss's ACC arrived at independently and from outside — neither source cites the other, and
the convergence is the interesting part. The differences are informative:

| | **ACC** (deVadoss) | **Capability model** (Sadalage/Chandrasekaran) |
| --- | --- | --- |
| Unit described | An *agent* justified by a capability | An *operation* the agent may invoke |
| Autonomy | L0–L4 assigned per agent | Staged ladder, but cut across by reversibility per action |
| Where it lives | A design artifact | Code in source control, reviewed and CI-tested |
| Risk key | Action risk / reversibility / confidence / evidence | **Reversibility class**, explicitly over transaction size |

Three things this adds that the page did not previously hold:

1. **Preconditions checked against live state at the moment of acting**, not against what the agent read
   earlier in its plan. In [[event-modeling]] terms this is a command slice's *given* — the article lands
   on the given/when/then decision shape without the vocabulary. See [[given-when-then]].
2. **Reversibility as the autonomy key** — "reversibility predicts safe autonomy better than the size of
   the transaction," with irreversible actions requiring human approval *whatever* stage the agent has
   reached. This cuts across [[autonomy-ladder]] rather than sitting on it.
3. **"Design capabilities, not endpoints."** Applied to tool surface: five to ten well-described business
   capabilities beat 50 thin API wrappers, and naive one-to-one API→MCP conversion is on the Thoughtworks
   Radar at HOLD. This makes [[model-context-protocol]] surface area a capability-boundary decision rather
   than a wiring one.

Their unifying formulation is worth keeping verbatim, because it is a general statement of why a
capability boundary is worth declaring at all: each model is *"a place where a guarantee is declared once,
in version control, instead of being worked out afresh by the model on every request."*

*Caveat:* the article is Thoughtworks-authored and cites Thoughtworks Radar placements in support of its
own positions, so the Radar citations are not independent corroboration.

## Strategy lens — capabilities × Wardley Mapping

Capabilities tell you the stable *what*; [[wardley-mapping]] tells you how each capability is
**evolving** (Genesis → Custom → Product → Commodity) and therefore how to treat it strategically
(build vs buy, differentiating vs utility). **Chris Daniel**'s *Event Modeling and Wardley Mapping*
series ([[daniel-event-modeling-wardley-mapping]]) frames the trio: **Wardley** = where to go and why;
**capabilities** = the stable units; **[[event-modeling]]** = what to build (the concrete design).
Adam Dymitruk has also referenced the EM × Wardley connection.

## Lineage / provenance

- **Primary, now captured:** [[ulrich-homann]] 2006 ([[homann-business-capabilities]]) — the
  capability-mapping foundation (cited by the BIZBOK Guide). Earlier business-architecture /
  capability-based-planning lineage and **DDD strategic design** (bounded contexts, subdomains) sit
  alongside it.
- **Practitioner application:** [[yves-goeleven]] ([[goeleven-event-model-to-code-series]]) — capability
  swimlanes in Event Modeling; the "contract between capabilities" coupling rule. [[rico-fritzsche]]
  ([[autonomous-domain-capabilities]]) — capability-as-RPU with local, event-sourced context (CCC).
- **Strategy primary, now captured (2026-06-15):** [[simon-wardley]]'s *Wardley Maps* (Ch.2 Value
  Chains, Ch.3 Evolution), via [[chris-daniel]] ([[wardley-maps-value-chains-and-evolution]]) — grounds
  the capabilities × strategy lens ([[wardley-mapping]]).
- **Agent-era extension, now captured (2026-07-31):** [[john-devadoss]]'s **CEAD** / Agent Capability
  Contract ([[devadoss-cead-capability-aligned-agent-design]]) — capability-before-agent for multi-agent
  architecture; and [[matthew-skelton]]'s value-flow-team-as-agent-boundary
  ([[skelton-team-topologies-foundation-ai-roi]]). The [[dora-roi-ai-assisted-software-development-2026|2026
  DORA ROI report]] — Skelton's primary, now captured — gives this an ROI spine: value realises through a
  chain of **seven capabilities** (quality internal platform, version control, AI-accessible internal
  data, …) → DORA delivery metrics → outcomes, so capability quality is literally the first link in the
  AI-return calculation.
- **Capability autonomy survives shared rules** ([[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]]):
  the objection that "shared invariants (identity/money/compliance) cut across capabilities" is answered by
  naming the *kind* of shared knowledge and giving each its own home — **state invariant** (enforced at
  commit), **external fact** (a Provider), **stable semantics** (a small pure type), **shared policy** (a
  versioned authority + conformance suite) — while the **final decision stays with the owning capability**.
  "A rule can have one authority and many local evaluators." The alternative — a central service layer —
  is exactly what capability ownership avoids. See [[autonomous-domain-capabilities]],
  [[command-context-consistency]].
- *To capture next:* a transcript of the Daniel EM × Wardley series; Dymitruk's EM × Wardley talk; the
  remaining Wardley chapters (doctrine/gameplay/PST); a BIZBOK-level treatment of capability maps; and
  the DORA **2025** *State of AI-Assisted Software Development* report (for the full DORA AI Capabilities
  Model — the ROI report's predecessor).

## The four rungs, and what each one enforces (added 2026-09-02)

The 2026-09-02 ingest added the two rungs this page was missing, and it is worth laying the ladder out
explicitly, because the same word is doing four different jobs and only one of them is checkable by a
machine:

| Rung | Source | The capability is… | Enforced by |
| --- | --- | --- | --- |
| **Strategy** | [[homann-business-capabilities]], [[daniel-event-modeling-wardley-mapping]] | a stable *what*, mapped for positioning | nothing — it is a map |
| **Organisation** | [[laycock-citizens-build-agents-execute-experts-govern]], [[skelton-team-topologies-foundation-ai-roi]] | who may build what, and who carries the judgement | people and governance |
| **Data / agent contract** | [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]], [[devadoss-cead-capability-aligned-agent-design]] | a bounded contract with declared authority | the ACC, review gates |
| **Code** | [[rico-fritzsche-autonomous-domain-capabilities-ccc]], [[nick-tune-enforced-application-architecture-agents-humans]] | a subdomain / capability folder with no lateral reach | the build |

**[[rachel-laycock]] supplies the organisational rung without using the word.** Her slogan —
*"Citizens build. Agents execute. Experts govern."* — is, in her own correction, **not** a statement
about roles or about who is permitted to do what: *"At first I thought I was talking about roles… But I
don't actually think that's what I meant. I think I was talking about where value is moving."* Reading
it as a capability boundary drawn around *permission and accountability* is **this wiki's extension**,
not her claim, and it should be labelled as such wherever it is used.

What is unambiguously hers, and what this page should carry, is the **scarcity inversion**: what is
scarce is not the ability to build but *"good engineering judgement: knowing what good looks like,
understanding the risks and knowing when something that works is actually safe to trust in
production."* The expert's output is the **environment** — guardrails, platforms, practices, feedback
loops — in which others and agents build safely. **Not independent**: Thoughtworks' CTO on
martinfowler.com, and this page already discounts Thoughtworks self-citation elsewhere; her convergence
with the outside CEAD source is what makes it interesting.

**[[nick-tune]] supplies the code rung with actual teeth.** Packages must live inside a subdomain, and
a slice's commands may import `domain` only from `ownSubdomain` — cross-subdomain reach fails the build
([[nick-tune-enforced-application-architecture-agents-humans]]). Fritzsche's CCC gives a capability a
*home*; Tune's DSL makes the home's walls **load-bearing**. *(Author self-report — Rivière is his own
tool, no before/after measurement.)*

The gap the table makes visible: **nothing connects the rungs.** A capability named on a Wardley map, a
capability an ACC governs, and a capability that is a folder the build protects are three different
artifacts with no traceability between them, and no source in this KB attempts the mapping. That is the
most useful open question on this page.

## Related

[[event-modeling]] · [[slice]] · [[team-topologies]] · [[event-sourcing]] · [[cqrs]] ·
[[rachel-laycock]] · [[nick-tune]] · [[fitness-functions]] · [[agent-governance]] ·
[[autonomous-domain-capabilities]] · [[command-context-consistency]] · [[coupling-taxonomy]] ·
[[balanced-coupling]] · [[wardley-mapping]] · [[multi-agent-orchestration]] · [[autonomy-ladder]] ·
[[agent-explainability]] · [[model-context-protocol]] · [[conways-law]] · [[harness-engineering]] ·
[[event-modeled-agent-design]] · [[locality-of-reference]] · [[entity-centric-thinking]]

_Sources: [[laycock-citizens-build-agents-execute-experts-govern]] · [[nick-tune-enforced-application-architecture-agents-humans]] · [[homann-business-capabilities]] · [[goeleven-event-model-to-code-series]] · [[goeleven-event-sourcing-not-auditing-for-free]] · [[daniel-event-modeling-wardley-mapping]] · [[rico-fritzsche-autonomous-domain-capabilities-ccc]] · [[rico-fritzsche-rpu-reactor-vocabulary]] · [[khononov-golden-age-of-modularity]] · [[devadoss-cead-capability-aligned-agent-design]] · [[skelton-team-topologies-foundation-ai-roi]] · [[dora-roi-ai-assisted-software-development-2026]] · [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-why-the-entity-model-is-an-illusion]]._
