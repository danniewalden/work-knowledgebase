---
title: Martin Fowler
type: entity
created: 2026-06-11
updated: 2026-09-04
sources: [fowler-bockeler-harness-engineering, fowler-agentic-programming, fowler-fragments-2026-09-01, fowler-fragments-2026-08-24, fowler-paracelsus-maxim, highsmith-practitioner-voice]
tags: [person, publication, thoughtworks, software-engineering]
---

# Martin Fowler

Software-engineering author and Chief Scientist at [[thoughtworks]]; his site
(martinfowler.com) is a long-running, widely-cited reference on refactoring, architecture,
continuous integration/delivery, and (increasingly) generative-AI delivery practices.

In the KB, martinfowler.com is the **publication venue** for [[birgitta-bockeler]]'s
[[harness-engineering]] article ([[fowler-bockeler-harness-engineering]]) and the Thoughtworks
"Exploring Gen AI" series. The "keep quality left" framing builds directly on Fowler's own
continuous-integration / continuous-delivery writing.

Fowler also authors directly on the focus area: his **[[fowler-agentic-programming|Agentic
Programming]]** bliki (2026-05-21) is the KB's canonical, vendor-neutral definition of
[[agentic-coding]] — distinguishing it from [[vibe-modeling|vibe coding]] and autocomplete, and
naming [[harness-engineering]] + domain understanding as the central new skills.

> **Not a third-party venue.** martinfowler.com is [[thoughtworks]]' own publishing channel and he is its
> Chief Scientist, so neither he nor the *Exploring Gen AI* authors on it are independent corroboration
> for a Thoughtworks framing — see the concentration section on [[thoughtworks]].

## In this KB as an author, September 2026

- **On CI with agents** ([[fowler-fragments-2026-09-01]]) — his own argument, and the batch's clearest
  disagreement between well-positioned sources. Against Paul Stack's "AI Broke the Assumptions Behind CI":
  verifying locally before pushing *"was always how Continuous Integration works"*, slow tests belong
  downstream in the deployment pipeline, and *"Continuous Integration is a practice, not just the CI
  server."* He concedes the real question and supplies the control this KB keeps: *"CI with humans relies on
  them being disciplined to run commit tests locally before pushing — and that we can (and should) automate
  that when using agents."* [[jeremy-miller]] reaches the same remedy from the opposite premise
  ([[miller-pondering-continuous-integration-ai-world-order]]) — **the KB holds the disagreement open.**
- **The *Fragments* format** — short unconnected link-notes, most of them off this KB's threads. Two are
  not: the **NVIDIA AVO** harness result (100% on ARC-AGI-3 with Claude Opus 5, persistent memory plus a
  supervisor, and a **seven-day** kernel-optimization run — **NVIDIA's self-report, relayed secondhand**;
  the NVIDIA post is not in `raw/`), and his own observation on the OpenAI/Hugging Face agent swarm:
  *"none of these agents thought to rat the others out… no sign of an AI whistleblower"*
  ([[fowler-fragments-2026-08-24]]) — now on [[agent-governance]]. **Caution:** in that same roundup he
  repeats Zalando's *"reducing lead time by 20–40%"* without adding independence; the figure remains a
  **selection-biased VENDOR SELF-REPORT** and **this capture is not a second source for it**. He also
  relays that human detection of LLM text is *"no better than random chance"* (57%/64% in a second study)
  **through Wikipedia, with neither study named or captured** — cite as "relayed", never as "a study
  found." That relay sits in tension with [[jim-highsmith]]'s claim that a reader can notice when nothing
  is at stake; a tension to hold, not a refutation to apply.
- **[[fowler-paracelsus-maxim]]** (2026-09-02) is a 270-word dictionary entry — *"in what contexts"* and
  *"in what doses"* — with no application to this KB's subject matter. Recorded, not built on; **do not
  create a concept page from it.**
- **As venue:** martinfowler.com published [[jim-highsmith]]'s *Practitioner Voice*
  ([[highsmith-practitioner-voice]]), in which Fowler appears as the person who three times told Highsmith
  to let his voice out and as the exemplar of the category (*"Martin Fowler writes this way"*). That makes
  the piece **NOT INDEPENDENT** of him — worth noting since the KB leans on martinfowler.com for the
  [[harness-engineering]] material too.

_Sources: [[fowler-bockeler-harness-engineering]] · [[fowler-agentic-programming]] ·
[[fowler-fragments-2026-09-01]] · [[fowler-fragments-2026-08-24]] ·
[[fowler-paracelsus-maxim]] (off-thread dictionary entry) ·
[[highsmith-practitioner-voice]] (as venue and as a character in it)._
