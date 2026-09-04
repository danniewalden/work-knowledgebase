---
source_url: https://adamtornhill.substack.com/p/beyond-lambdas-raising-the-abstraction
title: "Beyond Lambdas: Raising the Abstraction Level of Functional Code"
author: Adam Tornhill
publication: Code for Humans and Machines (Substack)
published: 2026-09-01
retrieved: 2026-09-04
type: article
---

# Beyond Lambdas: Raising the Abstraction Level of Functional Code

### Good software design raises the abstraction level until the code communicates the domain rather than the mechanics.

[Adam Tornhill](https://substack.com/@adamtornhill)

Sep 01, 2026

Anonymous functions — aka lambda functions — have made their way into virtually all mainstream languages by now. These languages have been adopting functional programming techniques for the past decades (e.g. LINQ in C#, Streams in Java), and lambda functions are an inherent part of that paradigm.

The nice thing about lambdas is that they optimize for writing code. When coding, it’s quite convenient to stay within a function’s boundaries and just flesh out detailed steps as lambdas that are then being passed to map/filter/reduce-like operations.

The *bad* thing about lambdas is that they optimize for writing code. They do so at the expense of reading code, which is arguably a much more frequent activity.

So let’s start from a specific lambda example and then refactor our way towards better abstractions.

## **Name the nameless**

Quick, what is the following code doing?

```
rolls.stream()
    .map(roll -> roll + 2)
    .filter(roll -> roll >= 15)
    .sum();
```

It’s a mere 3 lines of code, and the mechanics of each one is trivial. Yet the purpose, intent, and business rules remain opaque. It could be anything.

The lack of explicit domain concepts is a warning sign. Instead, we should raise the abstraction level by naming those lambdas to reveal the code’s intent:

```
rolls.stream()
    .map(AttackRoll::applyStrengthModifier)
    .filter(AttackRoll::isSuccessfulHit)
    .sum();
```

The preceding code is no longer a stream of seemingly random operations. Instead it communicates the concepts and rules from the domain. (In this case: Dungeons & Dragons).

The new methods — `applyStrengthModifier` and `isSuccessfulHit` — are trivial one-liners. You implement them according to the idioms and features in your programming language of choice. For Java, I’d go with either private static methods or, if I notice groups of related abstractions, a private class. In Python or Clojure, we get away with even less syntactic noise: just use private module-level functions.

## **Balance the trade-offs**

A fair objection at this point is that the proposed approach leads to more lines of code. That’s true, but not necessarily a problem:

- Abstractions can be simple. Ridiculously simple.

- Abstractions don’t have to be re-used to motivate their existence.

- Lines of code are not a finite resource. Some abstractions might lead to more code. That’s a trade-off.

My short test for any abstraction is: if it elevates the level of the code, then it has earned its rights.

Granted, the recommendation to avoid lambdas didn’t come easily. I’m a Lisp hacker by birth. (No, not really, but I always wanted to write that sentence.) But I did spend the past 20 years doing functional programming, and have watched my style gradually migrate away from lambdas.

Naming functions — even those trivial one-liners — makes a large difference when returning to code you wrote months or years earlier.

## **Abstract the pipeline steps**

I usually take this abstraction a step further when the programming language allows it. Java doesn’t fall naturally into that category, so let me switch to a simple Clojure example.

Here’s the same problem in Clojure:

```
(->> rolls
     (map (partial + 2))
     (filter #(>= % 15))
     (reduce +))
```

If you haven’t seen Clojure before, then the threading macro `->>` probably looks odd. It’s just a convenient way of passing the result of one function as the input to the next.

And just like in the Java example, refactoring away the lambdas clarifies the intent:

```
(->> rolls
     (map apply-strength-modifier)
     (filter successful-hit?)
     (reduce +))
```

But we can take it one step further, and also name the pipeline elements. This makes all the difference:

```
(->> rolls
     with-strength-modifier
     successful-hits
     ->damage)
```

With that, the code now reads like a story, telling the rules of the domain. We’ve come a long way with simple steps. Anonymous functions are anonymous thoughts.

## **Optimize for reconstruction work**

By naming lambdas, we raise the abstraction level and add information that wasn’t previously visible. This is important since much code needs to be prepared to evolve.

When picking up a new coding task, that work often happens within the context of an existing codebase. This is where proper abstractions pay off by limiting the necessary reconstruction work. And the closer our abstractions reflect the problem domain, the easier that will be.

That’s also true for coding agents as captured in the [CLEAR principles for AI-first codebases](https://adamtornhill.substack.com/p/clear-software-design-principles). We will all do a better job when the code’s purpose is expressed structurally. Small abstractions add up, so make them a habit.

[image: hero illustration for the post — https://substack-post-media.s3.amazonaws.com/public/images/a109ff23-de9e-4399-aaed-64275b699623_1729x910.png]
