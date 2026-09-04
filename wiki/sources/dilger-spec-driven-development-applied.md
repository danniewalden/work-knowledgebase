---
title: "Dilger — Spec-Driven Development applied"
type: source
created: 2026-06-13
updated: 2026-06-13
sources: [dilger-spec-driven-development-applied]
raw_file: [raw/articles/dilger-spec-driven-development-applied.md]
tags: [event-modeling, agentic-coding, spec-driven-development, harness, prompt-engineering, focus]
---

# Dilger — Spec-Driven Development applied

LinkedIn post by **[[martin-dilger]]** (2026-06-11, edited; carries a video walkthrough and a
`#specdrivenbook` hashtag). The clearest statement of his core thesis: **you can't force an agent;
you design the environment.** Raw capture: `raw/articles/dilger-spec-driven-development-applied.md`.

## Key points

- His early agent attempts were "miserable" — more time wrestling the AI than building. The
  industry's first answer, **prompt engineering**, he dismisses as "a desperate attempt to force a
  language model to behave through better wording" that "didn't work." (A pointed counter to the
  prompt-as-lever view; compare the harness thread's move from prompting to environment design —
  [[harness-engineering]], [[context-engineering]].)
- Memorable framing: **"AI is like a teenager. It doesn't care what you say."** Getting angry just
  earns a hollow "you are absolutely right." The more he tried to *control* it, the worse it got.
- The fix "wasn't a better prompt. It was a better environment." He already had [[event-modeling]] —
  "a process that forces clarity of intent before a single line of code gets written" — and connected
  it to AI: **every process that worked well without AI worked even better with AI**, because those
  processes "made it easier to do the right thing than the wrong thing."
- Closing principle: **design an environment where good behavior is the path of least resistance, and
  build feedback loops that constantly answer one question — "am I holding this right?"** This is
  [[feedforward-and-feedback-controls]] / [[fitness-functions]] in plain language, and the
  guides-and-sensors logic of [[harness-engineering]] arrived at independently from the Event Modeling
  side.

## Why it matters

This is the conceptual spine under his other posts: spec-driven development = Event Modeling's
"clarity of intent before code" repurposed as the agent's operating environment. It supplies the
*method* claim that [[event-modeled-agent-design]] tracks, and names the discipline
([[spec-driven-development]]) the rest of the Dilger material sits inside.

## Caveats

Marketing post for a workshop and the *Spec Driven* book; the video (the actual worked walkthrough)
isn't captured here. Assertion-level, not a case study.

## Links

Entities: [[martin-dilger]], [[eventmodelers-ai]]. Concepts: [[spec-driven-development]],
[[event-modeling]], [[event-modeled-agent-design]], [[agentic-coding]], [[harness-engineering]],
[[context-engineering]], [[feedforward-and-feedback-controls]].
Related sources: [[dilger-faros-ai-report-amplifies-unclear-requirements]],
[[dilger-keep-command-handlers-pure]], [[dilger-automatic-domain-discovery-claude-code]],
[[hashimoto-my-ai-adoption-journey]], [[jwilger-agent-skills-event-modeling]].
