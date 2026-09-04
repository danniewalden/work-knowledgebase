---
source_url: https://www.linkedin.com/pulse/how-does-dcb-affect-event-modeling-martin-dilger-u1mkf
title: How does DCB affect Event Modeling?
author: Martin Dilger
publication: LinkedIn ("Event Modeling applied" newsletter)
published: 2026-07-06
retrieved: 2026-07-06
type: article
---

# How does DCB affect Event Modeling?

*Martin Dilger — Helping Teams Navigating the Spec-Driven Development Process | Agentic Software Modeling on Eventmodelers.ai | Author "Understanding Eventsourcing" and "Spec Driven" — July 6, 2026*

One of the real innovations for me in Event Sourcing - not necessarily in terms of technology - but in terms of mindset has been DCB ( Dynamic Consistency Boundary ).

Instead of having to define up front how to structure events into streams ( typically using Aggregates ) - we technically treat all events within a bounded context as one global stream. That sounds counterintuitive in the beginning, but makes a lot of sense. Let´s dive in.

First benefit - this makes those cumbersome technical discussions go away immediately.

Where is the aggregate?
How to structure streams

Where are the boundaries?

Looking at the picture above, at some point in time we had to make a decision - "what belongs to Customer Management" - "What belongs to Course Subscriptions"

Latest when we move to production, this is often set in stone. But things change, Business Models change and some of those early decisions turn out to be wrong or at least not ideal.

That´s also why I refer to Aggregates as "Static Consistency Boundaries", changing those decisions later is not impossible, but typically a lot of work and typically nobody does that. We have to live with past decisions for better or worse typically.

## DCB changes the focus

With DCB we focus on "What actually happened?" - the whole big idea of Event Sourcing in general.

But one question has been bothering me - how will this affect Event Modeling? With Event Modeling - we reason about systems, not with engineers - no, with everybody. It´s a visual plan we build. A visual language.

Now that I modeled a few systems with DCB, I found my answer - it´s not affected at all. Quite the opposite, everything gets simpler.

Event Modeling has been surprisingly hesitant to change. Which shows how mature it is. Keeping things simple is the hardest thing to do.

Now we can show "what actually happened" - using one swimlane per system / bounded context.

And swimlanes become what they always were meant for - showing the interaction between systems and teams, not stream-design itself.

Payments for example - that´s a different system managed by a different team. So we show that using swimlanes. They become integration points. Whenever information crosses a lane, we need to pay attention, this is important.

## Micro-Decisions and Business Rules

It´s all about Consistency.

To execute the command "Subscribe to Course", the system needs to know which rules apply.

DCB has not changed that. Let´s make an example. Only registered customers can subscribe to a course. We discover those rules in collaboration and express them with Given / When / Then Scenarios.

Those scenarios can be expressed easily on the Eventmodelers-Plattform

Rule 1 - registered customers can subscribe to courses
Scenario 2 - needs to be registered to subscribe
Scenario 3 - cannot subscribe twice

Now to implement the business logic for a course registration, we need to know which information we need to decide whether a subscription is allowed or not.

How do we know?

It´s the Given / When / Thens that provide this information automatically. We just have to look at the GIVEN Part.

This is what I couldn´t wrap my head around in the beginning - how do we model the "Decision Model", the information the system needs to process a command. The answer that came up surprised me - we don´t... at least I don´t.

Aggregates or DCB - it has no effect on Event Modeling.

## The Context for Decisions

With Aggregates, it was quite simple.. to make a decision you had to load all the Events guarded by this one aggregate. Consistency across Aggregates required orchestrations, Saga Pattern or some steps to handle compensating transactions.. this becomes complicated quickly.

Those aggregates can become large over time.. and they can become performance bottle necks. That´s why we introduce some technical optimizations like Snapshotting - think of it like a cache for big aggregates.

With DCB, those decisions become much more granular. We basically just decide on a command by command basis, what needs to be done.

How that is done varies from Framework to Framework, from technology to technology. In the Axon-Framework for example, for each command handler you define a Criteria. Think of it like an SQL-Query to fetch all events necessary to decide, whether the command can be processed or not.

"Give me all the Events of type Customer Registered for the email, but also all the Events of SubscribedToCourse for this email and the course id, the customer wants to subscribe to.. so I can check whether a subscription is possible or not.."

Writing this by hand is cumbersome.

That´s why we typically generate this code directly from the specifications. AI is really good at that - and the Axon Build Kit for the Eventmodelers-Platform knows how to translate the Event Model to the executable Code.

You focus on the business - the Platform takes care of the rest. This especially pays off later, because rules change.. adding given / when / thens - will automatically be reflected in code.

Generating the Test Cases of course as well..

## Tags are indices, not domain concepts

How do you model Tags in the Event Model? Probably the question I hear most. You don´t.. Tags aren´t a domain concept, it´s not essential to the business.. it´s a technical optimization.

So there´s no place for it in the Event Model.

To be able to query a certain Event for a Decision in a command handler, it has to be tagged though. How do you express this so AI can generate that?

We use a publicly available and documented schema. This allows anyone to build Code Generators that can plug into the Eventmodelers-Plattform. And many tools and code generators already do. It has proven to work for years in countless projects.

We typically have 2 kinds of modeling sessions. Discovery and Detailed-Modeling.

In Discovery, there´s no place for technical details like Tags.. nobody cares. And stakeholders the least.

But later, we might want add those details to support Code Generation, often just with engineers before handing the slice to an Agent.

In the Eventmodelers-Plattform - you can add meta information to the schema of Events, Commands and Read Models.

One of them we used in the past was the "id"-attribute. In the UI, you can specificy for each attribute, whether it´s an identifiying attribute. In the Code-Generation, this can be used to identify the stream. Something like a "customer id" for example might be a good candidate.

For DCB, I just reuse this attribute for now. We might add a new attribute at some point in time named "indexed" - but I´m slow in changing the public schema - for now we just re-use the id-attribute.

In the UI you can see the id-attributes if you look for the '*

AI can figure this out by itself pretty well, but I typically want to have a little more control over that. If you use it or not - completely up to you.

In Code this becomes something like this.

With the attributes being tagged, they are now basically indexed and can be used in Command Handlers to make decisions.

## Conclusion

With DCB we can put more focus on the business domain itself. Within on context, just model "what happened".

Inter-Context Communication - use swimlanes to show how systems integrate / communicate. Showing "Integration", not "Implementation".

Use Event Modeling to plan, generate Code where possible. Use the Build-Kit for Axon for example.

Links:
- What is Event Modeling?
- Event Modelers Plattform
- Event Modeling Use Cases
- Building with AI
- Grab the book: https://leanpub.com/eventmodeling-and-eventsourcing
- And the accompanying Online Course
