---
title: "Martin Dilger — My Wife Asked Me to Build a Flea-Market Registration (model → code → deploy in 30 min)"
type: source
created: 2026-07-01
updated: 2026-07-01
sources: [dilger-flea-market-model-to-deploy]
raw_file: [raw/notes/dilger-flea-market-model-code-deploy-30min.md]
tags: [event-modeling, vibe-modeling, event-sourcing, spec-driven-development, communication, focus]
---

# Martin Dilger — My Wife Asked Me to Build a Flea-Market Registration (model → code → deploy in 30 min)

LinkedIn post by **[[martin-dilger]]** (2026-07-01; captured same day).
Source file: `raw/notes/dilger-flea-market-model-code-deploy-30min.md`. A "real story" vignette that is the
KB's strongest concrete instance of **[[vibe-modeling]]** — a non-technical stakeholder co-modeling a
system without knowing the method.

## What happens

Dilger's wife asks him to build a flea-market registration form. He opens the
[[eventmodelers-ai|Eventmodelers platform]] ("she was a bit surprised") and they **brainstorm by drawing
screens** — he pointedly **doesn't explain what Event Modeling is or name it**. Through ordinary questions
("why do you need it?", "what happens after someone registers?", "how do you track who's paid?") the model
emerges: parents register → she needs a **spreadsheet of names + emails** → a **5 EUR table fee collected
by hand** (she rejects his reflexive "Stripe or Copecart?") → a **button in a screen** to filter who hasn't
paid yet.

The load-bearing line:

> "She understood exactly what we were doing. Not because I taught her Event Modeling — she has no idea what
> that is. And she doesn't care… Just by drawing the screens as we usually do she could easily follow along."

**Modeling, building, and deploying took under 30 minutes.** His stated reason: the **tooling already made
the hard decisions** — no project setup, no architecture debate, no "which event store" — so *"you are
literally one button click away from Building."* The loop: **Model → Code → Deploy → rinse repeat.**

## The three takeaways he draws

1. **The stakeholder shouldn't care about the method** — "it's just a tool. She wanted her problem solved.
   That's it." (Vibe modeling's whole point: the method is invisible; drawing screens is the shared language.)
2. **Planning earns its keep with complexity** — he concedes Claude could have built *this* trivial app
   with no modeling and it "wouldn't have mattered," but "the more complex a system gets, the more that
   planning step starts to earn its keep." A candid, non-dogmatic framing of when the model pays off.
3. **Event Sourcing isn't complicated** — he'd use [[event-sourcing]] even for something this small, "not
   because it's the fancy choice, but because it's actually simpler than the alternatives once you're used
   to it"; "I'm not dogmatic about the method — I just like keeping things simple."

## Why it matters here

This is the demonstration [[vibe-modeling]] needed: the front-end where a **non-developer co-designs by
drawing screens with the practitioner + tooling**, capturing the "vibes" as an explicit model *before* any
code — exactly the collaborative structure the podcast coined the term for. It doubles as evidence for
[[eventmodelers-ai]]'s **"model → code → deploy" pitch** (cf. build kits, "model to generated code in 30
seconds," [[dilger-build-kits-model-to-generated-code]]) and for the [[spec-driven-development]] claim that
pre-made architecture decisions are what make the spec-first loop fast. The screen-drawing-as-discovery move
also connects to [[domain-discovery]] — here discovery is human-led and conversational rather than an agent
walking a UI. Takeaway 2 is a rare **honest boundary** on the method: for trivial systems, ceremony-free
vibe coding is fine; the model is insurance that scales with complexity.

## Caveats

Short marketing anecdote on his own platform; "under 30 minutes" and "one button click" are unverified
self-report, and the app is deliberately trivial (no payment integration, manual fee handling). It argues
the *communication* value by example, not measurement.

## Touches

[[martin-dilger]] · [[vibe-modeling]] · [[eventmodelers-ai]] · [[event-modeling]] · [[event-sourcing]] ·
[[spec-driven-development]] · [[domain-discovery]] · [[event-modeled-agent-design]] ·
[[dilger-build-kits-model-to-generated-code]]

_Source: `raw/notes/dilger-flea-market-model-code-deploy-30min.md`._
