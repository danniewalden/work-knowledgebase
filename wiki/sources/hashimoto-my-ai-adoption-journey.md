---
title: "Source: Hashimoto — My AI Adoption Journey"
type: source
created: 2026-06-11
updated: 2026-06-11
sources: [hashimoto-my-ai-adoption-journey]
raw_file: [raw/articles/hashimoto-my-ai-adoption-journey.md]
tags: [harness-engineering, coding-agents, adoption, workflow]
---

# Source: Hashimoto — My AI Adoption Journey

Personal essay by [[mitchell-hashimoto]] (founder of HashiCorp; creator of Ghostty), 2026-02-05.
The **primary source** in which Hashimoto names "harness engineering" — previously cited only
secondhand via [[firecrawl-what-is-an-agent-harness]]. Written entirely by hand. Raw capture:
`raw/articles/hashimoto-my-ai-adoption-journey.md`.

## Summary

A measured, first-person account of moving from AI skeptic to productive user across six steps —
deliberately working through phases of "inefficiency → adequacy → discovery." Notable for its
restraint: Hashimoto stresses knowing *when not* to use an agent and keeping the human in control
of interruptions.

## Key points (the six steps)

1. **Drop the chatbot.** Coding via a chat interface is inefficient (copy/paste, repeated
   correction). To get value you *must* use an **agent** — an LLM that invokes tools in a loop;
   minimally it can read files, execute programs, and make HTTP requests.
2. **Reproduce your own work.** He did every task twice — manually, then forced an agent to match —
   to build first-principles expertise. Lessons: break work into clear tasks (don't "draw the owl"
   in one mega-session); split planning vs. execution for vague requests; **give the agent a way to
   verify its work and it fixes its own mistakes.**
3. **End-of-day agents.** Spend the last 30 min/day kicking off agents to "do more in the time I
   don't have" — deep research surveys, parallel exploration of vague ideas, and issue/PR triage
   (report-only) for a "warm start" next morning.
4. **Outsource the slam dunks.** Delegate high-confidence tasks to a background agent while doing
   deep manual work on something else. **Turn off agent notifications** — the human controls when to
   interrupt, not the agent. Frames this as trading off skill-formation on delegated tasks while
   still forming skills on manual ones (re: the Anthropic skill-formation paper).
5. **Engineer the harness.** *(The term's origin.)* "Anytime you find an agent makes a mistake, you
   take the time to engineer a solution such that the agent never makes that mistake again." Two
   forms: (a) **better implicit prompting** via AGENTS.md — each line derived from an observed bad
   behavior (he cites Ghostty's AGENTS.md); (b) **actual programmed tools** — screenshot scripts,
   filtered test runners — usually paired with an AGENTS.md note.
6. **Always have an agent running.** A goal, not yet fully realized (~10–20% of the day). Pairs well
   with slower, more thoughtful models. He deliberately runs *one* agent, not many — balancing
   enjoyable manual work against babysitting; and won't run agents "for the sake of it."

## Connections / contrast

This is the **definitional root** of [[harness-engineering]] — the "failure → permanent fix" stance
the whole cluster adopts, and which [[firecrawl-what-is-an-agent-harness]] attributes to him. His
"two forms" (AGENTS.md + programmed tools) map onto [[birgitta-bockeler|Böckeler]]'s feedforward
guides and feedback sensors ([[feedforward-and-feedback-controls]]). The "verify its work" insight
is the [[anthropic-effective-harnesses-long-running-agents|self-verification]] principle. His
background/end-of-day/always-running patterns are the individual-developer version of
[[unattended-coding-agents]] (cf. [[stripe-minions-one-shot-coding-agents]]). A useful counterweight
to the maximalist [[openai-harness-engineering-codex]] case study — same practice, modest scale.

_Source page: [[hashimoto-my-ai-adoption-journey]]._
