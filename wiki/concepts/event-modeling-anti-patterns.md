---
title: Event Modeling Anti-Patterns ("The Shapes")
type: concept
created: 2026-08-10
updated: 2026-09-04
sources: [dilger-the-shapes-event-modeling-anti-patterns, dilger-event-model-structure-linter-reference-catalog, dilger-podcast-episode-47-agentic-modeling-audit-trails, dilger-ui-only-interactions-filtering]
tags: [event-modeling, event-modeling-anti-patterns, event-modeled-agent-design, focus]
---

# Event Modeling Anti-Patterns ("The Shapes")

A diagnostic vocabulary from [[martin-dilger]] for spotting problems in an [[event-modeling|event model]]
by its **silhouette** — the structural shape of the board tells you where to look before you read the
detail. Introduced in [[dilger-the-shapes-event-modeling-anti-patterns]] (2026-08). Where the method itself
gives you 3 building blocks and 4 (constructive) patterns, this is the complementary catalog of *mis*-shapes.

## "The Shapes"

- **The bed** — *one screen, many commands.* The only **hard red flag**: a single UI surface driving many
  commands usually signals an over-loaded screen / muddy command boundaries.
- **The left chair** — *one command, many events.* A **warning**, not wrong by default (a command can
  legitimately emit several events) — look closer.
- **The right chair** — *one read model, many events.* A **warning**: a view fed by many event types; may
  be fine, may signal a bloated projection.
- **The shelf** — *one slice, all scenarios.* A **warning**: a single slice absorbing every scenario.

Severity is **graded**: only the bed is a categorical problem; the chairs and shelf are heuristics — "places
to look closer before you commit to a design," not defects. Dilger's line: "Once you see them, you can't
unsee them."

**Not a Shape, but an anti-pattern the method names elsewhere: Commands invented to justify Events.**
[[dilger-ui-only-interactions-filtering]] (2026-07-31) — filtering, sorting, expanding a row, switching
a tab *"are all views on data you already have. Model them as Views, not as Commands looking for an
Event to justify them."* Unlike the Shapes this is not readable off a silhouette; it shows up as
domain-meaningless events on the swimlane. See [[event-modeling]] and [[screens-as-specification]].

## Why it matters for agents

The taxonomy is built to be **agent-operable**. Dilger's most-used AI-skill on [[eventmodelers-ai]],
invoked with **`/wdyt`** ("what do you think"), walks a model, challenges assumptions, and calls out these
anti-pattern shapes where they apply — an **agent as model-reviewer** working *upstream of code*, on the
spec itself. This complements the two dominant directions in [[event-modeled-agent-design]] (agent *authors*
the model; model *governs* the agent) with a third: agent *critiques* the model.

A sibling idea from the same week attacks model quality from the other end: an **EM "linter"** that grades a
board's **structure** (not its correctness) by having Claude Code compare it against a curated **reference
catalog** of well-structured boards ([[dilger-event-model-structure-linter-reference-catalog]]). Heuristic
shape-detection and reference-conformance are two routes to the same goal — an automated, agent-run quality
gate on the model, sitting upstream of the [[given-when-then|GWT]] acceptance gates that grade generated
code.

## A second class: anti-patterns the *agent* induces (Ep 47, date unresolved)

"The Shapes" catalogues bad models humans draw. [[dilger-podcast-episode-47-agentic-modeling-audit-trails]]
surfaces the inverse — a model degraded by an agent pointed at it.

The `/wdyt` skill's first version *"flooded the model with 100 comments inventing hypothetical gaps."*
[[adam-dymitruk]] names why that is worse than ordinary review noise: an over-eager agent flooding a
[[given-when-then|given-when-then]] list with edge cases *"can make a simple slice look far more complex
than it really is, **since event modeling is visual**."* The damage is to **legibility**, the property
the whole method trades on — and a bloated slice is still *well-formed*, so neither a linter nor a
structural diff against a reference catalog would flag it.

**Name it over-specification, and note the fix is a restriction on the reviewer, not on the model:**
*"don't just look at what is there — don't comment on something because it's not specified. Just look at
what is there and make sense of it, then give me comments. And then it got significantly better."*
The method's own defence predates the tooling: **specification by example** — *"draw a few
representative example paths and trust the implementer to infer the rest, rather than trying to specify
everything."*

This is the same failure [[bockeler-tdd-inside-the-agent-loop|Böckeler]] found one altitude down, where
agent-authored micro-tests suppressed up-front design: **an agent inventing its own acceptance criteria
degrades the artifact it is checking.** Both point at the same rule — the criteria come from outside the
loop.

*(**Date unresolved** — see the source page; it post-dates 2026-04-27 and may be a previously unpolled
channel. **Show-notes level, not verified against audio. VENDOR SELF-REPORT** — the skill ships on
[[eventmodelers-ai]]. The comment counts are impressions.)*

## Relationships

Extends [[event-modeling]] (the constructive patterns' negative image) and [[event-modeled-agent-design]]
(agent-as-reviewer seam). Adjacent to [[ai-readable-code]] (structural conformance as a machine-checkable
property) and [[given-when-then]] (the downstream, code-level gate). A platform feature of
[[eventmodelers-ai]].

## Caveat

Dilger's own coinage from workshop/conference experience; the shape names are informal and **not part of the
EM "Standard."** No external validation, and the reference-catalog "linter" is a mooted feature, not a
shipped/evaluated one.

_Source pages: [[dilger-the-shapes-event-modeling-anti-patterns]] · [[dilger-event-model-structure-linter-reference-catalog]] · [[dilger-podcast-episode-47-agentic-modeling-audit-trails]] · [[dilger-ui-only-interactions-filtering]]._
