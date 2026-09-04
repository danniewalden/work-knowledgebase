---
title: "Source: Osmani — AI Won't Teach You the Lesson Unless You Force It"
type: source
created: 2026-09-04
updated: 2026-09-04
sources: [osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]
raw_file: [raw/notes/osmani-ai-wont-teach-you-the-lesson-unless-you-force-it.md]
tags: [comprehension-debt, loop-engineering, skill-decay, note, focus]
---

# Source: Osmani — AI Won't Teach You the Lesson Unless You Force It

Source: [[addy-osmani]], LinkedIn post, **2026-09-02**. Raw capture:
`raw/notes/osmani-ai-wont-teach-you-the-lesson-unless-you-force-it.md`. A short note (~230 words), not
an article — it **announces and summarises a longer free write-up on expertise which is linked but not
yet captured** (candidate for a follow-up capture).

**Carry the capture note's warnings.** Captured verbatim via a live logged-in Chrome session (the
headless scheduled watch cannot render this feed); the only edit was collapsing LinkedIn's rendered
`hashtag\n#x` markup back to `#x`. The **date is derived from a relative age stamp** at retrieval and is
accurate to the day, not the hour. It is a **PRACTITIONER SELF-REPORT** about his own practice and career
(*"Early in my career…"*, *"here is how I keep myself in the loop"*), and **the skill-decay claim is
asserted as a risk, not measured.**

## Summary

*"AI can build the feature, but it won't teach you the lesson unless you force it to."* Osmani's claim:
engineering intuition came from *"thousands of hours debugging failures, reading diffs, and wrestling
with abstractions,"* and agents *"can short-circuit that entire journey. You get the completed task, but
**you miss the reps**."* The risk he names is **skill decay**: *"If we treat agents/loops/software
factories purely as code vending machines, we risk severe skill decay. We might become incredibly fast at
prompting, but lose the deep expertise required to actually verify the output when assumptions no longer
fit the system."* His epigram: **"Verification is the floor. Imagination is the ceiling."**

## Key points

- **The mechanism is loss of reps, not loss of knowledge.** The expertise at risk is specifically the
  kind produced by *doing* the debugging — which is why reading the agent's output does not replace it.
- **Three deliberate countermeasures**, all cheap and all placed *around* the loop rather than inside it:
  - **Form a hypothesis first.** *"Before prompting, predict what the solution should look like or where
    an architecture might fail."* A pre-registration habit: it makes the agent's output falsify something
    of yours, which is what turns a task into a rep.
  - **Anchor on explanation.** *"Instead of just generating net-new features, actively use agents to
    analyze and explain existing codebases. Forcing the AI to break down complex, pre-existing logic
    helps build your mental model much faster than just asking it to 'write this.'"* Note the inversion —
    the agent as a **comprehension instrument**, not a production one.
  - **Codify the lessons.** *"Don't let your learnings die when the chat window closes. Turn corrected
    assumptions into **linting rules, documentation, or tests** in your repo so both you and the next
    agent can benefit from them."*
- **The dependency he is pointing at.** The reason skill decay matters operationally is that it degrades
  *"the deep expertise required to actually verify the output"* — so the loss of reps eventually
  undermines the very verification the whole loop-engineering discipline depends on. That is a
  **second-order** argument, and it is the note's actual contribution.
- **Limits.** A LinkedIn note, not an argued piece: **no evidence of any kind** for the skill-decay claim
  — no study, no measurement, not even a personal before/after. Osmani frames it as a **risk** ("we
  risk"), and it must be carried that way. The three countermeasures are unevaluated personal habits. The
  substantive write-up it points to is **not in `raw/`**, so this capture holds only the summary. Plus the
  capture-note caveats above (day-accurate date, logged-in single-pass capture of a platform post that
  may be edited or deleted at source).

## Connections / contrast

**This is the KB's first source naming *skill decay* as distinct from [[comprehension-debt]], and the
distinction is worth preserving on that page.** Comprehension debt, as the KB has it, is a gap between
*what exists* and *what you understand about this codebase* —
[[addyosmani-human-judgment-relocates|Osmani's own]] "I couldn't explain to you how the feature worked"
is the canonical instance. **Skill decay is a gap between what you can do and what you could once do** —
it is portable across codebases, does not heal by reading the diff, and shows up as degraded
*verification capability* rather than degraded local knowledge. Same author, two different debts, and the
KB should not collapse them: you can pay down comprehension debt by reading the code; you cannot pay down
skill decay that way, because the missing thing is the reps.

**"Codify the lessons" is the individual-scale version of the hill-climbing loop.** Turning a corrected
assumption into a lint rule, a doc or a test is exactly
[[anthropic-getting-started-with-loops|Anthropic's]] *"don't stop at fixing the individual issue; encode
it to improve the system for all future iterations"* and
[[addyosmani-code-agent-orchestra|his own]] `REFLECTION.md`-with-lead-approval — but aimed at the
**human's** learning as much as the harness's. Note the pleasing asymmetry with
[[addyosmani-agentic-code-quality|Agentic Code Quality]]: there, encoding a lesson as a constraint is how
you stop *reading* every diff; here, it is how you stop *forgetting*. Same artifact, two purposes.

**"Anchor on explanation" is a use of agents the KB barely files.** Every other source in this batch
treats the agent as a producer whose output must be checked. Osmani proposes the agent as an
**explanation engine over existing code** — which is the same instinct behind
[[borg-tornhill-code-for-machines-not-just-humans|code health as an input]],
[[willison-understand-to-participate|Willison's "understand to participate"]], and the
[[llm-wiki]] pattern this KB itself runs on. It is also the practice most directly opposed to
[[addyosmani-human-judgment-relocates|the wrong-project prompt]] and the feature-he-had-to-relearn:
the fix for both was, in the end, reading and re-deriving.

**Converges with [[addyosmani-earning-taste-and-judgment]] and closes a loop in his own arc.** That piece
argues taste is the ungradeable residue once loops automate the reps that used to produce judgment. This
note asks the obvious follow-up — *if the reps produced the judgment, and the loop takes the reps, where
does the next generation's judgment come from?* — and answers it with deliberate practice rather than
with structure. It is the same worry [[voss-what-the-hell-is-a-loop-anyway|Voss]] relays from Geoffrey
Litt (*"those who delegate understanding get replaced by the agent"*) and
[[macmanus-prs-not-welcome-software-factories|MacManus]] finds at community scale (external PRs were how
maintainers were grown; close them and the pipeline closes too). **Three levels of the same problem —
individual, career, institution — and none of the three has evidence.**

## Links

[[comprehension-debt]] · [[loop-engineering]] · [[software-factory]] · [[agentic-coding]] ·
[[addy-osmani]] · [[ai-readable-code]] · [[fitness-functions]] · [[llm-wiki]] ·
[[addyosmani-earning-taste-and-judgment]] · [[addyosmani-human-judgment-relocates]] ·
[[addyosmani-agentic-code-quality]] · [[addyosmani-code-agent-orchestra]] ·
[[addyosmani-own-the-outer-loop]] · [[willison-understand-to-participate]] ·
[[voss-what-the-hell-is-a-loop-anyway]] · [[macmanus-prs-not-welcome-software-factories]] ·
[[anthropic-getting-started-with-loops]] · [[borg-tornhill-code-for-machines-not-just-humans]] ·
[[dilger-describing-without-solving-burns-you-out]]

_Source: [[osmani-ai-wont-teach-you-the-lesson-unless-you-force-it]] (raw: `raw/notes/osmani-ai-wont-teach-you-the-lesson-unless-you-force-it.md`)._
