---
title: "Source: Wong — Loop Engineering: Teaching AI Agents How to Think"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [wong-loop-engineering-teaching-ai-agents-how-to-think]
raw_file: [raw/articles/wong-loop-engineering-teaching-ai-agents-how-to-think.md]
tags: [loop-engineering, harness-engineering, context-engineering, verification, definition, focus]
---

# Source: Wong — Loop Engineering: Teaching AI Agents How to Think

Source: **Andy Wong**, *"Loop Engineering: Teaching AI Agents How to Think"*, Power of Eloquence
(awongcm.io), **2026-08-23**. Raw capture:
`raw/articles/wong-loop-engineering-teaching-ai-agents-how-to-think.md`. Third post in the author's own
ladder series (context → harness → loop → graph); the sequel is
[[wong-graph-engineering-wiring-agents-into-an-organization]].

## Summary

The **tightest single definition of a loop in the KB**, and the most implementable: *"a loop is a task
plus a check. A task without a check is just hope."* Wong decomposes every agent loop into **four
components — trigger, goal, verifier, stop rules** — argues that a broken loop is always a missing or
weak version of one of the four, and supplies a ~30-line `LoopController` that decides nothing except
*whether to let the harness run again*. His slogan: **"The intelligence still lives in the model. The
reliability now lives in the loop."**

## Key points

- **The boundary he draws between the three disciplines** (the clearest statement of the ladder in the
  KB): [[context-engineering]] answers *what do I put in front of the model right now?*;
  [[harness-engineering]] answers *how does the model act on that — which tools, how is one step
  validated and executed?*; loop engineering answers *what happens after that step — do we go again,
  with what, and for how long?* **"A harness governs one step. A loop governs the campaign."**
- **Trigger.** A schedule, an event (PR opens, test fails, ticket lands), or a person's instruction.
  "The trigger is what lets a loop run without you sitting there to press go."
- **Goal — a verifiable end state, not a vibe.** "Make the code better" is not checkable; "all tests
  pass," "P95 latency under 300ms," "zero open Sev-1 issues" are. **"If you can't write a check for it,
  the loop can't know when it's done."**
- **Verifier — "the part worth being paranoid about."** Prefer a **deterministic** check (test-suite
  exit code, schema validator, linter) over asking the same model to grade its own output: *"A model
  marking its own homework is the one failure mode that quietly poisons every other safeguard you
  build."* When a model verifier is unavoidable, make it **a separate agent with different
  instructions**. This is the KB's **maker ≠ checker** rule stated as an ordering preference —
  deterministic first, second model only after the deterministic option is exhausted.
- **Stop rules — plural and independent.** Minimum three: a **success exit** when the verifier confirms
  the goal, a **hard iteration cap**, and a **budget cap**. "Skipping the iteration and budget caps is
  how people wake up to a five-figure API bill and an agent that looped for nine hundred rounds on a
  problem it was never going to solve."
- **The failure table is the reusable artifact.** Declares victory early → vague goal. Runs forever →
  no iteration cap, or a verifier that never returns cleanly true/false. Fixes the same thing repeatedly
  → **no feedback path** (the failure isn't fed back into the next attempt). Surprise bill → cap not
  wired to actually halt. Convinces itself it's done → **the verifier reached for a second LLM call
  before exhausting the deterministic check sitting right there.**
- **The deepest failure is premature architecture.** "Reaching for a five-agent orchestration with a
  planner and a vector memory before you've proven that one act-verify cycle works at all. **A loop
  amplifies whatever is inside it** — a weak verifier doesn't make the loop safer, it just makes the
  agent's mistakes more expensive to repeat."
- **Loops and harnesses nest, they don't compete.** The dividing line is *one step* vs *the whole task*:
  "the harness's own loop guard stops a single step from spinning, while the loop's stop rules stop the
  entire campaign."
- **Operational checklist worth lifting.** Write the goal as an executable check *before* writing loop
  code; add iteration + budget caps to anything already running unattended; build the feedback path
  (feed the *exact* failure back, not "try again"); **instrument iteration count, stop reason, and cost
  per run** so a stuck loop shows up on a dashboard rather than an invoice; **separate the loop's
  persistent state from the model's conversation history** so a restarted loop isn't amnesiac; and
  **track which verifier caught which class of failure**, "so you know where to tighten the check
  rather than add another agent."
- **Limits.** A practitioner explainer with **no measurement of any kind** — no benchmark, no A/B, no
  case study, not even a self-reported before/after; the code is illustrative pseudocode, not a shipped
  library. Its Cherny quote ("I don't prompt Claude anymore. I have loops running that prompt Claude")
  is **cited third-hand** via a Build Fast with AI blog post, not from the original stage remark, and
  the wording differs from the version the [[loop-engineering]] page carries. Four of its seven
  references are secondary "what is loop engineering" content-marketing posts from mid-2026 — this is
  a synthesis of the discourse, not independent evidence about it. The author's own framing is
  prospective ("if I were to actually ship the same loop into production" in the sequel), which
  suggests parts of the ladder are reasoned rather than run.

## Connections / contrast

**Wong's definition contradicts [[voss-what-the-hell-is-a-loop-anyway|Voss's]] head-on, and the
contradiction is the point.** For Wong there is *one* loop construct (task + check) with four
components, sitting at a fixed rung of a four-layer ladder. For Voss there are *at least four
different loop architectures* that differ in what they iterate on, what stops them, and where the human
sits — and he denies the innermost one is even designed ("nobody designs the token loop"). Voss's
*product loop* (the whole software lifecycle) and *system loop* (the harness improving itself) are not
"a task plus a check" in any recognisable sense. Neither author cites the other; published four weeks
apart. **Do not merge these into one definition.**

**Wong contradicts [[morris-humans-and-agents-in-software-engineering-loops|Morris]] on the layering.**
Wong: the loop is *above* the harness ("a harness governs one step, a loop governs the campaign").
Morris (five months earlier): the harness *is* "the collection of specifications, quality checks, and
workflow guidance that control different levels of loops inside the how loop" — i.e. the harness is
what governs the loops, and working on it is what "on the loop" means. The KB's [[loop-engineering]]
page opens on Wong's ordering ("one floor above the harness," per Osmani); that ordering is **not
settled**, and that page's own *"Does the loop sit above the harness, or inside it?"* section records
the dispute.

**Where Wong strengthens existing pages.** His verifier ordering — *deterministic check first, second
model only when forced* — is a sharper rule than the KB's current maker ≠ checker framing, which
treats "use a different model" as the primary move; it converges with
[[bockeler-tdd-inside-the-agent-loop|Böckeler's]] finding that a self-graded step is not a check, and
with [[addyosmani-practical-loop-engineering|Osmani's]] note that the evaluator behind `/goal` "does not
look at the content to see if it's good or bad… all it does is examine the conversation transcript to
see if the hard rules you specified have been met." Three sources, same conclusion: **a grader that
reads intent is not the same instrument as a grader that reads output.**

His "**a loop amplifies whatever is inside it**" is the loop-level statement of
[[addyosmani-code-agent-orchestra|Osmani's]] "the human bottleneck was a feature, not a bug" and of
[[wong-graph-engineering-wiring-agents-into-an-organization|his own]] graph-level restatement ("a graph
amplifies whatever's inside its nodes"). The "separate the loop's persistent state from the
conversation history" instruction is the same on-disk-memory move the KB files under
[[long-running-agents]] and [[loop-engineering]]'s "the agent forgets, the repo doesn't."

## Links

[[loop-engineering]] · [[harness-engineering]] · [[context-engineering]] · [[graph-engineering]] ·
[[agent-harness]] · [[feedforward-and-feedback-controls]] · [[agent-observability-and-evals]] ·
[[long-running-agents]] · [[unattended-coding-agents]] · [[token-budget-quality-cliff]] ·
[[agent-vs-workflow]] · [[claude-agent-sdk]] · [[anthropic]] ·
[[wong-graph-engineering-wiring-agents-into-an-organization]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[morris-humans-and-agents-in-software-engineering-loops]] ·
[[addyosmani-practical-loop-engineering]] · [[bockeler-tdd-inside-the-agent-loop]] ·
[[langchain-the-art-of-loop-engineering]] · [[anthropic-getting-started-with-loops]]

_Source: [[wong-loop-engineering-teaching-ai-agents-how-to-think]] (raw: `raw/articles/wong-loop-engineering-teaching-ai-agents-how-to-think.md`)._
