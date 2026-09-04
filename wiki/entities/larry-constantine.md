---
title: Larry Constantine
type: entity
created: 2026-06-22
updated: 2026-06-22
sources: [coupling-research-note]
tags: [person, software-design, coupling-cohesion, structured-design, historical]
---

# Larry Constantine

American software engineer and pioneer of **structured design**; originator of the classical
**coupling/cohesion** vocabulary. Constantine developed the coupling taxonomy in the mid-1960s and first
presented it at the **1968 National Symposium on Modular Programming**. It reached wide circulation in
**Stevens, Myers & Constantine, "Structured Design," *IBM Systems Journal* 13(2), May 1974** (DOI
10.1147/sj.132.0115), and was formalized in **Yourdon & Constantine, *Structured Design* (1979)**, which
defined coupling as "the measure of the strength of interconnection" between modules.

His six coupling levels — content, common, external, control, stamp, data (strongest → weakest) — are
the historical root of every later coupling model, including [[vlad-khononov|Khononov's]]
[[balanced-coupling]] (whose "Intrusive" strength maps to Constantine's content coupling). See the
[[coupling-taxonomy]] page.

## In the KB

The **historical anchor** of the coupling thread. His 1974/1979 taxonomy is *settled* but a vocabulary
mismatch for capability-graph edges (intra-program modules, pre-distributed-systems), so it informs the
landscape rather than the recommended model — see [[coupling-research-note]]. Biographical detail per the
[IEEE Computer Society pioneer profile](https://history.computer.org/pioneers/pdfs/C/Constantine.pdf).

_Source pages: [[coupling-research-note]]._
