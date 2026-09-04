---
title: Model-as-Code vs Model-as-Language
type: concept
created: 2026-08-30
updated: 2026-09-02
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy, dilger-markdown-is-a-suggestion-dressed-as-a-spec, nick-tune-enforced-application-architecture-agents-humans, dilger-one-million-tokens-self-training-modeling-agent, dilger-spec-driven-tools-need-event-modeling-front-half, esdm-event-sourced-domain-modeling, dilger-drawio-model-in-code, dilger-eventmodelers-supports-esdm-export, dilger-triplet-flexible-agent-enabled-architecture, ng-spec-driven-development-is-waterfall-in-markdown, jwilger-agent-skills-event-modeling, proophboard-skills-ai-agent-event-modeling, fraktalio-event-modeler-connect-ai-agents-mcp]
tags: [event-modeling, agentic-coding, spec-driven-development, controversy, focus]
---

# Model-as-Code vs Model-as-Language

**An open, live disagreement about where the authoritative description of a system should live when
an agent is going to build it.** One camp says a **separate formal modeling language** with its own
artifact, authored before code; the other says the **code itself**, with the model recovered from it by
visualization.

> **A framing caution added 2026-08-31.** It is tempting to say both camps "reject Markdown as a
> specification." Dilger does, explicitly and at length. **Miller does not discuss prose or Markdown
> specs at all** — his scepticism is aimed at diagrams, low-code visual modeling, and YAML/XML/custom
> textual DSLs, and he in fact lists "a markdown input?" among the open options he would consider for
> expressing tests. The two are not mirror images, and the disagreement below should be read as being
> about **where the authored artifact lives**, not about Markdown.

This page exists because in the last week of August 2026 two of the practitioners this KB tracks most
closely staked opposite ground on exactly this question, within four days of each other, neither
naming the other. It is the sharpest unresolved controversy the wiki holds, and it lands directly on
the premises of [[agent-readable-model-artifacts]] and [[spec-driven-development]].

> **Status: unresolved.** This page states both positions and the evidence each side can point to. It
> does not adjudicate, and it should not be read as the wiki taking a side.

## The two positions

| | **Model-as-Language** | **Model-as-Code** |
| --- | --- | --- |
| Champion | [[martin-dilger]] (also [[adam-dymitruk]], [[john-wilger]], [[prooph-board]], [[fraktalio]]) | [[jeremy-miller]] |
| The artifact of record | An **event model** in a dedicated notation/format, authored before code | The **code**, with a model view generated on top of it |
| What's wrong with the other side | Prose and code both under-specify *behavior*; code shows how, not what, and can't be reviewed by the business | Intermediate DSLs (YAML/XML/custom textual) and low-code visual modeling have a bad historical track record and cost more than they return |
| Direction of generation | Model → code (codegen from slices) | Code → model (visualization, `dotnet watch`, live diagram) |
| What the agent is handed | Exported slices, GWT specs, model files | Exported slice definitions *derived from* code, plus AI Skills |

## The Model-as-Language case

The clearest statement is Dilger's, 2026-08-25 ([[dilger-markdown-is-a-suggestion-dressed-as-a-spec]]):

> "The Markdown we use is a suggestion dressed up as a spec… Spec-Driven Development requires suitable
> language. Event Modeling is the one that works for me. A precise specification of behavior."

His supporting argument is an economy-of-description one: "Pages of prose to produce a handful of
lines. If the explanation outweighs the thing it's explaining, the tool doing the explaining is wrong."
Note that he does *not* dismiss code as a formal language — he calls it one — his objection is that code
specifies implementation while the thing needing specification is **behavior over time**, which is what
[[event-modeling]]'s timeline gives you.

The position has accumulated infrastructure rather than just advocacy: a validated file format with an
offline linter ([[esdm-event-sourced-domain-modeling]]), format-agnostic export on demand
([[dilger-eventmodelers-supports-esdm-export]]), model-in-git via draw.io XML
([[dilger-drawio-model-in-code]]), board-level MCP access
([[fraktalio-event-modeler-connect-ai-agents-mcp]], [[proophboard-skills-ai-agent-event-modeling]]),
and an autonomous coding factory whose contract *is* the model
([[jwilger-agent-skills-event-modeling]]). See [[agent-readable-model-artifacts]] for the full ladder
of surfaces this camp has built.

## The Model-as-Code case

Miller's statement, 2026-08-21 ([[miller-jasperfx-critterstack-ai-event-modeling-strategy]]):

> "I'm also not enthusiastic about any of the intermediate DSL approaches I'm seeing for modeling event
> driven architectures using YAML, XML, or custom built textual DSLs… I think that we're better off just
> adding the visualization capabilities on top of the code rather than trying for a hugely time
> consuming user interface effort."

He grounds this in lineage rather than in argument-from-first-principles: a background in code-and-TDD/BDD
Extreme Programming, and explicit scepticism of "low code" visual modeling and application generators
like JHipster. The design consequence is visible in what JasperFx says it will build — a fluent API in
`JasperFx.Events` for declaring event types and read models, a Bobcat UI that *visualizes* the resulting
slices, `dotnet watch` integration so you can "interactively doodle with slice definitions and see the
model change", and CLI options to export slice definitions for agent use. **This is a proposal, not
shipped product** — the raw introduces the list with "the concept that I'm proposing so far is" and
calls Bobcat "pretty mushy as far as details." What the design *intends* is a model that is real and
agent-consumable but **downstream of the code**: "have the specified model overridden when real code is
built in the system."

There is a second, subtler move in his position: rather than have people "waste time writing intermediate
models for policies, constraints, or validation rules in a diagram", go **straight to BDD specifications
that become actionable specs**. That is not a rejection of [[given-when-then]] as the unit of
specification — it is a claim that GWT is the *only* part of the model worth authoring by hand, and the
rest should be inferred.

## Where they actually agree

The disagreement is narrower than it first appears, and the agreements are load-bearing:

- **Hand-authoring a separate description of the rules is waste.** Dilger, of prose: Markdown is "a
  suggestion dressed up as a spec." Miller, of diagrams: don't have people "waste time writing
  intermediate models for policies, constraints, or validation rules in a diagram" — write executable
  specifications instead. Note this is an *analogous* objection aimed at **different targets**, not a
  shared rejection of Markdown; see the framing caution above. Dilger's target is also
  [[ng-spec-driven-development-is-waterfall-in-markdown]]'s, from a third direction.
- **The slice is the right unit.** Both build tooling around slices, and both give the agent slice
  definitions.
- **[[vertical-slice-architecture]] is token economics, not taste.** Miller's "layered architectures…
  force AI agents to burn more tokens traversing the code" and Dilger's "Slices are like Candy for AI"
  are the same claim, arrived at independently.
- **Event Modeling concepts belong in the runtime.** Miller is pushing EM concepts into Wolverine and
  the Marten/Polecat/Fisher stores; Dilger's Triplet ([[dilger-triplet-flexible-agent-enabled-architecture]])
  binds EM to [[event-sourcing]] the same way.

## Why the disagreement matters here

Three consequences, in rough order of how much they should change what you do:

1. **It is a direct test of the model-first premise.** The `.chspec.yml` direction — a validated,
   version-controlled model file authored before code — falls squarely inside what Miller names and
   rejects: "intermediate DSL approaches… using YAML, XML, or custom built textual DSLs." His objection deserves an answer rather than an assumption, and the
   honest form of that answer is empirical: does a model-first pipeline produce better agent output
   than a code-first one with visualization? Neither side has published a comparison.
2. **It splits [[agent-readable-model-artifacts]] in two.** That page's ladder implicitly assumes the
   model is authored and then made machine-tractable. Miller's position adds a rung the ladder does
   not have — *derived* model artifacts, where the export is a projection of code — and the ladder
   should be extended rather than treated as complete.
3. **The evidence is currently asymmetric.** Dilger has a working self-improving modeling agent graded
   against a corpus of hand-crafted models ([[dilger-one-million-tokens-self-training-modeling-agent]]),
   which is real evidence that a formal model makes agent output **gradeable** — the mechanism being a
   **structural diff**, a property a schema has and Markdown does not.
   Miller has a track-record argument and tooling in progress, but no comparable demonstration. That is
   not a verdict — an unshipped comparison is not a refutation — but it is where the burden currently
   sits.

## Open questions

- Has anyone run the comparison directly — same requirements, model-first vs code-first-with-visualization,
  measured on agent output quality? Nothing in the KB does.
- Does Miller's objection survive contact with **grading**? His argument is about authoring cost; Dilger's
  strongest evidence is about *verification* (a structural diff against good models). These may not be in
  conflict at all — code could be the authoring surface and a derived model still be the rubric.
- Is the split correlated with **who is in the room**? Dilger's tooling assumes business stakeholders
  co-author the model in a workshop; Miller's assumes developers. If so this is a disagreement about
  organizational context, not about notation — see [[conways-law]].

## Related

[[event-modeling]] · [[agent-readable-model-artifacts]] · [[spec-driven-development]] ·
[[event-modeled-agent-design]] · [[vertical-slice-architecture]] · [[given-when-then]] ·
[[vibe-modeling]] · [[em-standardization-foundation]]

## What each side's own material adds, once compiled (2026-08-31)

Both primaries are now source pages, and reading them in full sharpens the disagreement in three ways
the quotes alone did not.

- **Miller's argument is from lineage and cost, not from principle.** He does not claim a model cannot
  specify behavior; he claims the authoring surface is expensive and historically disappointing (JHipster,
  low-code visual modeling), and that visualization-over-code is the cheaper route to the same legibility.
  That is a *falsifiable economic claim*, not a philosophical one — which is why the missing comparison
  matters so much.
- **Dilger does not reject code as formal, and his test is a ratio.** "We have a formal language - it's
  called Code." His objection is about *what* code is formal about — implementation rather than behavior
  over time — plus reviewability by the business. The economy-of-description test ("if the explanation
  outweighs the thing it's explaining, the tool doing the explaining is wrong") is aimed at **prose**,
  and on that target the two men agree entirely.
- **The direction of fit is now explicit on Miller's side.** *"Have the specified model overridden when
  real code is built in the system"* — the code wins, which is why JasperFx is pushing EM concepts into
  Wolverine and the Marten/Polecat/Fisher stores rather than maintaining a separate artifact.

Both are also **hedged more than the quotes suggest**: Miller says JasperFx is "trying to throw all the
spaghetti up against the wall right now and see what ends up sticking," calls Bobcat "pretty mushy as far
as details," and presents the Event Modeling work as "the concept that I'm proposing so far"; Dilger says
Event Modeling is the one that works "**for me**." Neither claims settled ground — a reason to keep this
page unresolved rather than a reason to discount either side.

## A third position: model-as-constraint (added 2026-09-02)

The two-column table above is a false binary, and [[nick-tune]] occupies the missing cell
([[nick-tune-enforced-application-architecture-agents-humans]], 2026-08-13). His authoritative artifact
is neither a model file authored before code nor the code's own content, but the **set of constraints
the code must satisfy to build at all** — package classification, layer import rules, and role-based
rules with per-role shape constraints, expressed in a DSL (Rivière) and enforced by build failure.

What makes it a genuinely distinct position rather than a variant:

- **Markdown's failure is his premise, not his thesis.** Dilger argues *toward* the conclusion that prose
  under-specifies; Tune opens by assuming it — *"One of the most frustrating parts of AI-generated code
  is that it does not follow architectural guidelines that are written in skill files, ADRs, and various
  other places in the repo"* — and spends the post on the enforcement mechanism instead. On the framing caution at the top of this page, note
  that Tune's target includes **skill files and ADRs**, i.e. exactly the prose artifacts Miller never
  discusses and Dilger attacks by argument.
- **The direction of fit is neither model→code nor code→model.** It is *code ⊨ constraint*. Nothing is
  generated in either direction; the model is a **predicate over the codebase**, and its enforcement
  point is CI rather than a codegen step or a visualisation.
- **It answers Miller's cost objection without conceding Dilger's artifact.** Miller's case is economic —
  intermediate DSLs and visual modeling cost more than they return. Tune's DSL describes *permitted
  structure*, not behaviour, so it is far smaller than a model of the system, and it pays out on every
  agent run rather than once at generation. Whether it *actually* pays is unmeasured: the post has no
  before/after numbers, and **Rivière is his own tool** (interested-party marker travels with any claim
  taken from it).
- **What it cannot do is specify behaviour.** This is the honest limit and the reason it does not
  dissolve the controversy: a role constraint can forbid an aggregate from appearing inside a value
  object, but nothing in the tier stack says what should happen when a reservation is priced. Dilger's
  objection to code — that it is formal about implementation while the thing needing specification is
  *behaviour over time* — applies to constraints with equal force. Tune's rules and an event model are
  therefore **complements, not rivals**: one fixes where code may live, the other what it must do.

The practical upshot for this page's open question about **grading**: Tune supplies a third grader
alongside Dilger's structural diff and Miller's derived visualisation — a deterministic, always-on
build gate. Of the three it is the only one demonstrably running on its author's own repo today
(Miller's is a proposal; Dilger's is a research loop), and the only one that produces no artifact a
business stakeholder could read. "Running" is as far as the claim goes: the raw contains no
measurement, and he calls the deepest tier of it unsettled — *"still playing around with that. Come
back in 6 months. I feel confident it's the right approach."*

*Sourcing note: written 2026-08-30 citing raw captures; re-grounded 2026-08-31 when Batch C compiled both
primaries into source pages; third position added 2026-09-02 from the Tune ingest.*
