---
title: Given-When-Then (GWT)
type: concept
created: 2026-06-17
updated: 2026-09-04
sources: [adaptech-given-when-then-executable-tests-before-implementation, dilger-todo-lists-storylines-one-scenario, dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, sadalage-chandrasekaran-making-data-ready-for-agentic-ai, ng-spec-driven-development-is-waterfall-in-markdown, event-modeling-event-sourcing-podcast, eventmodeling-what-is-event-modeling, jwilger-agent-skills-event-modeling, jwilger-agent-skills-factory-pipeline, fraktalio-event-modeler-connect-ai-agents-mcp, dilger-spec-editor-free-eventmodelers-alliance, dilger-how-does-dcb-affect-event-modeling, esdm-event-sourced-domain-modeling, bockeler-tdd-inside-the-agent-loop, adzic-spec-driven-development-revenge-of-waterfall-or-bdd, dilger-ui-only-interactions-filtering, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-ux-as-first-class-in-spec-driven-development, tornhill-controlling-the-uncertainty-machine]
tags: [event-modeling, testing, bdd, specifications, agentic-coding]
---

# Given-When-Then (GWT)

The specification format [[event-modeling]] uses to pin down behaviour, one scenario per **command** or
**view**. **Given** a set of prior events (the state-so-far), **When** a command is issued (or a new
event arrives), **Then** the expected events / read-model results follow. It is the
Behaviour-Driven-Development form of **Arrange-Act-Assert / Specification by Example**, but expressed in
terms of *events* rather than mutable object state — which is what makes it fall straight out of an
event model and an [[event-sourcing|event-sourced]] design.

## Why it matters here

- **The contract on every slice.** In Event Modeling each [[vertical-slice-architecture|slice]] carries
  its GWT scenarios; because a command handler is a pure function of (past events) → (new events), the
  "Given/Then" are literally lists of events and the test needs no mocks or database
  ([[eventmodeling-what-is-event-modeling]]). The podcast returns to this repeatedly — GWTs on a
  *timeline* (Eps 3, 7) and the refined GWT format in "Event Modeling 2.0" (Ep 24)
  ([[event-modeling-event-sourcing-podcast]]).
- **The agent feedback backbone.** GWT is the seam where [[event-modeled-agent-design]] becomes
  concrete: the model's GWT scenarios are the **TDD/BDD acceptance gates** an autonomous coding agent
  must pass. [[john-wilger]]'s factory pipeline turns slices + GWT into the gates that govern autonomy
  ([[jwilger-agent-skills-event-modeling]]; v4.1 in [[jwilger-agent-skills-factory-pipeline]] adds
  **boundary enforcement** — a GWT gate *rejects* a scenario unless it exercises an external boundary
  (HTTP/CLI/queue/websocket/UI), and a slice missing a GWT-with-boundary can't even enqueue);
  [[fraktalio]]'s Event Modeler MCP has an agent *generate*
  GWT per command, including business exceptions ([[fraktalio-event-modeler-connect-ai-agents-mcp]]);
  and [[martin-dilger]]'s Event Modeling Agent Harness uses GWT as the BDD feedback loop
  ([[dilger-event-modeling-agent-harness]]). Tooling is following: Dilger's [[eventmodelers-ai]] made
  its Miro **Spec Editor** free for authoring GWT scenarios per slice "where the conversations happen"
  ([[dilger-spec-editor-free-eventmodelers-alliance]]).

- **The GIVEN clause *is* the decision context (Dilger, 2026-07-06).** Under
  [[dynamic-consistency-boundaries|DCB]], the events a command handler must read to decide are exactly
  the scenario's **GIVEN** list — so you never model a separate "Decision Model," and the same GWT that
  specifies behaviour also *derives* the handler's event query (an Axon **Criteria**), which the Axon
  Build Kit generates from the model along with the tests ([[dilger-how-does-dcb-affect-event-modeling]]).
  This is why GWT is load-bearing rather than decorative: it is simultaneously the acceptance gate *and*
  the read-set specification for the decision.

- **GWT as a validated file format (ESDM, 2026-07).** [[thenativeweb|thenativeweb]]'s
  [[esdm-event-sourced-domain-modeling|ESDM]] ships **Given-When-Then as an extension schema** —
  preceding events → triggering action → expected outcomes, captured as its own YAML document kind and
  checked by the same linter as the core model. This makes GWT a *machine-validated, version-controlled
  artifact next to the code*, not just a whiteboard convention — the concrete substrate under the
  "GWT is the agent's acceptance gate" claim.

- **Externally authored, not loop-generated (Böckeler, 2026-08-10).** The one empirical check the KB has
  on tests-in-the-agent-loop is a *negative* result — but it lands on a different target than GWT.
  [[bockeler-tdd-inside-the-agent-loop]] found that instructing an agent to do **TDD inside its own loop**
  bought no measurable quality (blind-ranked non-TDD solutions often scored higher) at 3–8.5× the tokens,
  because step-by-step test-writing suppressed the up-front design the non-TDD runs did, and because a
  self-confirmed red step proves nothing: "a red test tells you the agent ran it and saw failure, **not
  that the failure was for the right reason**." Her three-mode taxonomy makes the distinction precise —
  she tested *mode 3* (agent invents its own tests incrementally), while the GWT-as-agent-gate claim is
  *mode 1* (the specification exists before the agent runs, authored by a human or derived from the
  model). So this is a **boundary condition, not a refutation**: it argues the acceptance spec must come
  from *outside* the loop, which is exactly what a slice's GWT scenarios are. Her endorsement of Ivett
  Ördög's **"Approved Scenarios"** — human-frozen functional scenarios that must be re-approved when
  violated — is structurally the same artifact as a frozen GWT gate, arrived at independently. Her
  caution that applies *with* full force here: coverage and green tests are weak signals, so pair the
  gate with an outcome sensor like [[mutation-testing]].

**A limit that only shows up once agents write the scenarios (Ep 47).** In
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]], a gap-finding agent's first version
*"flooded the model with 100 comments inventing hypothetical gaps"*, and [[adam-dymitruk]] names the
specific damage: an over-eager agent flooding a given-when-then list with edge cases *"can make a simple
slice look far more complex than it really is, since event modeling is visual."* The method's own answer
is older than the tooling — *"draw a few representative example paths and trust the implementer to infer
the rest, rather than trying to specify everything"* — which is specification by example's whole
premise, and the reason **more GWT is not monotonically better**. The tuning fix was a restriction:
comment only on **what is present**, never invent scenarios. *(Date unresolved; show-notes level;
**VENDOR SELF-REPORT**.)*

## The provenance condition: agreed in the room, not written at a desk (Ng, 2026-03)

Böckeler's boundary condition asks *who authored the test*; [[ng-spec-driven-development-is-waterfall-in-markdown]]
adds a second question the KB had left implicit — *who agreed to it*. His critique of
[[spec-driven-development|SDD]] toolkits turns on acceptance criteria produced by one person: the designer,
DevOps lead and PM each hold a different notion of "done," and a solo-authored spec "flattens all of these
perspectives into a single voice: yours." Note he does **not** drop acceptance criteria from his
replacement workflow — he relocates their authorship, pulling them out of a recorded cross-functional sync
into the ticket ([[decision-trace]]).

So a GWT scenario carries two independent quality conditions, and the KB has been tracking only the first:

1. **Outside the loop** (Böckeler) — the agent must not be the author, or the red step proves nothing.
2. **Agreed by the people who hold the constraints** (Ng) — otherwise the scenario is one person's guess
   with a formal syntax, and "spec rot" starts immediately.

Event Modeling's claim to satisfy (2) is that GWT scenarios come out of a facilitated session in the
stakeholders' vocabulary rather than off an architect's desk — a claim about *practice* that this wiki
has no independent evidence for (see [[event-modeled-agent-design]]). [[gojko-adzic]] was read here as making the same point from the tradition that invented the format —
that BDD's examples were always meant to be *derived collaboratively*, so a generated acceptance
criterion nobody discussed is the shell without the practice. **That reading does not survive the
primary, captured 2026-08-31.** "BDD taken to a new level" is his title's question, and he answers it
"it does not, really." His actual objection is about *depth*, not provenance: Spec Kit's given/when/then
acceptance criteria sit "on such a high level that it fits more the scope of work than a specification,"
so the real spec migrates into unit and integration tests "readable only for developers." That is a
sharper complaint for this page than the one attributed to him — it says GWT at the wrong altitude stops
being a specification at all — but it is a *different* complaint, and the collaborative-derivation
argument above is the wiki's, not his.

## GWT-shaped is not GWT — the first-party test (Adzic, 2025-09-29)

[[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] is [[gojko-adzic]], author of
*Specification by Example*, assessing whether [[spec-driven-development|SDD]] is *"BDD taken to a new
level."* His answer: **"It does not, really."**

The generated Spec Kit spec has Given-When-Then acceptance scenarios and MUST/SHOULD functional
requirements — it is GWT-shaped — and his verdict is that *"this is on such a high level that it fits
more the scope of work than a specification… **This is not a spec, it lacks a ton of detail.**"* What
happens instead:

> "The real 'spec' then ends up being in unit and integration tests that are generated based on these
> requirements… readable only for developers. It just seems as a missed opportunity to create
> human-readable specs and drive the work from that."

So the failure is not that GWT is absent but that the **executable** specification and the
**human-reviewable** one have come apart — the exact thing specification by example exists to prevent.
The test he offers is the most checkable one the KB holds for any spec artifact: *"a source of truth
that's detailed enough for people to approve/complain about, but not just in code."*
**Can a non-developer approve or complain about it?**

Two things this changes on this page:

- **A GWT scenario at scope-of-work granularity is not an acceptance gate.** The KB's strongest GWT
  claims ([[jwilger-agent-skills-event-modeling]]'s TDD gates rejected unless they exercise an external
  boundary; [[adaptech-given-when-then-executable-tests-before-implementation]]) all depend on
  scenarios being specific enough to fail for the right reason. Adzic's finding is that generated ones
  routinely are not — which is [[bockeler-tdd-inside-the-agent-loop|Böckeler's]] *"a self-confirmed red
  test proves only that the agent saw a failure, not that the failure was for the right reason"*
  arriving from the requirements side.
- **It is a *scoping* complaint, not a notation one.** His second objection is a **missing scoping
  phase**: with a spec at that granularity *"the tool tried to do too much and kind of went off the
  rails… the whole 'human in the loop' idea was no longer feasible."* That converges independently with
  [[dilger-spec-driven-development-needs-four-phases|Dilger's phase 1]], neither citing the other.

*(One session at a conference workshop, one greenfield toy problem, three weeks into Spec Kit's life,
and **no figures in the piece**. He is also the interested party in the comparison, being the author of
the tradition whose ground is in question — and his overall verdict is warmer than any other critic's:
*"definitely something to keep an eye on."*)*

## The *given* arrived at from outside — declared preconditions (2026-08)

A convergence worth recording because it comes from data architecture with no Event Modeling vocabulary
anywhere in it. [[pramod-sadalage]] and [[prem-chandrasekaran]] require that every acting capability
declare **preconditions** — "the conditions that must hold before the action may proceed, checked
against live state *at the moment of acting* rather than against whatever the agent read earlier in its
plan" ([[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]]). Their example: a refund needs an original payment, not
yet refunded, within the amount the invoking user may authorise.

That is a command slice's **given**, restated: the decision's input is the current relevant state, the
check is deterministic, and reading something plausible earlier in the plan does not substitute for it.
Their insistence that retrieved prose may *inform* the proposal but never *gate* the action is the same
boundary GWT draws between context and precondition — see [[prompt-injection]]. The gap on their side is
the **then**: they specify what must hold before acting and what class of damage the action can do
(reversibility), but not the expected consequence as a testable assertion, which is exactly what a slice
adds. See [[business-capabilities]], [[autonomy-ladder]].

## Storylines — one scenario instead of several (Dilger, 2026-08)

A compaction of the format, shipped on [[eventmodelers-ai]] 2026-08-15
([[dilger-todo-lists-storylines-one-scenario]]). Where a TODO list would traditionally take several
GWT scenarios that repeat most of their setup, a **Storyline** uses *one* scenario to describe the whole
behavior — "examples that tell a story," laid out vertically below a slice. Dilger originally called them
**Vertical Specs**, renamed them when the term confused people; the naming episode is a small
[[ubiquitous-language]]-in-practice case, since the concept didn't change, the audience's reading did.

The stated motive is legibility "by human and AI alike," and the tradeoff — compactness against
per-case addressability — is not discussed in the source.

What makes this more than a feature note: his **self-training modeling agent independently rediscovered
the convention**, noticing from a structural diff against his hand-crafted models that he uses storylines
rather than plain GWT for Read Models attached to Automations, and writing itself a new rule for TODO
lists ([[dilger-one-million-tokens-self-training-modeling-agent]], [[dilger-modeling-agent-improved-by-learning-loop]]). A GWT
convention that existed only as tacit practice was recovered from the artifacts.

**The read-side "Query" WHEN, now used as ordinary practice (2026-07-31).**
[[dilger-extending-event-modeling-query-when]] (2026-06-29) proposed an optional WHEN named *Query* for
read-side scenarios and was explicit it was **not ratified** — *"I wouldn't add this myself — I'm seeking
feedback."* A month later [[dilger-ui-only-interactions-filtering]] simply uses it, without restating
the status: *"Given two `Book registered` events - one for Harry Potter, one for Lord of the Rings -
When you query by title with the key 'Harry Potter', Then the `Books` Read Model returns just that one
match."* And it draws the point that makes it worth having: *"Nothing about this Scenario depends on the
UI plumbing. It's stated purely in terms of the data."* — i.e. the Query WHEN lets a **UI-only
interaction** be specified without inventing a Command or an Event
([[screens-as-specification]], [[event-modeling-anti-patterns]]).

**Status has not changed, only usage.** No ratification is reported anywhere; it remains an opt-in
extension on one vendor's platform (**VENDOR SELF-REPORT**), and any page citing it must carry that.

## Related

[[event-modeling]] · [[event-sourcing]] · [[vertical-slice-architecture]] · [[spec-driven-development]] ·
[[event-modeled-agent-design]] · [[agentic-coding]] · [[mutation-testing]] · [[decision-trace]] ·
[[gojko-adzic]] · [[agent-readable-model-artifacts]] · [[feedforward-and-feedback-controls]] ·
[[model-as-code-vs-model-as-language]] · [[verification-burden]] · [[gojko-adzic]] · [[adam-tornhill]]

## First-party: GWT as executable tests before implementation (Adaptech, 2026-08)

The method's own consultancy stating the pipeline plainly, which the KB previously held only from tool
vendors and practitioners ([[adaptech-given-when-then-executable-tests-before-implementation]]):

> "Given/When/Then scenarios define the starting state, the action being taken, and the expected result.
> **These become executable tests before implementation begins.** The developer starts with failing tests
> and builds the slice until those tests pass."

Framed as ambiguity reduction rather than as testing — "How much ambiguity is still left when a developer
starts building a feature?" — with the payoff stated as agreement plus an objective completion test.

The distinction that matters against [[bockeler-tdd-inside-the-agent-loop]], whose eval found TDD *inside*
the agent loop buys no quality because a self-confirmed red test proves nothing: here **the test predates
the implementer entirely** and is derived from a model rather than written by whoever writes the code.
Whether that difference survives contact with evidence is untested, but it is the right place to look —
and it makes the [[slice]] the unit of the test loop explicitly rather than by inference.

**Arrived at from outside EM, from the code-health side (Tornhill, 2026-08-20).** The same structure
appears with none of this vocabulary in [[tornhill-controlling-the-uncertainty-machine]]: after
planning, he instructs the agent to *"generate the end-to-end (e2e) tests first,"* reviews and iterates
on **those** with the agent, and only then lets it write the implementation — *"a strong test suite
serves as a boundary between the code I do inspect and the code I give the AI autonomy to develop…
Starting with e2e tests solves the validation problem: how do I ensure that the AI generates the right
code?"* Test-before-implementation, human-reviewed, as the human/agent contract — i.e. what a slice's
given/when/then already is.

Three details sharpen the comparison. He designs the tests *"to optimize for ease of inspection"* and
refactors them toward the domain, adding "abstractions to document the intent" — the same legibility
requirement a GWT scenario satisfies by construction. He reports the quality inversion that EM
practitioners should expect too: AI application code is "usually decent," *"the test code? Not so
much,"* so the human effort is in the test refactoring. And his boundary is *movable* — it follows task
uncertainty ([[autonomy-ladder]]), where a model-derived GWT set is fixed before the work starts.

The difference from the Adaptech position remains the **provenance** condition this page already tracks:
Tornhill's tests are agent-generated and human-reviewed, not derived from a model agreed in the room,
so they inherit whatever the agent misunderstood about intent — the gap
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] eval warns about, only partly closed by his review
step. Still, an independent practitioner converging on *executable spec before implementation* as the
answer to the [[verification-burden]] is the strongest external support this seam has.

_Sources: [[event-modeling-event-sourcing-podcast]] · [[eventmodeling-what-is-event-modeling]] · [[jwilger-agent-skills-event-modeling]] · [[jwilger-agent-skills-factory-pipeline]] · [[fraktalio-event-modeler-connect-ai-agents-mcp]] · [[dilger-spec-editor-free-eventmodelers-alliance]] · [[esdm-event-sourced-domain-modeling]] · [[bockeler-tdd-inside-the-agent-loop]] · [[ng-spec-driven-development-is-waterfall-in-markdown]] · [[sadalage-chandrasekaran-making-data-ready-for-agentic-ai]] · [[dilger-todo-lists-storylines-one-scenario]] · [[dilger-one-million-tokens-self-training-modeling-agent]] · [[dilger-modeling-agent-improved-by-learning-loop]] · [[adzic-spec-driven-development-revenge-of-waterfall-or-bdd]] · [[dilger-ui-only-interactions-filtering]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] · [[dilger-ux-as-first-class-in-spec-driven-development]] · [[tornhill-controlling-the-uncertainty-machine]]._
