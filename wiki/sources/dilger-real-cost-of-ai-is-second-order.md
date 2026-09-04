---
title: "Dilger — The real cost of AI coding is second-order"
type: source
created: 2026-08-03
updated: 2026-08-03
sources: [dilger-real-cost-of-ai-is-second-order]
raw_file: [raw/notes/dilger-real-cost-of-ai-is-second-order.md]
tags: [comprehension-debt, agentic-coding, ai-roi, software-factory, focus]
---

# Dilger — The real cost of AI coding is second-order

LinkedIn post by **[[martin-dilger]]** (2026-07-27), captured verbatim. Raw:
`raw/notes/dilger-real-cost-of-ai-is-second-order.md`. A worked **[[comprehension-debt]]** anecdote from a
CTO conversation.

## What it says

A CTO's engineering costs climbed **~30% with flat headcount**; he assumed it was the AI tooling bill —
but that was a small part. The rest hid in **second-order costs that never appear as a line item**:

- **Incident response up** — more incidents, each slower to diagnose "because the code involved was less
  understood."
- **Onboarding up** — new hires slower to become productive (real salary on people not yet contributing).
- **Senior time reallocated** from building to firefighting — "silently converts a team's most expensive
  people from asset to overhead."
- **The quiet one:** features that took **three attempts instead of one**, "because the first two collided
  with things nobody knew were there."

The reframe: he'd evaluated AI on **direct cost** (licenses/tokens/tooling) and measured benefit in
**velocity** — but the economics were being decided in **second-order costs he wasn't tracking**. "On the
tooling line, AI looked cheap and productive. On the full ledger, it was expensive and roughly
break-even." The fix wasn't "stop using AI" but "fix the things converting our speed into cost" — a
smaller, more tractable problem. *"What's your real cost of AI? Not the bill, the ledger?"*

## Why it matters here

- The KB's most concrete field anecdote for [[comprehension-debt]] — the widening gap between code
  produced and code understood, showing up as incidents on "less-understood code," collisions with
  "things nobody knew were there," and senior firefighting. It's the cost-accounting face of the
  environment-over-model thesis and pairs directly with the [[dora-roi-ai-assisted-software-development-2026|DORA
  ROI report]]'s **verification + instability taxes** and **J-Curve** (the "productivity dip" is exactly
  these second-order costs), and with [[addyosmani-software-factories-light-and-dark|Osmani's dark
  factory]] (shipping unread code takes on comprehension debt "with the tests green").
- Caveat: a single second-hand anecdote in a LinkedIn post — illustrative, not data.

## Links

Entities: [[martin-dilger]]. Concepts: [[comprehension-debt]], [[agentic-coding]], [[software-factory]],
[[ai-readable-code]], [[loop-engineering]].
Related sources: [[dora-roi-ai-assisted-software-development-2026]],
[[addyosmani-software-factories-light-and-dark]], [[willison-understand-to-participate]],
[[dilger-harness-is-20-percent-requirements-are-80]].

_Raw source: `raw/notes/dilger-real-cost-of-ai-is-second-order.md`._
