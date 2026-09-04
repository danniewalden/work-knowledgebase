---
source_url: https://ricofritzsche.me/why-the-entity-model-is-an-illusion/
title: Why the Entity Model Is an Illusion
author: Rico Fritzsche
publication: Rico Fritzsche (ricofritzsche.me)
published: 2026-08-26
retrieved: 2026-08-27
type: article
---

# Why the Entity Model Is an Illusion

*What Remains When You Model What Happens*

By [Rico Fritzsche](https://ricofritzsche.me/author/rico/) in [Software Engineering](https://ricofritzsche.me/tag/software-engineering/) — 26 Aug 2026

*[Image: "Why the Entity Model Is an Illusion" — photo by Randy Jacob on Unsplash, "man's reflection on body of water".]*

The field of enterprise software development is characterized by centralized data models and structures, object-oriented programming in the style of languages like C++, Java, and C#, bloated frameworks, relational databases, and, of course, a whole lot of unnecessary complexity. At first, this might sound like I'm just spouting off. But I come from this world and know the struggles it causes. And regardless of the possibilities for deploying AI agents, complexity—especially unnecessary complexity—is the main reason why software development remains cumbersome, slow, and expensive.

#### Conditioned to Central Data Models

In my day-to-day work, I still see how deeply developers, teams, and often even business experts are conditioned to think in terms of central data models. It seems that the prevailing belief is that once we've stored the data in a normalized database, the problem is largely solved. But is that really the case?

I am now firmly convinced, more than ever before, that for years we've been laboring under the fallacy that we must model objects that represent the real world, endow them with properties and behavior, and make them capable of changing on their own. Trapped in this way of thinking, we often forget that things happen and that business processes consist of more than just an input form. Things that happen often have an impact on various other things, without the events themselves having any idea what they're causing.

I don't think we need entities that we have to define in advance. That limits us too much. It makes systems rigid and inflexible. We can't just start with the knowledge we have and use real feedback to see if we're building the right thing. The standard software development process is still, to this day, a process based on assumptions. And the longer the process takes, the more the product deviates from reality.

#### Two Worlds

And it doesn't help much if the customer can only test the system with test data. Why? Because they don't care whether it works with test data. I've seen this happen too often: the bugs weren't noticed until the system went into production and was handling real data. That's because business people think differently and see value in their data and workflows.

Software developers live in a different world. They want to apply patterns, use new technology, and write beautiful code. But if the system follows SOLID and the Hexagonal Architecture, then it must be good.

That's the point! It doesn't matter which patterns are used. Added value must be created. And when two worlds collide—worlds with completely different worldviews that exchange Jira tickets for months on end—the disconnect can only grow over time.

Okay, what am I getting at? We need fewer dependencies at various levels. Thinking in terms of flows, processes, and events is a central element. The real world consists of events that occur somewhere and at some point; their consequences are unknown to the event itself.

#### What Actually Happens

Let's say we want to build a system for managing and renting vehicles. We can discuss many things with the business experts here, but we don't need to know everything to start building the product. The core idea is to deliver capabilities in small, independent steps and receive immediate feedback.

Perhaps we'll first talk with the domain expert about adding new vehicles. At this stage, we need to avoid using data-processing terminology. Of course, I know from experience that you'll often end up in contact with the IT people, who naturally already think they know that this needs to be stored in the "Vehicle" table and has already prepared a data model. That's counterproductive because it immediately takes you into the "how" phase.

It often takes a lot of effort to make it clear at this stage that it doesn't matter how the data is persisted. We're mapping processes, not a central data model. To have a finished data model, we'd need to know every aspect—which is rarely the case. And we'd also have to anticipate things that aren't even relevant right now. This limits flexibility, even for future changes.

So the correct question are: What does the initial registration of a new vehicle look like? What actually happens there?

Here, you'll quickly realize that it's not "Create Vehicle", because that merely describes a database operation anyway. After all, the car rental company doesn't actually "create" a vehicle. Perhaps if you set aside all these typical data-processing terms, you'll come to understand the real process.

Presumably, the registration of a new vehicle turns out to be a sequence of domain events:

```plaintext
VehicleAcquired → VehicleReceived → VehicleInfleeted → VehicleReleasedForRental
```

With each event, the system is enriched with new information.

#### The Vehicle Is a Projection

Now one might ask, but what exactly is the "Vehicle"? From my current perspective, it is not an entity in our software. It is something that can appear in different forms as a projection.

And that's very simple. Because perhaps someone in the company asks for a view of the system where all received vehicles should be listed. In that case, there is a "Received Vehicles" projection with the relevant data.

This perspective on software development has significant implications. We don't need to know how information should be evaluated or displayed. We can address that when it's requested. We can focus on a single capability, implement it in a targeted manner, and then immediately gather user feedback.

A domain capability is something like "AcquireVehicle" or "ReceiveVehicle." They are independent of one another. They are autonomous, self-contained, and coherent. They share only the Application State—in this implementation, an Event Store and the event definitions. However, they know nothing about each other.

But how do we know which processes belong together? Let's say we start by implementing "Acquire Vehicle," and when the vehicle arrives, we need a mapping—a reference to the vehicle that was ordered. Well, that's quite easy to solve. The reference can be an artificial identifier, such as an ID, or an immutable, unique, natural attribute. For a vehicle, this could be the so-called VIN.

```plaintext
{
    "eventType": "VehicleAcquired",
    "vehicleId": "VEH-1042",
    "occurredAt": "2026-08-20T10:15:00Z",
    "data": {
      "vin": "WVWZZZCDZRW123456",
      "acquisitionType": "Lease",
      "vehicleModel": "Volkswagen Golf"
    }
  }
```

In my opinion, the existence of a unique identifier does not automatically constitute an entity in the sense of a specific data object. The vehicle itself is an entity because it physically exists. In our domain, it is a reference. From the events associated with the reference, one can deduce the state that possibly describes the physical entity at a specific point in time.

#### Conclusion

As we can see, data structuring remains important—but in a different way. Data is immutable and can only be superseded by a new version.

The key point is that retrieving entities from a database to mutate them in memory and then write them back is an ineffective approach because it costs us two things:

1) It destroys the information about what happened,

2) it turns every concurrent request into a conflict we have to defend against.

So why do I say the entity is an illusion?

The database contains one row for each vehicle. The row resembles the vehicle itself, and is actually only the result of the last write. It holds the values that survived the last update and says nothing about how they got there. The reason why almost every system has audit tables, history tables, status columns, timestamps and change logs is a workaround to keep this information.

What matters is the connection to the real world, which is established through an artificial or natural reference. Against that reference we record what happened. Within a domain, there are different interests, which is why perspectives on a "thing" vary and there isn't just one "right" way. To stick with the example of a vehicle, it's simply a different matter from the perspective of purchasing versus that of the repair shop. Every form that someone needs is derived from these events. It is a projection.

*Cheers*!
