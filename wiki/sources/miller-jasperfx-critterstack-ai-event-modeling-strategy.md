---
title: "Miller — The JasperFx / CritterStack AI and Event Modeling Strategy"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [miller-jasperfx-critterstack-ai-event-modeling-strategy]
raw_file: [raw/articles/miller-jasperfx-critterstack-ai-event-modeling-strategy.md]
tags: [event-modeling, vertical-slice-architecture, event-sourcing, agentic-coding, spec-driven-development, dotnet, controversy, focus]
---

# Miller — The JasperFx / CritterStack AI and Event Modeling Strategy

Blog post by **[[jeremy-miller]]** (*The Shade Tree Developer*, jeremydmiller.com), 2026-08-21. Raw
capture: `raw/articles/miller-jasperfx-critterstack-ai-event-modeling-strategy.md` (1,873 words).
Surfaced only via an X search hit (@jeremydmiller, quote-tweeted by @lxztlr) on the 2026-08-26
live-Chrome sweep — his blog index had reported "newest Aug-03" on every recent headless run, making
this a headless blind-spot.

The **Model-as-Code** pole of [[model-as-code-vs-model-as-language]], stated by someone building the
tooling rather than arguing the position — though most of the Event Modeling work described here is
proposed rather than shipped. Miller's own framing is deliberately unsettled: *"we're trying
to throw all the spaghetti up against the wall right now and see what ends up sticking."*

## The position, in his words

> "Philosophically, I'm coming from a background in code-and-TDD/BDD-centric Extreme Programming and
> I've long been very dubious about the efficacy of 'low code' visual modeling approaches or application
> generators like JHipster. I'm also not enthusiastic about any of the intermediate DSL approaches I'm
> seeing for modeling event driven architectures using YAML, XML, or custom built textual DSLs. Because
> of the Critter Stack's relentless focus on low ceremony code, I think that we're better off just adding
> the visualization capabilities on top of the code rather than trying for a hugely time consuming user
> interface effort."

Note the shape of the argument: it is **from lineage and cost**, not from first principles. He does not
claim a model cannot specify behavior; he claims the authoring surface is expensive and historically
disappointing, and that visualization-over-code is the cheaper path to the same legibility.

## What JasperFx says it will build

Careful here: this is a **proposal, not a changelog**. The raw introduces the list below with *"The
concept that I'm proposing so far is:"*, the final item begins *"Probably invest in…"*, and Miller calls
Bobcat "pretty mushy as far as details." Read it as direction of travel:

- A new model and **fluent interface API in `JasperFx.Events`** for declaring event types, read model
  types, "and any other common elements of Event Storming or Event Modeling."
- A **Bobcat UI that visualizes the Event Modeling slices** defined by that model.
- **`dotnet watch` integration** so you can "interactively doodle with slice definitions and see the
  model change."
- **"Have the specified model overridden when real code is built in the system"** — which is the
  direction-of-fit statement: the code wins, and it is why EM concepts are being pushed *directly into
  Wolverine and the Marten/Polecat/Fisher event stores*.
- **CLI export of event slice definitions for AI agent usage**, plus AI Skills teaching agents to use
  Bobcat specifications and the models.
- *"Probably invest in"* extending existing codegen "to build out the shell of a 'slice' from the model
  as a first step."

What *is* shipped, by contrast, is listed under "The rest of the strategy" below: CritterWatch 1.0 and
the Wolverine 9.0 CLI.

## The second, subtler move — skip the intermediate model, go to BDD

> "Rather than have people waste time writing intermediate models for policies, constraints, or
> validation rules in a diagram, go straight to Behavior Driven Development specifications that become
> actionable specs."

This is not a rejection of [[given-when-then]] — Bobcat has a **Gherkin capability** for executable
specifications (chosen largely for existing VS Code / Rider editing support; a Reqnroll dependency is
undecided). It is a claim that **GWT is the only part of the model worth authoring by hand**, and the
structural rest should be inferred from code. Bobcat's spec output is being made to record which
Wolverine messages occurred, which events were appended, and which HTTP calls were received during a
test, with timings — tests instrumented to help an agent diagnose its own failures.

Bobcat also carries a **"Supervisor"** built on the Microsoft Testing Platform that manages parallelism,
selective retries, and recycling Docker containers or test processes when health degrades — motivated,
he says, by his own CritterWatch test suites degrading as containers and processes stay up too long.
*Separately*, he is building a small web application for watching ongoing results, because with a long
agent-driven run "you can't always tell if it's active." Both are [[harness-engineering]] plumbing
arrived at from the test-infrastructure side.

## VSA as token economics

> "Wolverine's very terse approach to VSA is already very optimized for AI agentic development —
> especially when contrasted with more traditional server side .NET code organization that leans into
> layered architectures that force AI agents to burn more tokens traversing the code."

He calls the early VSA emphasis "accidentally prescient," and is candid that the claim is unproven:
*"it's incumbent upon people like me to prove that out over time."* This is the same claim as Dilger's
"slices are like candy for AI," reached independently from the other side of the controversy — see
[[vertical-slice-architecture]].

He also flags the real adoption friction: users arriving from Clean Architecture bring the projects,
layers and abstractions that neither the stack nor the agent wants.

## The rest of the strategy

- **CritterWatch 1.0** is live — a commercial MCP **and** CLI surface over the Marten/Polecat/Fisher
  event stores, with "every single bit of information... and every single action" exposed through MCP
  endpoints, including cross-application workflow and dead-letter-queue access. See
  [[model-context-protocol]].
- **CLI as agent interface.** Wolverine 9.0 CLI output is explicitly "optimized for AI agents" —
  explaining message routing, previewing generated handler source, diagnosing missing handlers. The
  human-facing `dotnet run describe` stays.
- **AI Skills** for Marten, Polecat, Wolverine and Alba, sold commercially, teaching both idiomatic
  usage and how to drive the CLI.
- **LLM callouts** from Wolverine and projections via `Microsoft.Extensions.AI` (client work, no details).
- **Agent orchestration + durable agent memory** on the Critter Stack, with Fisher (SQLite event
  sourcing) as the substrate; he names KurrentDb's Capacitor as the impressive prior art. Commercial.

## Why it matters here

1. **It is the strongest counter-position in the KB to the model-first premise.** The `.chspec.yml`
   direction falls squarely inside what he names and rejects — "intermediate DSL approaches… using YAML,
   XML, or custom built textual DSLs." See [[model-as-code-vs-model-as-language]].
2. **It adds a rung [[agent-readable-model-artifacts]] does not have** — a *derived* model artifact,
   where the agent-consumable export is a projection **of code** rather than a serialization of an
   authored model.
3. **It is a second vendor putting Event Modeling into a runtime**, alongside Dilger's Triplet
   ([[dilger-triplet-flexible-agent-enabled-architecture]]) — evidence that "EM concepts belong in the
   stack" is converging even where the authoring surface is disputed.

## Caveats

- **Vendor strategy post, and mostly a proposal.** The Event Modeling capability is what he is
  *proposing*, not what has shipped; Bobcat's scope is explicitly undecided and he frames the whole
  strategy as throwing "all the spaghetti up against the wall… and see what ends up sticking." Do not
  cite any of the EM-into-the-stack items as existing product.
- **He is not against Markdown.** His scepticism is aimed at diagrams, low-code visual modeling and
  YAML/XML/custom textual DSLs. Markdown is in fact on his own list of open options for expressing
  tests: "A markdown input? Something completely different?" This matters when placing him opposite
  Dilger, whose whole argument *is* about Markdown.
- **No comparison.** He offers no evidence that code-first-with-visualization beats model-first for agent
  output — as Dilger offers none the other way. Neither side has run the experiment.
- Commercial interest throughout: CritterWatch, AI Skills, and the agent orchestrator are all paid
  products.

## Related

[[jeremy-miller]] · [[critter-stack]] · [[model-as-code-vs-model-as-language]] ·
[[agent-readable-model-artifacts]] · [[vertical-slice-architecture]] · [[event-modeling]] ·
[[given-when-then]] · [[spec-driven-development]] · [[event-sourcing]] · [[model-context-protocol]] ·
[[dilger-markdown-is-a-suggestion-dressed-as-a-spec]]
