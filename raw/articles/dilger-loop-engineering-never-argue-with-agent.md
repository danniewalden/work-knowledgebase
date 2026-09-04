---
source_url: https://www.eventmodelers.ai/docs/blog/loop-engineering-never-argue-with-agent/
title: "Loop Engineering - Or Why You Should Never Argue With an Agent"
author: Martin Dilger
publication: eventmodelers.ai (nebulit | Event Modeling Toolkit)
published: 2026-06-10
retrieved: 2026-08-18
type: article
---

# Loop Engineering - Or Why You Should Never Argue With an Agent

*Clean iterations with recorded learnings outperform long, polluted conversations with AI agents - every single time.*

June 10, 2026 · 10 min read · AI & Architecture

Most engineers right now are trying to put their head around "Loop Engineering." What does that even mean, and why does everybody keep claiming it's the "new thing" after "Spec-Driven Development"?

Let me explain.

Most developers are slowly poisoning their AI agents. And they have no idea it's happening.

When "loop engineering" started trending, my first reaction was: finally. Not because it was new to me - but because it was getting a name. A real one. Something people could point to and say: this is the method.

It started for me back in 2025, when I read Geoffrey Huntley's papers. He called it the RALPH loop. My first reaction was honest: running an agent in a loop? Nonsense. But then I kept thinking about it. And I realized - wait. I'm already doing this. I just didn't have a word for it.

## What Loop Engineering Actually Is

First, people heavily overcomplicate things. It's very simple, that's why it works so well.

You define a list of tasks your agent needs to accomplish. You run them one by one in a loop. After each task, you record what you learned along the way - an architectural insight, a way to prevent a failure, a small hint that makes the next task a little easier. Then you clear the context completely. The next iteration starts from scratch. No bias. No bad decisions lingering. No wrong information. Just the learnings - and the next task.

That last part - clearing the context - is the part people instinctively fight. It feels wrong. It feels like losing progress. It's the opposite.

## Why Context Is the Enemy

Here's what actually happens when you have a long conversation with an agent.

You try something. It doesn't work. You correct it. You go back and forth. You finally get it working. And along the way, the context fills up with every bad decision, every reversal, every disagreement, every dead end. The agent is carrying all of that.

The longer this goes on, the more confused the model becomes. And confusion is what produces hallucination. It's not a random event. It's the predictable result of a polluted context window.

Most people respond by prompting harder. They try to argue their way out of the spiral. Define more rules. Define more guardrails. Just add another instruction in capitals. They are making things worse.

## I Never Argue With an Agent

Every agent will immediately tell you how right you are. That's not learning. That's hand-waving agreement.

Think about what a conversation looks like after you've been going back and forth for an hour. Arguing. Correcting. Reverting. Finally getting something to work. If the agent were to look back at that conversation and try to draw conclusions - what would it actually conclude? Nobody knows. The signal is completely buried in the noise.

> "The agent isn't learning from your corrections. It's just agreeing with you - and carrying the confusion forward."

So my rule is simple. Each iteration has clearly defined goals. Each iteration has clearly defined rules. If a rule is broken, there's no discussion. I throw everything away - except the learnings - and retry in the next loop. Clean slate. Every time.

## Do Not Fine-Tune the Loop

Just yesterday someone reached out to me wanting to engineer the loop. Add complexity. Add layers. Make it smarter.

Essentially the idea was - if an agent is working on a task, and someone is changing the task, the agent should stop, revert everything and restart. My question was "why?" - let that sit. You are engineering around the loop - the loop already takes care of this.

In detail, we were discussing how the build-agents on the Eventmodelers platform orchestrate their tasks.

I understood the instinct. But it completely misses the point. I'll show you why.

## Event Modeling Is "Loop Engineering" Applied

The hard part in Loop Engineering is not implementing the loop, it's defining the list of tasks. In Event Modeling this happens naturally and is part of the process.

Every "slice" of functionality becomes a task.

*[Image: Every slice on the timeline becomes a task an agent can pick up]*

Tasks have a status. You can assign a task, mark it blocked, or mark it "planned" - planned means this slice can now be picked up by an agent.

*[Image: Each Slice has a status - Planned means ready to be picked up by an agent]*

An agent can subscribe to changes on a board. Whenever a slice changes, subscribed agents get notified.

*[Image: Agents like Claude Code, Codex, and Hermes subscribe to slice:changed events]*

Each of those agents run in a loop. Essentially waiting for something to do, sleeping while not. One agent will pick up the slice.

*[Image: An agent claims a slice: I'll take that one!]*

The agent then puts the slice in progress. Much like assigning a ticket to an engineer. If it's assigned, no other developer or agent can take it.

*[Image: A slice moved into in-progress status while an agent works on it]*

Now essentially one of three things can happen.

- Task finishes (agent puts the slice in "Done")
- Task is blocked (something is missing, agent puts the slice in "Blocked")
- Agent dies (task stays in progress and times out after a while, another agent can pick up on it)

This picture shows it best.

*[Image: Event Modeling Agent Harness diagram - the full 24/7 loop from Draft to Ready to Working to Done]*

## No Prompting, Looping

The beauty of it - there's no manual prompting involved. Just change a slice and wait until the agent did the work.

Changing an existing slice? Just move it from "Done" to "In Progress," make your adjustments and then move it to "Planned." An agent will pick it up, find the difference between the specified slice and the code, and adjust the code to match the spec again - adding scenarios, adding fields, whatever.

If something fails, the problem is in the spec, not the prompt. Just throw away the failed attempt, let it record the learning, adjust the model, and put the slice back into "Planned." The next one will pick it up again and retry from scratch.

I use comments on the slice or each element to give implementation hints if necessary. When done, the agent will check off the comment.

*[Image: A comment on a slice giving the agent an implementation hint]*

## No (Over)Engineering Necessary

There is no need to stop an implementation of a slice if changes have been made. Just finish the loop and let the agent pick up the same slice again and adjust the changes. This often happens to me when I realize I forgot a few scenarios. Just add them in the model and put the slice back into "planned."

The beauty of loop engineering is its simplicity. The moment you start overengineering it - adding more state, more memory, more decision-making between iterations - you start reintroducing exactly the problems the loop was designed to eliminate. You're building back the noise.

Simplicity isn't a limitation of loop engineering. It is loop engineering.

## The Counterintuitive Truth

Clean iterations with recorded learnings will outperform long, polluted conversations every single time. Not sometimes. Every time.

Throwing away context feels like losing progress. Starting from scratch feels like going backwards. But what you're actually doing is protecting the signal. You're making sure the next iteration runs on clear information - not on the accumulated wreckage of everything that went wrong before.

That's the loop. That's why it works. And that's why "finally" was my first reaction when it got a name.

## The Spec-Driven Book

*[Image: Cover of the book Spec Driven - a hands-on guide to becoming an agentic engineer]*

This whole approach is essentially what I describe in detail in my book "Spec Driven." Follow me here on LinkedIn if you want to stay up to date.

The Eventmodelers platform is the one place where agents and humans come together. "Loop engineering" built in by design.

The build-kits provide ready-made loop setups. You can get started in 30 seconds.

And of course - don't forget. I can teach your team how to do this, as I did for hundreds of engineers already. Book a free 15-minute call (German or English) to discuss the potential.
