---
title: Martin Dilger
type: entity
created: 2026-06-13
updated: 2026-08-31
sources: [dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, dilger-todo-lists-storylines-one-scenario, dilger-eventmodelers-supports-esdm-export, dilger-highlighting-markers-give-context-to-agents, dilger-describing-without-solving-burns-you-out, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-spec-driven-development-applied, dilger-keep-command-handlers-pure, dilger-automatic-domain-discovery-claude-code, dilger-model-is-a-living-spec-always-on-agent, dilger-hold-my-beer-engineer, dilger-craft-conf-idea-to-event-model-to-code, dilger-dcb-is-what-event-sourcing-should-have-been, dilger-event-modeling-agent-harness, dilger-is-code-still-the-source-of-truth, dilger-adding-perspectives-to-event-modeling, dilger-done-is-done-open-closed-new-slice, dilger-spec-editor-free-eventmodelers-alliance, dilger-build-kits-model-to-generated-code, dilger-event-modeling-knowledge-hub-emlang, dilger-harness-is-20-percent-requirements-are-80, dilger-first-event-modeling-conference-munich-recap, dilger-how-does-dcb-affect-event-modeling, dilger-planning-like-excel-legible-to-human-and-ai, dilger-user-stories-need-event-modeling-framework, dilger-local-llm-distributed-agent-setup-event-modeling, dilger-extending-event-modeling-query-when, dilger-drawio-model-in-code, dilger-flea-market-model-to-deploy, event-modeling-event-sourcing-podcast, dilger-triplet-flexible-agent-enabled-architecture, dilger-spec-driven-tools-need-event-modeling-front-half, dilger-real-cost-of-ai-is-second-order, dilger-the-shapes-event-modeling-anti-patterns, dilger-agentic-collaboration-freeform-drawings, dilger-99-percent-software-boring-two-patterns, dilger-event-model-structure-linter-reference-catalog]
tags: [person, event-modeling, event-sourcing, agentic-coding, spec-driven-development, focus]
---

# Martin Dilger

Event-sourcing / Event Modeling practitioner and consultant; founder of **[[nebulit]] GmbH**; author
of **"Understanding Eventsourcing"** (the first German-language book on Event Modeling) and **"Spec
Driven"**, and co-host of the **[[event-modeling-event-sourcing-podcast|Event Modeling & Event Sourcing podcast]]**
(46 eps with [[adam-dymitruk]]). He is building
**[[eventmodelers-ai]]** ("eventmodelers.ai"), an *agentic software modeling* platform meant to "bring
business, engineering and AI together." Associated with the [[prooph-board]] community. A prolific LinkedIn writer — his recent activity is one of the most
on-target running feeds for Dannie's focus area ([[event-modeled-agent-design]]), tracked in
`watch-config.json`. He **organized and hosted the first Event Modeling Conference** (Munich, Oct 2025;
recap [[dilger-first-event-modeling-conference-munich-recap]]) and announced there a **joint venture
with [[adam-dymitruk]] — a new company for Event Modeling tooling + standardization** ("the engineering
part"), plus a planned EM **certification program**. The 2nd conference ran 25–26 June 2026.

## Position — Event Modeling as the spec for agents

Across the captured posts Dilger argues one consistent thesis from the [[event-modeling]] side of the
[[event-modeled-agent-design]] question, converging on the same conclusions as the harness thread
([[harness-engineering]], [[mitchell-hashimoto]], [[birgitta-bockeler]]) but arrived at independently:

- **AI amplifies unclear requirements, it doesn't fix them** — he reads the Faros AI Report's
  throughput-up / quality-down numbers as proof the fix must be upstream, a clear spec before code
  ([[dilger-faros-ai-report-amplifies-unclear-requirements]]).
- **You can't force an agent; you design the environment** — prompt engineering "didn't work"; Event
  Modeling supplies "clarity of intent before a single line of code," making good agent behavior the
  path of least resistance ([[dilger-spec-driven-development-applied]]). This is his
  [[spec-driven-development]] framing.
- **The model defines where logic may live** — a Claude Code anecdote where the agent ignored the
  event model and put a business rule in the routing layer; a written skill was necessary but not
  sufficient, so guardrails must be enforced ([[dilger-keep-command-handlers-pure]]).
- **Agents can do the discovery, too** — an agent that maps a product's UI into a visual storyboard,
  automating the Event Modeling discovery phase ([[dilger-automatic-domain-discovery-claude-code]];
  [[domain-discovery]]).
- **The spec is the work; the model is a *living* spec** — describes a background agent left in a
  loop that kept building from his board edits in real time ("one continuous flow," no hand-off), and
  his 24/7 pipeline: slice→`planned`→agent generates tests from the spec (the harness)→implements→PR,
  with an optional modeling-agent→builder-agent "full autopilot"
  ([[dilger-model-is-a-living-spec-always-on-agent]]; [[long-running-agents]],
  [[unattended-coding-agents]]).
- **"What if your requirements were something you could run?"** — his Craft Conference talk frames the
  whole thesis as one structured arc, idea→event model→code→back, with the model as a *living spec* that
  drives code generation and agentic coding; names the full **EM + [[event-sourcing]] + [[cqrs]] +
  [[agentic-coding]]** stack ([[dilger-craft-conf-idea-to-event-model-to-code]]).
- **DCB naming take (2026-06-15)** — argues [[dynamic-consistency-boundaries|DCB]] is just
  [[event-sourcing]] "what it always should have been," and the aggregate-based approach is the one that
  deserved a qualifier ("Static Consistency Boundaries"); DCB features prominently in the 2nd edition of
  *Understanding Eventsourcing* ([[dilger-dcb-is-what-event-sourcing-should-have-been]]).
- **The Event Modeling Agent Harness (2026-06-17)** — names/diagrams a 24/7 [[ralph-loop]] harness
  whose unit of work is the [[event-modeling]] *slice* (Draft→Ready→In Progress→Done), with the model's
  Given-When-Then scenarios as the BDD feedback backbone; cheap local models for coding, stronger for
  modeling/review; "coupling, not context-window" ([[dilger-event-modeling-agent-harness]];
  [[agent-harness]], [[long-running-agents]]).
- **The harness, implemented (2026-07-02)** — a two-part build report putting real hardware behind the
  harness: **3× on-prem Asus GX10** running **Gemma4 / Qwen3.6:27B via Ollama**, 6–10 agents in
  [[ralph-loop|ralph-loops]] 24/7, self-provisioning Build/Modeling-Kits, voice-to-text spawning modeling
  tasks — and the **claim-lock synchronization mechanism** (a slice hitting "Planned" is claimed+locked by
  exactly one agent → "In Progress"), which makes parallel multi-agent work collision-free *because slices
  are decoupled* ("no merge conflicts, no coupling hell"); "triplet of flexible architectures" = EM + ES +
  Slice-Based ([[dilger-local-llm-distributed-agent-setup-event-modeling]]).
- **Is Code still the source of truth? (2026-06-16)** — no: code is a *lagging indicator* of intent;
  the model/spec is the source of truth and AI (which generates code from the spec and detects drift)
  makes code "almost disposable" — the sharpest statement of his [[spec-driven-development]] thesis
  ([[dilger-is-code-still-the-source-of-truth]]).
- **Adding Perspectives to Event Modeling (2026-06-17)** — [[eventmodelers-ai]] feature: project one
  event model into audience-specific views (C-Level/Engineer/Architect/Stakeholder), first shipping a
  "High-Level View"; floats deriving architecture views / **C4** from the model — model-as-single-source
  projected into diagrams ([[dilger-adding-perspectives-to-event-modeling]]).
- **"Done is Done" — a new concept is a new slice, not an extension (2026-06-18)** — frames the
  [[open-closed-principle]] as a pre-build question ("can I build this without touching working code?");
  models a distinct concept (Guest Invitations) as a **new [[vertical-slice-architecture|slice]]** rather
  than extending existing logic, partly to avoid migrations/upcasters on a live event-sourced system; he
  modeled it in 30 min so an agent could implement it during a workshop — coupling-over-reuse
  ([[dilger-done-is-done-open-closed-new-slice]]).
- **Spec Editor goes free; the Miro ↔ Eventmodelers "Alliance" (2026-06-19)** — makes the Miro Toolkit
  **Spec Editor** free (define [[given-when-then|GWT]] scenarios per slice in Miro) and frames a
  two-surface tooling story: Model in Miro → Enhance with AI → Generate Code → Scale, keeping the Miro
  toolkit alongside [[eventmodelers-ai]] ([[dilger-spec-editor-free-eventmodelers-alliance]]).
- **Build kits — model to generated code "in 30 seconds" (2026-06-20)** — pitches build kits as a
  *learning* on-ramp: a beginner modeled two [[vertical-slice-architecture|slices]] and handed them to an
  agent to build; seeing the modeled system built to best practices makes learning ~10x faster
  ([[dilger-build-kits-model-to-generated-code]]).
- **Event Modeling as a knowledge hub; EmLang support (2026-06-20)** — reframes EM as the single
  accessible store of how a system works (not "modeled software"), a blueprint "for humans and for agents
  alike"; format-agnostic (YAML/JSON/Markdown/agent-via-[[model-context-protocol|MCP]]) and adds **EmLang**
  (a YAML dialect) as an import format to [[eventmodelers-ai]] ([[dilger-event-modeling-knowledge-hub-emlang]]).
- **How does DCB affect Event Modeling? "Not at all — it gets simpler" (2026-07-06)** — answers the
  Munich-conf "where does the Decision Model go?" question from the modeling side: with
  [[dynamic-consistency-boundaries|DCB]] you model **one swimlane per bounded context** and swimlanes
  revert to showing **integration** between systems/teams, not stream design; you never model a separate
  decision context because the **GIVEN** clause of the [[given-when-then|GWT]] scenarios supplies it; the
  Axon **Build Kit** generates the per-handler Criteria query + tests from the model; **tags are indices,
  not domain concepts** (added in Detailed-Modeling before handing a slice to an agent)
  ([[dilger-how-does-dcb-affect-event-modeling]]; [[event-modeling]], [[event-modeled-agent-design]]).
- **"Planning like it's Excel" — structure makes a spec legible to human and AI (2026-07-09)** —
  freeform whiteboards (and Event Models) **degrade** without an owner; an **Excel-like left-to-right
  grid** enforces a plot/storyboard *and* gives every element a **cell-reference coordinate**, so an
  agent can be told *"add a field in B3, adjust all dependents"* and can talk back the same way
  (*"there's a problem in B3…"*). "Clear structure… is what makes a spec legible to a human and an AI at
  once." He built [[eventmodelers-ai]] around this idea and is releasing a video series on agentic event
  modeling ([[dilger-planning-like-excel-legible-to-human-and-ai]]; [[event-modeled-agent-design]],
  [[ai-readable-code]]).
- **The harness is 20%; the first 80% is the problem (2026-06-29)** — his sharpest framing of the
  spec-over-harness thesis: building AI harnesses is "throwing technology at problems that can't be solved
  with technology alone"; the harness + code are only ~20% of the solution, the other **80% is clarifying
  requirements and understanding business processes** — a human/communications problem with "no technical
  solution." He focuses on the 80% (Event Modeling); the field over-invests in the 20% because "taming the
  agent is way more fun" ([[dilger-harness-is-20-percent-requirements-are-80]];
  [[harness-engineering]], [[spec-driven-development]]).

- **User stories need a framework; Event Modeling is it (2026-07-12)** — the requirements-first thesis
  for a mainstream audience: a user-story template is "a sentence structure with no framework behind it"
  (a mandated-user-stories team sat in weeks of writer's block); what was missing "wasn't discipline… it
  was a visual way to design the business solution." Add a timeline and "you always know what comes next";
  user stories then generate *from* the model, then the team hands over the modeled timeline itself
  (claimed 60–80% faster, no handovers) — the same model-as-source-of-truth inversion as
  [[dilger-is-code-still-the-source-of-truth]] ([[dilger-user-stories-need-event-modeling-framework]];
  [[event-modeling]], [[spec-driven-development]]).

- **Extending Event Modeling — an optional read-side "Query" (WHEN) (2026-06-29)** — his **first
  deliberate deviation from the EM "Standard."** Read-side [[given-when-then|GWT]] previously dropped the
  WHEN (GIVEN event → THEN data available); he adds an optional WHEN named **"Query"** (GIVEN registered /
  WHEN we query by email / THEN user returned) so scenarios can express *how* a read model is queried. It
  came out of independent Munich-conference discussions (and a prior chat with [[adam-dymitruk]]); he ships
  it as optional, explicitly seeking feedback, and had "noted every single feedback from the conference and
  addressed every one" ([[dilger-extending-event-modeling-query-when]]; [[event-modeling]], [[cqrs]]).
- **Draw.io model-in-code needs a framework + MCP guardrails (2026-06-30)** — agrees the model belongs in
  the repo/git, but raw draw.io XML fails the **agent** case: "AI has no framework to follow, no rules — so
  it's easy to make mistakes" (plus: unreadable XML, non-technicians can't contribute, uncommitted = doesn't
  exist). His fix on [[eventmodelers-ai]]: standardized JSON in git + local agent [[claude-agent-sdk|skills]]
  + an **[[model-context-protocol|MCP]] that validates changes before commit** so the agent self-corrects —
  the model-layer analogue of a deterministic external sensor ([[dilger-drawio-model-in-code]];
  [[ai-readable-code]], [[spec-driven-development]]).
- **Flea-market registration — non-technical stakeholder co-models, model→code→deploy in <30 min
  (2026-07-01)** — his wife asks for a flea-market registration form; he opens [[eventmodelers-ai]] and they
  **co-model by drawing screens without him ever naming or teaching the method** — "she has no idea what
  [Event Modeling] is. And she doesn't care." Under 30 min end-to-end because architecture decisions were
  pre-made ("one button click away from Building… Model → Code → Deploy → repeat"). Candid boundary: for a
  trivial app, ceremony-free AI coding would've been fine — "the more complex a system gets, the more that
  planning step earns its keep." The KB's strongest concrete [[vibe-modeling]] instance
  ([[dilger-flea-market-model-to-deploy]]; [[event-sourcing]], [[domain-discovery]]).
- **"The Shapes" — a named EM anti-pattern taxonomy (2026-08-10)** — recurring *mis*-shapes readable off a
  board's silhouette: the **bed** (one screen, many commands; the only hard red flag), **left chair** (one
  command, many events), **right chair** (one read model, many events), **shelf** (one slice, all
  scenarios); the rest are graded warnings, not defects. His most-used AI-skill `/wdyt` on
  [[eventmodelers-ai]] auto-detects them — **agent as model-reviewer**, upstream of code
  ([[dilger-the-shapes-event-modeling-anti-patterns]]; [[event-modeling-anti-patterns]]).
- **Free-form drawings the agent reads and draws back (2026-08-09)** — adds a freeform layer beside the
  Excel-like grid; voice-mode sketching; **the agent reads the drawings for context** (inside/outside a
  lasso, arrow direction) and, via **[[model-context-protocol|MCP]] tools, draws *back*** (sketches, arrows,
  question marks) as part of the `/wdyt` review — "a remote colleague joining the Board." A new EM×agents
  interaction modality beyond structured YAML ([[dilger-agentic-collaboration-freeform-drawings]]).
- **"99% of software is boring — it's only two patterns" (2026-08-08)** — every system reduces to **State
  change + State view** ([[cqrs]] write/read); he tells workshops "four" to not bore them. The point:
  the *repetitive* nature is exactly what makes EM a great fit for AI — "tight guardrails and clear
  instructions instead of an open-ended blank page"; EM alone suffices for SDD but he's bridging it to
  Spec-Kit/Kiro/Spec-Kitty to "meet companies where they are"
  ([[dilger-99-percent-software-boring-two-patterns]]; [[vibe-modeling]], [[spec-driven-development]]).
- **A "linter" for Event Modeling (2026-08-07)** — a reader (William Power) used **Claude Code to compare
  boards against Dilger's public "well-structured" reference catalog** to judge structural (not semantic)
  soundness; Dilger mulls it as an [[eventmodelers-ai]] feature — a second agent-driven EM quality gate
  alongside `/wdyt` ([[dilger-event-model-structure-linter-reference-catalog]]; [[event-modeling-anti-patterns]]).
- **Highlighting: screen markers the agent reads (2026-08-12)** — a long-taught best practice (complex
  screens are fine; mark the *one* part that matters *right now*) becomes an [[eventmodelers-ai]] feature
  (selectable markers, optional blur outside), and — "again something I didn't think of" — the markers
  **give context to agents**, which "can read them… validate them and use them to build the UI." A third
  machine-readable modeling surface after grid coordinates and freeform marks
  ([[dilger-highlighting-markers-give-context-to-agents]]; [[agent-readable-model-artifacts]]).
- **ESDM export — the model in whatever format the agent asks for (2026-08-13)** — after meeting
  [[golo-roden]] at the Munich conference, he adds export of any Event Model to
  [[esdm-event-sourced-domain-modeling|ESDM]] via **UI, API, MCP and CLI**: "so your agent can request any
  modeled slice or chapter in the format it needs." Under an hour to build because "the whole plattform is
  an extension model." He will work *with* Roden on an ESDM extension carrying Event Modeling's **timeline**
  notion. The first captured instance of an EM board tool emitting a third-party open format — board-camp
  and file-camp converging ([[dilger-eventmodelers-supports-esdm-export]];
  [[agent-readable-model-artifacts]], [[em-standardization-foundation]]).
- **Where spec-driven development goes wrong (2026-08-14)** — his first published *caveat against his own
  thesis*: burnout from supervising 5 parallel agent sessions "like a kindergartner," and the observation
  that "a few years ago we were obsessed with protecting people from context switching; now we call the
  same thing productivity." The failure mode: teams "stop solving problems and just describe them, and then
  hand it to AI and hope it figures out the solution — that's not being in charge, that's checking out
  before it gets interesting." Done right, SDD "still means you're in charge of solving the problem. You
  hand over the boring part" ([[dilger-describing-without-solving-burns-you-out]];
  [[spec-driven-development]], [[comprehension-debt]]).

## The self-training modeling agent (2026-08) — his strongest evidence to date

Late August is where Dilger's material stops being framing and produces something the KB can point at
([[dilger-one-million-tokens-self-training-modeling-agent]] 08-27, [[dilger-modeling-agent-improved-by-learning-loop]] 08-28). He put the
[[eventmodelers-ai]] Modeling Agent in a loop against a **grader**: model a requirement set, structurally
diff the output against a corpus of his own hand-crafted "well crafted" models, have the agent rewrite
its own skill files from the differences, re-model, repeat. Local hardware, QWEN3.7:27b, >1M tokens in a
night, running continuously.

It matters for this page because it is **the first captured Dilger claim with a mechanism behind it
rather than an assertion**. The loop recovered three conventions he holds tacitly but had never stated as
rules — storylines over plain GWT for Read Models on Automations
([[dilger-todo-lists-storylines-one-scenario]]), linked elements bridging events across chapters, and Read-Model copies
instead of back arrows. He also reported the failure mode honestly: roughly every fifth iteration
degrades as the model nears its token budget ([[token-budget-quality-cliff]]), which is the kind of
disclosure the "vendor marketing" caveat below does not predict.

The caveat still applies in a different form: the grader is *his own taste*, so "improvement" means
convergence on Dilger's conventions rather than on an external standard, and there is no held-out
evaluation. See [[event-modeled-agent-design]] and [[loop-engineering]].

## In the KB

He is the most active *practitioner-evangelist* voice for [[event-modeled-agent-design]], sitting
alongside [[adam-dymitruk]] (the method's creator) and [[john-wilger]] (the worked factory pipeline).
Where Dymitruk supplies the role-mapping claim and Wilger a shipping example, Dilger supplies the
day-to-day **why** — requirements, guardrails, and the spec-first operating model — plus a commercial
platform betting on it. Caveat: most of his captured material is LinkedIn marketing for
[[eventmodelers-ai]] and the *Spec Driven* book — strong on framing, light on independent evidence.

His **[[dilger-triplet-flexible-agent-enabled-architecture|"Triplet"]]** article (2026-07-26) is the
definitive naming of the operating model that runs through all of the above: a **flexible, agent-enabled
architecture** = [[event-modeling|Event Modeling]] (plan) + [[vertical-slice-architecture|Vertical Slices]]
(structure) + [[event-sourcing|Event Sourcing]] (store), used *in union*, with coupling as the disease it
cures and requirements treated as *part of* the architecture. Its agent seam — an agent works one slice,
needing only that slice's context + event log + model, so adding agents makes delivery faster not slower —
is the structural precondition behind [[dilger-event-modeling-agent-harness|his agent harness]]. It is the
full version of the long-stubbed [[dilger-hold-my-beer-engineer|"Event Modeling applied" teaser]].

## Related

[[model-as-code-vs-model-as-language]]

_Source pages: [[dilger-one-million-tokens-self-training-modeling-agent]] · [[dilger-modeling-agent-improved-by-learning-loop]] · [[dilger-todo-lists-storylines-one-scenario]] · [[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] · [[dilger-keep-command-handlers-pure]] ·
[[dilger-automatic-domain-discovery-claude-code]] · [[dilger-model-is-a-living-spec-always-on-agent]] ·
[[dilger-hold-my-beer-engineer]] · [[dilger-craft-conf-idea-to-event-model-to-code]] ·
[[dilger-dcb-is-what-event-sourcing-should-have-been]] · [[dilger-event-modeling-agent-harness]] ·
[[dilger-is-code-still-the-source-of-truth]] · [[dilger-adding-perspectives-to-event-modeling]] ·
[[dilger-done-is-done-open-closed-new-slice]] · [[dilger-spec-editor-free-eventmodelers-alliance]] ·
[[dilger-build-kits-model-to-generated-code]] · [[dilger-event-modeling-knowledge-hub-emlang]] ·
[[dilger-harness-is-20-percent-requirements-are-80]] · [[dilger-how-does-dcb-affect-event-modeling]] ·
[[dilger-planning-like-excel-legible-to-human-and-ai]] ·
[[dilger-user-stories-need-event-modeling-framework]] ·
[[dilger-extending-event-modeling-query-when]] · [[dilger-drawio-model-in-code]] ·
[[dilger-flea-market-model-to-deploy]] · [[event-modeling-event-sourcing-podcast]] ·
[[dilger-triplet-flexible-agent-enabled-architecture]] ·
[[dilger-spec-driven-tools-need-event-modeling-front-half]] (EM as the front half of Spec-Driven tools; the `eventmodelers export --spec-kitty` bridge, 2026-08-02) ·
[[dilger-real-cost-of-ai-is-second-order]] (the real cost of AI coding is second-order / comprehension debt, 2026-07-27) ·
[[dilger-the-shapes-event-modeling-anti-patterns]] ("The Shapes" EM anti-pattern taxonomy + `/wdyt` reviewer, 2026-08-10) ·
[[dilger-agentic-collaboration-freeform-drawings]] (agent reads/draws freeform board marks via MCP, 2026-08-09) ·
[[dilger-99-percent-software-boring-two-patterns]] (State change / State view; repetition = AI-friendliness, 2026-08-08) ·
[[dilger-event-model-structure-linter-reference-catalog]] (EM "linter" via Claude Code vs a reference catalog, 2026-08-07) ·
[[dilger-highlighting-markers-give-context-to-agents]] (screen markers as agent context, 2026-08-12) ·
[[dilger-eventmodelers-supports-esdm-export]] (ESDM export via UI/API/MCP/CLI; joint timeline extension with Roden, 2026-08-13) ·
[[dilger-describing-without-solving-burns-you-out]] (where SDD goes wrong: describing instead of solving, 2026-08-14)._
