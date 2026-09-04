---
source_url: https://www.oreilly.com/radar/what-the-hell-is-a-loop-anyway/
title: "What the Hell Is a Loop, Anyway?"
author: Laurie Voss
publication: O'Reilly Radar (originally published on LinkedIn, republished with the author's permission)
published: 2026-07-29
retrieved: 2026-08-16
type: article
---

# What the Hell Is a Loop, Anyway?

*The AI engineering world adopted a new favorite word this month, and it means at least four different things.*

By Laurie Voss — July 29, 2026 • 10 minute read

> *The following article originally appeared on [LinkedIn](https://www.linkedin.com/pulse/what-hell-loop-anyway-laurie-voss-ldmdc/) and is being republished here with the author's permission.*

We're currently at the peak of the hype cycle. On June 7, Peter Steinberger posted that [you shouldn't be prompting coding agents anymore](https://x.com/steipete/status/2063697162748260627?lang=en); you should be designing loops that prompt your agents. That same week, [Boris Cherny](https://www.linkedin.com/in/bcherny/) of Anthropic said on stage that he doesn't prompt Claude anymore: "I write loops; [the loops do the work](https://x.com/sairahul1/status/2064279904989147577?lang=en)." Addy Osmani published an essay called "[Loop Engineering](https://addyosmani.com/blog/loop-engineering/)" on June 7, swyx published "[Loopcraft: The Art of Stacking Loops](https://www.latent.space/p/ainews-loopcraft-the-art-of-stacking)" on June 12, and LangChain published "[The Art of Loop Engineering](https://www.langchain.com/blog/the-art-of-loop-engineering)" on June 16. Then came the AI Engineer World's Fair, where the word [dominated the main stage](https://www.latent.space/p/aiewf-daily-dispatch-loops). Swyx's keynote was about Loopcraft, an entire track was devoted to software factories, speaker after speaker reached for the same word, and the conference closed on July 2 with an hour-long debate about whether the hype behind loops has outrun what works in practice.

The problem is that the people talking about loops aren't all discussing the same thing. I counted at least four distinct architectures hiding behind that one word. So this post is an attempt to map out what everyone means.

## The execution loop: The agent's own act-observe cycle

This is the loop most people picture when they say "agent": call a tool, read the result, decide the next action, and repeat until there are no more tool calls to make. It's what Addy calls the inner execution loop, the part agents can now run largely on their own, and it's the innermost loop you can engineer. (swyx's stack has a token loop, but nobody designs the token loop. It's just part of the model.)

![Loopcraft: The art of stacking loops](https://www.oreilly.com/radar/wp-content/uploads/sites/3/2026/07/image-30.png)

**Swyx's original Loopcraft diagram**

The execution loop iterates on steps within one task. It ends on environment feedback: the test output, the API response, and the file contents. Humans are usually absent mid-loop and appear at the boundaries, approving plans or reviewing results. The execution loop also ends whenever the agent decides it's done, whether or not it actually is. The first fix the field found for that was to wrap this loop in another one that doesn't take the agent's word for it.

## The task loop: Restart the agent until the spec is satisfied

This was the first loop to get a name and it's Geoffrey Huntley's Ralph loop, which got name-checked from the AI Engineer World's Fair main stage when Allie Howe of Keycard introduced the software factories track by citing Geoffrey's article "[Everything Is a Ralph Loop](https://ghuntley.com/loop/)." A Ralph loop restarts a coding agent against the same specification over and over, allocating a completely fresh context window every iteration and doing exactly one task per loop. The apparent waste is the point: Refeeding the full spec each time prevents the context rot and compaction events that quietly degrade long-running sessions.

What this loop iterates on is a single artifact. What ends the loop is spec compliance and passing tests. The human writes the spec and judges doneness, and in Geoffrey's telling the human has one more job that I'll return to later: watching the loop, spotting failure patterns, and fixing them so they never recur. In the closing debate on the conference's final day, he compared the role to a locomotive engineer, someone whose whole job is keeping the train on the rails. Zoom out from a single spec though, and a much bigger loop comes into view: the one that runs an entire codebase.

## The product loop: The software factory

This was the loudest version at the AI Engineer World's Fair. Tereza Tizkova of Factory defined a software factory as "the whole loop, the whole lifecycle of developing software with autonomy," and Zach Lloyd of Warp got specific about what that lifecycle is in an [interview with *Latent Space*](https://www.latent.space/p/aiewf-daily-dispatch-loops): triage, specification, implementation, review, verification, shipping, and monitoring. Zach's claim is that software engineering becomes factory engineering, and that you'll be building the thing that builds the product. Warp is dogfooding this: The company placed its own open-sourced repo under the control of Oz, its factory platform. Zach describes the adoption path as starting with low-risk repos and ratcheting the automatic PR merge rate upward from 20 percent toward 60. Anthropic appears to be running the same experiment internally. The company says [65% of its product team's code](https://www.anthropic.com/news/introducing-claude-tag) is now created by its internal version of Claude Tag, and Mike Krieger described his team's use of it at the World's Fair as delegated and proactive: not "fix this bug" but take responsibility for this part of the codebase, monitor this feedback channel, and pick up tasks on your own.

The task loop and the execution loop have defined exit conditions. The product loop iterates on a codebase and its backlog, continuously, and its closing signals come from outside the codebase entirely: new issues, production logs, user feedback, review outcomes. The human role becomes configurable. In Zach's framing, you pick the parts of the lifecycle to automate and the points where humans get brought in, and organizations differ on questions like whether code review stays human for high-risk changes. A factory improves a product. The next loop improves the factory itself.

## The system loop: Autoresearch

Roland Gavrilescu of Introspection calls this autoresearch. Here's how he framed the concept in a [*Latent Space* interview](https://www.latent.space/p/autoresearch-introspection): The inner loop is your primary system doing user-facing work, and the outer loop studies and maintains the primary system. It iterates on prompts, harnesses, model choices, and the evals themselves. His one-liner is that the loop is the product.

This pattern now has real existence proofs at both ends of the scale. The minimal case is Andrej Karpathy's autoresearch from March 2026, roughly 630 lines of Python that ran 50 hypothesis-edit-evaluate experiments overnight on one GPU. The shipped case is Meta's Brain2Qwerty v2, [announced in late June](https://ai.meta.com/blog/brain2qwerty-brain-ai-human-communication/), where the researchers report that agents iteratively modified the codebase to invent better decoding architectures, producing a substantial improvement in word error rate. Meta's caveat is instructive: Final training configurations were still selected by hand. Even the flagship system loop keeps a human at the last checkpoint.

What ends this loop is the most demanding signal set of the four: evals, judges, filtered product feedback, and, in Roland's design, an explicit ask-a-human tool through which the agent accumulates tacit knowledge the way a new employee does. And that's the top of the stack. Put the four together and the shape of the whole system becomes visible.

## The four loops side by side

![](https://www.oreilly.com/radar/wp-content/uploads/sites/3/2026/07/image-31.png)

*[Image: comparison table of the four loops — execution / task / product / system — across what they iterate on, what ends them, and the human role. Not reproduced as text in the source page.]*

## What about Agentic MapReduce?

One famous pattern from the same week is missing from this map on purpose. Cognition's [Devin Security Swarm](https://cognition.com/blog/introducing-devin-security-swarm) fans parallel bounded agents out across a repository and aggregates their findings, a shape the company calls Agentic MapReduce, and it gets called a loop. I don't think it is one. Dispatch, gather, validate is a pipeline: Nothing feeds back into a next cycle, and a loop without feedback is just a for statement. Fan-out is a topology you can deploy inside any of the four loops, not a loop of its own.

## The unnamed loop at the top is the oversight loop

In swyx's loop diagram, the outermost ring, the one above the loop that makes loops, is literally labeled "???? loop." Its verbs are "set goals, allocate, cull." Its exit condition is listed as none.

I think that loop has a name. I'm calling it the oversight loop: It's where goals get set, budgets get allocated, and work gets culled, and it's the one ring where a human should live. Addy said on the AIEWF stage: "That inner loop is capability. The outer loop is agency." Agency is exactly what the oversight loop holds.

![The loop stack, tidied up a bit.](https://www.oreilly.com/radar/wp-content/uploads/sites/3/2026/07/image-32.png)

**The loop stack, tidied up a bit.**

And the sharpest disagreements at AIEWF were all, once you translate them, arguments about who runs that top ring. Zach and Roland make the case for turning the dial up: pick your checkpoints deliberately, ratchet autonomy as trust accumulates, and, in Roland's memorable distinction, build orchestras before factories, where an orchestra is a system that keeps a human conductor. The other camp says the dial has a stop. Geoffrey Litt of Notion called factories a depressing vision on X and argued, in a talk he has since [published as an essay](https://www.geoffreylitt.com/2026/07/02/understanding-is-the-new-bottleneck.html), that those who delegate understanding get replaced by the agent. Paul Bakaus [put it as flatly as it can be put](https://www.latent.space/p/skill-engineering-design): "There is no auto, and there will be no auto." His argument isn't only about quality; it's about ownership. People need purpose, and they want a role in what they create.

The closing debate, covered in *Latent Space*'s conference reporting, put both positions on one stage. Dex Horthy of HumanLayer took pains to say he isn't anti-loop, pointing out that Kubernetes is built on control loops, but deterministic ones. His worry is that enthusiasm has gotten ahead of the engineering, and his advice was to step down an abstraction level rather than up. Geoffrey took the other side and called loops inevitable. And Mike offered the most honest data point of all: Even inside Anthropic, the team running Tag reports being bottlenecked on reviews and on the human ability to conceptualize what the system is doing. The checkpoint humans kept for themselves is now the constraint.

Autonomy is a dial that exists separately on every one of the four loops. You can run a fully autonomous execution loop inside a heavily supervised product loop. You can hand the system loop to agents while keeping goal-setting entirely human. The interesting engineering question isn't "Which camp wins?"; it's "What information do you need to set each dial correctly?"

The table above is my attempt to fill in those blanks. Every loop, including the top one, has a nameable exit condition, and the top one is you. But naming a signal isn't the same as wiring it in. A loop without its signal doesn't converge. It just runs until something external stops it. Knowing whether your loops are actually closing, at production scale, means sweeping traces and clustering failures continuously instead of spot-checking transcripts, which is exactly the job [Arize AX](https://arize.com/) was built to do.

## Which one are you building?

Now the loops have names, that's the question to ask. The word loop is doing a lot of work this month, because this field loves nothing more than jumping on the next hot thing. But real practice underlies all four loops, and it's the same practice in each: people are dialing up their level of abstraction and pushing human judgment further up the stack. That's the actual lesson of loops. We get more done by climbing up the stack, and now you have a map, you know where you should climb.

---

*Capture note (not part of the source): the two diagram images and the four-loops comparison table are images on the original page and are noted inline above rather than transcribed. The closing paragraph contains a vendor plug for Arize AX (the author's sponsor/employer context); tracking parameters stripped from that link.*
