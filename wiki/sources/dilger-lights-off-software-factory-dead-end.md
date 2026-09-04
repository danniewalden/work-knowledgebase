---
title: "Dilger — The lights-off software factory is a dead end"
type: source
created: 2026-08-31
updated: 2026-08-31
sources: [dilger-lights-off-software-factory-dead-end]
raw_file: [raw/notes/dilger-lights-off-software-factory-dead-end.md]
tags: [software-factory, agentic-coding, unattended-coding-agents, code-review, slice, focus]
---

# Dilger — The lights-off software factory is a dead end

LinkedIn post by **[[martin-dilger]]**, 2026-08-16. Raw capture:
`raw/notes/dilger-lights-off-software-factory-dead-end.md`.

**The dissent [[software-factory]] was missing.** That page's light-vs-dark section had no named
practitioner arguing the dark factory is a dead end; this is one, and from someone who is otherwise
maximally bullish on agentic engineering.

## The claim

> "lights-off is generally used to describe a software process where the code remains in the dark. No one
> reads it, no one reviews it - no one but agents. **Every single team I know who went down that route
> circled back.** I don't practice it either, even though I'm all in on agentic engineering."

The failure mode is specifically an **incident** failure mode: *"It's fun trying to solve an issue, with
production burning and no one there to navigate the code base ( as no one has ever seen it )."* That is
[[comprehension-debt]] with a due date.

And he states the bind precisely: *"you can't do full code reviews - it'll not be sustainable with the
increased output - you just moved the bottleneck. But you can't do no code-reviews either it seems."*

## His answer — layers of trust

The most concrete verification pipeline in the KB from a practitioner:

1. **The Event Model as spec**, with guard rails as [[given-when-then]] scenarios.
2. Those scenarios **translated to executable specifications** — "Test-First Development if you will ( as
   we define the tests long before any code )." *"If all those tests are green, I'm pretty confident it
   does what it should."*
3. **Static checks**, each with a defined consequence:
   - were any tests adjusted → requires review
   - are there tests outside the specification → requires review
   - were files changed outside the **SUD (Slice Under Development)** → **immediate fail**
   - were dependencies changed → requires review
4. **A 2–3 minute manual review that is explicitly not functional**: *"at this point we already know it
   works. I look at the structure, does it match my mental map?"*

Failure handling is disposal, not repair: *"Almost always, this means we throw away everything, record a
learning 'why' this was not good enough and start from scratch ( my [sic] moving the Slice back into 'planned' )."*

## Why it matters here

- **It reframes the review question from volume to placement.** Not "how much do we review" but "what is
  each check *for*" — functional correctness to tests, structural conformance to static gates, mental-map
  maintenance to a human. That is the KB's cleanest instance of
  [[feedforward-and-feedback-controls]] applied to agent output.
- **The stated reason for keeping a human in it is comprehension, not correctness**: *"I keep connected
  to the code base. It allows me to keep a map of it in my head. If something goes wrong, I roughly know
  where to look."* That is an argument [[software-factory]] and [[comprehension-debt]] both need.
- **"Files changed outside the SUD → immediate fail"** makes the [[slice]] boundary a machine-checkable
  invariant, not just a design intention.
- His asymmetry of concern is worth recording: *"I don't care too much how a slice is implemented
  internally, as any bad implementation can be easily replaced. I do care a lot about the overall
  structure of the system and **the shape of the persisted data ( our Events )**. If that is broken, we
  got a serious issue."* Event schema as the one irreversible decision — compare the reversibility axis
  in [[autonomy-ladder]].

## Caveats

- "Every single team I know who went down that route circled back" is the load-bearing empirical claim
  and it is unattributed hearsay — no teams named, no numbers.
- Vendor-adjacent, and the pipeline described is the one his platform supports.
- The 2–3 minute review figure is self-reported.

## Related

[[software-factory]] · [[unattended-coding-agents]] · [[comprehension-debt]] · [[slice]] ·
[[given-when-then]] · [[feedforward-and-feedback-controls]] · [[autonomy-ladder]] ·
[[dilger-trust-needs-to-be-engineered]] · [[addyosmani-software-factories-light-and-dark]] ·
[[martin-dilger]]
