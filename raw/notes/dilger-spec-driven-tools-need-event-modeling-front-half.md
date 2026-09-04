---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7489568450927869952/
title: "I honestly don't understand spec driven development (the way most tools do it)" — Event Modeling as the front half that feeds Spec-Driven toolkits
author: Martin Dilger
publication: LinkedIn (post)
published: 2026-08-02
retrieved: 2026-08-03
type: note
---

(Captured via live logged-in Chrome from Martin Dilger's LinkedIn activity feed; posted ~1 day before retrieval. Verbatim.)

I honestly don't understand spec driven development. Not the concept. The way most of these tools currently do it.

Yesterday I tested Spec Kitty. Basically a set of skills that guide you through the "specification"-part. I gave it a list of requirements, intentionally vague, to see what it would do with them. It went straight to work, asking questions to dig into the details. Good! That's the whole idea behind these frameworks. Sounds right. Sounds like what I do in every event modeling workshop.

Except the third question was already about the tech stack. That confused me. I stopped it. Shouldn't we spend some more time understanding the problem first? Then it came up with a "domain model" almost immediately. Structures for a book, a catalog entry, defined before it had any real grasp of the problem. The requirements covered a few different functionalities, and the questions came back in arbitrary order, jumping between features with no structure. I could follow it as a technical person. A business stakeholder on the other end of that conversation would have no idea if they're supposed to answer feature by feature or think about the whole system at once.

We ended up with 46 markdown files after 20 min. High level spec down to concrete implementation tasks. And then it suggested the next step was implementation. What? no way can we implement this now, I mentioned in a friendly tone.

Here's the part I've been sitting with. I'm currently writing a book called "Spec Driven" - and I'm intentionally leaving these tools out of it. That comes with a bit of imposter syndrome, being honest. But it's not something I made up. Every team I've watched try to work this way genuinely struggles. Twenty minutes in, you have fifty markdown files. Who is reading all of that? Who is maintaining it. So much assumption gets baked in early - the shape of the model, the technology choices - before anyone has actually agreed on the problem.

But I watched myself lose track of a spec after twenty minutes of markdown madness. Skipping the visual model doesn't remove the complexity. It just removes the thing that was managing it.

In a recent workshop we combined AWS Kiro with Event Modeling. The event model did the hard part - breaking the problem down, getting everyone aligned on what's actually happening. Then we used a special skill to translate that model directly into Kiro Tasks. I did the same for Spec Kitty. The result is a clear, broken-down requirements feeding a spec-driven framework that finally had something real to work from.

That´s actually simple to do, as the Event Modeling Format is standardized and documented. I´ll gradually add this to the Event Modelers CLI, which makes it a natural bridge between Event Modeling and all those Spec-Driven Toolkits ( Spec-Kit, Spec-Kitty, Kiro and so on ). It´ll be just an "eventmodelers export --spec-kitty".

That's the symbiosis, and it works. The tools aren't the problem. Skipping the digging is.
