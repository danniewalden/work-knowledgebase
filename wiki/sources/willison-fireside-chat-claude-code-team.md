---
title: "Willison — A Fireside Chat with Cat and Thariq from the Claude Code team"
type: source
created: 2026-07-27
updated: 2026-07-27
sources: [willison-fireside-chat-claude-code-team]
raw_file: [raw/articles/willison-fireside-chat-claude-code-team.md]
tags: [agentic-coding, agent-harness, loop-engineering, evals, prompt-injection, focus]
---

# Willison — Fireside Chat with the Claude Code team (Cat Wu & Thariq Shihipar)

[[simon-willison|Willison]]'s edited+annotated transcript of his AI Engineer World's Fair fireside chat with
**Cat Wu** and **Thariq Shihipar** of [[anthropic|Anthropic]]'s Claude Code team (simonwillison.net,
2026-07-21). Vendor-team practitioner testimony on how Anthropic actually builds with coding agents — most
valuable for its concrete data points on **automated code review, evals, on-disk memory, and prompt design**.

## The load-bearing data points

- **Claude Tag lands 65% of the Claude Code product-eng team's PRs.** Claude Tag is a "multiplayer by
  default," *proactive* Claude living in Slack (monitor a channel's bug reports, open PRs, tag the last
  engineer to touch that code, for the channel's lifetime). Anthropic sees it as "the evolution of Claude
  Code"; Claude Code stays best for complex interactive work.
- **Code review is being moved off humans deliberately, over months.** Critical cores keep a **code owner**
  who must approve every PR (the system prompt is one); but "outer layer" changes are increasingly reviewed
  *fully by Claude*. The method: start with human review everywhere → find files where automated review
  "catches 100% of the issues" → drop the human there → after any incident, "update code review to catch
  that" and **add the causing PR to an eval set so the metric never regresses.** A real-world **hill-climbing
  / maker≠checker** loop (ties [[loop-engineering]], [[langchain-the-art-of-loop-engineering]]).
- **On-disk memory primitive:** "**How it works right now in Claude Tag is a markdown file per channel**" —
  shared channel memory, per-session instances that contribute back. The same "the agent forgets, the repo
  doesn't" file-based memory the KB tracks across [[loop-engineering]] and [[event-sourcing]]; team
  preferences stated in natural language persist for everyone.
- **The Claude Code system prompt shrank ~80%** for frontier models (Fable 5, Opus 4.8) — a *different system
  prompt per model*. Two prompting reversals worth flagging against KB priors: **adding examples is no longer
  best practice** (removing them "was extremely helpful… more creative than the examples we gave it"), and
  **"don't do X" lists can lower quality** (hard negative constraints conflict with later user/skill
  instructions and confuse the model). Guidance: fewer hard constraints, more context; **"soften" any prompt
  that's only 90% true** (think how a well-intentioned human could misread it), because "you're giving this
  prompt to the model 100% of the time." Relying on the model's *judgment* to decide e.g. when to verify is
  now viable — an Opus/Fable-level capability.

## Themes that reinforce KB threads

- **Auto mode + prompt-injection.** Anthropic "really believe in auto mode" and see it as what *enabled*
  Claude Tag. A **Sonnet classifier** judges each tool call + conversation context; honors **dynamic
  permissions** stated in the prompt ("push this" allow / "don't push" deny) and gates **sandbox escapes**
  (e.g. network requests). Cat's strong claim: for prompt injection + data exfiltration "the risks are far
  lower than the average human reviewer," red-teamed extensively (Willison flags it as "a big claim"; evals
  promised). **Credential injection** pattern: the agent can *use* a Datadog credential via a proxy without
  *holding* it (audit + inject on the fly) — a clean [[prompt-injection]]/least-privilege control.
- **Evals as the trust substrate.** New models are "drop-in replacements" only after passing the full eval
  suite (capability first, then **behavioral evals** for annoyances — "don't say it's time to sleep," "don't
  stop at 2 of 5 parts"); the constraint on evals is customer *skill* at writing them, not tooling.
- **Tool design is "a biology not a physics."** Trend toward *fewer, more general* tools with distinct
  functions; removed grep/glob in favor of native bash; kept the file-edit tool mainly so the **edit can be
  rendered** in a review UI (may be unnecessary under auto mode). "Claude prompting Claude all the way down"
  — subagents and **workflows** (Claude orchestrating many subagents, each with a detailed prompt).
- **The human shift.** "A codebase is a spec — maybe the only copy you have"; **rewrites are now good** (a
  good rewrite forces a good test suite; cf. [[willison-rewriting-bun-in-rust]] — Bun-in-Rust shipping
  internally). Product/business taste rises as the idea→build timeline drops 6–12 months → a week (echoes
  [[addyosmani-earning-taste-and-judgment]]); "the way you offset [the grief/[[willison-directly-responsible-individuals|Deep
  Blue]]] is by being more ambitious." Working "internally in public" (Claude Tag in public Slack channels)
  is framed as a culture hack — the same prompt-in-public dynamic Midjourney used to teach prompting.

## Why it matters here

A rare inside-the-vendor look at the practices the KB has been assembling from the outside: automated review
as a trust-built-over-months loop with an eval-set regression guard, markdown-per-channel on-disk memory,
credential injection, and a concrete reversal of the "give examples / list don'ts" prompting advice for
frontier models. Caveat: **an interview transcript, not Willison's own argument**, and it's Anthropic
describing Anthropic's tools (marketing-adjacent) — treat the strong safety claims as vendor-stated pending
the promised evals. Willison's bolding/annotations are his editorial lens.

## Connections

[[simon-willison]] · [[anthropic]] · [[agentic-coding]] / [[agent-harness]] (tool design, auto mode) ·
[[loop-engineering]] (automated-review hill-climbing, on-disk memory) · [[langchain-the-art-of-loop-engineering]]
(maker≠checker) · [[agent-observability-and-evals]] (eval-as-trust) · [[prompt-injection]] (auto mode,
credential injection) · [[willison-rewriting-bun-in-rust]] (rewrites-are-good, Bun-in-Rust) ·
[[addyosmani-earning-taste-and-judgment]] (taste/ambition).

_Source: [[willison-fireside-chat-claude-code-team]] (raw/articles)._
