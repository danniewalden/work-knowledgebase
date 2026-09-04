---
title: "Dilger — Spec-Driven tools need Event Modeling as their front half"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [dilger-spec-driven-tools-need-event-modeling-front-half]
raw_file: [raw/notes/dilger-spec-driven-tools-need-event-modeling-front-half.md]
tags: [spec-driven-development, event-modeling, event-modeled-agent-design, agentic-coding, focus]
---

# Dilger — Spec-Driven tools need Event Modeling as their front half

LinkedIn post by **[[martin-dilger]]** (2026-08-02), captured verbatim. Raw:
`raw/notes/dilger-spec-driven-tools-need-event-modeling-front-half.md`. A genuinely new EM × agents
seam: **Event Modeling as the problem-understanding front half that feeds Spec-Driven Development
toolkits.**

## What it says

- Dilger tested **Spec Kitty** (a skills set that guides the "specification" phase) with deliberately
  vague requirements. It dug in with questions — good — but **its third question was already about the
  tech stack**, and it produced a "domain model" (book, catalog entry) almost immediately, "before it had
  any real grasp of the problem." Questions jumped between features in arbitrary order: a *technical*
  person could follow, a **business stakeholder could not**.
- Result: **46 markdown files after 20 minutes**, high-level spec down to implementation tasks — then it
  suggested *implementing*. "Who is reading all of that? Who is maintaining it?" So much assumption
  (model shape, tech choices) gets baked in **before anyone agreed on the problem**. "Skipping the visual
  model doesn't remove the complexity. It just removes the thing that was managing it."
- He's writing a book called **"Spec Driven"** and deliberately **leaving these tools out** — not because
  they're bad, but because every team he's watched work this way struggles with the markdown sprawl.
- **The resolution (the seam):** in a workshop he combined **AWS Kiro + Event Modeling** — the event
  model "did the hard part: breaking the problem down, getting everyone aligned on what's actually
  happening," then a skill translated the model directly into **Kiro Tasks**; he did the same for Spec
  Kitty. Because the **Event Modeling Format is standardized and documented**, this becomes a CLI bridge
  in the Event Modelers CLI: **`eventmodelers export --spec-kitty`** (Spec-Kit, Spec-Kitty, Kiro, …).
  "The tools aren't the problem. Skipping the digging is."

## Why it matters here

- A concrete instance of the KB's recurring thesis that the hard 80% is **requirements /
  problem-understanding** ([[dilger-harness-is-20-percent-requirements-are-80]]) — here aimed at
  [[spec-driven-development]] tooling specifically: EM is the **front half** that gives SDD toolkits
  "something real to work from," a **bridge** rather than a competitor. Extends
  [[event-modeled-agent-design]] with a new export/interop direction (EM → SDD task lists) and rhymes with
  [[dilger-planning-like-excel-legible-to-human-and-ai]] (structure is what keeps a spec legible to human
  *and* agent) and [[dilger-user-stories-need-event-modeling-framework]].
- Caveat: a LinkedIn musing / product-roadmap note (the CLI bridge is announced, not shipped); vendor
  framing (eventmodelers.ai).

## Links

Entities: [[martin-dilger]], [[eventmodelers-ai]]. Concepts: [[spec-driven-development]],
[[event-modeling]], [[event-modeled-agent-design]], [[agentic-coding]], [[domain-discovery]].
Related sources: [[dilger-harness-is-20-percent-requirements-are-80]],
[[dilger-user-stories-need-event-modeling-framework]],
[[dilger-planning-like-excel-legible-to-human-and-ai]], [[dilger-craft-conf-idea-to-event-model-to-code]].

_Raw source: `raw/notes/dilger-spec-driven-tools-need-event-modeling-front-half.md`._
