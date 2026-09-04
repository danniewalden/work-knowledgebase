---
source_url: https://www.linkedin.com/feed/update/urn:li:activity:7498452358599786496/
title: "I am more convinced than ever that... we must model objects that represent the real world"
author: Rico Fritzsche
publication: LinkedIn
published: 2026-08-28
retrieved: 2026-09-04
type: note
capture_note: LinkedIn post captured verbatim via live logged-in Chrome (the headless
  scheduled watch cannot render this feed). Author's own wording; only edit is collapsing
  LinkedIn's rendered 'hashtag\n#x' markup back to '#x'. Date derived from the relative age
  stamp at retrieval (2026-09-04 11:08 UTC), so accurate to the day, not the hour.
  source_url is the canonical per-post permalink, not the recent-activity feed.
  Companion post to his article "Why the Entity Model Is an Illusion" (already captured at
  raw/articles/fritzsche-why-the-entity-model-is-an-illusion.md). PRACTITIONER POSITION,
  with the vehicle-rental worked example as illustration, not evidence.
---

I am more convinced than ever that, for years, we have been laboring under the misconception that we must model objects that represent the real world.

Trapped in this way of thinking, we often forget that things happen and that business processes consist of more than just an input form to store data in a table.

I don't think we need entities that we have to define in advance. To have a finished data model, we'd need to know every aspect - which is rarely the case.

Let's say we want to build a system for managing and renting vehicles. The correct question is: What does the initial registration of a new vehicle look like? What actually happens there?

Here, you'll quickly realize that it's not "CreateVehicle", because that merely describes a database operation anyway. After all, the car rental company doesn't actually "create" a vehicle.

The registration of a new vehicle turns out to be a sequence of domain events:

VehicleAcquired -> VehicleReceived -> VehicleInfleeted -> VehicleReleasedForRental

Now one might ask, but what exactly is the "Vehicle"? From my current perspective, it is not an entity in our system. It is something that can appear in different forms as a projection.

In the entity-centric approach the database contains one row for each vehicle. The row resembles the vehicle itself, and is actually only the result of the last write. It holds the values that survived the last update and says nothing about how they got there.

The vehicle physically exists, but in our system we only hold a reference. Every form that someone needs is derived from these events.

In my latest article I discuss why the entity we think we are storing is an illusion.

Full article: https://lnkd.in/eD2uyvCP
