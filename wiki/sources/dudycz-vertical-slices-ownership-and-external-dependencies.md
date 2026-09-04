---
title: "Source: Dudycz — Vertical slices, their ownership and external dependencies"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [dudycz-vertical-slices-ownership-and-external-dependencies]
raw_file: [raw/articles/dudycz-vertical-slices-ownership-and-external-dependencies.md]
tags: [vertical-slice-architecture, slice, cqrs, coupling, ddd, agentic-coding, substrate, focus]
---

# Source: Dudycz — Vertical slices, their ownership and external dependencies

Long-form article by **[[oskar-dudycz]]** (event-driven.io, 2026-08-10). Raw capture:
`raw/articles/dudycz-vertical-slices-ownership-and-external-dependencies.md`. This is the **VSA↔slices
source the [[vertical-slice-architecture]] page has been waiting for** (that page names Dudycz's VSA
material as its top open capture).

**Register:** experience-based design guidance with TypeScript examples. "Technological splits… have
always ended badly **in my projects**", "I held it myself for a while", "Most module-level cycles **I've
run into**" — **IMPRESSION NOT MEASUREMENT** throughout; no benchmark, no case study. Closes with a
consulting offer, so an interested party for the pattern he teaches.

## Summary

The article answers one question — **"what does a slice do when it needs something from the outside
world?"** — and starts by dissolving the vocabulary that makes the question unanswerable:

- **A vertical slice is one piece of functionality cut through the whole application.** "For me, a slice
  is more a function than an entity. *'Verify a transport order'* is a slice… If you're thinking of it as
  a thing with a lifecycle, you're probably thinking of an entity, which is a different concept that
  lives *within* the slice's reach rather than being the slice."
- **A module is a logical grouping of slices**, and "the criterion I use is **what changes together**."
- **A bounded context is a linguistic barrier** — "a set of functionality that the business uses the same
  vocabulary for." Consequences he draws: "A frontend and a backend aren't two bounded contexts; they're
  two **deployment targets**", and "Seven features of one application are almost always slices, or at
  most modules, sitting inside a single context. That's good news, because it means **they were never
  obliged to be autonomous**." He goes further: "I don't love the term 'bounded context'… If the word
  causes arguments on your team, drop it and talk about **which functionalities share a vocabulary**."

The mechanism is **consumer-declared narrow function types, composed by hand at the entry point**. A
handler takes dependencies first, message second; the dependency types (`CheckContractor`,
`CheckDriver` — three cases each) are declared **in the slice's own folder, in the slice's vocabulary**,
not imported from the provider. Nothing declares that it implements them; **structural/duck typing** means
any compatible function satisfies them, so "you can write the need, the handler, and the tests before
anyone has decided who will serve it." One composition file near the entry point builds the real things
and passes them in — "partial application, done by hand, in a file whose job is to know about everything
so that nothing else has to. No container, no registration, no lifetime scopes." Tests use the same
shape, "because there's nothing to mock."

And the rule that generalises it: **"From inside a slice, there's one category of thing: external.
Another slice next door, the parent module, a different module, a third-party API, the database. All the
same."**

## Key points

- **The assumption he names as the source of the confusion:** "a slice ought to be self-contained, so
  needing something from elsewhere means the cut was wrong… **Minimise isn't zero**, so what does the
  non-zero look like once you type it out?"
- **Two directions across the same boundary, and you want both.** A module's `api.ts` is what a module
  **offers** (the surface it owns and will support); a declared `CheckContractor` is what a slice
  **asks for** (a need owned by the consumer, in the consumer's terms). "Without the module API,
  everything is reachable… Without consumer-declared needs, the consumer is coupled to the shape of
  whatever the provider decided to expose, including the parts it never calls." **The composition root
  is where the two meet** — "that adapter is a few lines, it lives in one place, and it's the only code
  that knows both vocabularies."
- **Cycles dissolve rather than get resolved.** Orders needs contractor standing; Pricing needs order
  history. "But there's no cycle if neither module imports the other" — each declares its own narrow
  need and the composition root supplies it. His diagnosis: "**Most module-level cycles I've run into
  were a shared concept whose owner hadn't been decided yet.** Declaring narrow needs lets you defer that
  decision rather than resolve it early and wrong." And the pointed warning about the usual escape: "The
  usual [fix] is to extract the shared parts into a common module. That works twice; then the common
  module becomes the place everything ambiguous lands, and changing it means changing everything."
- **Boundary rules describe your import graph, not your design.** "If your dependency rules forbid the
  arrangement your domain wants, it's worth checking whether they're describing your design or your
  import graph. Rules that block a module from reaching another module are useful. **Rules that block it
  because two files sit at the same 'layer' are enforcing a layering you may have already outgrown.**"
- **Naming is what creates something to slice along** — and he credits [[greg-young]]'s *Task-Based UI*:
  when the client posts data-centric structures, "the domain has no verbs, and the user's intent is lost
  on the way in." "If every operation is 'update the order', you have one feature and nothing to divide.
  Once you have `VerifyOrder`, `ConfirmOrder`, `RejectOrder`, you have folders." Crucially: **"This holds
  for plain CRUD systems too. The name is the value, and the underlying implementation can be a single
  `UPDATE`."**
- **Also: the system records that the order is verified; "it doesn't record that anybody verified it"** —
  a one-line statement of what a status column loses.
- **The three-part answer on persistence, which is the part most often mangled:**
  **business logic per entity or aggregate** ("the rules about what states an order can be in… belong to
  the order. One place… Slices don't each get a private notion of what an order is");
  **read models per query** ("this is where a table per feature is right… Resist making a single query
  serve five screens by expanding columns");
  **database schemas per module** ("A slice is a feature, not a persistence boundary. A schema per slice
  gives you migrations that correspond to nothing").
- **Reuse policy:** "I'd reuse a policy or a calculator, say a pure function like
  `settlementFor(order, tariff)`… before I'd reuse a whole handler. **The pure function is a function of
  its arguments and cheap to share. Handlers differ in what they load, check and record**, and that's the
  part that tends to change." Two entry points for the same operation (dispatcher UI, carrier event) live
  side by side in the same folder, share the business logic, and **do not share dependencies** — the
  event-triggered one needs no carrier check because the event came from the carrier.
- **Frontend:** "Don't force a 1:1 mapping between the UI and the backend." Either compose at the page
  (components take props and know nothing about origins — "for the same reason that handlers take
  dependencies as arguments") or write a **backend-for-frontend**: "It's still a slice; it's named after
  a screen because that's honestly what it is." Plus a HATEOAS fragment he does endorse: **return the
  available actions with the data**, rather than letting the frontend re-derive them from status fields.
- **On hiding coupling — his explicit rejection of independence-as-a-value:** "**None of this is about
  hiding the coupling.** For me, independence isn't a value in itself. I'd rather know the connections I
  need to have and be able to look at the code… Hidden dependencies are still there, only harder to find.
  What I'm optimising for is **cohesion**, and explicit dependencies serve that."
- **Wrongness should stay cheap:** "your first grouping will still be wrong somewhere. Mine usually is.
  That's fine, as long as being wrong stays cheap" — his argument for *removability over
  maintainability*. "A slice that states its dependencies is one you can move."
- **The agent note, added last and framed as a bonus:** "Everything a feature needs sits in one folder,
  with a handful of function types crossing the boundary. To change how verification works, you open
  `verifying-order`… The same property determines how much can fit in a context window and how much of a
  codebase an agent has to read before it can safely change one behaviour. A layered structure that needs
  five folders touched for one feature **costs an agent the same way it costs us, faster.** So it's an old
  argument that happens to have got more valuable."

## Connections / contrast

- **Fills the [[vertical-slice-architecture]] page's named gap** and adds the thing that page never had:
  a **positive, worked answer to cross-slice dependency**, plus the slice/module/context vocabulary that
  makes "seven areas" a non-problem. His "everything outside is external" rule is a stricter, simpler
  statement of the boundary than either [[jimmy-bogard|Bogard's]] "minimize coupling between slices" or
  [[nick-tune-enforced-application-architecture-agents-humans|Tune's]] no-cross-feature-imports rule —
  and note it **permits** what Tune's rule forbids, provided the connection goes through a
  consumer-declared type and the composition root. The two are not in conflict about goals, but they
  would grade the same codebase differently.
- **A direct disagreement with Fritzsche, in the same batch.**
  [[fritzsche-vsa-does-not-fix-entity-centered-thinking]] argues that starting from "the record that
  changes" makes the entity lifecycle the use-case boundary, and
  [[fritzsche-why-the-entity-model-is-an-illusion]] denies the entity any place in software. Dudycz
  **agrees on the naming half** (CRUD verbs give you nothing to slice along; name the business operation)
  and **disagrees on the entity**: business logic *belongs* per entity/aggregate, precisely so slices
  don't each invent their own notion of an order. Two substrate primaries, same week-range, opposite
  conclusions on where the rules live — the KB should carry the disagreement rather than merge it.
- **Coupling made concrete.** A narrow consumer-declared function type is **Contract-level coupling by
  construction** in [[khononov-coupling-should-be-weighed-not-counted|Khononov's]] Integration Strength
  scale, and importing a provider's wide interface is Model-level at best. Dudycz reaches the same
  ranking from cohesion; [[balanced-coupling]] gives it the vocabulary. His "what changes together" module
  criterion is Khononov's balance rule in one phrase.
- **Also compatible with [[event-sourcing]] but explicitly not dependent on it:** "You can do all of this
  with one status column and an ORM. If you want the four distinct operations that currently collapse into
  `status = 'cancelled'` to stay distinguishable, appending them as facts is what Event Sourcing offers,
  and it composes well with this. **Nothing above depends on it.**" Same separation
  [[fritzsche-thinking-in-events]] draws between the method and the store.
- **The backend-for-frontend passage is the article behind his LinkedIn note**
  [[dudycz-backend-for-frontends-for-event-driven-apis]], which carries the idea into event-driven APIs.
- Adjacent: [[slice]] · [[cqrs]] · [[locality-of-reference]] · [[agent-legibility]] ·
  [[open-closed-principle]] · [[business-capabilities]] · [[conways-law]] ·
  [[bogard-vertical-slice-architecture-webinar-recording-whats-next]] (the same agent argument, asserted
  in three sentences instead of worked out).

## Limits

- **Experience report, no evidence.** No measurement of any claim — not the token/context-window benefit,
  not cycle reduction, not test cost. The agent paragraph in particular is an **assertion appended to a
  design argument**, and he presents it as such ("an old argument that happens to have got more
  valuable").
- **The examples are TypeScript and lean on structural typing**; he acknowledges the nominal-typing
  world (C#/Java habits, .NET method injection) but the pattern's ergonomics there are asserted, not
  shown.
- **Hand-rolled composition is presented without its scaling costs** — one file that "knows about
  everything" is a coordination point, and he does not discuss what happens when it grows, or how
  lifetimes/scopes (request-scoped connections, transactions) are handled without a container.
- **Duplication is prescribed but unbounded** ("let handlers duplicate"): no guidance on when duplicated
  application logic becomes the [[khononov-coupling-should-be-weighed-not-counted|Functional-strength]]
  coupling it is meant to avoid.
- **The persistence rules are stated as conclusions**, with no discussion of the awkward middle (a read
  model needed by two modules, a rule spanning two aggregates — the case
  [[dynamic-consistency-boundaries|DCB]] exists for, which this article does not mention).
- Commercially interested (consulting/training offer in the closing p.s.).

_Source: `raw/articles/dudycz-vertical-slices-ownership-and-external-dependencies.md`._
