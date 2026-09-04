---
title: Autonomous Domain Capabilities (CCC / RPU)
type: concept
created: 2026-06-15
updated: 2026-08-03
sources: [rico-fritzsche-autonomous-domain-capabilities-ccc, rico-fritzsche-rpu-reactor-vocabulary, rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb, fritzsche-ccc-atomic-append-serialized-write-order, fritzsche-clean-architecture-capability-over-layers, devadoss-cead-capability-aligned-agent-design, fritzsche-command-context-consistency-principle, fritzsche-who-owns-a-rule-shared-across-domain-capabilities, fritzsche-why-your-software-cannot-explain-business-decisions]
tags: [business-capabilities, vertical-slice-architecture, event-sourcing, agentic-coding, ddd, focus]
---

# Autonomous Domain Capabilities (CCC / RPU)

A design pattern from **[[rico-fritzsche]]** ([[rico-fritzsche-autonomous-domain-capabilities-ccc]],
2026-06-08) for giving a **[[business-capabilities|domain capability]]** a real "home" instead of
smearing it across technical layers or anchoring it to a shared object model. Sharpened, he says, by
the AI-agent era: agents make change cheap and fast, which exposes architectures where behavior isn't
local and must be reconstructed.

## The idea

- **The problem of ownership.** Layered (Clean/Hexagonal) splits one capability across request
  handling, application layer, repositories, mappings, and shared domain structures —
  repositories especially become shared access points for unrelated capabilities. Even
  [[vertical-slice-architecture]] only *partly* fixes this: it makes Commands/Queries explicit and moves
  code near the request, but the handler often still depends on shared domain models / repositories /
  aggregates, so the slice is a local *entry point into* a larger shared structure rather than the place
  the capability fully owns its processing.
- **Command Context Consistency (CCC).** Don't route a Command into a shared object model to give it
  meaning. A Command **defines the facts it needs, builds a *local* context from those facts, makes a
  decision, and produces consequences.** A Query does the same for reading (define facts → derive a
  projection → return). The unit that does this is a **Request Processing Unit (RPU)** — one per
  capability — which builds its own context, decides, and keeps behavior local.
- **Recorded facts ≠ the domain.** Recorded events are the *Application State*; the **domain** only
  becomes visible through the capabilities that interpret those facts and produce new ones. So
  *domain = recorded state + the capabilities that know how to work with it.* The result: behavior,
  ownership, and change all stay **local to the capability** (an outer ring of RPUs around a central
  recorded-events core).

## Where it sits

- **Refines [[business-capabilities]].** It's a concrete realization strategy for capability-as-boundary:
  the RPU is the capability's executable home.
- **Sharpens [[vertical-slice-architecture]].** Names precisely where VSA still leaks ownership (shared
  models/repos/aggregates under the handler) and pushes the slice to own its context fully — close to
  [[jeremy-miller|Miller's]] "*small* slices, no shared services layer" point
  ([[miller-codebase-is-the-prompt-vertical-slices-ai]]).
- **Built on [[event-sourcing]].** Application State = recorded events; the RPU rebuilds decision
  context from the log. This is strikingly parallel to [[dynamic-consistency-boundaries|DCB]]
  (build a decision's consistency scope from the *relevant events*, not from a fixed aggregate) —
  CCC is arguably DCB framed as a capability-ownership pattern rather than a consistency mechanism.
- **Agent boundary.** A capability that owns its context, decision, and consequences is a natural unit
  for [[event-modeled-agent-design|agent ownership]]: contracted blast-radius, build-context-from-the-log,
  decide, emit — the same instinct as capability-scoped agent autonomy.

## The named vocabulary (2026-06-19) — "goodbye, Feature Slices"

Fritzsche's two 2026-06-17 posts ([[rico-fritzsche-rpu-reactor-vocabulary]]) turn the sketch above into
a precise, named vocabulary and **retire the term "Feature Slice"** ("a feature can mean anything; a
slice describes *shape, not responsibility*"):

- **RPU** — the capability unit (one Command or Query). Now explicitly **transport-free** — a reversal
  of his earlier "a slice contains everything incl. HTTP" stance, since "an RPU is not an external
  interface, it is an internal processing unit of the domain." Internally it is **Functional Core /
  Imperative Shell**; duplication between RPUs is accepted (independence > DRY).
- **Reactor** — optional, lightweight coordinator for an Interaction that needs several RPUs/Providers;
  it does **not** own their decisions and is explicitly **not** an event handler / saga / projection /
  process manager (it coordinates the *response to an interaction*, it doesn't react to recorded facts).
- **Interaction** (user-facing process) / **Use Case** (stakeholder grouping of Interactions) /
  **Delivery Mechanism** (thin HTTP/CLI translation) / **Providers** (injected infrastructure) /
  **Application State = Event Store** (single source of truth).

The deeper argument: layered architecture is **"distributed technical ownership"** (one capability
fragmented across controller/service/repo/entity/mapper → coordination pressure as shared structures
become bottlenecks); even VSA leaves shared ownership *under* the slice. The fix is to make the
**capability itself the ownership boundary**, with technical separation living *locally* (FC/IS) inside
the RPU rather than *globally* across layers. A pointed new distinction: **user interaction ≠ domain
capability** — they evolve for different reasons, so conflating them is what spawns oversized
handlers/orchestration layers. And a deliberate jab: business rules belong "in the domain, **not in
aggregates** — that is precisely where the problem with DDD lies."

## Enforcing CCC under concurrency (2026-06-29)

The CCC guarantee an RPU relies on ("reject the append if the relevant event context changed first")
needs a real **write-ordering** mechanism, not just an atomic statement.
[[fritzsche-ccc-atomic-append-serialized-write-order|Fritzsche shows]] that an atomic conditional append
(PostgreSQL CTE) still admits two incompatible decisions under READ COMMITTED — two commands can observe
the same context version and both write. CCC therefore requires **serialization** (e.g. a per-append
metadata-row lock): writes ordered globally, the conflict decision kept *local* to the capability's
command context. See [[dynamic-consistency-boundaries]] for the same point on the DCB side — this is the
implementation contract beneath both.

## Capability over layers — the Clean Architecture critique (2026-06-28)

[[fritzsche-clean-architecture-capability-over-layers|Fritzsche turns]] the capability-as-boundary
argument directly against **Clean/Hexagonal architecture**: Dependency Inversion changes the *direction*
of dependencies but doesn't remove the *functional* ones (the business logic still depends on I/O);
Separation of Concerns isn't achieved by horizontal technical layers — "the real concern is the domain
capability"; and **CRUD is not domain language** (experts think in processes/decisions/state
transitions). [[fritzsche-functional-core-imperative-shell-agentic-coding|FC/IS]] is offered as the
stronger foundation. Same throughline as the "distributed technical ownership" critique below — layers
fragment a capability; make the capability the boundary, with technical separation living *locally*.

## Independent corroboration — deVadoss's CEAD (2026-05)

[[john-devadoss|deVadoss's]] **CEAD** ([[devadoss-cead-capability-aligned-agent-design]]) reaches the
same "give the capability a home" conclusion from the **multi-agent architecture** side rather than the
code-structure side. Its first design principle, **"capability before agent,"** is the direct analog of
Fritzsche's *domain = recorded state + the capabilities that interpret it*: define the durable business
capability and its owner before naming any agent role or prompt. Where the RPU is the capability's
**executable** home inside one codebase, CEAD's **Agent Capability Contract** is the capability's
**contracted** home for an autonomous agent — both make the capability (not a layer, object model,
aggregate, or role) the ownership boundary. CEAD's warning that undisciplined decomposition yields
**micro-agent proliferation / a distributed monolith** is the same coordination-pressure critique
Fritzsche levels at "distributed technical ownership," raised to the agent tier. See
[[business-capabilities]] for the joined-up lineage.

## What's open / to capture next

The worked detail is now captured ([[rico-fritzsche-rpu-reactor-vocabulary]], superseding the earlier
teaser). RPU/Reactor/CCC remains **Fritzsche's own coinage** with no independent adoption yet — watch
whether it spreads.

**CCC vs DCB — now answered (2026-06-19).** The standing open question (how does CCC differ from
[[dynamic-consistency-boundaries|DCB]]?) is addressed in
[[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]: **same rejection principle, different
layer.** CCC defines the consistency guarantee *representation-agnostically* (tags/indexes are optional
optimizations); DCB pins the same principle to a concrete event-store contract (event-types + tags as the
query contract, opaque payload). So CCC is the conceptual guarantee and DCB one tag-based implementation
of it — not a re-labeling but a more abstract framing. The same post insists **Event Sourcing does not
require aggregates** (the aggregate-rebuild recipe is one implementation, not the definition) — the
ES-side root of the "give the capability a home" argument.

## The RPU as the explainable, shared-rule-safe boundary (2026-07)

Three later Fritzsche pieces sharpen what the RPU is *for*. **[[command-context-consistency|CCC]]** is the
commit contract the RPU carries: it reads the context, decides, and appends only while that context holds,
mapping a guard conflict to a **business** outcome, not a technical error
([[fritzsche-command-context-consistency-principle]]). The RPU is also the unit that makes a decision
**explainable** — the visible `command → context → decide → guard → outcome` path a developer can follow
without reconstructing the app ([[fritzsche-why-your-software-cannot-explain-business-decisions]];
[[agent-explainability]]). And capability autonomy **survives shared rules**: instead of a central service
layer, name the kind of shared knowledge — state invariant (enforced at commit), external fact (a
Provider), stable semantics (a small pure type), shared policy (a versioned authority + conformance
suite) — while the **final decision stays with the owning capability**
([[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]]). *"A rule can have one authority and
many local evaluators."*

_Sources: [[rico-fritzsche-autonomous-domain-capabilities-ccc]] · [[rico-fritzsche-rpu-reactor-vocabulary]] · [[devadoss-cead-capability-aligned-agent-design]] · [[fritzsche-command-context-consistency-principle]] · [[fritzsche-who-owns-a-rule-shared-across-domain-capabilities]] · [[fritzsche-why-your-software-cannot-explain-business-decisions]]._
