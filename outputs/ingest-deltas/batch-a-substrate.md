# Ingest deltas — Batch A "substrate" (2026-09-04)

**Scope.** 17 raw captures ingested; 17 new pages in `wiki/sources/` (all written, `raw_file:` keys
exact). This file is the work order for the **entity/concept** edits, which the orchestrator applies
serially. I touched nothing in `wiki/entities/`, `wiki/concepts/`, `index.md`, `overview.md`, `log.md`.

**Source pages created (for `index.md` / `log.md` housekeeping, item 27):**
`pellegrini-dcb-tag-dilemma` · `klijs-skilj-rust-dcb-library` ·
`khononov-ai-doesnt-fix-your-real-bottleneck` · `khononov-coupling-should-be-weighed-not-counted` ·
`bogard-vertical-slice-architecture-webinar-recording-whats-next` ·
`axoniq-government-ai-explainability-requirements` · `fritzsche-why-the-entity-model-is-an-illusion` ·
`fritzsche-how-event-sourcing-grows-with-the-business` · `fritzsche-thinking-in-events` ·
`fritzsche-the-entity-is-a-projection-not-a-row` ·
`fritzsche-event-sourcing-is-not-an-audit-feature` ·
`fritzsche-vsa-does-not-fix-entity-centered-thinking` · `dudycz-fixing-bugs-in-event-sourcing` ·
`dudycz-vertical-slices-ownership-and-external-dependencies` ·
`dudycz-backend-for-frontends-for-event-driven-apis` ·
`dudycz-archiving-events-stream-lifetime-slicing` · `dudycz-checklist-first-event-sourcing-feature`

## Conflicts this batch introduces (each is landed by a numbered item below — do not silently resolve)

1. **What a DCB tag *is*.** Pellegrini (originator): a tag is "the identifier of a historic route in the
   domain," semantically tied to the business rules. Dilger (already on the DCB page): tags are
   "indices, not domain concepts," absent from Discovery models. Fritzsche (already on the page): tags
   are an optional implementation optimization of a store-agnostic principle. Three different statuses
   for the same construct. → items 3, 11.
2. **Does the entity belong in software at all?** Fritzsche: no — the row is an illusion, the entity is a
   projection. Dudycz, same week: "business logic goes per entity or aggregate… slices don't each get a
   private notion of what an order is." Both are substrate primaries in this batch. → items 1, 2, 6, 7.
3. **Is event sourcing an audit capability?** AxonIQ (vendor, two captures) sells it as exactly that;
   Fritzsche says that motivation "has misunderstood its purpose"; Goeleven (already in KB) says audit
   isn't even free. → items 5, 13, 14.
4. **Fritzsche against himself, July vs August 2026.** "Thinking in Events" lists strong auditability
   among the reasons ES is compelling; the August note calls audit-motivated ES fundamentally wrong. His
   position **hardened over July–August**; neither month is his settled view. → items 1, 6.
5. **Retain forever, or archive by lifetime?** AxonIQ: public institutions carry history forward
   indefinitely, and that is the selling point. Dudycz: slice streams per lifetime, keep the summary
   event, archive the rest. → items 5, 14.
6. **Adopt where it's cheap, or where it hurts?** Dudycz's checklist selects for off-critical-path,
   reversible, "slightly rogue" features; AxonIQ advises starting where auditability matters most
   (interested party). → items 5, 14.

---

## 1. `wiki/concepts/entity-centric-thinking.md` — **CREATE**

*Why:* four captures in this batch argue one connected thesis (the entity is the root problem; the entity
is a projection not a row; ES is not an audit feature; VSA does not fix it). Without a page it smears
across four source pages and three concept pages, and the KB already has the symptom pages
(`autonomous-domain-capabilities`, `command-context-consistency`, `vertical-slice-architecture`) with no
page for the cause. Slug chosen to name the *problem*, so the page can hold counter-positions.

Paste as the whole file:

```markdown
---
title: Entity-Centric Thinking (and why it survives good architecture)
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-why-the-entity-model-is-an-illusion, fritzsche-the-entity-is-a-projection-not-a-row, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-vsa-does-not-fix-entity-centered-thinking, fritzsche-event-sourcing-is-not-an-audit-feature, fritzsche-thinking-in-events, dudycz-vertical-slices-ownership-and-external-dependencies, dudycz-fixing-bugs-in-event-sourcing]
tags: [entity-centric-thinking, business-capabilities, event-sourcing, vertical-slice-architecture, ddd, substrate, focus]
---

# Entity-Centric Thinking (and why it survives good architecture)

The habit of organising a system around **the things that change** (nouns, rows, entity lifecycles)
rather than around **what happens in the business** (operations, decisions, facts). Named as a single
problem by **[[rico-fritzsche]]** across four captures in Aug 2026, whose claim is that this habit —
not layering, not the wrong framework — is the root defect that other architectural moves fail to fix.

## The claim, in four steps

1. **The entity is an illusion.** "The database contains one row for each vehicle. The row resembles the
   vehicle itself, and is actually only the result of the last write. It holds the values that survived
   the last update and says nothing about how they got there"
   ([[fritzsche-why-the-entity-model-is-an-illusion]]). The tell: "almost every system has audit tables,
   history tables, status columns, timestamps and change logs" — workarounds for what the row destroys.
2. **The entity is a projection, not a row.** A physical vehicle exists; in the software there is only a
   **reference** (an ID, or an immutable natural attribute like a VIN) against which facts are recorded.
   "Every form that someone needs is derived from these events"
   ([[fritzsche-the-entity-is-a-projection-not-a-row]]). Perspectives are plural by design — purchasing
   and the repair shop want different views of the "same" thing.
3. **Mutation costs two things.** Load-mutate-write "(1) destroys the information about what happened,
   (2) turns every concurrent request into a conflict we have to defend against" — which is why this page
   connects to [[command-context-consistency]] and [[dynamic-consistency-boundaries]] and not only to
   modelling.
4. **The replacement unit is the capability.** `AcquireVehicle`, `ReceiveVehicle` are "autonomous,
   self-contained, and coherent… they share only the Application State" — an event store and the event
   definitions — "however, they know nothing about each other." See
   [[autonomous-domain-capabilities]] and [[business-capabilities]].

## Why good architecture doesn't fix it

The sharpest consequence, and the reason this page exists rather than a paragraph on another one:
**[[vertical-slice-architecture|VSA]] improves locality *after* a team chooses a request boundary; it
does not discover that boundary** ([[fritzsche-vsa-does-not-fix-entity-centered-thinking]]). Noun
folders with `Create/Get/Update/Delete` beneath them are vertically organised *and* entity-centred:
"Starting with the record that changes makes the entity lifecycle the use-case boundary. **That is an
ownership problem.**" The same charge lands on Clean Architecture: "Horizontal layers and vertical slices
arrange code differently. Both preserve the same ownership problem when entity lifecycles determine the
use cases."

His three-question design test (a heuristic, **not a study**): list the business changes a generic update
accepts; count how many slices depend on the shared entity model; change one business rule and observe
what else must move. Note that the last two are coupling measurements by inspection — the quantity
[[balanced-coupling]] formalises.

An event store does not fix it either: "If the stored events are named `ReservationUpdated`,
`GuestUpdated`, or `PropertyChanged`, the system may technically use Event Sourcing while still
preserving a CRUD-shaped understanding of the domain. **Storing vague events only preserves the vagueness
permanently**" ([[fritzsche-thinking-in-events]]). The messaging twin of the same failure is
[[oskar-dudycz|Dudycz's]] **"Poor Man's replication through the queue"** — publishing
`SthSthCreated/Updated/Deleted` as if they were events
([[dudycz-backend-for-frontends-for-event-driven-apis]], and see [[internal-vs-external-events]]).

## What it costs when it breaks

[[dudycz-fixing-bugs-in-event-sourcing]] is the operational bill for step 1. After a bad deploy, the row
holds a total with no record of the inputs that produced it, so the corrective migration must recompute
against *today's* configuration — repricing rows that were never wrong, and destroying the evidence
needed to check the fix, so "the input to migration three is the output of migration two." **A bug and a
deliberate human correction look identical: a number in a column. There's nothing to branch on.**
(Illustrative scenario, not measured data.)

## The counter-position, held on purpose

**The entity is not universally rejected.** [[oskar-dudycz]], in the same week, keeps it as a deliberate
rule: **"Business logic goes per entity or aggregate.** The rules about what states an order can be in and
which transitions are legal belong to the order. One place, and every slice that decides about an order
goes through it. **Slices don't each get a private notion of what an order is**"
([[dudycz-vertical-slices-ownership-and-external-dependencies]]). He agrees entirely on the *naming* half
— CRUD verbs give you nothing to slice along, name the business operation, and he cites [[greg-young]]'s
Task-Based UI for it — and disagrees on where rules live. Fritzsche argues from information loss; Dudycz
from cohesion. **The KB carries the disagreement rather than picking a winner.**

Related: [[sara-pellegrini]]'s "Kill Aggregate" line removes the aggregate as a *consistency* unit
([[dynamic-consistency-boundaries]]); Fritzsche removes the entity as a *modelling* unit. Both can hold;
neither implies the other.

## Evidence standing

**Weak, and uniformly so.** Every claim on this page is practitioner argument — position papers, LinkedIn
posts, and one worked vehicle-rental example authored by the person making the claim. No measurement, no
case study, no failed-adoption report, and the fuller article behind the VSA argument is **uncaptured**
(linked in a LinkedIn first comment, unresolved at capture). Read it as a well-articulated hypothesis
with a named counter-position, not a settled finding.

## Related

[[event-sourcing]] · [[event-modeling]] · [[business-capabilities]] ·
[[autonomous-domain-capabilities]] · [[command-context-consistency]] ·
[[vertical-slice-architecture]] · [[slice]] · [[cqrs]] · [[domain-driven-design]] ·
[[dynamic-consistency-boundaries]] · [[internal-vs-external-events]] · [[balanced-coupling]] ·
[[locality-of-reference]] · [[event-modeling-anti-patterns]]

_Sources: [[fritzsche-why-the-entity-model-is-an-illusion]] · [[fritzsche-the-entity-is-a-projection-not-a-row]] · [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-thinking-in-events]] · [[fritzsche-event-sourcing-is-not-an-audit-feature]] · [[dudycz-vertical-slices-ownership-and-external-dependencies]] · [[dudycz-fixing-bugs-in-event-sourcing]]._
```

---

## 2. `wiki/concepts/vertical-slice-architecture.md` — **UPDATE** (five edits, one file visit)

*Why:* this batch closes the page's own top open capture (Dudycz on VSA), resolves an un-ingested
reference it already carries, and adds the first statement from the pattern's originator connecting it to
agents — plus the counter-position that every agent claim on the page depends on.

**2a. Frontmatter.** Add to `sources:` (keep existing entries):
`dudycz-vertical-slices-ownership-and-external-dependencies, bogard-vertical-slice-architecture-webinar-recording-whats-next, fritzsche-vsa-does-not-fix-entity-centered-thinking`
and set `updated: 2026-09-04`.

**2b. Resolve the un-ingested pointer.** Anchor — line 130, exactly:

`  un-ingested). Tune does not put it in those terms; he simply reports that agents violate written`

Replace that line with:

`  now ingested as [[bogard-vertical-slice-architecture-webinar-recording-whats-next]]). Tune does not put it in those terms; he simply reports that agents violate written`

**2c. Replace the "What's open" body.** Anchor — the three lines under `## What's open / to capture next`:

`A source explicitly mapping VSA slices to Event Modeling slices and to agent task units — **Oskar`
`Dudycz**'s "Vertical Slices, CQRS, Semantic Diffusion" (flagged on the watch list) and the`
`verticalslicearchitecture.com material are the named candidates.`

Replace with:

```markdown
**Closed (2026-09-04):** the long-flagged Dudycz capture landed — not "Semantic Diffusion" but
[[dudycz-vertical-slices-ownership-and-external-dependencies]] (2026-08-10), which is the deeper
source. *Still open:* verticalslicearchitecture.com, the Codeartify webinar recording behind
[[bogard-vertical-slice-architecture-webinar-recording-whats-next]] (the argument's primary; the blog
post is its trailer), and the Medium article behind
[[fritzsche-vsa-does-not-fix-entity-centered-thinking]] (linked in a LinkedIn first comment, unresolved).
```

**2d. Append two new sections at the end of the body, before the closing `_Sources:` line:**

```markdown
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
```

**2e.** Append to the closing `_Sources:` line: `· [[dudycz-vertical-slices-ownership-and-external-dependencies]] · [[bogard-vertical-slice-architecture-webinar-recording-whats-next]] · [[fritzsche-vsa-does-not-fix-entity-centered-thinking]]`

---

## 3. `wiki/concepts/dynamic-consistency-boundaries.md` — **UPDATE** (four edits, one visit)

*Why:* the concept's **originator** has published for the first time since her 2023 naming post, and her
type-vs-tag argument is the missing mechanism for why a DCB selection can be wider than an aggregate. It
also puts her in direct tension with Dilger's "tags are indices" position already on the page.

**3a. Frontmatter.** Add `pellegrini-dcb-tag-dilemma, klijs-skilj-rust-dcb-library` to `sources:`;
`updated: 2026-09-04`.

**3b. Add the implementation entry.** Anchor — the line ending the tooling bullet:

`  *These are the canonical current implementations to capture if/when an in-window development lands.*`

Replace with:

```markdown
  *These are the canonical current implementations to capture if/when an in-window development lands.*
  **Added 2026-08-28:** **skilj** ([[klijs-skilj-rust-dcb-library]]) brings DCB to **Rust on PostgreSQL**
  — but at **v0.0.1**, author self-announced, **nothing evaluated**, and its capture's `source_url` is
  **RECONSTRUCTED and unverified** (the repo path as tweeted, `codeberg.org/gklijs/SklilJ`, does not match
  the crate name `skilj`). A signal that the store contract is spreading beyond the JVM/.NET, and nothing
  more than that.
```

**3c. Insert a new section immediately after the `## The idea` section (before
`## Where it sits / why it's in the focus`):**

```markdown
## Type and tag are orthogonal — the mechanism that makes a boundary wider than an aggregate (Pellegrini, 2026-03)

DCB's originator returns to define her own terms ([[pellegrini-dcb-tag-dilemma]]), and supplies the piece
this page was missing: *why* a DCB selection can span what an aggregate could not.

- **Event type = what happened.** `StudentSubscribedToCourse` "conveys the kind of thing that occurred,
  describing the fact without tying it to the specific entities involved." Type is also "semantically
  tied to the business logic," since events of one type are generally handled by the same logic.
- **Tag = which domain elements were involved** — formally, **"the identifier of a historic route in the
  domain,"** and "semantically tied to the **business rules**." A tag "captures a shared property across
  a set of facts": all events sharing it involve the same domain element, "concrete entity, or something
  more abstract."
- **The load-bearing paragraph:** the aggregate carried the same *meaning* of consistency boundary, but
  **"the limitation was that an aggregate is only one historic route. In reality, a single decision may
  advance more than one historic route. The tags of DCB make it possible for the consistency boundaries
  to involve more than one historical route."** And bringing type into the selection "avoids unnecessary
  collisions between things that are actually irrelevant."
- **Tag candidates are a domain-constraint decision, not a schema one.** Actor *and* target (student ID
  and course); and **context can be tagged** — on `UsernameChanged`, the *released* previous username
  should be a tag **if** the taken/available state matters when validating another user's claim.
- **Her one-sentence form:** "An event's type tells you what kind of thing happened; the tags tell you
  which historic routes were advanced by the event." Her closing rule is deliberately loose: "add a tag
  whenever you believe it will be a useful grouping key for protecting the consistency of your business
  model."

**Markers.** **NOT INDEPENDENT** — this is the concept's author defining her own construct:
authoritative on intent, not corroboration that tags are the right mechanism. **The piece contains no
measurements, benchmarks or claims of outcome**, and "historic route" is introduced without formal
definition while doing most of the argumentative work. Out-of-window backfill (2026-03).

### Three incompatible statuses for a tag — hold all three

| Source | A tag is… | Where it enters |
|---|---|---|
| [[sara-pellegrini]] ([[pellegrini-dcb-tag-dilemma]]) | a **domain-level identifier** of a historic route, semantically tied to the business rules | domain modelling, from domain constraints |
| [[martin-dilger]] ([[dilger-how-does-dcb-affect-event-modeling]]) | **"indices, not domain concepts"** | absent from Discovery; added in Detailed Modeling, "before handing the slice to an Agent" |
| [[rico-fritzsche]] ([[rico-fritzsche-es-does-not-require-aggregates-ccc-vs-dcb]]) | an **optional implementation optimization** of a store-agnostic principle ([[command-context-consistency]]) | nowhere necessarily — CCC names no store |

These are reconcilable in practice (an index whose keys happen to be domain identifiers) but they are not
the same claim about where tags belong in the process, and they imply different answers to "who decides
the tag set." Pellegrini's is the originator's view; Dilger's is the modelling-workflow view; Fritzsche's
demotes tags furthest.
```

**3d.** Add `· [[pellegrini-dcb-tag-dilemma]]` to the closing `_Sources:` line.

---

## 4. `wiki/concepts/internal-vs-external-events.md` — **CREATE**

*Why:* the KB has no page for the distinction between the events a system **stores** and the events it
**publishes**, and no home for "Poor Man's replication through the queue" — the single most useful
constraint this batch puts on the agent-EDA thread. It would otherwise have to hide inside
`event-driven-architecture`, which is about brokers.

Paste as the whole file:

```markdown
---
title: Internal vs External Events (and messages that aren't events)
type: concept
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-backend-for-frontends-for-event-driven-apis, fritzsche-thinking-in-events, axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember]
tags: [event-driven-architecture, event-sourcing, integration, coupling, substrate, focus]
---

# Internal vs External Events (and messages that aren't events)

The events a module **records** and the messages it **publishes** are different populations with
different design rules. Stated by **[[oskar-dudycz]]**
([[dudycz-backend-for-frontends-for-event-driven-apis]], 2026-08-29, #EventDrivenDiary) as an extension
of **backend-for-frontends**: we already accept that different API consumers need different surfaces —
"why don't we do the same for other types of APIs? For instance, an event-driven API?"

## Poor Man's replication through the queue

The failure mode he names, and the phrase worth keeping: teams satisfy "totally different customer needs
by publishing uniform events. What's worse, those events aren't actually events; most of the time,
**they're just state notifications: `SthSthCreated`, `SthSthUpdated`, `SthSthDeleted`.** I'm calling
them: **Poor Man's replication through the queue.**"

That is database replication wearing an event's clothes — and the messaging twin of
[[fritzsche-thinking-in-events|Fritzsche's]] "storing vague events only preserves the vagueness
permanently." Both authors, in the same fortnight, identify `SomethingUpdated` as the tell that the
domain's reasons have been discarded and only its mutations kept. See [[entity-centric-thinking]].

## The two splits

**1. Internal vs external events.**

- **Internal** (also *private*, *domain*) — "meaningful inside the module context… typically smaller and
  more focused, as internally we know our domain."
- **External** (also *public*, *integration*) — "meaningful in the whole system context," close to
  **pivotal events** from [[event-storming]] or to **summary events** (which do double duty as the
  archiving hinge — see [[event-sourcing]]).

**2. Messages are not only events** (Dudycz credits **Gregor Hohpe**, not captured in the KB):

- **State change** "just tells us what has changed; consumers won't know why this state changed or what
  has happened. This is useful for the data sync between modules" — a legitimate message type *provided
  you call it what it is*.
- **Commands** "represent the intention to perform a certain business operation; they're **directed, not
  broadcast** as events. They can also be **rejected**. If we mistake them for events, we end up with
  **passive-aggressive communication**, which can lead to dropped communication if we accidentally throw
  an error."

## The two failure modes

- "If we broadcast **all internal** events, we create a **leaking abstraction and a spider web of
  dependencies.**" (In [[khononov-coupling-should-be-weighed-not-counted|Integration Strength]] terms:
  Model- or Intrusive-strength coupling, to everyone at once.)
- "If we broadcast events while **ignoring other message types**, our communication looks like
  parliament: a room filled with shouting people. **This is a first step to a distributed monolith.**"

His framing principle: "We shouldn't lie to ourselves about our intentions, as that ends badly."

## Why this constrains the agent-EDA thread

[[agentic-event-driven-systems]] and its vendor sources ([[atlan-event-driven-architecture-for-ai-agents]],
[[confluent-agentic-event-driven-systems-architecture]],
[[solace-multi-agent-systems-real-time-context-eda]]) argue that agents should coordinate over events.
This page says **what those events must not be**: if inter-agent traffic is `AgentStateUpdated`
broadcasts, the architecture has bought a distributed monolith with extra latency and no explanation of
*why* anything happened. The commands-vs-events distinction — directed, rejectable — is precisely what
agent-to-agent protocols must get right ([[agent2agent-protocol]], [[multi-agent-orchestration]],
[[process-managers-and-todo-lists]]).

It also restates the [[axoniq-ai-agent-explainability-why-infrastructure-needs-to-remember|event store
vs. event stream]] line as a **modelling** decision rather than a product choice: AxonIQ separates them
by capability (a store records *why*, a stream moves *what*); Dudycz separates internal facts, external
integration messages and state sync by *intent*.

## Limits

A ~450-word LinkedIn post: definitions with no code and no worked example. **Nothing measured** — "the
common motive I see (in my past projects, in my client work)" is an experience report. It gives no
guidance on the hard part: how to *derive* an external event from internal ones, how to version the
public contract, or who owns it. Summary/pivotal events are referenced from uncaptured chapters of his
series, and Hohpe is cited second-hand.

## Related

[[event-driven-architecture]] · [[event-sourcing]] · [[cqrs]] · [[event-storming]] ·
[[coupling-taxonomy]] · [[balanced-coupling]] · [[vertical-slice-architecture]] ·
[[entity-centric-thinking]] · [[agentic-event-driven-systems]]

_Sources: [[dudycz-backend-for-frontends-for-event-driven-apis]] · [[fritzsche-thinking-in-events]]._
```

---

## 5. `wiki/concepts/event-sourcing.md` — **UPDATE** (frontmatter + four appended sections)

*Why:* this batch adds three things the page has never covered — **bad-data recovery** (as opposed to
schema change), **additive evolution as a mechanism**, and **stream lifetime / archiving** — plus a live
dispute about whether audit is the point.

**5a. Frontmatter.** Add to `sources:`:
`dudycz-fixing-bugs-in-event-sourcing, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-thinking-in-events, fritzsche-event-sourcing-is-not-an-audit-feature, dudycz-archiving-events-stream-lifetime-slicing, dudycz-checklist-first-event-sourcing-feature, axoniq-government-ai-explainability-requirements`
and `updated: 2026-09-04`.

**5b. Append before the closing `_Source pages:` line:**

```markdown
## Fixing bad data: fix forward, and the `buildSha` trick (Dudycz, 2026-07)

The standard objection — "you can't fix bad data in an immutable log" — gets its first proper answer in
the KB ([[dudycz-fixing-bugs-in-event-sourcing]]), by running one incident twice. **All figures in it are
an invented hotel-pricing scenario, not data.**

- **Why the state-based recovery compounds.** The row holds a total with no record of the inputs, so the
  migration must **recompute** — against a rate plan revised since the booking, repricing rows that were
  never wrong; and its `WHERE` clause cannot distinguish "changed" from "changed because of the bug."
  Migration two is then written against migration one's output: "If we get that wrong, the input to
  migration three is the output of migration two." Preparing a state-based system is possible (JSON
  breakdown, version column, `price_history` table, `corrected_by` marker) but each is added after the
  incident that taught you to — "what we're building at that point is a **partial event log, decided per
  column, under time pressure.**"
- **Why the event-sourced recovery doesn't.** `RatePlanApplied` still says v4 at 180.00; the per-night
  breakdown is still beside the wrong tax. The fix is a calculation, not a reconstruction — and if the
  *correction* is wrong, attempt three is still computed from the booking, not from attempt two.
- **`buildSha` in event metadata** — the commit the service was running when it appended the event, "an
  environment variable and a few lines in whatever builds our metadata." It makes blast radius exact
  (`WHERE metadata->>'buildSha' = 'a4f9c2e'` returns the events the broken binary produced and nothing
  else); `correlationId` groups one user action and `causationId` chains back to the command. A
  [[decision-trace]] primitive, directly reusable for agent-written events.
- **Fix forward, never rewrite** — append a corrective event (`previousTotal`, `correctedTotal`,
  `reason`), rebuild read models, fix the bug. "Having precise history, bugs included, is a valid
  scenario. It's often the only way to see later what really went wrong." If a clean stream is later
  needed for a regulator, **copy and transform into a new stream and keep the original.**
- **The argument that decides it** is not about arithmetic: a front-office agent had already corrected
  one reservation by hand with a goodwill discount. A blind bulk recalculation is *correct* and **undoes a
  deliberate human decision**. With a stream you can branch on it ("skip if any price-affecting event
  follows the bad one"); **"in the mutable model, a bug and a deliberate correction look identical: a
  number in a column. There's nothing to branch on."**
- **Make correction a feature.** Ask the business "how do you fix this today?", then model it —
  `CorrectReservationPrice` with permissions, validation and a **mandatory reason** — so the bulk fix runs
  through the same command as the front desk and "nobody connects to the production database at 23:00."
  His follow-up when told something can never happen: "fine, how often?"

Keep this distinct from [[event-versioning-and-upcasting]]: that is an event's *shape* changing; this is
an event's *value* being wrong.

## Additive evolution, and the schema you cannot design up front (Fritzsche, 2026-08)

[[fritzsche-how-event-sourcing-grows-with-the-business]] inserts a fifth step (`Inspect`) into a running
four-step flow and counts the change. "For events, the schema consists of a set of event types, and that
set **only grows**": a new event type, a new function, and a change to existing capabilities **only where
the new fact is relevant to their context** — `AcquireVehicle` and `ReceiveVehicle` untouched,
`InfleetVehicle` plus one fold case and one rule, **no data migration** ("vehicles already in the fleet
simply do not have a `VehicleInspected` event"). The mechanism is the **fold** (Greg Young, 2012:
"Current State is a Left Fold of previous behaviours"): each capability derives its own state from the
events its rules read, and "events that the rules do not read are not taken into account."

His statement of why this works is the most useful sentence: "**events are additive, since no reader needs
to know the big picture. Functions remain small because they derive their specific perspective precisely
from the events.**" Contrast the entity-centred path, where "every new step is a change to a shared
structure, because the database represents a global, shared, mutable state" (Kleppmann, 2014) and
normalization "must be complete before the first record is written" (Pat Helland, 2015). He is explicit
about where cost *does* land: a new projection "is new code with its own rebuild." One authored example,
no measurement, and the favourable case is chosen.

He also draws the method/store line the page should keep: **[[event-modeling]] is a modelling discipline,
event sourcing is a storage decision** ([[fritzsche-thinking-in-events]]), and the authority test decides
which you have — "if the current tables are authoritative and events only appear in the model, logs,
messages, audit trails, or integration notifications, the system may be event-aware or event-driven, but
it is not Event Sourcing." With the symmetric warning: "an event store does not guarantee a good model…
**storing vague events only preserves the vagueness permanently.**"

## Is history the point? — three positions, unresolved

- **[[axoniq]]** sells event sourcing *as* an audit and explainability capability in both captures, most
  fully in [[axoniq-government-ai-explainability-requirements]] (an interested party; its one number, an
  80% audit-prep reduction, is a **VENDOR SELF-REPORT** with the customer unnamed).
- **[[rico-fritzsche]]** rejects that motivation outright: "anyone who thinks Event Sourcing is an audit
  feature has misunderstood its purpose… the fact that the history is preserved is a **consequence** of
  that very property, but it is not the reason for it." His stated motivation is **independent domain
  capabilities not tied to a central shared data structure**
  ([[fritzsche-event-sourcing-is-not-an-audit-feature]],
  [[fritzsche-how-event-sourcing-grows-with-the-business]]). Note he is not wholly consistent — in July
  ([[fritzsche-thinking-in-events]]) he lists "strong auditability" among the conditions that make ES
  compelling; his position **hardened over July–August 2026**.
- **[[yves-goeleven]]** ([[goeleven-event-sourcing-not-auditing-for-free]]) attacks from a third side:
  auditing is not something the log hands you free.
- **[[oskar-dudycz]]** adds an oblique data point: his 14-question checklist for choosing a first
  event-sourced feature ([[dudycz-checklist-first-event-sourcing-feature]]) **never asks whether you need
  a history** — it selects on decision-shape (can a command be rejected for a business reason?),
  ownership, stream lifetime, and reversibility. Also note his adoption strategy is the **opposite** of
  the vendor's: off the critical path, "wrong for a day" survivable, reversible in a week, "small enough
  to do slightly rogue" — learn cheaply, rather than start where the pain is. His own disclaimer travels
  with it ("that's why I don't like checklists!"), and the fuller article is uncaptured.

## Storage does not grow forever — slice streams by lifetime (Dudycz)

[[dudycz-archiving-events-stream-lifetime-slicing]] answers the infinite-growth worry. First, often do
nothing: "event stores usually scale well with the number of streams. If they're not actively accessed
and are not long, then it's okay to keep them." Second, archiving need not be uniform — "you don't need
to have a uniform archiving strategy for all." Third, **slice streams per lifetime** ("bank account to
accounting period, point of sales to cashier shifts") and "keep just the **last summary event**, archive
the rest," so a reopening starts from the summary rather than the full history. The objection he takes
seriously is not storage but the **long legal tail** (invoice corrections, cashier-shift recalculations,
late-arriving data).

Two things to hold. **Stream lifetime is a modelling decision, not an ops setting** — the grain decides
whether archiving is ever possible. And it is in **tension with the retain-forever framing** of the audit
sources: [[axoniq-government-ai-explainability-requirements]] treats indefinite retention as the selling
point, while this treats it as a cost to manage — so indefinite retention is not a settled property of
event sourcing. It also bounds [[dudycz-fixing-bugs-in-event-sourcing]], which depends on old events
still being there; he does not draw that connection himself. (Distinct from a **snapshot**, which is a
performance device leaving history in place.) Caveats: ~300-word post, no mechanics, no cost figures, and
its date is a **repost** date at best.
```

**5c.** Append to the closing `_Source pages:` line:
`· [[dudycz-fixing-bugs-in-event-sourcing]] · [[fritzsche-how-event-sourcing-grows-with-the-business]] · [[fritzsche-thinking-in-events]] · [[dudycz-archiving-events-stream-lifetime-slicing]]`

---

## 6. `wiki/entities/rico-fritzsche.md` — **UPDATE**

*Why:* six new captures (three articles, three notes) — the largest single-author addition in the batch —
and his position visibly hardened in Aug 2026, which the page must record rather than overwrite.

**6a. Frontmatter.** Append to `sources:`:
`fritzsche-thinking-in-events, fritzsche-why-the-entity-model-is-an-illusion, fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-the-entity-is-a-projection-not-a-row, fritzsche-event-sourcing-is-not-an-audit-feature, fritzsche-vsa-does-not-fix-entity-centered-thinking`;
`updated: 2026-09-04`; add `entity-centric-thinking` to `tags:`.

**6b. Insert a new section immediately before `## In the KB`:**

```markdown
## Position — the entity itself is the problem (Jul–Aug 2026, six captures)

Through July–August 2026 his argument moves one level below capability ownership: not "the capability has
no home" but **"the entity was never the right unit."** Four captures argue one connected thesis, now
carried on [[entity-centric-thinking]]:

- **[[fritzsche-thinking-in-events]]** (2026-07-03) — the *mildest* of the set, and the KB's cleanest
  statement of **[[event-modeling]] ≠ [[event-sourcing]]**: one is a modelling discipline, the other a
  storage decision, and "confusing both turns a useful way of thinking into another technical
  prescription." Quotes [[adam-dymitruk]]'s "Events happen — whether we store them or not is our
  choice," insists on rigorous ubiquitous language (`ReservationUpdated` "preserves the mutation and
  loses the reason"), and warns symmetrically that "an event store does not guarantee a good model…
  **storing vague events only preserves the vagueness permanently.**" Note: here relational tables are a
  legitimate implementation of a good event model, and **auditability is listed as a reason to choose
  ES**.
- **[[fritzsche-why-the-entity-model-is-an-illusion]]** (2026-08-26) — the root article. The row "is
  actually only the result of the last write"; audit/history/status columns are workarounds for what it
  destroys; a physical thing has a **reference** in software, not an entity; the "Vehicle" is a
  **projection**, and different interests get different projections. Mutation costs two things: it
  destroys what happened, and it turns every concurrent request into a conflict.
  Companion LinkedIn post: **[[fritzsche-the-entity-is-a-projection-not-a-row]]** (the article is the
  fuller primary).
- **[[fritzsche-how-event-sourcing-grows-with-the-business]]** (2026-08-30) — the sequel and the most
  concrete piece he has published: inserts a fifth process step into a running system and counts the
  change. The **fold** per command context, "events that the rules do not read are not taken into
  account," the event-type set that only grows, and **no data migration**. Also his clearest formulation
  of why: "events are additive, since no reader needs to know the big picture."
- **[[fritzsche-vsa-does-not-fix-entity-centered-thinking]]** (2026-08-28) — the architectural corollary
  and the sharpest line: **"VSA improves locality after a team chooses a request boundary. It does not
  discover that boundary."** Noun folders + CRUD verbs are vertical *and* entity-centred; "that is an
  ownership problem"; and Clean Architecture has the same defect. **The fuller article is uncaptured**
  (linked in a LinkedIn first comment, unresolved at capture) — a named gap.
- **[[fritzsche-event-sourcing-is-not-an-audit-feature]]** (2026-08-31) — "anyone who thinks Event
  Sourcing is an audit feature has misunderstood its purpose"; history is a **consequence**, not a
  reason; the motivation is independent capabilities free of a central shared structure. "The problem
  with entity-centric thinking is **less of a technical nature.**"

**His position hardened — record it, don't average it.** In July, auditability is a legitimate reason to
choose ES and relational tables are fine; by late August, audit-motivated ES is "fundamentally wrong" and
the entity model is an illusion. He does not reconcile the two, so **no page should quote one month's
framing as his settled view.**

**Where he now disagrees with a KB peer.** [[oskar-dudycz]], in the same fortnight
([[dudycz-vertical-slices-ownership-and-external-dependencies]]), keeps "business logic per entity or
aggregate" as a deliberate rule while agreeing entirely on the naming half (CRUD verbs give you nothing
to slice along). Same diagnosis, opposite conclusion about where rules live.

**Evidence standing, unchanged:** position papers, LinkedIn posts and one authored vehicle-rental
example. No measurement, no case study, no counter-case. The blog-visibility note below still applies —
and all three LinkedIn captures in this batch were retrieved via **live logged-in Chrome**, with dates
accurate to the day only.
```

**6c.** Append the six new slugs to the closing `_Source pages:` line.

---

## 7. `wiki/entities/oskar-dudycz.md` — **UPDATE**

*Why:* five new captures move him from a two-page walk-on (Strictland, a fork post) to the KB's most
substantial substrate practitioner — and the page's own note that his VSA material is "a flagged
out-of-window source" is now out of date.

**7a. Frontmatter.** Append to `sources:`:
`dudycz-vertical-slices-ownership-and-external-dependencies, dudycz-fixing-bugs-in-event-sourcing, dudycz-backend-for-frontends-for-event-driven-apis, dudycz-archiving-events-stream-lifetime-slicing, dudycz-checklist-first-event-sourcing-feature`;
`updated: 2026-09-04`.

**7b. Replace the sentence beginning `Watch-listed in` and ending `on VSA↔slices.` (it spans three lines
in the opening paragraph) with:**

```markdown
Watch-listed in `watch-config.json`. **As of the 2026-09-04 batch he is the KB's most substantial
substrate practitioner**, with five captures spanning vertical slices, incident recovery, message design,
stream lifetime and adoption — superseding the earlier note that his VSA material was an out-of-window
gap ("Vertical Slices, CQRS, Semantic Diffusion", Aug-2025, remains uncaptured but is no longer the best
available source).
```

**7c. Insert before the closing `_Source pages:` line:**

```markdown
## Position — cohesion over independence, and the slice as a function (2026-08/09)

- **[[dudycz-vertical-slices-ownership-and-external-dependencies]]** (2026-08-10) — his substantive VSA
  primary. Fixes the vocabulary (**slice** = one piece of functionality, "more a function than an
  entity"; **module** = grouping of slices by "what changes together"; **bounded context** = a linguistic
  barrier, so a frontend and a backend are "two deployment targets"), then answers the question the
  pattern usually dodges: **"From inside a slice, there's one category of thing: external."** A slice
  declares **narrow function types in its own vocabulary**, satisfied structurally, composed by hand in
  one file near the entry point — no container. Module `api.ts` (what it *offers*) and consumer-declared
  need (what it *asks for*) are two directions across one boundary and you want both. Cycles dissolve
  because neither module imports the other. Persistence: **logic per entity/aggregate, read models per
  query, schemas per module.** And the stance that distinguishes him: "**independence isn't a value in
  itself**… hidden dependencies are still there, only harder to find. What I'm optimising for is
  **cohesion**."
- **[[dudycz-fixing-bugs-in-event-sourcing]]** (2026-07-27) — the KB's answer to "you can't fix bad data
  in an immutable log." Runs one pricing incident twice; introduces **`buildSha` in event metadata** for
  exact blast radius; **fix forward with a corrective event**, never rewrite; and the argument that
  actually settles it — a blind bulk recalculation is arithmetically correct and **undoes a human's
  deliberate goodwill correction**, because "in the mutable model, a bug and a deliberate correction look
  identical: a number in a column." Then: **make correction a feature** (a permissioned command with a
  mandatory reason), so "nobody connects to the production database at 23:00." *All figures are an
  invented scenario.*
- **[[dudycz-backend-for-frontends-for-event-driven-apis]]** (2026-08-29) — **"Poor Man's replication
  through the queue"**: `SthSthCreated/Updated/Deleted` published as if they were events. Splits
  **internal vs external** events and insists messages are also **commands** (directed, rejectable) and
  **state** (Hohpe). Anchors the new [[internal-vs-external-events]] page.
- **[[dudycz-archiving-events-stream-lifetime-slicing]]** — **slice streams per lifetime**, keep the last
  summary event, archive the rest; archiving strategy need not be uniform. (Date is a repost date at
  best.)
- **[[dudycz-checklist-first-event-sourcing-feature]]** (2026-09-01) — 14 questions for picking a first
  event-sourced feature, selecting for decision-shape, ownership, and **reversibility** ("off the critical
  path", "wrong for a day", "small enough to do slightly rogue"). He disclaims it himself ("that's why I
  don't like checklists!") and the fuller article is uncaptured.

**Register and interests.** Experience reports from client work, no measurement anywhere; he sells
consulting/training on these patterns (the VSA article closes with the offer). His agent claims are
appended to design arguments and framed as such — "an old argument that happens to have got more
valuable." The three LinkedIn captures came via **live logged-in Chrome**, dates day-accurate only.

**Where he disagrees with [[rico-fritzsche]]** (same fortnight): both reject CRUD-shaped operation names
and cite intent-carrying commands ([[greg-young]]'s Task-Based UI), but Dudycz **keeps the entity as the
home of business rules** where Fritzsche calls it an illusion. See [[entity-centric-thinking]].
```

**7d.** Append the five new slugs to the closing `_Source pages:` line.

---

## 8. `wiki/concepts/balanced-coupling.md` — **UPDATE** (four edits, one visit)

*Why:* the page's standing want is "a first-party capture of the book's own text on the BALANCE formula
and the Integration Strength definitions." Two Feb-2026 blog posts get most of the way there — and one of
them is the actual source of the triad the page attributes to the book.

**8a. Frontmatter.** Add `khononov-ai-doesnt-fix-your-real-bottleneck, khononov-coupling-should-be-weighed-not-counted`
to `sources:`; `updated: 2026-09-04`.

**8b. Insert immediately after the `## The three dimensions` section (before
`## The dimensions in detail (from the 2024 book)`):**

```markdown
**First-party statement of the triad (2026-02).** The three dimensions above were sourced to the book and
the [[coupling-research-note]]; [[khononov-ai-doesnt-fix-your-real-bottleneck]] states them in the
author's own current words, and names the first axis **"shared knowledge"** rather than *strength*: "the
knowledge components share about each other. The more knowledge is shared, the higher the likelihood that
a change in one will trigger cascading changes in others." Distance is "physical **and
organizational**"; volatility is "the probability that a component will need to change in the first
place. High volatility amplifies design problems; low volatility neutralizes them." His balance rule, in
prose: components that change together are located close; components that don't are spread apart; and
"ultimately, **volatility multiplies** the effects of complexity." Same model, and the terminology drift
(shared knowledge ≈ Integration Strength) is worth knowing when reading him. **NOT INDEPENDENT** — the
model's own author, closing with his own book via an affiliate link. **No data in either post.**
```

**8c. Insert after the Integration Strength table, before the `**Distance**` paragraph:**

```markdown
**Why weigh rather than count (2026-02, first-party prose).**
[[khononov-coupling-should-be-weighed-not-counted]] gives the four levels in his own words and the
argument for the scale's existence: each level down "removes an *entire category* of shared reasons for
change," which is why "a single intrusive dependency can cause more cascading changes than a hundred
contract-based ones." His illustration: a component with 1 outgoing and 100 incoming dependencies scores
~0.01 on `I = Ce / (Ce + Ca)` — "textbook stability" — while its one outgoing dependency reaches into
another component's internals (a service reading another service's database) and the 100 incoming ones go
through stable contracts. "The metric says: rock-solid stability. Reality says: ticking time bomb." Each
level restated: **intrusive** = "you have to assume that *all* knowledge is shared… reasons for cascading
changes are essentially unbounded"; **functional** = "switches from 'how?' to 'what'" (the same rule
implemented twice); **model** = "shifts from logic to structure… entities, relationships, and concepts";
**contract** = "the contract encapsulates everything behind it… only modifications to the contract itself
propagate."

The generalisable warning: "Static analysis tools count because counting is easy to automate. But easy to
automate and useful are not the same thing. A metric that treats use of reflection to modify a private
field and an API call as equivalent is likely to point you in the wrong direction." Worth reading against
the KB's measurement-based sources — [[tornhill-codescene-unhealthy-code-agentic-token-cost]] (**VENDOR
SELF-REPORT** figures), [[fitness-functions]], [[fowler-bockeler-maintainability-sensors]] — as the
sharpest sceptical frame on automatable design metrics the KB has. Caveats: **NOT INDEPENDENT**; the
100-dependency component is a **constructed illustration**; "in my experience, chasing those metrics never
really made the design more modular" is a **practitioner self-report**; and the post never addresses the
obvious rejoinder that direct DB access *is* automatically detectable.
```

**8d. Update the "To capture next" section.** Anchor the sentence beginning
`*Still wanted:* a first-party capture of the book's own text on`. Replace that sentence with:

```markdown
*Partly closed (2026-09-04):* [[khononov-coupling-should-be-weighed-not-counted]] gives the Integration
Strength definitions in the author's own prose, and [[khononov-ai-doesnt-fix-your-real-bottleneck]] the
triad and balance rule. *Still wanted:* the book's own text on the **BALANCE formula** (neither post
states it), and a resolution of the **per-site → per-partition** scoring gap.
```

**8e.** Append `· [[khononov-ai-doesnt-fix-your-real-bottleneck]] · [[khononov-coupling-should-be-weighed-not-counted]]` to the closing `_Sources:` line.

---

## 9. `wiki/entities/vlad-khononov.md` — **UPDATE**

*Why:* two new captures, and one is a distinct position the page does not carry — the
Theory-of-Constraints argument that **comprehension, not code production, is the bottleneck**.

**9a. Frontmatter.** Add both Khononov slugs to `sources:`; `updated: 2026-09-04`; add
`comprehension-debt` to `tags:`.

**9b. Insert immediately after the `## Position — boundaries are the thing AI depends on` section:**

```markdown
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
([[khononov-coupling-should-be-weighed-not-counted]]) covers **only the Integration Strength axis**; the
triad above belongs to this post, not that one.
```

**9c.** Append both slugs to the closing `_Source pages:` line.

---

## 10. `wiki/concepts/comprehension-debt.md` — **UPDATE**

*Why:* the page is entirely practitioner-derived (Osmani's coinage, Dilger's ledger anecdote, Ng's role
argument). Khononov supplies the first *theoretical derivation* of the same phenomenon, which changes how
much weight the concept can carry.

**10a. Frontmatter.** Add `khononov-ai-doesnt-fix-your-real-bottleneck` to `sources:`;
`updated: 2026-09-04`; add `balanced-coupling` to `tags:`.

**10b. Insert as a new section immediately before `## It shows up on the ledger, not the tooling invoice (Dilger, 2026-07)`:**

```markdown
## Derived, not just observed — the Theory-of-Constraints version (Khononov, 2026-02)

[[khononov-ai-doesnt-fix-your-real-bottleneck]] reaches this concept from design theory rather than from
watching a loop run, which is worth having because everything else on this page is observation. His
argument: throughput is set by the single bottleneck, so **improving a non-bottleneck makes the system
worse** — more work-in-progress piled in front of the constraint, "more inventory. More cost. More
waste." The bottleneck in software is **"our ability to comprehend systems"**, capped by working memory.
Therefore AI-accelerated code production is textbook over-production upstream of the constraint, and "the
Theory of Constraints predicts exactly what happens next: the system degrades."

Two things this adds:

- **Comprehension debt becomes a predicted consequence rather than an observed surprise.** Osmani's
  reckoning is "quiet and late"; Khononov says it is *inevitable* given the queue shape — which is why
  [[dilger-real-cost-of-ai-is-second-order|Dilger's]] ~30%-at-flat-headcount anecdote and the
  [[dora-roi-ai-assisted-software-development-2026|DORA]] J-curve are what the model expects, not
  anomalies.
- **A different remedy.** The page's defences are read-the-diffs, move judgment upstream, stay fluent.
  Khononov's is **modularity** — reduce the cognitive load the system *induces*, by balancing
  [[balanced-coupling|shared knowledge × distance × volatility]] so that "when you need to make a change,
  you know exactly which components are affected, and the outcome." Reading pays the debt down;
  modularity slows the rate at which it is incurred. His P.S. blocks the obvious shortcut: "generating
  code that *looks* modular and designing a system that *is* modular are two very different things…
  **that's not a prompting problem.**"

**Markers:** **NOT INDEPENDENT** (his own model and book, affiliate-linked) and **IMPRESSION NOT
MEASUREMENT** — the argument is analytical throughout, and the 4±1 / 7±2 working-memory figures are cited
as "studies" **with no reference on the page**. Do not promote them to citable findings.
```

**10c.** Add `[[khononov-ai-doesnt-fix-your-real-bottleneck]] · [[vlad-khononov]] ·` to the `## Related`
list.

---

## 11. `wiki/entities/sara-pellegrini.md` — **UPDATE**

*Why:* the page has one source (2023) and describes her only historically. Her first substantial new
capture in the KB deserves recording, along with the fact that she is now in explicit tension with two
other KB voices on what a tag is.

**11a. Frontmatter.** Add `pellegrini-dcb-tag-dilemma` to `sources:`; `updated: 2026-09-04`; add
`substrate` to `tags:`.

**11b. Insert before the final `_Source pages:` line:**

```markdown
## Still publishing on DCB — the tag argument (2026-03)

[[pellegrini-dcb-tag-dilemma]] (Event Thinking, 2026-03-05) is her first substantial capture in the KB
since the naming post, and it supplies the mechanism the [[dynamic-consistency-boundaries]] page was
missing. **Type and tag are orthogonal dimensions of one fact:** the type is "the nature of the fact
itself: what happened"; a tag is **"the identifier of a historic route in the domain,"** semantically
tied to the *business rules* rather than to storage. Hence the payoff over the aggregate, in her words:
"the limitation was that **an aggregate is only one historic route**. In reality, a single decision may
advance more than one… The tags of DCB make it possible for the consistency boundaries to involve more
than one historical route." Involving types in the selection "avoids unnecessary collisions between
things that are actually irrelevant." Tags can mark actor, target, or **context** (the previous username
released by a `UsernameChanged` event, if username availability is a constraint elsewhere).

**Note where this puts her against the KB's other DCB voices.** She treats a tag as a **domain-level**
construct; [[martin-dilger]] treats tags as "indices, not domain concepts" added late in modelling; and
[[rico-fritzsche]] demotes them to an optional implementation optimization of a store-agnostic principle.
Three statuses for one construct — see the comparison table on [[dynamic-consistency-boundaries]].

**Markers:** **NOT INDEPENDENT** as corroboration that tags are the right mechanism (she originated the
concept — authoritative on intent), and the piece **contains no measurements, benchmarks or outcome
claims** at all. Also an **out-of-window backfill** (2026-03), not a new development.
```

**11c.** Append `· [[pellegrini-dcb-tag-dilemma]]` to the closing line.

---

## 12. `wiki/entities/jimmy-bogard.md` — **UPDATE**

*Why:* the page says he is "still shipping AutoMapper/MediatR" and nothing about the pattern's agent-era
life. His own first statement on that is now captured.

**12a. Frontmatter.** Add `bogard-vertical-slice-architecture-webinar-recording-whats-next` to `sources:`;
`updated: 2026-09-04`; add `agentic-coding` to `tags:`.

**12b. Insert before the `## Related` section:**

```markdown
## Now teaching VSA as AI guardrails (2026-09)

[[bogard-vertical-slice-architecture-webinar-recording-whats-next]] (2026-09-01) is the first time the
KB has **the pattern's originator** connecting it to agentic development: a Codeartify webinar with 700+
registrations titled *"Vertical Slice Architecture: Effective Guardrails for AI Development"*, plus a
six-hour two-part course and a Zurich workshop (17–18 Nov). His argument in three sentences: "we've made
**writing** code nearly free and left the cost of **verifying and changing** it exactly where it was…
**An agent doesn't read your architecture diagram. It reads your repo and copies what it finds.** That's
why structure matters more now, not less. Slices hold up under an agent because a change fits in one
context window, the blast radius stops at the slice boundary, and the tests still mean something after a
refactor."

That middle sentence is the KB's best one-line statement of why an advisory boundary fails and a
structural one doesn't — the missing rationale under
[[nick-tune-enforced-application-architecture-agents-humans|Tune's build-time enforcement]]. Caveats: a
~350-word promotional post selling training, **no measurement**, and the substance is in an uncaptured
recording. The condition it omits is [[fritzsche-vsa-does-not-fix-entity-centered-thinking|Fritzsche's]]:
a CRUD-shaped slice bounds nothing.
```

**12c.** Append `· [[bogard-vertical-slice-architecture-webinar-recording-whats-next]]` to the closing
line.

---

## 13. `wiki/entities/axoniq.md` — **UPDATE**

*Why:* second AxonIQ capture, with a materially wider regulatory survey, a new adoption posture
(brownfield now recommended rather than roadmap), and one number that must carry a vendor marker
wherever it travels.

**13a. Frontmatter.** Add `axoniq-government-ai-explainability-requirements` to `sources:`;
`updated: 2026-09-04`; add `public-sector` to `tags:`.

**13b. Insert before the `## Related` section:**

```markdown
## Second capture — the public-sector argument (2026-08-31)

[[axoniq-government-ai-explainability-requirements]] is the same thesis aimed at government, with three
additions worth recording:

- **The widest regulatory survey in the KB** — nine jurisdictions (US FOIA + federal AI guidance + state
  algorithmic-accountability laws; Canada's Directive on Automated Decision-Making; EU AI Act + GDPR; UK
  AI framework + Algorithmic Transparency Recording Standard; South Korea, Singapore, Japan; Australia's
  voluntary guardrails; New Zealand's Algorithm Charter; Brazil's PL 2338/2023). **AxonIQ's reading of
  the instruments, not verified against primary law.**
- **Two arguments beyond the earlier post:** explainability as **legitimacy** ("a government that cannot
  explain itself is a government asking to be trusted on faith"), so the regulatory patchwork is "a
  symptom rather than a subject"; and **institutional memory on government timescales** ("private
  companies archive for seven years and move on"), with decisions questioned "by an oversight body that
  does not yet exist, under a legal standard that has not yet been set."
- **Brownfield is now the recommended path**, not a roadmap item: adopt incrementally, start where
  auditability matters most, run alongside existing systems. Named reference: the **Indiana Department of
  Workforce Development** modernization (AxonIQ's own use-case page).

**The one figure — and it must never travel without this marker:** "a large U.S. bank… **reduced audit
preparation time by 80 percent** after moving to an event-sourced foundation" is a **VENDOR SELF-REPORT**
— unnamed customer, no methodology, no baseline — despite the post's phrase "the results are measurable."
Also note the **event store vs. event stream** distinction that made the first post sharp is **absent
here**; this post argues against state-based storage, not against Kafka. Corporate byline (no named
author), and it closes with a sales CTA. The standing counter-position on framing ES as an audit
capability is [[fritzsche-event-sourcing-is-not-an-audit-feature]] and
[[goeleven-event-sourcing-not-auditing-for-free]]; its retain-forever framing is also in tension with
[[dudycz-archiving-events-stream-lifetime-slicing]].
```

**13c.** Append `· [[axoniq-government-ai-explainability-requirements]]` to the closing line and add
`[[agent-governance]]` to `## Related`.

---

## 14. `wiki/concepts/agent-explainability.md` — **UPDATE**

*Why:* the page's regulatory grounding is three instruments from one vendor post; this batch multiplies
it, and adds the public-sector-specific driver no other source covers.

**14a. Frontmatter.** Add `axoniq-government-ai-explainability-requirements` to `sources:`;
`updated: 2026-09-04`.

**14b. Insert as a new section immediately before the `## Caveat` section:**

```markdown
## The regulatory map, widened — and where it comes from (AxonIQ, 2026-08)

[[axoniq-government-ai-explainability-requirements]] takes the page's three instruments (EU AI Act, SR
11-7, GDPR Art. 22) to roughly a dozen across nine jurisdictions: US FOIA and records-retention rules
plus federal AI guidance and state algorithmic-accountability laws; **Canada's Directive on Automated
Decision-Making** (impact assessment and meaningful explanations, scaled by impact level); the EU AI Act
layered over GDPR and national administrative law's duty to give reasons; the **UK's Algorithmic
Transparency Recording Standard**; South Korea's AI framework law, Singapore's Model AI Governance
Framework, Japan's national guidelines; Australia's voluntary guardrails pending mandatory high-risk
ones; New Zealand's **Algorithm Charter**; Brazil's PL 2338/2023. AxonIQ's framing: "None of these
frameworks asks it in quite the same words, but the direction is clear" — and an agency treating each as
a separate compliance project "will run that project forever."

It also supplies a driver specific to the public sector that no other KB source carries: **explainability
as legitimacy** rather than compliance, and **retention on institutional timescales** — a decision
questioned "in a decade, by an oversight body that does not yet exist, under a legal standard that has
not yet been set," where "institutional memory lives in retired databases, departed employees, and file
formats nobody can open."

**Read it as a checklist of instruments to verify, not as a statement of obligation:** this is a
**vendor's** reading (AxonIQ sells an event store), unverified against primary law here, with a corporate
byline. Its single number — an 80% reduction in audit-preparation time at an unnamed large US bank — is a
**VENDOR SELF-REPORT** and must carry that marker at every use. And the post contains **no agent-specific
evidence**: the AI section is argument, with nothing measured about an agent decision being explained.
```

**14c.** Add `[[axoniq-government-ai-explainability-requirements]]` to the `## Related` list.

---

## 15. `wiki/entities/gerard-klijs.md` — **CREATE**

*Why:* the author of the first Rust DCB implementation now appears in the KB and is linked from two pages;
without a stub the link dangles and the v0.0.1 / unverified-URL caveats have nowhere to live.

Paste as the whole file:

```markdown
---
title: Gerard Klijs
type: entity
created: 2026-09-04
updated: 2026-09-04
sources: [klijs-skilj-rust-dcb-library]
tags: [person, event-sourcing, dcb, rust, tooling]
---

# Gerard Klijs

Developer (`@GKlijs` on X) and author of **skilj**, a **Rust** library for event-sourced applications on
**PostgreSQL** that uses **[[dynamic-consistency-boundaries|Dynamic Consistency Boundary]] instead of the
classic aggregate pattern** — announced 2026-08-28 at **v0.0.1**
([[klijs-skilj-rust-dcb-library]]). His pitch: "No more sagas for rules that span two entities."

**Everything the KB knows about him comes from one two-tweet self-announcement**, so treat this page as a
stub. Three caveats travel with it:

- **VENDOR SELF-REPORT / author self-announcement** — the saga-elimination claim is a design pitch, not a
  demonstrated result, and **nothing about the library has been independently evaluated**.
- **v0.0.1**, "early days" by his own description; the post is a request for feedback "especially from
  anyone who's hit the aggregate-boundary problem before."
- **The capture's `source_url` is RECONSTRUCTED and unverified** (X returned the status link as
  blocked/base64 content); the handle, timestamps and text *are* observed. The repo path as tweeted,
  `codeberg.org/gklijs/SklilJ`, **does not match** the crate name `skilj` (`crates.io/crates/skilj`) —
  unresolved. **Resolve both before citing a URL.**

In the KB he matters only as a signal that the **DCB store contract is spreading beyond the JVM
([[axoniq]]'s Axon Framework 5) and .NET ([[critter-stack]]'s Marten 9.0)** — a much weaker signal than
either. Notably, the capture says nothing about the concurrency contract
([[fritzsche-ccc-atomic-append-serialized-write-order|serialized write order]]), which is where an
evaluation of a Postgres-backed DCB library should start.

## Related

[[dynamic-consistency-boundaries]] · [[event-sourcing]] · [[sara-pellegrini]] ·
[[command-context-consistency]]

_Source pages: [[klijs-skilj-rust-dcb-library]]._
```

---

## 16. `wiki/concepts/event-versioning-and-upcasting.md` — **UPDATE**

*Why:* the page is where readers look for "how do I fix events" and currently only covers *shape* change.
The distinction between shape and value is worth stating explicitly, with a pointer.

**16a. Frontmatter.** Add `dudycz-fixing-bugs-in-event-sourcing` to `sources:`; `updated: 2026-09-04`.

**16b. Insert immediately before the `## Related` section:**

```markdown
## Not the same problem: an event whose *value* is wrong

Versioning and upcasting are about an event's **shape** changing. A separate and more common Tuesday
morning problem is an event whose shape is fine and whose **value** is wrong — a bad deploy wrote a
miscalculated number. [[dudycz-fixing-bugs-in-event-sourcing]] treats that case, and the answer is not an
upcaster: **append a corrective event** (the accountant's correcting entry — `previousTotal`,
`correctedTotal`, `reason`), rebuild the read models, fix the bug, and **never edit in place** ("having
precise history, bugs included, is a valid scenario"). If a clean stream is genuinely needed later, copy
and transform into a **new** stream and keep the original.

Two techniques from it belong on this page:

- **`buildSha` in event metadata** — record the commit the service was running when it appended. Then the
  blast radius of a bad deploy is a query (`WHERE metadata->>'buildSha' = '…'`) rather than a guessed
  `WHERE` clause over timestamps, which is exactly the failure that makes state-based corrective
  migrations compound. `correlationId`/`causationId` do the same job for diagnosis.
- **Model the correction as a capability** — a permissioned `CorrectReservationPrice` command with a
  mandatory reason, so bulk fixes and front-desk fixes emit the same events. The same "add a slice rather
  than change the past" instinct as [[dilger-done-is-done-open-closed-new-slice|"Done is Done"]], applied
  to operations — and it composes with
  [[fritzsche-how-event-sourcing-grows-with-the-business|additive evolution]]: a correction is just
  another event type.

*Caveat: an invented hotel-pricing scenario throughout; `buildSha` is advice, not a reported practice.*
```

**16c.** Add `· [[dudycz-fixing-bugs-in-event-sourcing]]` to the closing `_Sources:` line, and
`[[decision-trace]]` to `## Related`.

---

## 17. `wiki/concepts/slice.md` — **UPDATE**

*Why:* the page exists to disambiguate the model unit from the code unit. Dudycz adds a third precise
definition plus the module/context vocabulary — exactly what a disambiguation page should carry.

**17a. Frontmatter.** Add `dudycz-vertical-slices-ownership-and-external-dependencies` to `sources:`;
`updated: 2026-09-04`.

**17b. Insert immediately after the `## Two senses of the word` section:**

```markdown
### A third precise definition, plus the words around it (Dudycz, 2026-08)

[[dudycz-vertical-slices-ownership-and-external-dependencies]] argues most slice confusion is vocabulary,
and gives three definitions that are useful precisely because they are narrower than usual:

- **Slice** — "one piece of functionality, cut through the whole application… **For me, a slice is more a
  function than an entity.** *'Verify a transport order'* is a slice. It has a way in, some business
  logic, and whatever it reads and writes. If you're thinking of it as a thing with a lifecycle, you're
  probably thinking of an entity, **which is a different concept that lives within the slice's reach
  rather than being the slice.**"
- **Module** — "a logical grouping of slices… the criterion I use is **what changes together**."
- **Bounded context** — "a **linguistic barrier**… a set of functionality that the business uses the same
  vocabulary for." Consequences: "a frontend and a backend aren't two bounded contexts; they're two
  **deployment targets**", and "seven features of one application are almost always slices, or at most
  modules, sitting inside a single context. That's good news, because it means **they were never obliged
  to be autonomous.**" He is also willing to drop the term: "If the word causes arguments on your team,
  drop it and talk about which functionalities share a vocabulary."

**Slice-as-function is the sharpest available statement of what this page disambiguates**: the
Event-Modeling slice is a step in a process, Bogard's is a request cut through the layers, and Dudycz's is
a *function with declared dependencies*. All three exclude the reading that causes the trouble — a slice
as a noun with a lifecycle. Compare [[fritzsche-vsa-does-not-fix-entity-centered-thinking]]: folders named
after nouns with CRUD verbs beneath them are exactly the entity-with-a-lifecycle reading, wearing slice
clothing.
```

**17c.** Append `· [[dudycz-vertical-slices-ownership-and-external-dependencies]]` to the page's sources
line and add `[[entity-centric-thinking]]` to `## Related`.

---

## 18. `wiki/concepts/cqrs.md` — **UPDATE**

*Why:* the page has read/write separation as theory plus one production reference. Dudycz gives the
crispest practical rule for the read side and a naming argument for the write side.

**18a. Frontmatter.** Add `dudycz-vertical-slices-ownership-and-external-dependencies` to `sources:`;
`updated: 2026-09-04`.

**18b. Insert before the closing `_Source pages:` line:**

```markdown
**Read models per query, and why naming the command is the whole game (Dudycz, 2026-08).**
[[dudycz-vertical-slices-ownership-and-external-dependencies]] states the read-side rule in one line —
"**Read models go per query.** This is where a table per feature is right… Build a table that answers
that. The settlement report needs something else and gets its own. **Resist making a single query serve
five screens by expanding columns**" — while keeping write-side logic per entity/aggregate and schemas per
module. On the write side he grounds command-as-intent in [[greg-young]]'s **Task-Based UI**: when the
client posts data-centric structures, "the domain has no verbs, and the user's intent is lost on the way
in." The consequence: "If every operation is 'update the order', you have one feature and nothing to
divide. Once you have `VerifyOrder`, `ConfirmOrder`, `RejectOrder`, you have folders." **And it applies
without event sourcing: "the name is the value, and the underlying implementation can be a single
`UPDATE`."** A status column "records that the order is verified. It doesn't record that anybody verified
it."

Two more, from the same source: **return the available actions with the data** rather than letting the
frontend re-derive them from status fields ("the part of HATEOAS I find useful, without the rest of the
ceremony"); and a **backend-for-frontend is a legitimate slice** — "it's named after a screen because
that's honestly what it is" — since "one screen is routinely composed of data gathered from several
modules." *Experience report, no measurement.*
```

**18c.** Append the slug to the closing `_Source pages:` line.

---

## 19. `wiki/concepts/event-modeling.md` — **UPDATE**

*Why:* Fritzsche gives the KB its cleanest statement of the method/store boundary, from a non-advocate,
plus the sharpest available warning that adopting an event store does not buy you a good model.

**19a. Frontmatter.** Add `fritzsche-thinking-in-events` to `sources:`; `updated: 2026-09-04`.

**19b. Insert before the page's closing sources line:**

```markdown
## Event Modeling does not require Event Sourcing (Fritzsche, 2026-07)

[[fritzsche-thinking-in-events]] is the source to cite for the boundary: "Event Modeling describes
behavior. Event Sourcing decides how state is persisted," and confusing them "turns a useful way of
thinking into another technical prescription." He anchors it on [[adam-dymitruk]]'s own line — **"Events
happen — whether we store them or not is our choice"** — and notes Dymitruk demonstrates EM against table
storage. The test for which you have is **where authority lives**: "If the current tables are
authoritative and events only appear in the model, logs, messages, audit trails, or integration
notifications, the system may be event-aware or event-driven, **but it is not Event Sourcing.**"

Two further contributions:

- **Why a model is less forgiving than a schema.** "A table can contain a status column without
  explaining who is allowed to change the status, when the change is valid, or which consequence
  follows… An Event Model is less forgiving because **every fact has to stand in the timeline and explain
  its place.**" Naming a fact forces the next questions (who cancelled, before or after the
  free-cancellation window, does availability return, is a refund due) — the [[given-when-then]] material
  this page already carries, stated from the naming side. `ReservationUpdated` "preserves the mutation
  and loses the reason."
- **The symmetric warning.** "An event store does not guarantee a good model. If the stored events are
  named `ReservationUpdated`, `GuestUpdated`, or `PropertyChanged`, the system may technically use Event
  Sourcing while still preserving a CRUD-shaped understanding of the domain. **Storing vague events only
  preserves the vagueness permanently.**" A vocabulary-level anti-pattern that survives adopting the
  right technology — complementing [[event-modeling-anti-patterns]] (which grades board *shape*) and
  paralleling [[internal-vs-external-events|"Poor Man's replication through the queue"]] on the messaging
  side.

He also separates EM from [[event-storming]] on purpose: Storming "is mainly used to explore the problem
space"; EM "takes the discovered behavior and describes how the system should work over time." *No
measurement, no agent content; a definitional essay with a booking-domain illustration, and its
Fowler/Dymitruk/Azure citations are second-hand.*
```

**19c.** Append `· [[fritzsche-thinking-in-events]]` to the closing sources line.

---

## 20. `wiki/concepts/command-context-consistency.md` — **UPDATE**

*Why:* CCC has been stated as a principle and a guard; this batch supplies the fold as working code, which
is what a reader trying to apply it needs.

**20a. Frontmatter.** Add `fritzsche-how-event-sourcing-grows-with-the-business` to `sources:`;
`updated: 2026-09-04`.

**20b. Insert before the page's closing sources line** (outer fence is `~~~~` here only so the inner
C# fence survives the copy — paste the content between the `~~~~` markers):

~~~~markdown
## The fold, as code (2026-08)

[[fritzsche-how-event-sourcing-grows-with-the-business]] shows the context-building step the principle
describes: "Each domain capability comes with its own command context. The context defines the scope and
what is needed to process a request… the capability has to query a relevant list of events and derive the
state from it. This functional operation is called a **fold**" — Greg Young, 2012: *"Current State is a
Left Fold of previous behaviours."*

```csharp
var state = events.Aggregate(InfleetState.Empty, (s, e) => e switch
{
    VehicleReceived r => s with { Received = true, Vin = r.Vin },
    VehicleInfleeted  => s with { Infleeted = true },
    _                 => s
});
```

The two disciplines that make it CCC rather than a small aggregate: **"events that the rules do not read
are not taken into account"** (so the context is exactly what the decision needs, never wider — the same
"cover the context and never less" rule this page states for the guard), and the state is **transient**:
"it is created, the rules are applied to it, and the result is one or more new events." Two capabilities
over the same events fold different subsets — "there is no shared vehicle object that both would need to
share."

Consequence for evolution: adding a fact means adding a fold case and a rule **only in the capabilities
that need it** ("`AcquireVehicle` and `ReceiveVehicle` remain unchanged, since they do not require the
information from the new event type"). *One authored example; no measurement.*
~~~~

**20c.** Append the slug to the closing sources line and add `[[entity-centric-thinking]]` to the related
links.

---

## 21. `wiki/concepts/business-capabilities.md` — **UPDATE**

*Why:* the page's capability-boundary material is definitional (Homann) plus Fritzsche's RPU vocabulary.
This batch adds the smallest concrete statement of what a capability *is* operationally — a
command/event name pair with its own fold — and the additive-growth consequence.

**21a. Frontmatter.** Add `fritzsche-how-event-sourcing-grows-with-the-business, fritzsche-why-the-entity-model-is-an-illusion`
to `sources:`; `updated: 2026-09-04`.

**21b. Insert immediately after the `## Giving a capability a "home" — Fritzsche's Autonomous Domain Capabilities` section:**

```markdown
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
```

**21c.** Append both slugs to the page's closing sources line and add `[[entity-centric-thinking]]` to
`## Related`.

---

## 22. `wiki/concepts/decision-trace.md` — **UPDATE**

*Why:* the page is about making decisions legible after the fact; `buildSha` + correlation/causation is a
concrete, cheap primitive for exactly that, and it transfers directly to agent-written events.

**22a. Frontmatter.** Add `dudycz-fixing-bugs-in-event-sourcing` to `sources:`; `updated: 2026-09-04`.

**22b. Insert before the page's closing sources/related line:**

```markdown
## A cheap primitive: stamp the build that made the decision (Dudycz, 2026-07)

[[dudycz-fixing-bugs-in-event-sourcing]] adds one field to event metadata and gets a decision trace for
free: **`buildSha`**, "the commit the service was running when it appended the event… an environment
variable and a few lines in whatever builds our metadata." Then "which decisions did *that* version of
the system make?" is a query, not an archaeology exercise — his case returns exactly the events the broken
binary produced, and excludes records merely touched in the same window. Alongside it,
**`correlationId`** groups everything from one user action and **`causationId`** chains back to the
triggering command: "when the bad value comes out of a handler three hops from the request, that chain is
how we find which request it was."

**Why it matters beyond event sourcing.** This is the "which version of the system decided this" question
that [[agent-explainability]] and [[agent-governance]] ask of agents, answered at the cheapest possible
layer — and it transfers directly to agent-written records (which agent, which model, which prompt or
skill version stamped on the fact it produced). Contrast the heavier instruments on this page: it is
detection-grade metadata rather than a narrative trace, and it is **advice, not a reported practice** —
offered inside an invented scenario, and it assumes one deployable per stream and immutable build tags.
```

**22c.** Append the slug to the closing sources line.

---

## 23. `wiki/concepts/coupling-taxonomy.md` — **UPDATE**

*Why:* the page lands the historical→modern arc; "weighed, not counted" is the first-party argument for
*why* the modern end of that arc exists, plus a warning about the metric tradition.

**23a. Frontmatter.** Add `khononov-coupling-should-be-weighed-not-counted` to `sources:`;
`updated: 2026-09-04`.

**23b. Insert before the page's closing sources line:**

```markdown
## Weighed, not counted — the argument against the metric tradition (Khononov, 2026-02)

[[khononov-coupling-should-be-weighed-not-counted]] is the first-party case for why a *qualitative*
taxonomy survives alongside automatable metrics. Ca/Ce and `I = Ce / (Ce + Ca)` are "simple. Automatable.
And deeply misleading," because they cannot see what flows through a dependency: his illustration is a
component scoring ~0.01 ("textbook stability") whose single outgoing dependency reaches into another
component's internals while its hundred incoming ones go through stable contracts. "The metric says:
rock-solid stability. Reality says: ticking time bomb." Hence: "**Each level down removes an entire
category of shared reasons for change**", so one intrusive dependency can out-cascade a hundred
contract-based ones — and the general warning worth keeping on this page: "**easy to automate and useful
are not the same thing.** A metric that treats use of reflection to modify a private field and an API
call as equivalent is likely to point you in the wrong direction."

*Markers:* **NOT INDEPENDENT** (his own model, and he runs coupling.dev); the 100-dependency component is
a **constructed illustration**; "in my experience, chasing those metrics never really made the design more
modular" is a **practitioner self-report**; **no data in the post**. He also never engages the rejoinder
that direct database access is itself statically detectable. Full four-level scale on
[[balanced-coupling]].
```

**23c.** Append the slug to the closing sources line.

---

## 24. `wiki/concepts/event-driven-architecture.md` — **UPDATE**

*Why:* the page describes brokers and decoupling but has no guidance on message design, which is where the
distributed-monolith failure actually happens.

**24a. Frontmatter.** Add `dudycz-backend-for-frontends-for-event-driven-apis` to `sources:`;
`updated: 2026-09-04`.

**24b. Insert before the closing sources line:**

```markdown
## The messages matter as much as the broker

[[dudycz-backend-for-frontends-for-event-driven-apis]] supplies the design constraint this page lacks:
publishing uniform `SthSthCreated / SthSthUpdated / SthSthDeleted` messages is not event-driven
architecture but **"Poor Man's replication through the queue."** Two splits fix it — **internal
(private/domain) vs external (public/integration)** events, and the recognition that messages are also
**commands** (directed, rejectable) and **state** (Gregor Hohpe's taxonomy, cited second-hand). Two named
failure modes: broadcasting *all* internal events gives "a leaking abstraction and a spider web of
dependencies"; ignoring the other message types makes communication "look like parliament: a room filled
with shouting people. **This is a first step to a distributed monolith.**"

This is a direct constraint on the agent-EDA claims above: if inter-agent traffic is
`AgentStateUpdated` broadcasts, the loose coupling this page credits to EDA has not been bought. Full
treatment on [[internal-vs-external-events]]. *~450-word practitioner post; no measurement.*
```

**24c.** Append the slug to the closing sources line and add `[[internal-vs-external-events]]` to the
page's links.

---

## 25. `wiki/concepts/open-closed-principle.md` — **UPDATE**

*Why:* the page argues new features should add code; this batch gives the storage-level mechanism for why
that is *structurally* true in an event-sourced system, and its limits.

**25a. Frontmatter.** Add `fritzsche-how-event-sourcing-grows-with-the-business` to `sources:`;
`updated: 2026-09-04`.

**25b. Insert before the closing sources/related line:**

```markdown
**The mechanism under "additive," and where it stops (Fritzsche, 2026-08).**
[[fritzsche-how-event-sourcing-grows-with-the-business]] explains *why* an event-sourced system extends by
addition rather than modification: "for events, the schema consists of a set of event types, and that set
**only grows**", and "**events are additive, since no reader needs to know the big picture.** Functions,
on the other hand, remain small because they derive their specific perspective precisely from the events."
Inserting a fifth process step into a running four-step flow touches one existing capability (one fold
case, one rule) and requires **no data migration**, because old records simply lack the new event. Compare
the entity-centred path, where "every new step is a change to a shared structure, because the database
represents a global, shared, mutable state," and a new status value forces a decision about every existing
row.

Where it stops, in his own words: a new **projection** "is new code with its own rebuild." So the
open–closed property holds for the write model and the stored facts, not for the read side. This is the
storage-level counterpart to [[dilger-done-is-done-open-closed-new-slice|"Done is Done"]] (prefer a new
slice to modifying a live flow). *One authored example, no measurement, and the favourable case is
chosen — he does not test a fact every capability must read.*
```

**25c.** Append the slug to the closing line.

---

## 26. `wiki/concepts/agentic-event-driven-systems.md` — **UPDATE**

*Why:* every source on that page sells EDA tooling; this batch supplies a non-vendor practitioner
constraint on what agent event traffic must look like for the page's claims to hold.

**26a. Frontmatter.** Add `dudycz-backend-for-frontends-for-event-driven-apis` to `sources:`;
`updated: 2026-09-04`.

**26b. Insert before the page's closing sources line:**

```markdown
## A non-vendor constraint on what agent events must be (Dudycz, 2026-08)

Every source above sells EDA tooling. [[dudycz-backend-for-frontends-for-event-driven-apis]] is a
practitioner constraint on whether their conclusion is even reachable: if the messages are
`SthSthCreated / Updated / Deleted`, they "aren't actually events… **Poor Man's replication through the
queue**," and broadcasting all internal events buys "a leaking abstraction and a spider web of
dependencies" — a **distributed monolith**, not the loose coupling the vendors credit to EDA. Two
distinctions the agent literature here mostly skips: **internal vs external (integration) events**, and
**commands are not events** — "directed, not broadcast… they can also be **rejected**. If we mistake
them for events, we end up with passive-aggressive communication." For agent-to-agent traffic that is
exactly the property a protocol must carry ([[agent2agent-protocol]], [[multi-agent-orchestration]]).
See [[internal-vs-external-events]]. *Experience report, no measurement.*
```

**26c.** Append the slug to the closing sources line.

---

## 27. Housekeeping owned by the orchestrator (not edited by me)

- **`wiki/index.md`** — add the **17 new source pages** listed at the top of this file, plus the **three
  new pages** proposed here: `wiki/concepts/entity-centric-thinking.md`,
  `wiki/concepts/internal-vs-external-events.md`, `wiki/entities/gerard-klijs.md`.
- **`wiki/log.md`** — suggested entry:
  `## [2026-09-04] ingest   | Batch A "substrate" (17 captures: Pellegrini DCB tags, Khononov ×2, Bogard VSA/AI, AxonIQ gov, Fritzsche ×6, Dudycz ×5, skilj) — touched: 17 source pages + 26 delta items`
- **`wiki/overview.md`** — three shifts worth considering: (1) the KB now has a named root-cause concept
  (`entity-centric-thinking`) under the capability/slice/CCC cluster, with an explicit
  Fritzsche-vs-Dudycz disagreement; (2) the VSA agent argument has a fourth independent asserter — its
  originator — and its first stated *precondition*, still with zero measurement; (3) event sourcing gains
  an operational register (incident recovery, archiving, adoption selection) alongside the modelling one.

**Named capture gaps this batch leaves** (for the next research sweep, not for the wiki):
the Medium article behind `fritzsche-vsa-does-not-fix-entity-centered-thinking` (LinkedIn first comment);
the article behind `dudycz-checklist-first-event-sourcing-feature` (`lnkd.in/dAurDQ4B`);
the Codeartify webinar recording behind Bogard's post; earlier `#EventDrivenDiary` chapters (summary
events, pivotal events, "keep streams short"); Gregor Hohpe's message-taxonomy primary; and the real
permalink + correct repo path for `klijs-skilj-rust-dcb-library`.

**Delta item count: 26 page-level items** (3 CREATE, 23 UPDATE), plus item 27 (orchestrator housekeeping).
