---
title: "Source: Fritzsche — What AI changes is which part of the work stays difficult"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [fritzsche-what-ai-changes-is-which-work-stays-hard]
raw_file: [raw/notes/fritzsche-what-ai-changes-is-which-work-stays-hard.md]
tags: [domain-discovery, agentic-coding, relocation-of-judgement, opinion, short]
---

# Source: Fritzsche — What AI changes is which part of the work stays difficult

LinkedIn post by **[[rico-fritzsche]]**, 2026-09-04. Raw capture:
`raw/notes/fritzsche-what-ai-changes-is-which-work-stays-hard.md` (captured verbatim via logged-in
Chrome; date accurate to the day). **PRACTITIONER OPINION about where skill value moves — no measurement
of any kind**, as the capture note states. Short page: it is a short post, and its content is one
well-put claim.

## Summary

Fritzsche's argument: discussions default to implementation detail, and implementation detail is exactly
what is getting cheap. *"If the actual implementation becomes cheaper and faster, then people who are able
to figure out what actually needs to be built will become more important."* The specific version of "what
needs to be built" is domain-shaped: *"the question of which rules apply and what consequences a technical
decision has will become increasingly important. In the next years, this will have to be an essential
trait of a developer."*

## Key points

- **The line that names the whole strand, and the reason this capture is worth keeping:**
  *"Nothing has changed in that regard. **What AI changes is which part of that work remains
  difficult.**"* That is a sharper formulation than "AI does the easy part" — it says the *distribution*
  of difficulty moved while the job did not.
- **"A framework isn't a foundation."** *"If you're proficient in ASP.NET Core, Spring, React, and so on,
  then you're proficient in tools. These are interchangeable implementation options. And if you focus on
  them, then you yourself become interchangeable."* His list of actual fundamentals: *"system design,
  reliability, data, consistency, system structure and boundaries."*
- **A shot at diagram-shaped architecture** consistent with his standing position: *"it's no longer (and
  I guess it never was) relevant to draw a pretty picture made up of circles, call it 'Clean Architecture'
  or 'Onions,' and claim that's what architecture is. Building systems is about understanding a problem
  and finding the best solution."*
- **The sharpest and most checkable claim, offered as an aside:** *"thanks to AI agents, it's becoming
  increasingly clear that **developers often created and solved problems that had absolutely nothing to do
  with the domain or the business problem**."* Read as a hypothesis this is testable — accidental
  complexity becomes visible when its production cost drops toward zero — and it is a genuinely different
  mechanism from "agents write the boring code." Nothing in this capture tests it.

## Limits

- **Opinion, unmeasured, unsourced.** A LinkedIn post; no examples, no data, no cases. It is a
  well-positioned practitioner's forecast, and the forecast form ("will become," "in the next years") is
  not evidence.
- **Self-interested in the ordinary way**: Fritzsche's published position and consulting practice are
  built on domain-and-capability-first design, so "domain judgement becomes the scarce skill" is his own
  thesis winning.
- The framework/foundation argument is asserted; no account is given of how someone acquires system-design
  judgement without going through framework proficiency first.

## Connections / contrast

- **Extends [[rico-fritzsche]]'s standing position** ([[autonomous-domain-capabilities]],
  [[fritzsche-clean-architecture-capability-over-layers]]) from *how to structure code* to *what skill is
  scarce* — the same argument one level up.
- **Third independent voice on the relocation-of-judgement strand**, alongside Osmani's *"human judgment
  doesn't leave the software factory. It relocates"* ([[addyosmani-human-judgment-relocates]]) and
  [[laycock-citizens-build-agents-execute-experts-govern]]. Fritzsche's contribution is the crispest
  phrasing (*"which part of that work remains difficult"*) and the accidental-complexity mechanism, which
  the others do not name. **Three practitioner opinions converging is not measurement** — that caveat
  travels with the strand.
- **Direct support for [[domain-discovery]] and [[event-modeling]] as the residual hard part**, and the
  natural counter to [[swyx-gpt6-astra-automated-ai-engineer]]'s "fully capable AI Engineers" claim in
  this same batch: if the hard part is knowing which rules apply, a model that writes the code has not
  taken the job.
- Rhymes with Dumpleton's disclaimer in [[willison-introducing-wrapture]] — *"the AI was the means of
  producing it rather than the source of the design"* — which is this claim demonstrated on one library
  by someone who had the domain knowledge already.
- Its blunter sibling, [[fritzsche-dotnet-scene-stuck-in-mid-2000s]] (2026-09-03), makes the same point
  wrapped in a community complaint.

## Related

[[rico-fritzsche]] · [[domain-discovery]] · [[agentic-coding]] · [[comprehension-debt]] ·
[[addyosmani-human-judgment-relocates]] · [[laycock-citizens-build-agents-execute-experts-govern]] ·
[[fritzsche-dotnet-scene-stuck-in-mid-2000s]] · [[autonomous-domain-capabilities]] ·
[[highsmith-practitioner-voice]] · [[event-modeling]]
