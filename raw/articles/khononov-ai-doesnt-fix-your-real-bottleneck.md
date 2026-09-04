---
source_url: https://vladikk.com/2026/02/23/ai-toc-bc/
title: "AI Doesn't Fix Your Real Bottleneck"
author: Vlad Khononov
publication: Rants on Software Design (vladikk.com)
published: 2026-02-23
retrieved: 2026-09-04
type: article
capture_note: Out-of-window backfill (2026-02) filed on the 2026-09-04 sweep — a
  recency-bounded watch cannot reach it. Retrieved via WebFetch and transcribed verbatim;
  site nav, sidebar, footer, share widgets and the related-posts list stripped, the lead
  image noted inline as [image: ...]. Full body present from title through the closing
  "P.P.S."; no portion missing or truncated. The "Posted on February 23, 2026 | 5 min
  (935 words)" line is the page's own byline block. source_url observed in search results
  and confirmed by the fetched page, not reconstructed.
  NOT INDEPENDENT: Khononov is the author of the balanced coupling model and of
  "Balancing Coupling in Software Design", and the post closes by linking that book (via an
  amzn.to affiliate link) and coupling.dev — this is the model's own author arguing that his
  model is the answer to the AI-era bottleneck, not external corroboration.
  IMPRESSION NOT MEASUREMENT: the Theory-of-Constraints argument is analytical, not measured.
  "Every other post on my feed celebrates...", the "hundred-fold productivity gains" he is
  rebutting, and the claim that the system degrades are all argument and observation, not
  data from this post. The 4±1 / 7±2 working-memory figures are cited as "studies" with no
  reference given on the page.
---

# AI Doesn't Fix Your Real Bottleneck

Posted on February 23, 2026 | 5 min (935 words)

[image: An assembly line where an AI robot speeds up code production, creating a massive pile of blocks in front of an overwhelmed human operator with a warning alarm — illustrating how accelerating code generation creates a bottleneck at human comprehension.]

Every other post on my feed celebrates how AI lets us write code faster: whole apps built in a matter of a few hours, 99% AI-generated codebases, hundred-fold productivity gains, and on and on. But does writing code faster actually make us more productive?

## A Quick Detour Through a Factory

The Theory of Constraints says that every system's throughput is limited by a single constraint: its bottleneck. What makes a system more effective? Improving the bottleneck. What makes a system less efficient? Improving anything else.

I know, that second part is counterintuitive. Here's the thing: if you speed up a non-bottleneck, you don't improve the system; you produce more work-in-progress that piles up in front of the bottleneck! More inventory. More cost. More waste. The system becomes more expensive to operate, not more productive.

This is a well-established principle in manufacturing, and software manufacturing is no exception.

## What's the Bottleneck?

Think about what makes software engineering hard. Is it typing? If you have a clear understanding of the business domain and requirements, is it that hard to codify the domain knowledge? Not really. Writing new code is the easy part.

The hard part is evolving a system. You might not be the one who built it. But to add new functionality or change existing behavior, you need to understand what the system does, how its components interact, and what will happen when you change one of them.

Our cognitive capacity for untangling such dependencies is limited. Studies put the number of information units we can hold in working memory at around 4±1. More optimistic ones say 7±2, but that research is dated. The exact number doesn't matter. The point is: there's a hard ceiling, and it's not very high.

**The bottleneck in software engineering is our ability to comprehend systems.**

## Code Piles Up, Clarity Doesn't

When the cognitive load required to understand a system exceeds our cognitive capacity, we can no longer predict the outcomes of changes. We change things and watch what happens. Did it work? Did something else break? — No way to know until you try. Changes become dangerous, and development slows to a crawl of trial and error.

That's *complexity*. Not complexity as in "this is a hard problem," but complexity as in "we don't know what will happen when we touch something."

And it's not just us. Your AI-robot-friends suffer from complexity too. The larger the codebase an LLM has to work with, the faster its context fills up and the less effective it becomes.

Now consider what happens when AI generates more code, faster. Cognitive load piles up and the bottleneck gets squeezed harder. We're accelerating a non-bottleneck (code production) while piling up inventory (code we need to understand and maintain) in front of the real constraint: our cognitive limits.

The Theory of Constraints predicts exactly what happens next: the system degrades.

## Invest in the Bottleneck

If the bottleneck is our cognitive capacity, the way to make the process more efficient is to reduce the cognitive load the system induces. The answer is **modularity**.

What's the goal of modularity? When you need to make a change, you know exactly which components are affected, and the outcome of the change. No guessing, no trial and error. Confident reasoning instead of complexity. Sounds good? Getting there requires balancing three dimensions of coupling.

### Shortcut to Modularity

Every system is made of components that are connected to each other. Those connections, that coupling, can either produce modularity or complexity. The outcome depends on three dimensions:

- **Shared knowledge**: the knowledge components share about each other. The more knowledge is shared, the higher the likelihood that a change in one will trigger cascading changes in others.
- **Distance**: the physical and organizational distance between coupled components. The greater the distance, the more expensive cascading changes become.
- **Volatility**: the probability that a component will need to change in the first place. High volatility amplifies design problems; low volatility neutralizes them.

When these dimensions are balanced, the design is modular:

- Components that change together (shared knowledge is high) are located close to each other (distance is low); and
- Components that don't change together (shared knowledge is low) are spread apart (distance is high).

When the dimensions are not balanced, you get cognitive load (=complexity):

- Closely related components (shared knowledge is high) located far away (high distance) make dependencies hard to trace; and
- Unrelated components (shared knowledge is low) located close to each other (low distance) clutter the codebase.

Ultimately, volatility multiplies the effects of complexity.

That's the **balanced coupling** model.

## The Right Question

The question isn't "how do we write code faster?" It's "how do we keep systems understandable as they grow?"

AI can help with that too. But only if we point it at the right problem. Using AI to generate more code without investing in the modularity of our systems is like speeding up a machine that's already overproducing. The bottleneck doesn't care how fast the upstream station works.

Invest in the constraint. Design for modularity. Balance your coupling.

## Learn More

To learn more about balanced coupling and how it drives modular design, check out the [Balancing Coupling in Software Design](https://amzn.to/4irApMt) book and [blog](https://coupling.dev).

## P.S.

"But my AI already writes modular code!" Yeah, sure. Generating code that *looks* modular and designing a system that *is* modular are two very different things. Modularity is a system-level property. It requires understanding the business domain, the organizational structure, and the trade-offs between them. That's not a prompting problem. At least, not at the moment…

## P.P.S.

If you found this useful, share it. The bottleneck conversation is one worth having.
