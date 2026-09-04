---
title: Eventmodelers.ai
type: entity
created: 2026-06-13
updated: 2026-09-04
sources: [dilger-git-as-primary-persistence-for-event-models, dilger-ui-only-interactions-filtering, dilger-only-engineers-care-about-consistent-systems, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-agentic-engineer-program-stack-agnostic-spec, dilger-one-million-tokens-self-training-modeling-agent, dilger-modeling-agent-improved-by-learning-loop, dilger-todo-lists-storylines-one-scenario, dilger-eventmodelers-supports-esdm-export, dilger-highlighting-markers-give-context-to-agents, dilger-spec-driven-development-applied, dilger-automatic-domain-discovery-claude-code, dilger-faros-ai-report-amplifies-unclear-requirements, dilger-model-is-a-living-spec-always-on-agent, dilger-spec-editor-free-eventmodelers-alliance, dilger-build-kits-model-to-generated-code, dilger-event-modeling-knowledge-hub-emlang, dilger-planning-like-excel-legible-to-human-and-ai, dilger-extending-event-modeling-query-when, dilger-drawio-model-in-code, dilger-flea-market-model-to-deploy, dilger-triplet-flexible-agent-enabled-architecture, dilger-the-shapes-event-modeling-anti-patterns, dilger-agentic-collaboration-freeform-drawings, dilger-event-model-structure-linter-reference-catalog]
tags: [tool, platform, event-modeling, agentic-ai, spec-driven-development, focus]
---

# Eventmodelers.ai

An **agentic software modeling platform** being built by **[[martin-dilger]]**, positioned to "bring
business, engineering and AI together" — i.e. [[event-modeling]] as the shared spec that drives
[[agentic-coding]]. Known only from Dilger's LinkedIn posts so far (no captured product docs), so this
page is provisional.

## What's claimed

- A platform where **Domain Discovery runs on autopilot**: an agent explores a product's live UI and
  produces a visual storyboard / timeline of how it actually works
  ([[dilger-automatic-domain-discovery-claude-code]]; [[domain-discovery]]).
- Built on composable agent **skills** ("it´s just another skill") that can be extended to comment on
  screens or find UX flaws — the same [[claude-agent-sdk|skills]] pattern as
  [[prooph-board]]/[[jwilger-agent-skills-event-modeling]].
- Embodies Dilger's [[spec-driven-development]] thesis: design the environment so the agent's good
  behavior is the path of least resistance, with the Event Model as the source of truth.
- Operated as a **live spec**: Dilger describes a background agent that builds continuously from board
  edits, and a slice→tests-as-harness→implement→PR loop, optionally fully autonomous
  ([[dilger-model-is-a-living-spec-always-on-agent]]; [[long-running-agents]]).

## Storylines, and an agent that trains itself (2026-08)

**Storylines shipped 2026-08-15** ([[dilger-todo-lists-storylines-one-scenario]]): one narrative GWT scenario in place of
several repetitive ones, laid out vertically below a slice, previously called "Vertical Specs." Aimed at
being legible "by human and AI alike." See [[given-when-then]].

**The Modeling Agent now improves itself** ([[dilger-one-million-tokens-self-training-modeling-agent]] 08-27,
[[dilger-modeling-agent-improved-by-learning-loop]] 08-28). Dilger runs it in a grading loop against a corpus of hand-crafted good
models, structurally diffing output and letting the agent rewrite its own skills. Reported gains: proper
translation modeling, TODO lists specified via storylines, screens broken into functional blocks with
dedicated Read Models (explicitly *"this allows to generate the UI much more easily"*), and back arrows
avoided via Read Model/Screen copies. Runs on **local hardware, QWEN3.7:27b** — the platform's leverage is
claimed to come from the rubric, not from model scale.

This is the platform's most substantive evidence so far, and it is still vendor self-report: no held-out
set, no numbers beyond a token count, and "better" defined as closer to the founder's own models. But it
is a *mechanism*, which the earlier captures were not. He also discloses a failure mode against interest —
the [[token-budget-quality-cliff]]. See [[event-modeled-agent-design]], [[loop-engineering]].

## Where it sits

One of a small cluster of **AI-assisted Event Modeling tools** in the KB — alongside [[qlerify]]
(generates models + code from descriptions) and [[prooph-board]] (online EM tool + Cody Engine +
agent skills/MCP). Distinctive angle: **discovery-from-running-UI** and a spec-driven agentic build
loop, rather than diagram-authoring assistance. Evidence is vendor-self-report; no demo, pricing, or
independent review captured.

**Two-surface story (2026-06-19).** Dilger frames the platform as an "Alliance" with the existing
**Miro Toolkit** rather than a replacement: *Model in Miro → Enhance with AI → Generate Code → Scale to
Enterprise*. He has begun moving previously-commercial Miro features to free, starting with the **Spec
Editor** for defining [[given-when-then|GWT]] scenarios per slice
([[dilger-spec-editor-free-eventmodelers-alliance]]).

**"Planning like it's Excel" — the core design bet (2026-07-09).** Dilger says he **built the platform
around the Excel idea**: an **Excel-like left-to-right grid** rather than a freeform whiteboard, chosen
because freeform models degrade without an owner while a grid enforces a plot/storyboard. The
distinctive claim is **coordinate-addressability** — every element has a cell reference, so an agent can
be instructed *("add a field in B3, adjust all dependents")* and report back *("there's a problem in
B3…")* against precise handles. Pitched as what makes one spec "legible to a human and an AI at once"
([[dilger-planning-like-excel-legible-to-human-and-ai]]; [[ai-readable-code]],
[[event-modeled-agent-design]]).

**Build kits + knowledge hub (2026-06-20).** Two further positioning moves: (1) **build kits** — "from
model to generated code in 30 seconds," pitched as a *learning* on-ramp where a modeled
[[vertical-slice-architecture|slice]] is handed to an agent to build
([[dilger-build-kits-model-to-generated-code]]); (2) the platform as a **knowledge hub** — the single
accessible store of how a system works and the blueprint "for humans and agents alike" — made
**format-agnostic** with **EmLang** (a YAML dialect) added as an import format alongside JSON/Markdown and
agent ingestion via [[model-context-protocol|MCP]] ([[dilger-event-modeling-knowledge-hub-emlang]]).

**Model-in-code workflow + MCP guardrails (2026-06-30).** Dilger positions the platform against keeping an
Event Model as raw **draw.io XML** in git. He agrees the model belongs in the repo, but raw XML gives an
agent "no framework to follow, no rules." The platform's supported loop: edit → **export standardized
JSON** → version in git → **local agent [[claude-agent-sdk|skills]] manipulate the JSON** → an
**[[model-context-protocol|MCP]] validates changes before commit** (guardrails + feedback so the agent
self-corrects) → visualize in the **Model-Viewer** (shareable with anyone) → generate code via **Build-Kits
(Node, Java, Kotlin)**. The MCP-as-validator is the distinctive claim — the model-layer analogue of a
deterministic external code-health sensor ([[dilger-drawio-model-in-code]]; [[ai-readable-code]]).

**Model → Code → Deploy demonstrated (2026-07-01).** The flea-market vignette is the platform's clearest
end-to-end demo: a non-technical stakeholder (his wife) **co-modelled by drawing screens without being
taught the method**, and the app was modelled, built, and deployed in **under 30 minutes** because the
platform pre-makes the setup/architecture/event-store decisions — "one button click away from Building…
Model → Code → Deploy → repeat." Doubles as the KB's strongest [[vibe-modeling]] instance and backs the
build-kits "model to code" pitch ([[dilger-flea-market-model-to-deploy]]).

**First method extension shipped — read-side "Query" (2026-06-29).** The platform is where Dilger ships the
optional read-side WHEN ("Query") element (see [[event-modeling]]) — the first deviation from the EM
standard, born of Munich-conference feedback, released as optional and "closest to the standard" tooling
([[dilger-extending-event-modeling-query-when]]).

Dilger's **[[dilger-triplet-flexible-agent-enabled-architecture|"Triplet"]]** article (2026-07-26) states
the thesis the platform is built to serve: app.eventmodelers.ai is "specifically built around the
Triplet-Architecture" — plan (Event Modeling) / build (Event Sourcing) / structure (slices) — with agents via
provided skills + an MCP server, and the "nasty problems" solved as platform features: **Git-backed version
control**, JSON import/export (backup/restore), and **Build-Kit code generation**.

**Agent-as-reviewer features (2026-08).** Two model-quality capabilities in the same week: (1) the **`/wdyt`
("what do you think") AI-skill** — Dilger's most-used — walks a model, challenges assumptions, and flags the
[[event-modeling-anti-patterns|"Shapes" anti-patterns]] ([[dilger-the-shapes-event-modeling-anti-patterns]]);
and (2) a mooted **EM "linter"** grading a board's *structure* against a curated reference catalog via Claude
Code ([[dilger-event-model-structure-linter-reference-catalog]]). Both put an agent on the *model*, upstream
of the code-level [[given-when-then|GWT]] gates.

**Free-form drawings the agent reads and draws (2026-08-09).** A freeform layer added beside the Excel-like
Chapters grid: users sketch (including by **voice**), lasso nodes and write questions inside; **agents read
the drawings as spatial/graph context** (inside/outside, arrow direction), and via **[[model-context-protocol|MCP]]
tools the agent draws *back*** — the `/wdyt` review now returns sketches, arrows and question marks, not just
text. Dilger: "like having a colleague somewhere remote joining the Board." Extends the platform's
human-and-agent-legibility bet ([[dilger-planning-like-excel-legible-to-human-and-ai]]) from structured
coordinates to freeform marks ([[dilger-agentic-collaboration-freeform-drawings]]).

**Screen markers (2026-08-12).** A third machine-readable surface: select any region of a screen, with
optional dynamic blurring outside it, to mark what matters *right now* on the timeline. Dilger reports the
agent-facing payoff as unplanned — agents "can read them… validate them and use them to build the UI."
Also a craft note on the platform's screens: he now generates **HTML screens off the provided design
systems** rather than sketching, while keeping "ugly screens are better" for early modeling
([[dilger-highlighting-markers-give-context-to-agents]]; [[agent-readable-model-artifacts]]).

**Format-agnostic export, delivered (2026-08-13).** The "knowledge hub / format-agnostic" positioning
([[dilger-event-modeling-knowledge-hub-emlang]]) gets its first *third-party* format: the platform now
exports any Event Model to [[esdm-event-sourced-domain-modeling|ESDM]] via **UI, API,
[[model-context-protocol|MCP]] and CLI**, "so your agent can request any modeled slice or chapter in the
format it needs." Dilger credits an **extension-model architecture** (languages, datastores, formats are
all extensions) for making it an under-an-hour change, and announces joint work with [[golo-roden]] on an
ESDM extension for the EM **timeline**. This is the platform's strongest interop claim to date and the
point where the board camp and the file camp stop being alternatives
([[dilger-eventmodelers-supports-esdm-export]]; [[agent-readable-model-artifacts]]).

## Platform changes recorded in the 2026-07 → 2026-09 captures

**All of the following are VENDOR SELF-REPORT — Dilger's own platform, his own posts — and several are
announcements rather than reports of use.** The marker belongs at each use on any page that cites them.

- **Git as primary persistence, and BYODS** — one repository per board, branching supported, no
  relational database required (*"No relational database. All data lives in Git."*), with
  Redis/S3/YAML/SharePoint named as possible stores and **WORM-drive storage offered for auditability**.
  Prior stores: Supabase/Postgres, then SQLite (*"Both are live and used heavily"*, unquantified). The
  model store is itself event-sourced.
  ([[dilger-git-as-primary-persistence-for-event-models]], 2026-09-02 — **announced as being added, not
  reported in use; and no regulation, standard or auditor is named behind the WORM claim.**)
- **Multi-Screen Views, HTML Views, built-in Query support**, and `npx @eventmodelers/cli init-modeling`
  to connect an agent in ~15 seconds ([[dilger-ui-only-interactions-filtering]], 2026-07-31).
- **Screen Preview** — hand-sketched screens, HTML mockups and Figma screens in one storyline
  ([[dilger-only-engineers-care-about-consistent-systems]], 2026-09-01).
- **The `/wdyt` gap-finding skill, worked and tuned** — an agent reads slices and posts
  clarifying-question comments; restricting it to comment only on what is *present* (no invented
  scenarios) turned ~100 noisy comments into useful ones. **The "100 comments" → "genuinely useful"
  pairing is impressions, not counts to compare.** And **two agents (Claude Code + Hermes) modelling
  concurrently** alongside Dilger, reported as *"indistinguishable from modeling with humans"* —
  **IMPRESSION NOT MEASUREMENT**, a felt comparison on his own platform, and show-notes level rather
  than verified against audio.
  ([[dilger-podcast-episode-47-agentic-modeling-audit-trails]], **date unresolved — do not assign one**.)
- **Build Kits** named for Axon, Marten, Cratis, Emmett (Node) and Python, with a 12-month commercial
  EM-Studio licence bundled into the **paid** *Agentic Engineer* programme (on-prem hostable for
  enterprises); the *Spec Driven* book ships **2026-10-16**. The programme's headline affordance —
  *"they can even switch stacks mid-course or build in parallel in all Stacks"* — is
  **VENDOR SELF-REPORT · marketing**, hedged by its own author (*"almost doesn't matter"*) and
  **demonstrated nowhere** ([[dilger-agentic-engineer-program-stack-agnostic-spec]], 2026-09-03).
- **Channel note for the research config:** `eventmodelers.ai/docs/podcast` is a **separate and more
  current episode index** than podcast.eventmodeling.org — Episode 47 exists only there and appears in
  neither the RSS feed nor the `.org` index. It should be polled as its own channel.

_Source pages: [[dilger-automatic-domain-discovery-claude-code]] ·
[[dilger-spec-driven-development-applied]] ·
[[dilger-faros-ai-report-amplifies-unclear-requirements]] ·
[[dilger-model-is-a-living-spec-always-on-agent]] ·
[[dilger-spec-editor-free-eventmodelers-alliance]] ·
[[dilger-build-kits-model-to-generated-code]] ·
[[dilger-event-modeling-knowledge-hub-emlang]] ·
[[dilger-planning-like-excel-legible-to-human-and-ai]] ·
[[dilger-extending-event-modeling-query-when]] · [[dilger-drawio-model-in-code]] ·
[[dilger-flea-market-model-to-deploy]] ·
[[dilger-triplet-flexible-agent-enabled-architecture]] ·
[[dilger-the-shapes-event-modeling-anti-patterns]] · [[dilger-agentic-collaboration-freeform-drawings]] ·
[[dilger-event-model-structure-linter-reference-catalog]] ·
[[dilger-highlighting-markers-give-context-to-agents]] · [[dilger-eventmodelers-supports-esdm-export]] · [[dilger-one-million-tokens-self-training-modeling-agent]] · [[dilger-modeling-agent-improved-by-learning-loop]] · [[dilger-todo-lists-storylines-one-scenario]] ·
[[dilger-git-as-primary-persistence-for-event-models]] · [[dilger-ui-only-interactions-filtering]] ·
[[dilger-only-engineers-care-about-consistent-systems]] ·
[[dilger-agentic-engineer-program-stack-agnostic-spec]] ·
[[dilger-podcast-episode-47-agentic-modeling-audit-trails]] (**DATE UNRESOLVED**)._
