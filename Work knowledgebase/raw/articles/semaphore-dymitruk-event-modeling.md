---
source_url: https://semaphore.io/blog/adam-dymitruk-event-modeling
title: "Adam Dymitruk on How to Upgrade Your Toolbox with Event Modeling"
author: Darko Fabijan (Semaphore) — interview with Adam Dymitruk
publication: Semaphore (Semaphore Uncut, Episode 68)
published: 2022-08 (updated 2024-09-05)
retrieved: 2026-06-11
type: article
topic: event-modeling-methodology
capture: faithful full text (site nav/footer removed)
---

# Adam Dymitruk on How to Upgrade Your Toolbox with Event Modeling

Talk — Episode 68. Featuring Adam Dymitruk, CEO and founder of AdapTech.

Describing information systems is vital for software design. As a result, multiple tools have appeared over the years to optimize the process. In this way, event modeling is an evolution from traditional approaches. We asked Software Developer, CEO and founder of AdapTech Adam Dymitruk about event modeling and its relation with event sourcing, domain-driven design, and the Open/Closed Principle.

## Introduction

In this episode, we spoke with Software Developer Adam Dymitruk, CEO and founder of Adaptech Group and one of the people behind Event Modeling.

In software development, event modeling is a method for graphically representing a system by unfolding the actions that have brought it to its current state. Event modeling describes systems not by their current state, but through a timeline made of different steps known as events.

The detailed information about these events helps developers to grasp how to build a product, making event modeling perfect for specifying an event source system. Moreover, event modeling is also perfect for learning about a product since it provides information about how it was made.

Event modeling was born as an evolution from event storming.

> "We extended event storming to continue to be used as a set of a principle way of gathering requirements or at least getting scope initially and talking about what the user stories were going to be", Adam recalls.

He also understands that event **modeling helps create "a storyboard like a captured screencast of someone using the system you intend to build."**

In this way, developers can examine this storyboard and learn exactly what happens at each point in time.

Thanks to event modeling, Adam's software development company can offer its services based on a fixed price. The selling point is ensuring the project isn't either late, going over the budget, or delivered incomplete.

Thanks to the way events layout products, "by doing an event model showing how many state changes there are in the system, how many different projections there are in a system, would allow the granularity and visibility into why something costs X amount of money."

In this regard, Adam understands that event modeling has "reduced that next level of complexity in automating systems to be these easy to follow, formulaic ways of thinking of state." He believes that event modeling frees programmers from focusing on new frameworks as a way of reaching the new level since it

> "really help you to have a grounding in the integrity of your system so you have the confidence to continue, even though you might not be familiar with a new stack."

## Event modeling and domain-driven design

Domain-driven design (DDD) is a software development method that focuses on matching the code components with the domain of the business or application. DDD is used to optimize communication between domain experts and developers by identifying and unifying their language.

One of the strengths of DDD, according to Adam, is its capacity to "use subject matter experts in each area properly so that the terminology keeps consistent within each one". To represent DDD in event modeling, he recommends using

> "swim lanes that can be arranged to show separation between physical systems, separation between logical organizations of subsystems where they might have the same subject matter experts across, for example, inventory and invoicing."

## Event modeling and the Open Closed Principle

When designing a system, Adam regards the Open Closed Principle as one of the keys to speeding up production. This principle mandates that *software entities should be open for extension, but closed for modification*.

In other words, that code has to be open to meet new requirements, but not to an extent that its source code has to be modified. In this way, developers save time in working with the source code, keeping working with complex code to a minimum, and having the flexibility to add new features.

In Adam's words, "that allows us to also do a mix of technologies as we can treat each state transition almost with, if you're doing serverless, with a function written entirely in a different language."

When representing the Open Closed Principle, event sourcing helps maintain the state of the system, keeping a log of the new things and makes

> "it quite visible actually to not just programmers, but to, more importantly, business so that they understand how the information in their system evolves without getting distracted by the technicals".

## Event modeling and event sourcing

Event sourcing, for its part, is a design pattern based on storing the current state of data while relying on an append-only store (known as data stream) working as a backlog of the history of actions of that data. To compare it with traditional application design, which is based on "writing directly to the tables in a database underneath", Adam uses accounting as an analogy:

> "**instead of just changing some rows in the table, we're going to just keep adding events to some ledger that we can't change: We can only add things; Just like in accounting, no erasers are allowed**."

Event sourcing takes advantage of the storage capabilities of modern systems to save information about every action on the product. Since event sourcing keeps a register of the product events, developers have more information to audit it.

Besides, event sourcing can help as well to **"transform those events into the representation that you want"** by sharing vital information with the right people. Adam understands that in a traditional application "if you're going to change some data in one table, you have to be very careful to not adversely affect any of the other select statements and insert statements in the rest of the system."

In turn, in event sourcing, "**the only thing we're concerned about when we're changing state is putting one more event on the ledger and that's it**—We don't have to worry about the downhill effect."

With these tools, developers can create different views of those events and separate the data and the workflows important to you and isolate them from your colleague's work. In like manner, you can also learn what the work of somebody else on the code has been.

According to Adam, event modeling can be combined with event sourcing to provide

> "the blueprint to know the shape of the data and the workflows and what steps there are to get there, so you can have contracts between each workflow step in terms of what someone's work leaves behind on the ledger versus what someone is going to have in their projection of that for their screen."

## Common patterns that prevent companies from adopting event sourcing

Adam says that event sourcing isn't as much of a change for most tasks: "I would say that 80% of the actual work is still the same as dealing with some UI to display a model in a template in HTML."

He asserts that "the only thing that's added is the use of a ledger, which we use event store for, which is a database that's made specifically for being able to recall events in a guaranteed order that they were put in."

Therefore, when implementing event sourcing, it is utterly important to set up a good file storage and synchronization systems.

To familiarize with event sourcing, Adam also encourages incorporating **vertical slicing.** Vertical slicing stands apart from the traditional approach in which "people make every problem a brand new puzzle and it's very hard to figure out how to do something."

Instead, vertical slicing consists of breaking down functionalities by *slicing* their layers, hence "cutting through the UI, any of the architecture layers to see what it takes to get from point A to point B, across the one projection or storing one event as a result of someone pressing a button on the UI."

As procedures are stored thanks to event sourcing, newcomers can check out the event stored and mimic the steps taken by someone who previously did it:

> "They literally copy all of those things, rename the name of the event, rename the name of the screen, move things around, and they're up and running within an hour or two pushing to production if need be."

## The bottom line

You can follow Adam on his [LinkedIn](https://www.linkedin.com/in/eventmodeling/) and [Twitter](https://twitter.com/adymitruk). You can read Adam's original article on event modeling [here](https://eventmodeling.org/posts/what-is-event-modeling/). To learn more about domain-driven design topics (including event sourcing), he recommends searching on Youtube for a series of talks he has made on the topic. Lastly, you can also reach him at the company website, [AdaptechGroup.com](https://adaptechgroup.com).
