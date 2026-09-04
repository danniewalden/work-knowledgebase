---
title: Vertical Slice Architecture (VSA)
type: concept
created: 2026-06-14
updated: 2026-09-04
sources: [nick-tune-enforced-application-architecture-agents-humans, dilger-element-slice-chapter-story-context-ladder, dilger-slicing-keeps-the-cost-curve-flat, miller-jasperfx-critterstack-ai-event-modeling-strategy, bogard-vertical-slice-architecture, miller-codebase-is-the-prompt-vertical-slices-ai, rico-fritzsche-autonomous-domain-capabilities-ccc, fritzsche-functional-core-imperative-shell-agentic-coding, rico-fritzsche-rpu-reactor-vocabulary, dilger-triplet-flexible-agent-enabled-architecture, dudycz-vertical-slices-ownership-and-external-dependencies, bogard-vertical-slice-architecture-webinar-recording-whats-next, fritzsche-vsa-does-not-fix-entity-centered-thinking]
tags: [vertical-slice-architecture, cqrs, ddd, architecture, focus]
---

# Vertical Slice Architecture (VSA)

> **Disambiguation (2026-08-31).** This page is about **[[jimmy-bogard]]'s code-organisation pattern**.
> Event Modeling's **[[slice]]** — a unit of the *model*: one step of a business process with its
> given/when/then, existing before any code — now has its own page. The wiki used to alias both to this
> page, which hid the distinction; almost every agent-facing claim in the KB is about the model unit.
> The two are complementary: an EM slice is the specification a vertical slice of code implements, and
> [[triplet-architecture]] pairs them on purpose so the unit survives the trip from model to code.

VSA organizes code **by feature/request instead of by technical layer**: each "slice"
encapsulates all concerns front-to-back for one request. Named by **[[jimmy-bogard]]**
([[bogard-vertical-slice-architecture]], 2018), emerging from a move off onion/layered architecture
toward [[cqrs]]. Added 2026-06-14 when Dannie broadened the focus to the Event Modeling design
substrate; substantially grown 2026-06-15 with the **AI-substrate** angle (Miller, Fritzsche).

## The idea

"**Minimize coupling between slices, and maximize coupling in a slice.**" Remove the gates/barriers
between layers and couple along the **axis of change** — when you add a feature you touch UI, model,
validation, persistence for *that* slice, not a horizontal layer shared across features. Shared
abstractions (repositories/services/controllers) largely melt away; each slice picks its own
implementation, starting simple (Transaction Script) and refactoring as code smells appear. Splitting
requests into command vs. query means VSA "gives [[cqrs]] out of the gate." Caveat (Bogard): it
assumes a team fluent in refactoring and knowing when to push logic into the domain.

## Where it sits / why it's in the focus

- **Event Modeling fit (the key link).** Event Modeling builds a system as **vertical slices** of a
  feature (a UI→command→event→read-model path), each with its own Given-When-Then — the same
  feature-not-layer decomposition VSA names. The KB's focus material already leans on this: in
  [[jwilger-agent-skills-event-modeling]] the event model's **vertical slices + GWT** become the
  contract that governs an autonomous coding factory, and in
  [[dilger-model-is-a-living-spec-always-on-agent]] a "slice" placed in `planned` is the unit an agent
  picks up (generate tests → implement → PR). VSA is the architecture that those agent slices land in.
- **Substrate cluster.** Sits with [[event-sourcing]], [[cqrs]], [[domain-driven-design]] and
  [[open-closed-principle]] (new features *add* code rather than modify shared code — echoing Event
  Modeling's flat feature-cost curve).

## VSA as the AI substrate (2026-06-15)

Two sources reframe VSA as *the* AI-friendly code organization:

- **The codebase is part of the prompt** ([[jeremy-miller]], [[miller-codebase-is-the-prompt-vertical-slices-ai]]).
  Because an agent pays in tokens/latency/accuracy for every irrelevant file it loads, layered code
  (one behavior scattered across 6–7 directories) collapses context signal-to-noise and triggers
  hallucination — while feature slices load only what's relevant ([[locality-of-reference]]). Miller
  pushes further: *small* slices beat merely co-located ones, and shows Wolverine/[[critter-stack]]
  compressing a slice to "the decision and nothing else." Crucial caveat — compression shifts the
  implicit wiring into agent guesswork unless conventions are encoded as skill files
  ([[harness-engineering]] guides): "the skills are the constitution; the slices are the code."
- **Where VSA still leaks ownership** ([[rico-fritzsche]], [[autonomous-domain-capabilities]]). A slice
  is only a *local entry point into* a larger shared structure if the handler still depends on shared
  domain models / repositories / aggregates. His RPU/CCC pattern pushes the slice to fully own its
  context (built from recorded events) — VSA taken to a capability-owning, [[event-sourcing|event-sourced]]
  conclusion. Pairs with [[business-capabilities]] and [[dynamic-consistency-boundaries]]. **Update
  (2026-06-17, [[rico-fritzsche-rpu-reactor-vocabulary]]):** Fritzsche now **abandons the term "Feature
  Slice"** entirely in favour of **Request Processing Unit** — arguing "slice" names shape not
  responsibility, and that even a vertical slice leaves "distributed technical ownership" under it unless
  the *capability* (not the feature package) is the boundary. Note this also reverses his earlier "a
  slice contains everything incl. HTTP": an RPU is now transport-free, with HTTP pushed to a Delivery
  Mechanism.
- **The internal shape of an agent-friendly slice** ([[fritzsche-functional-core-imperative-shell-agentic-coding]]).
  Fritzsche answers "what does a slice look like *inside* so an agent generates it reliably": Functional
  Core / Imperative Shell (pure decision core + IO-only shell), behavior-describing file names over
  `service/manager/repository`, share-nothing-domain defaults, and **cross-feature dependencies as a
  structural exception** — all enforced by project-level skill files. Concrete how-to under
  [[locality-of-reference]]; templates at `github.com/ricofritzsche/agentic-feature-slice-templates`.

## A second independent statement of the token argument (Miller, 2026-08)

[[jeremy-miller]] reaches the same conclusion from the other side of the
[[model-as-code-vs-model-as-language]] disagreement, which makes it the KB's cleanest case of the VSA
token claim being arrived at independently ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]):

> "Wolverine's very terse approach to VSA is already very optimized for AI agentic development —
> especially when contrasted with more traditional server side .NET code organization that leans into
> layered architectures that force AI agents to burn more tokens traversing the code."

He calls Wolverine's original VSA emphasis "accidentally prescient" — it was not designed for agents —
and is explicit that the claim is **unproven**: *"it's incumbent upon people like me to prove that out
over time."* That candour is worth preserving, because this page's token argument still rests entirely on
assertion from both Miller and [[martin-dilger]] ("slices are like candy for AI"), with no measurement on
either side.

He also names the adoption friction the page otherwise lacks: users arriving from **Clean Architecture**
bring the projects, layers and abstractions that neither the framework nor the agent wants, so the
obstacle is an existing-codebase problem rather than a persuasion problem.

## What's open / to capture next

**Closed (2026-09-04):** the long-flagged Dudycz capture landed — not "Semantic Diffusion" but
[[dudycz-vertical-slices-ownership-and-external-dependencies]] (2026-08-10), which is the deeper
source. *Still open:* verticalslicearchitecture.com, the Codeartify webinar recording behind
[[bogard-vertical-slice-architecture-webinar-recording-whats-next]] (the argument's primary; the blog
post is its trailer), and the Medium article behind
[[fritzsche-vsa-does-not-fix-entity-centered-thinking]] (linked in a LinkedIn first comment, unresolved).

**VSA as the "structure" block of Dilger's Triplet.** [[dilger-triplet-flexible-agent-enabled-architecture|Dilger]]
(2026-07-26) casts vertical slices as the *natural result* of an Event Modeling session — you structure code
around the flows the model surfaced, so "a change to one flow stays inside that flow… typically affects only
one step." Two consequences he foregrounds: **estimation** by *Slice-Cycle-Time* (slices are roughly equal
size, so average build-time-per-slice beats story points), and the **agent economics** — a slice is the unit
of *agent* work, because an agent needs only that slice's context + event log + model, so parallel agents add
throughput without colliding. This is the same [[locality-of-reference|codebase-is-the-prompt]] argument
Miller makes, stated as the middle block of the EM+VSA+ES [[event-modeled-agent-design|triplet]].

## VSA as an enforced invariant, not a convention (Tune, 2026-08)

Everything above argues that slices are *better*. [[nick-tune]] is the KB's first source that makes them
**compulsory at build time** ([[nick-tune-enforced-application-architecture-agents-humans]]): in his
`use-cases` packages all feature code must live in `/features/{feature}` — glossed in the post as
*"(i.e. vertical slices)"* — with cross-feature imports forbidden outright (`importRules: { allow: {} }`),
and each feature folder required to provide its own `/commands`, `/queries`, `/data-access` and
`/adapters`. A violation is not a review comment; it fails the build.

Three things this adds to the page:

- **A mechanism under the collision-avoidance claim.** The agent-economics argument above (parallel
  agents don't collide because each works inside one slice) has rested on the *intent* of slicing. An
  enforced no-cross-feature-imports rule is what makes the property true of the codebase rather than
  true of the plan. (The reason an advisory boundary is not enough is stated best elsewhere — Bogard's
  *"An agent doesn't read your architecture diagram. It reads your repo and copies what it finds"*
  ([[bogard-vertical-slice-architecture-webinar-recording-whats-next]], 2026-09-01,
  now ingested). Tune does not put it in those terms; he simply reports that agents violate written
  guidance.)
- **An asymmetry worth borrowing.** He deliberately treats the two halves differently: the domain model
  is left free-form (*"domain models should express the business however necessary"*) while slices are
  forced to be uniform (*"I do want things to be highly standardised and boring"*). The KB's VSA
  material has not made that distinction; it is a sharper statement than "prefer slices" and it explains
  *why* slice uniformity is the thing worth enforcing — the value is comparability across slices, which
  is also what makes Dilger's Slice-Cycle-Time estimation work.
- **The boundary is a subdomain boundary too.** Packages must sit inside a subdomain and a slice's
  commands may import `domain` only from `ownSubdomain`, which is [[business-capabilities]] enforced at
  the same layer as the slice rule — the code-level counterpart to the capability boundary.

*Interested-party marker: Rivière is Tune's own tool and the post carries no before/after measurement —
mechanism described precisely, payoff asserted. He also rates the tiers honestly, calling
package/domain/layer rules indispensable for agentic work and the finest tier unproven ("come back in 6
months").*

## What a slice does when it needs something it doesn't own (Dudycz, 2026-08)

[[dudycz-vertical-slices-ownership-and-external-dependencies]] is the first source on this page to give a
**positive answer to cross-slice dependency**, and it starts by fixing the vocabulary that makes the
question unanswerable: **a slice is one piece of functionality cut through the application** ("more a
function than an entity"); **a module is a grouping of slices**, the criterion being "what changes
together"; **a bounded context is a linguistic barrier**, so "a frontend and a backend aren't two
bounded contexts; they're two deployment targets" and "seven features of one application are almost
always slices, or at most modules, sitting inside a single context — **they were never obliged to be
autonomous.**"

The mechanism: **"From inside a slice, there's one category of thing: external.** Another slice next
door, the parent module, a different module, a third-party API, the database. All the same." A slice
declares a **narrow function type in its own vocabulary** (`CheckContractor` with three cases, not the
carrier's fifteen-method interface), nothing declares that it implements it (structural typing), and a
single composition file near the entry point supplies the real functions — "partial application, done by
hand, in a file whose job is to know about everything so that nothing else has to. No container, no
registration, no lifetime scopes." Tests pass stubs of the same shape, "because there's nothing to mock."

Four consequences worth carrying:

- **Two directions across one boundary.** A module's `api.ts` is what it **offers**; a declared
  `CheckContractor` is what a slice **asks for**. You want both — without the module API everything is
  reachable; without consumer-declared needs the consumer is coupled to the shape of whatever the
  provider chose to expose. The composition root is the only code that knows both vocabularies.
- **Cycles dissolve rather than get resolved.** "There's no cycle if neither module imports the other."
  His diagnosis: "most module-level cycles I've run into were a shared concept whose owner hadn't been
  decided yet" — and the usual extract-a-common-module fix "works twice; then the common module becomes
  the place everything ambiguous lands."
- **Persistence, three rules, not one:** **business logic per entity or aggregate**, **read models per
  query** ("this is where a table per feature is right"), **schemas per module** ("a slice is a feature,
  not a persistence boundary").  Reuse pure policies and calculators; **let handlers duplicate**, because
  "handlers differ in what they load, check and record, and that's the part that tends to change."
  *(Note the first of those three is the live disagreement with [[rico-fritzsche]] — see
  [[entity-centric-thinking]].)*
- **He rejects independence as a value:** "**None of this is about hiding the coupling.** I'd rather know
  the connections I need to have… What I'm optimising for is **cohesion**, and explicit dependencies
  serve that." A narrow consumer-declared type is Contract-level coupling by construction in
  [[khononov-coupling-should-be-weighed-not-counted|Khononov's]] Integration Strength scale.

Note this **permits what [[nick-tune-enforced-application-architecture-agents-humans|Tune's]] rule
forbids** — a slice may reach another module, provided it goes through a consumer-declared type and the
composition root. Dudycz's own line: "Rules that block a module from reaching another module are
useful. Rules that block it because two files sit at the same 'layer' are enforcing a layering you may
have already outgrown." Same goals, different grading of the same codebase.

His agent paragraph is appended to the design argument and framed as a bonus — "an old argument that
happens to have got more valuable" — and is, like the rest of this page's agent material, **assertion
rather than measurement**.

## The originator's own agent argument — and the objection it depends on (2026-09)

**[[jimmy-bogard]]** finally states the agent case for his own pattern
([[bogard-vertical-slice-architecture-webinar-recording-whats-next]], 2026-09-01): "we've made
**writing** code nearly free and left the cost of **verifying and changing** it exactly where it was…
**An agent doesn't read your architecture diagram. It reads your repo and copies what it finds.** That's
why structure matters more now, not less. Slices hold up under an agent because a change fits in one
context window, the blast radius stops at the slice boundary, and the tests still mean something after a
refactor." He is teaching it as **"effective guardrails for AI development."** Note the evidentiary
standing does not improve: the page's token/blast-radius argument now has four independent asserters
(Bogard, Miller, Dilger, Dudycz) and **still no measurement** — and Bogard's post is promotional for paid
training.

**And the condition under which none of it holds.** [[rico-fritzsche]]
([[fritzsche-vsa-does-not-fix-entity-centered-thinking]], 2026-08-28) is the counterweight this page
lacked: **"VSA improves locality *after* a team chooses a request boundary. It does not discover that
boundary. A CRUD-shaped request remains CRUD-shaped inside its own slice."** Noun folders over
`Create/Get/Update/Delete` are vertically organised and entity-centred at once, and "starting with the
record that changes makes the entity lifecycle the use-case boundary. That is an ownership problem" —
a charge he extends to Clean Architecture ("both preserve the same ownership problem"). So every claim
above — blast radius, one context window, parallel agents without collision — is **conditional on the cut
having followed a business operation**, which no enforcement rule can check. Mechanised boundaries make a
*bad* boundary permanent; neither Tune nor Bogard draws that consequence. See
[[entity-centric-thinking]].

_Sources: [[bogard-vertical-slice-architecture]] · [[miller-codebase-is-the-prompt-vertical-slices-ai]] · [[rico-fritzsche-autonomous-domain-capabilities-ccc]] · [[fritzsche-functional-core-imperative-shell-agentic-coding]] · [[rico-fritzsche-rpu-reactor-vocabulary]] · [[dilger-triplet-flexible-agent-enabled-architecture]] · [[nick-tune-enforced-application-architecture-agents-humans]] · [[dudycz-vertical-slices-ownership-and-external-dependencies]] · [[bogard-vertical-slice-architecture-webinar-recording-whats-next]] · [[fritzsche-vsa-does-not-fix-entity-centered-thinking]]._
