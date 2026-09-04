---
title: "Dilger — Last night, I spent 1 Million+ Tokens to train my Modeling Agent"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-one-million-tokens-self-training-modeling-agent]
raw_file: [raw/notes/dilger-one-million-tokens-self-training-modeling-agent.md]
tags: [event-modeling, agentic-coding, loop-engineering, self-improvement, evals, focus]
---

# Dilger — Last night, I spent 1 Million+ Tokens to train my Modeling Agent

LinkedIn post by **[[martin-dilger]]**, 2026-08-27. Raw capture:
`raw/notes/dilger-one-million-tokens-self-training-modeling-agent.md` (458 words), collected 2026-08-30
in a live logged-in browser session. Follow-up:
[[dilger-modeling-agent-improved-by-learning-loop]] (2026-08-28).

**The KB's first worked instance of an [[event-modeling|event model]] used as the *grading rubric* for a
self-improving agent.** Not a model that describes an agent — a model corpus that scores one.

## What he did

The [[eventmodelers-ai]] platform's Modeling Agent — which Dilger describes as already knowing Event
Modeling "as well as me ( I taught it, soon it will teach me )" — was put in a loop against a **grader**:

1. Take a realistic set of requirements; have the agent model them.
2. **Structurally diff** the result against a corpus of Dilger's own hand-crafted "well crafted" models —
   "mainly from a structural perspective. Are Chapters laid out the same way? Are Read Models structured
   in a similar way? How are given / when / thens structured? Are we using the same patterns?"
3. Record the subtle differences and **have the agent rewrite its own skills** accordingly.
4. Re-model the same requirements with the adjusted skills, now comparing against both the previous
   version *and* the good corpus. Did it improve?

Runs on **local hardware using QWEN3.7:27b**; over a million tokens in one night; left running
continuously.

## What the loop discovered on its own

The findings are the interesting part, because each is a convention Dilger holds but had not written
down explicitly — the loop recovered them from the artifacts:

- **Storylines over plain GWT** for Read Models connected to Automations. It adjusted the skills to
  match and "made a new rule for 'Todo Lists'." (Independently rediscovering
  [[dilger-todo-lists-storylines-one-scenario]], which he had written up separately twelve days earlier.)
- **Linked elements bridge events between chapters.** This was "hinted to in the skills, but not clearly
  stated as a rule" — the loop promoted it to an explicit modeling rule.
- **Back arrows are not allowed**, but Dilger uses *copies* of Read Models to show how a later event
  affects an earlier one. The agent now "creates a copy of the slice, links the Read Model and shows how
  that affects the screen."

> "This is absolutely fascinating, it catches all those tiny little subleties that are really hard to
> explain." *(sic — "subleties" as posted.)*

## Why this matters here

- **A model corpus is a gradeable rubric.** The claim [[event-modeled-agent-design]] has been asserting
  — that a formal model makes agent output checkable in a way prose does not — now has a worked instance
  behind it. The mechanism is *structural diff against known-good models*, which is possible precisely
  because the model has a schema; you cannot structurally diff two Markdown specs.
- **Tacit knowledge extraction as the payoff.** All three findings are conventions the author could not
  articulate but could demonstrate. That reframes what the good-model corpus is *for*: not training data
  in the usual sense, but an externalization of taste — which bears directly on
  [[addyosmani-earning-taste-and-judgment|Osmani's "taste is the ungradeable residue"]] claim, since here
  a slice of it turned out to be gradeable after all.
- **Self-modifying skills.** The artifact the loop edits is the agent's own skill files, not weights —
  the [[loop-engineering]] thread's hill-climbing pattern applied to the harness rather than to the code
  under construction. See [[harness-engineering]].
- **Small local model.** QWEN3.7:27b on local hardware, not a frontier model. The leverage is claimed to
  come from the rubric, not from model capability.

## Caveats

- **Self-reported, by the vendor of the platform.** Dilger builds [[eventmodelers-ai]]; there is no
  independent evaluation, no held-out test set described, and no numbers beyond the token count.
- **The grader is the author's own taste.** The loop converges on *Dilger's* conventions, which is the
  stated goal — but "improvement" here means "closer to my models," not "better by an external measure."
  Whether his conventions are the right target is a separate question the setup cannot answer.
- **No mention of a held-out requirement set.** The loop re-models the *same* requirements each
  iteration, which risks overfitting the skills to one scenario. The follow-up post's report of broad
  improvements suggests otherwise but does not demonstrate it.

## Related

[[martin-dilger]] · [[eventmodelers-ai]] · [[dilger-modeling-agent-improved-by-learning-loop]] ·
[[dilger-todo-lists-storylines-one-scenario]] · [[event-modeled-agent-design]] · [[loop-engineering]] ·
[[given-when-then]] · [[agent-harness]] · [[token-budget-quality-cliff]]
