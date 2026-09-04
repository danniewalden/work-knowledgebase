---
title: "Source: Adam Tornhill — Task uncertainty decides what code you read"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [tornhill-task-uncertainty-decides-what-code-you-read]
raw_file: [raw/notes/tornhill-task-uncertainty-decides-what-code-you-read.md]
tags: [verification-burden, agentic-coding, ai-readable-code, self-report, focus]
---

# Source: Adam Tornhill — Task uncertainty decides what code you read

LinkedIn post by **[[adam-tornhill]]** (**2026-08-28**), captured verbatim at
`raw/notes/tornhill-task-uncertainty-decides-what-code-you-read.md` via logged-in Chrome. It
announces his article [[tornhill-controlling-the-uncertainty-machine]] (already ingested), but states
the principle in its own words and in a tighter form, so it stands as its own claim and its own
citable quote.

## Summary

Four moves in one post:

1. **The failure mode of doing it the old way:** *"If we approach agentic coding the way we tackle
   manual coding, **we'll turn ourselves into legacy code maintainers**. That's a mentally draining
   place to be and is unlikely to speed up anything."*
2. **The question is malformed:** *"a question like 'do we still need to read AI generated code' is
   pointless in isolation. The answer depends on the task, and more specifically on the **uncertainty**
   inherent in each type of task. That task uncertainty drives both the relative autonomy I grant a
   coding agent, and the effort I spend reviewing the resulting code."*
3. **The consequence, stated flatly:** *"I never read all AI-generated code. But, and this is
   important, **make the code you do read count**."*
4. **The cost of the habit change:** *"Given that I had typed out code by hand for almost 40 years,
   becoming comfortable with *not* reading code was a large mental shift when going agentic. A year
   into my agentic journey, I'm now quite confident that I don't need to know every line of code. I get
   that confidence by knowing that the system behaves as intended, remains maintainable, and lives
   within the established boundaries."*

## Key points

- **The two-dial formulation is the durable contribution**: one uncertainty judgement sets *both*
  agent autonomy *and* human review depth. That is a tighter statement than the article's, and the
  form worth quoting on concept pages.
- **"Turn ourselves into legacy code maintainers"** is the batch's best one-line diagnosis of what
  reading all agent output actually feels like — reading code nobody in the room wrote is the
  definition of legacy maintenance, no matter how new the code is.
- **The confidence is explicitly *derived*, not assumed**: behaves as intended (tests) + remains
  maintainable (code-health enforcement) + within established boundaries (architectural rules). The
  three legs of his safety net, in one sentence.
- **The habit-change framing is the honest part** — roughly 40 years of hand-coding against about one
  year of agentic practice, presented as a personal adaptation rather than a validated method.

## Limits

- **THIN CAPTURE / promotional.** A LinkedIn post whose purpose is to drive traffic to the article
  ("Check it out: …"). Cite it for the *phrasing* of the principle; cite
  [[tornhill-controlling-the-uncertainty-machine]] for the method.
- **IMPRESSION NOT MEASUREMENT.** "I'm now quite confident" and "a year into my agentic journey" are
  self-report. No defect data, no escaped-bug rate, no comparison with reading the code.
- **VENDOR SELF-REPORT travels with the remedy** even though it is not visible in this post: the "lives
  within the established boundaries" leg of his confidence rests on deterministic tooling that
  includes **CodeScene's own** CodeHealth MCP, and he is CodeScene's founder/CTO. The marker belongs on
  any page quoting the enforcement half of the claim.
- Duplicate content risk: the two Tornhill uncertainty pages are deliberately separate per-capture
  pages, not two independent sources. **They must never be cited side by side as corroboration.**
- LinkedIn-derived date (accurate to the day, from a relative age stamp).

## Connections / contrast

- **[[verification-burden]]** — the quotable form of the triage position. "I never read all
  AI-generated code. But… make the code you do read count" is the sentence for the page.
- **[[tornhill-controlling-the-uncertainty-machine]]** — the full method: uncertainty triage, e2e tests
  as the human/agent abstraction boundary, review findings captured as SKILLs, deterministic
  enforcement of what goes uninspected.
- **[[autonomy-ladder]]** — one dial in the KB, two here (autonomy *and* review depth, moved together
  by the same judgement). That refinement is the clearest thing this note adds to an existing concept.
- **[[comprehension-debt]]** — "legacy code maintainers" is the debt's endgame named as a role, and a
  useful counter to the page's current "read the diffs" defence.
- **[[willison-more-than-just-code-review]]** — same claim, six days earlier, independently.
- Also: [[ai-readable-code]], [[agent-legibility]], [[attention-bottleneck]] (why the reading budget is
  finite — see [[tornhill-compressed-cognition-cost-of-faster-coding]]).

## Links

Entities: [[adam-tornhill]] · [[simon-willison]]. Concepts: [[verification-burden]] ·
[[autonomy-ladder]] · [[ai-readable-code]] · [[comprehension-debt]] · [[attention-bottleneck]].
Related sources: [[tornhill-controlling-the-uncertainty-machine]] ·
[[tornhill-compressed-cognition-cost-of-faster-coding]] · [[willison-more-than-just-code-review]] ·
[[tornhill-cannot-trust-agent-codescene-mcp]].

_Raw source: `raw/notes/tornhill-task-uncertainty-decides-what-code-you-read.md`._
