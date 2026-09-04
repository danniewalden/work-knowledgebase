---
title: "Source: Agentic Software — How AI Agents Are Restructuring the Software Paradigm (Cao)"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [cao-agentic-software-restructuring-software-paradigm]
raw_file: [raw/papers/cao-agentic-software-restructuring-software-paradigm.md]
tags: [agent-engineering, agentic-ai, relocation-of-judgement, position-paper, academic, focus]
---

# Source: Agentic Software — How AI Agents Are Restructuring the Software Paradigm (Cao)

**Zhenfeng Cao, sole author — arXiv:2606.05608, v1 2026-06-04, v2 (current) 2026-06-10. 15 pages, 2 figures, 3 tables. Affiliation: Lingxi Intelligent Investment (Shenzhen) Development Co., Ltd. — a private company, not an academic lab. arXiv PREPRINT — NOT PEER-REVIEWED; arXiv is not peer review, and that caveat travels with every claim below.** Raw capture: `raw/papers/cao-agentic-software-restructuring-software-paradigm.md`. DOI: 10.48550/arXiv.2606.05608. (No licence is stated on the capture.)

**TITLE CHANGED BETWEEN VERSIONS — cite the current one.** v1 was "**The End of Software Engineering:** How AI Agents Are Fundamentally Restructuring the Software Paradigm"; v2, the current version, is "**Agentic Software:** How AI Agents Are Restructuring the Software Paradigm". Same identifier, same author. Anything in the wild citing "The End of Software Engineering" with this arXiv id is citing this paper. **The retitling is itself a datum: the strongest form of the claim was withdrawn from the title within six days.**

## Summary

A **single-author position paper** — it argues a paradigm rather than reporting an experiment, and cites other people's benchmark results rather than producing any. Its thesis: AI agents are "systems where large language models serve as the primary reasoning engine, **dynamically generating and discarding code as an instrumental resource**", and this "constitutes a fundamental restructuring of what software is, not an incremental tool improvement."

The formal distinction it draws is the useful part: **"in the former, code is the carrier of pre-written decision logic; in the latter, the agent itself is the software, and its decision logic is generated at runtime."** From that it traces a delivery arc — **licensed software → SaaS → Agent-as-a-Service (AaaS)** — arguing "each shift transferred additional complexity away from end-users — with the agentic shift transferring not just **operational** complexity but **decision-making** complexity itself." Its §3 headings sharpen this into "The Failure of 'AI → Software → Result'" and "'Agent → Result': Eliminating the Intermediary".

It then proposes **Agentic Engineering** as "an expansion of the software engineering discipline into a new paradigm, distinct in its **core object of study** (agent systems rather than static source code), its **control model** (LLM-driven rather than human-predefined), and **its human role (intent architect rather than code author)**" — that last clause verbatim from the abstract.

## Why this matters here — the academic statement of a relocation-of-judgement thesis

**This is the batch's most useful non-harness contribution.** The KB already holds, from practitioners, the claim that the human's job has moved *from producing the artifact to specifying intent and adjudicating quality* — [[addyosmani-earning-taste-and-judgment|Osmani on taste and judgment]], [[dilger-harness-is-20-percent-requirements-are-80|Dilger's 80% is requirements]], [[dilger-describing-without-solving-burns-you-out|Dilger on describing without solving]], the whole [[spec-driven-development]] and [[event-modeling]] case, and [[mcateer-evolution-of-the-agent-harness|McAteer's]] attention-interface. Until now that thesis rested **entirely on practitioner opinion**. Cao states it as an academic claim with a formal model behind it: *"its human role (intent architect rather than code author)"*.

That upgrade is real but modest, and the page should say both halves: it is **an academic *statement* of the thesis, not academic *evidence* for it.** A single-author position preprint from a private company is a different kind of source from a controlled study; what it adds is that the claim now exists in the literature in citable form, phrased independently of the practitioner discourse.

**Do not attribute the three-role phrasing to this capture.** Cao's paper is cited elsewhere for naming three roles - an intent-architect role, an agent-coordination role and an outcome-auditor role. The capture records that the retrieval tool **confirmed the phrase is present but located it inconsistently** (§4.1 on one pass, §4.3 on another) and **would not return a clean sentence-level quotation**, so no verbatim sentence containing it was filed. **That phrasing is therefore deliberately not reproduced in quotation marks anywhere on this wiki, including on this page.** What is verified verbatim is the abstract's own formulation of the same claim — "its human role (intent architect rather than code author)" — and the four differentiators below.

## Key points

- **The four "new human differentiators" (§4.3, verbatim from the captured excerpt; the original's bold/italic separation between each name and its gloss is flattened):**
  - **Intent articulation.** "The ability to specify goals with sufficient clarity and constraint that agents can operate autonomously without producing unintended outcomes."
  - **Architectural oversight.** "Understanding at the system level how multiple agents should coordinate, what memory should be shared, and where human judgment must intervene."
  - **Quality calibration.** "Defining what 'good' looks like and building evaluation frameworks that agents can use for self-correction."
  - **Ethical governance.** "Ensuring agent behavior aligns with organizational values, legal requirements, and societal expectations."
  His framing sentence: "In the traditional paradigm, human value was measured by the ability to produce correct, efficient code. In the agentic paradigm, **code-generation skill becomes commoditized.**" *(Preprint, not peer-reviewed; and a position claim, not a finding.)*
  These four map almost one-to-one onto KB pages: intent articulation → [[spec-driven-development]] / [[event-modeling]]; architectural oversight → [[multi-agent-orchestration]] / [[autonomous-domain-capabilities]]; quality calibration → [[agent-observability-and-evals]] / [[fitness-functions]]; ethical governance → [[agent-governance]]. That the mapping is that clean is worth noting — and worth treating with suspicion, since a four-item list of virtues is easy to write and hard to falsify.
- **"The agent itself is the software, and its decision logic is generated at runtime"** is a sharper formulation than the KB's [[agent-vs-workflow]] distinction, and pushes further: not just *agents decide the path* but *there is no durable artifact carrying the logic*. That is in direct tension with much of this KB's substrate thread ([[event-sourcing]], [[decision-trace]], [[agent-readable-model-artifacts]]), whose whole argument is that agent behaviour must leave **durable, inspectable artifacts**. **Record the tension; do not resolve it.** If decision logic is generated at runtime and discarded, auditability has to come from the log, which is exactly the [[event-sourced-agentic-patterns]] case.
- **A four-stage roadmap** (§6): Stage I Tool-Augmented (2023–2025) → Stage II Single-Task Autonomous (2025–2027) → Stage III Multi-Agent Teams (2026–2029) → **Stage IV Self-Evolving Ecosystems (2028+)**. Another [[autonomy-ladder]] to set beside the KB's existing ones. Dated predictions, so falsifiable — and note Stage IV's date (2028+) is *behind* this batch's harness-evolution papers, which are attempting self-evolution now.
- **§5 is titled "Empirical Evidence and Current Limitations"** with "Breakthrough Results", "Persistent Challenges" and "The Gap Analysis"; the abstract names **SWE-bench Verified, EvoClaw, and LangChain's multi-agent coordination studies** as its evidence base. **None of that body text was captured, so no result and no gap analysis can be sourced from this page.** Note also that this is a paper citing others' benchmarks, so any number in it would be third-hand by the time it reached this wiki.
- **AaaS is the commercial reading of the same shift** and connects to [[agentic-commerce]] and [[software-factory]]: if the intermediary product disappears, so does the software vendor's usual shape.

## Limits

- **PREPRINT, NOT PEER-REVIEWED.** Applies to everything above.
- **Position paper, single author, industrial affiliation.** It argues rather than measures; a private investment company's paper on the end of software engineering has a rhetorical stake in the strong version of the claim. **It is not independent corroboration of the practitioner thesis it restates** in the sense of adding evidence — it adds a citable academic statement.
- **The retitling.** v1's "The End of Software Engineering" became v2's "Agentic Software" in six days. Cite v2's title; note v1's. Read the change as a softening of the claim.
- **The capture is partial.** Captured verbatim: current title, author, abstract in full, comments, subject classes, cite-as, DOI, submission history, plus (from the v1 HTML) the v1 title, the author affiliation, the full section/subsection heading list, and the §4.3 four-differentiator excerpt. **NOT captured:** the body prose of all seven sections, **the formal model of §2.3**, the three-generations delivery table, the empirical-evidence discussion, the four-stage roadmap detail, the recommendations, and the references. The full PDF was not retrieved.
- **So the "formal model" this page credits it with is a claim about the paper's structure, not a model the wiki has seen.** Do not describe or rely on the formalisation until §2.3 is captured.
- **The three-role phrase is not quotable from here** (see above). This is the specific laundering risk on this page: the phrase is what the paper is best known for, it could not be verified verbatim, and it must therefore not appear in quotation marks anywhere on this wiki.

## Connections / contrast

- **[[agent-engineering]]** — "Agentic Engineering" as a named discipline with a stated object of study, control model and human role. The closest thing to an academic definition of that page's subject, and it should be added there *as a preprint position claim*.
- **[[mcateer-evolution-of-the-agent-harness]]** — the same relocation of the human's role, from product history rather than first principles; McAteer's residue (permissions, identity, trust, legibility) overlaps Cao's differentiators (oversight, calibration, governance) closely enough to be worth pairing.
- **[[addyosmani-earning-taste-and-judgment]] · [[dilger-harness-is-20-percent-requirements-are-80]] · [[dilger-describing-without-solving-burns-you-out]] · [[spec-driven-development]] · [[event-modeling]]** — the practitioner statements of the thesis this paper states academically. **This is the connection worth making explicitly on the concept pages: the KB's relocation-of-judgement claim is no longer practitioner-only.**
- **[[agent-vs-workflow]] · [[augmented-llm]]** — "the agent itself is the software" is the endpoint of that distinction.
- **[[event-sourcing]] · [[decision-trace]] · [[agent-readable-model-artifacts]] · [[event-sourced-agentic-patterns]]** — the tension above: runtime-generated, discarded decision logic vs. durable inspectable artifacts.
- **[[autonomy-ladder]] · [[agentic-ai]] · [[agentwashing]]** — the four-stage roadmap is another ladder; and a paper announcing the end of software engineering is exactly the genre [[agentwashing]] exists to watch, which is one more reason to keep the position-paper marker attached.
- **[[agentic-commerce]] · [[software-factory]] · [[business-capabilities]]** — the licensed → SaaS → AaaS arc as a commercial-model claim.
- **[[guo-survey-question-answering-to-task-completion-harness-design]]** — the contrast in genre worth noticing: two 2026-06 arXiv papers on agents, one a 17-author survey that decomposes machinery, one a single-author manifesto that renames the discipline. Both preprints; they are not the same kind of evidence and the wiki should not cite them the same way.

_Source page: [[cao-agentic-software-restructuring-software-paradigm]]._
