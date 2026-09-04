---
source_url: https://adamtornhill.substack.com/p/compressed-cognition-the-hidden-cost
title: "Compressed Cognition: The Cost of Faster Coding"
author: Adam Tornhill
publication: "Code for Humans and Machines (Substack)"
published: 2026-05-07
retrieved: 2026-09-04
type: article
capture_note: >-
  Contains one genuine MEASUREMENT, quoted here verbatim and worth keeping as such: a
  controlled trial of experienced open-source developers in which the AI-assisted group
  "claimed so themselves, estimating a 20% speedup. Only problem: they were not. They
  ended up 19% *slower* than the non-AI group." That is a measured effect (an RCT-style
  RCT design) set against a self-reported impression, and the gap between the two is the
  author's point — do not collapse the 20% (felt) and the 19% (measured) into one
  "figure". Caveat: the author does NOT name, date or link the study anywhere in the page
  text ("One of my favourite studies gave experienced open-source developers access to
  AI tools"), so the citation cannot be followed from this capture alone. The other
  research references — decision fatigue via "Danziger et al." on judicial rulings,
  Sweller on cognitive load, and the revision of "seven plus or minus two" down to "3-4
  things" in working memory — are likewise cited by author name only, without links.
  IMPRESSION NOT MEASUREMENT for the author's own experience claims ("I can usually
  sustain the pace for a couple of hours", "based on conversations with other engineers").
  NOT INDEPENDENT for the prescription that "automation and safeguards are the mechanisms
  for delivering trust, not manual inspection" — the author is founder and CTO of
  CodeScene, which sells automated code-quality safeguards. Full text captured; one image
  is noted inline as [image: ...].
---

# Compressed Cognition: The Cost of Faster Coding

My post on Coding Is Dead (...But It Still Smells Funny) touched upon developer flow. One of the big wins with agents is that they let us stay with the higher-level problem for longer. We get less sidetracked by details, dependency cleanup, and similar secondary tasks that used to break concentration.

But there is a cost we are still underestimating. Agentic coding is mentally expensive.

I can usually sustain the pace for a couple of hours. Then I need a break. The pace is simply too intense. And based on conversations with other engineers, I do not think I am alone in that.

That is the trade I want to unpack here. Agents help us stay with the problem longer, but they also compress too many meaningful decisions into too little time.

## The timeline collapse

Software development was always about making decisions. A typical product requirement quickly explodes into hidden design work that end users never see. Architecture, naming, boundaries, behavior, edge cases, test design, failure modes.

In the old days, say pre-2025, work unfolded at human speed, which meant the decisions were naturally spaced out. Today, agents compress the timeline. We have to deal with complexity and decisions that used to be spread over days in a single coding session.

But there's more. Agentic coding raises the engineering bar, and we just cannot afford to slip. Like skipping e2e tests, ignoring problematic dependencies, or rebuilding library functionality we should have reused.

So we're now a) facing more complex work, with b) a compressed timeline of decisions. No wonder agentic coding is draining.

## Decision density and mental energy

What we are experiencing as modern developers is not new. It just shows up in a new context.

Psychology has studied the mental cost of decision making for decades. One of the most well-known concepts is decision fatigue. Decision fatigue says that the quality of our decisions deteriorates after a long session of continuous choices.

One of the most cited examples comes from judicial decisions. Danziger et al. looked at thousands of rulings and found that favorable decisions dropped as judges moved through a work session. Interestingly, the decision quality then recovered after breaks.

The Danziger study shows what depletion looks like in practice. Other studies suggest the mechanism: making choices is itself mentally expensive. Agents accelerate the arrival rate of those decisions.

Manual coding had a built-in pacing mechanism. That was our implicit recovery break. And it's now gone.

[image: Cognitive load visualization]

## Why this is hard on the brain

This lines up neatly with cognitive load theory.

Sweller's classic work on cognitive load focused on problem solving. When too much information has to be held and manipulated at the same time, reasoning suffers. Agents might remove lower-level serial coding work, but they also increase the amount of high-level state you have to evaluate.

Working memory is limited too. You might have heard about the classic "seven plus or minus two" rule. Turns out that was over-optimistic. Modern cognitive scientists paint a more depressing picture: we can, at best, hold 3-4 things in our head at once and still be able to reason effectively.

Now, any non-trivial software task involves plenty of moving parts. Even with agents, we still have to decide which parts matter, how they interact, and whether the design still holds together. It's a lot more architecture per minute.

## The interruption problem on steroids

We all know that traditional task switching is cognitively expensive. It harms our focus, and hurts performance.

However, what's less known is that self-interruptions tend to be even more disruptive than external ones.

Coincidentally, agentic coding is like an open invitation for more self-interruption. The agent:

- asks a question,
- produces a diff,
- gets blocked by a missing tool,
- fails a test, or
- suggests a change that looks *almost* right but touches too much.

Each event pulls you into a new review-verify-steer decision.

## The AI productivity paradox

This also helps explain why the productivity story around AI coding tools is more complicated than the marketing slides suggest.

One of my favourite studies gave experienced open-source developers access to AI tools. It was a controlled trial, so half the participants were still coding in the old school way.

At first glance, the study seemed to confirm the usual story: the developers with AI tools felt faster. Indeed, they claimed so themselves, estimating a 20% speedup. Only problem: they were not. They ended up 19% *slower* than the non-AI group. Adding insult to Big Tech injury, the study also demonstrates that even expert developers overestimate the AI impact on developer productivity.

One plausible contributor is self-interruption. Developers get many natural pause points: waiting, reviewing, correcting, etc. Each of those pulls you into a different task.

## How I try to manage it

AI is now an integral part of our work, and we do not want agents to slow down. Speed is kind of their point.

But we do control when and how we actively interact with AI:

- The simplest tip is to keep agent tasks small and iterative enough so that the review fits in your head
- That includes designing for cognitive resourcefulness: automate everything that can be automated. (You don't want to spend time reviewing coding rules, checking test coverage, etc.)

There are also things that I actively avoid doing:

- **Don't review details, verify them.** This was a hard one personally, but we need to accept that we can no longer know every line of code. Again, automation and safeguards are the mechanisms for delivering trust, not manual inspection.
- **Avoid parallel work.** I typically have one long-running agentic maintenance task that I just babysit, and then one focus task. Never more.

That last point is important given the running-twenty-agents-in-parallel hype. I cannot even think about twenty *meaningful* things to build, and even less so about the resulting cognitive tax of the likely interruptions. It's exactly the wrong thing to even consider. At least for humans. (And yes, I understand sub-agents and machine parallelisation. That is not what I'm objecting to. It is the parallelisation of human attention that does not scale).

Finally, and this will bring me enemies from the corporate ladder who think software is built by typing: take breaks from your agents. And take those breaks earlier than you think you need them.

Those breaks are not just recovery. They are also a chance to build the skills the new developer role demands. So use those non-coding hours to deepen your domain expertise. A few ways to do that:

- **Train as an end-user.** This is the single best way towards becoming a domain expert. Master the problem domain.
- **Grab a coffee.** Many of the best ideas come *away* from the laptop. Your brain needs the occasional change of setting. Under the hood, it keeps operating. (The majority of all brain activity is automated and subconscious). When you relax, your brain delivers its insights that were worked on in the background.
- **Do exploratory testing.** Yes, automation is great, but there's no limit to the creative ways we humans can break a system. Make it a challenge.
- **Understand your product metrics and usage patterns.** What features are people using, what are they ignoring, etc. This gives a different perspective on your code. Promise.
- **Get involved in sales.** This one might not be for everyone, but technical sales is a challenging role that gives you a much deeper understanding of where your product needs to be.

The point is to re-invest the time agents save into activities that deepen your expertise while giving your brain a recovery window.

Agentic coding is still new. But it's becoming increasingly clear that the workflows around agents have to respect human cognitive limits. The future holds more software than ever, and we need to come prepared to build it in a sustainable way.
