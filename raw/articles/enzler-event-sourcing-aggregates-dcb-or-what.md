---
source_url: https://www.planetgeek.ch/2026/06/23/event-sourcing-aggregates-dynamic-consistency-boundaries-or-what/
title: "Event Sourcing: Aggregates, Dynamic Consistency Boundaries, or what?"
author: Urs Enzler
publication: planetgeek.ch
published: 2026-06-23
retrieved: 2026-07-02
type: article
---

In part eleven of this series on event sourcing, we make a small detour to discuss consistency boundaries. I never thought much about this aspect until recently, when I watched a couple of conference talks that all made a big fuss about domain-driven design’s aggregates, and had a discussion with Sara Pellegrini about dynamic consistency boundaries.

This post is less about the resulting solution we have and more about the reasoning that led to it (and that might lead to another solution in your context).

When designing a system, I start with the real problems at hand, not by applying so-called best practices widely in the hope that they will solve our specific problems well. So what problems are relevant to today’s topic?

## Why consistency matters

We should try never to show incorrect data to users. Often, it’s okay to show stale data – because the system couldn’t update it yet – but wrong data is clearly bad. Why do I think of LLMs now?🤔
This is typically called eventual consistency. The data will be consistent again shortly.

Consistency ensures that everyone sees the same truth. Without it, systems or users make wrong decisions.

An example: When a student registers for a course, the software may need to check that the course isn’t overbooked and that the student doesn’t have too many courses. So, we need to check both conditions before registering a student, and after successful registration or registration denial, both invariants need to hold again. Whether I query the student and their courses or a course and its registered students shouldn’t matter. In both cases, the data should remain consistent, even when querying it while the registration is being executed.

There exist two common solutions to this problem. The widely known aggregates from Domain Driven Design, and the less-known Dynamic Consistency Boundaries.

## Aggregates

In domain-driven design, aggregates are used to guarantee consistency. Everything that must change together atomically must be in the same aggregate. Therefore, any change to a set of entities that must remain consistent must be made by calling a method on the aggregate that guarantees that, when the method is executed, everything is again consistent.

Having to define aggregates for everything that needs consistency can quickly lead to overly large aggregates in more complicated systems, because anything that needs to be changed consistently must go into a single aggregate.
That is not an absolute truth, IMHO, but it reflects how I understood the DDD literature.

## Dynamic Consistency Boundaries

As described on the website:

> Dynamic Consistency Boundary (DCB) is a technique for enforcing consistency in event-driven systems without relying on rigid transactional boundaries.
>
> Traditional systems use strict constraints to maintain immediate consistency, while event-driven architectures embrace eventual consistency for scalability and resilience. However, this flexibility raises challenges in defining where and how consistency should be enforced.

I wait here until you have read how DCBs work on their website: https://dcb.events/#what-is-it
Yes, I stole the example from there – to lower your cognitive load 😉

DCBs are a powerful, but quite complicated. So, if possible, I prefer simpler solutions.

## Why we never cared

As I wrote in the intro, we never had a discussion in the team about aggregates or dynamic consistency boundaries (the term wasn’t even invented when we started working on our product). So, I wondered why this was never a topic (because we like to discuss architectural things).

We solve problems when they arise, not earlier, and surely we don’t “solve” problems we don’t have.

After looking at our architecture and the design decisions we made, it is clear that we solve the consistency problem, but differently.

## First, another question – concurrent changes of what?

As I wrote in an earlier post on this series, for most data in our system, there are no concurrent changes. Typically, an employee enters their data into the system. At the end of a month, the data is checked and maybe corrected by an HR person or a team lead. Or an HR person configures the system, or makes a change to the organisational chart. It is very unlikely that the same data is concurrently changed by different users so that the commands would overlap. Two commands would have to be executed within a couple of milliseconds.

Furthermore, we mitigate the risk by having “small data” and a task-based UI. Small data means we do not have big things (things = what we project from events). We split things up into smaller things, with smaller event streams. Task-based UI means that we have a command for every task a user (or service) can execute in our system. A task contains only the exact data needed for that task, nothing more. So we don’t load a big entity from storage, change something, and then get a conflict while storing the loaded data (which we may have only partially updated). Yes, no unit-of-work pattern in our code.
So collisions are even less likely with our approach.

We also need to clarify what “the same data” even means in our context, as well as when it actually is a problem. We have a potential conflict when two people change something that would violate an invariant – too many students in a course or too many courses for a student. Please keep in mind that even when two users change the same data, it’s often totally okay because we can just apply both changes:

Two changes to an employee’s name: we just take whichever change wins, since the changes are the same change done twice (unless a typo is involved).
Two changes that both make sense: changing an employee’s name and their address. These two changes do not have a conflict.

We can potentially only have a problem when we violate consistency.

## Solving concurrent consistency issues with non-concurrent designs, not aggregates or DCBs

Let’s take another look at the example of student registration for courses.
Fun fact, I actually implemented a system for a school where students could register for courses, so I think I know what I’m writing about – just saying.

Instead of allowing students to register for courses directly, which introduces concurrency and consistency issues, students can enter their intent to register for a course (a draft registration). After a draft registration phase, a single-threaded algorithm processes all draft registrations. This way, we can also prioritise certain students (e.g., those in their likely last year of studies, so they can fulfil the requirements to complete their studies). Or students can choose among multiple course schedules that the algorithm can pick from. So we eliminated the concurrency aspect of this problem – and even found a better overall solution. Finally, we need to inform the student of which courses they were enrolled in.

In general, we replace a concurrent design with a non-concurrent one to eliminate consistency issues. All rules still need to be checked, but we are sure that there are no race conditions.

Is this always possible? Probably not. But if it works, the solution is much simpler than ever-growing aggregates or dealing with dynamic consistency boundaries.

## A mostly conceptual deep dive

Let’s look at the command that deletes a manual activity in our system. A manual activity is a data entry that states that an employee worked on a specific task for a specific amount of time, and the entry was entered directly by a user – it was not calculated from other data.

First, the command tries to load the activity to be deleted. If it can’t be found, an error is returned.

Second, we authorise the user to execute this command on that activity. If validation fails, we return an error.

Third, we create the new event that we later store.

Then, we instruct the operation runner to log the command. As explained in an earlier post, the operation runner handles logging, auditing, and error recovery/compensation. The important part for today is the OperationRunner.handleChangedWorkday function.

When a workday changes, we need to calculate some dependent data and validate that the data fulfils all configured rules (e.g., no blocking-time violations, sufficient breaks, a limited maximum number of work hours, etc.). Since multiple commands can affect a workday, consistency is important. Therefore, we don’t validate the workday directly in the request, but instead put a message on the service bus indicating that the workday needs validation. Then a message handler consumes the message and validates the workday. Azure Service Bus supports the concept of sessions. Given sessions, the service bus guarantees that it will always execute maximally one message per session. So we can use sessions to serialise the validation of an employee’s workdays by putting the tenant-ID, employee-ID, and workday date into the session-ID. Therefore, no concurrency is possible within the consistency boundary of an employee’s workday. A quite simple solution to an otherwise complicated problem.

The service bus solves some additional issues for us:

We can schedule messages into the future: we don’t want to show violations immediately since the user might still be entering data. So we give the user a 5-minute grace period by scheduling validation messages 5 minutes into the future.
If a validation fails, we receive dead-letter messages that we can use to debug the system and reschedule to verify the fix. Luckily, we don’t need this often.
If the system is under heavy load, we can suspend the service bus queue to improve responsiveness. Once the load is back to normal, we can resume message consumption, and the violations will appear.

I think this is a good example of how we try to solve the architectural and design problems in a holistic way – not one problem isolated from the rest – to get the simplest overall solution possible.

_Tags: Event Sourcing, F#_
