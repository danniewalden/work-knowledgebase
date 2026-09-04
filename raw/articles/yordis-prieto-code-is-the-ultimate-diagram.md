---
source_url: https://yordisprieto.com/writing/code-is-the-ultimate-diagram
title: "Code Is The Ultimate Diagram"
author: Yordis Prieto
publication: yordisprieto.com
published: 2026-07-02
retrieved: 2026-07-31
type: article
---

_Verbatim capture. Site nav, avatar, "stay in touch"/subscribe, and footer/license
stripped; author's words kept._

# Code Is The Ultimate Diagram 🗺️

My position on diagrams sounds like a contradiction. I draw them all the time. I also refuse to keep them.

Both habits come from the same place. Standing at a whiteboard with a few people and pulling a design out of nothing is great work. That part I will defend. What I want to push back on is the idea that the picture, once drawn, is the design. It isn't. The design is still happening.

## Diagrams Are For Discovery

When you draw a diagram, you are looking for the shape of the problem with the other person in the room. The picture is the artifact of that conversation. The arrows and the boxes are scaffolding around the understanding you build together. That understanding is the end. The diagram is the means, even when it works as a blueprint, because nothing ships from a picture. The software is the software.

This is when diagrams are worth the most. Early. Cheap. Throwaway. You and I in front of the same surface. We ask what happens when a payment fails, where the boundary sits, who owns the retry. The picture moves while we talk. It should. That is the whole point.

If you anchor on the diagram too soon, you stop discovering. You start defending the picture instead of interrogating the problem. So I draw, but I do not grip the drawing tight.

## Diagrams Decay

Here is the part nobody wants to say out loud. The moment someone writes the first line of code, the diagram starts to drift.

Not because anyone is sloppy. Because the design keeps happening. The discovery did not stop. It moved into the code. Every commit is a small decision. A name changes. A boundary moves. A retry gets added. A type gets split. The code is where the design now lives, and the code does not call you back to update the picture.

You can try to keep the diagram in sync. People build entire processes around it. Architecture reviews, weekly sync sessions, "please update the diagram before merging." It does not hold. It cannot hold. Everyone changes the code. Someone updates the diagram. The asymmetry compounds. After a quarter, the diagram is a polite fiction. After a year, it is misinformation.

A recent diagram is close to accurate. A six month old diagram is a story about a system that does not exist anymore.

## Code Is The Diagram

So flip the direction.

Stop trying to drag the code back to the picture. Let the picture come from the code. The code already knows. It knows which modules call which, which types flow where, which events get published. It knows which boundaries are real and which were aspirational and never enforced.

When I say code is the diagram, I don't mean code looks like a diagram. I mean code is the source, and every picture is a view of it. Every box, every arrow, every layer you would have drawn is already in there. If you want a fresh picture, regenerate it. If the picture and the code disagree, the code wins. Always. The code is the only thing that runs.

There is a catch. The flip only works if the picture is cheap to get back. Ask a team for a fresh diagram today. Someone loses a day digging through modules. They redraw by hand what the code already knows about itself. That is a tooling gap, not a law of nature.

That is why code is the ultimate diagram. The picture is downstream of the code. Flip that order and it becomes a tax, not a tool.

Draw the diagram. Use it. Throw it away. Then read the code.

Talk to you later 🐊 alligator.
