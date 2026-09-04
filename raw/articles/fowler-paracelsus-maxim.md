---
source_url: https://martinfowler.com/bliki/ParacelsusMaxim.html
title: Paracelsus Maxim
author: Martin Fowler
publication: martinfowler.com
published: 2026-09-02
retrieved: 2026-09-04
type: article
---

# [Paracelsus Maxim](https://martinfowler.com/bliki/ParacelsusMaxim.html)

2 September 2026

[image: Photo of Martin Fowler]

[Martin Fowler](https://martinfowler.com/)

[dictionary](https://martinfowler.com/tags/dictionary.html)

**The difference between a medicine and a poison is dosage.**

Often we talk about certain habits, in programming or life, are good or
bad. But few things are simple binaries. Some vary with context: reading a
book is a good thing sitting in my garden, but not while driving my car. But
another variable is dosage: a little pain-killer salves my headache, but too
much will kill me.

The importance of dosage was noticed by a 16th century Swiss physician
called Paracelsus. His quote was originally in German “Alle Dinge sind Gift,
und nichts ist ohne Gift; allein die Dosis macht, dass ein Ding kein Gift
ist.” which ([according to Wikipedia](https://en.wikipedia.org/wiki/The_dose_makes_the_poison)) translates as “All things are poison, and nothing is without
poison; the dosage alone makes it so a thing is not a poison.” It's also known
as “The dose makes the poison” or if you prefer your sayings in Latin “dosis
sola facit venenum”.

In programming, global data is a good example of the Paracelsus Maxim (as I
like to call it). A little global data, especially when immutable, can be a
handy way of propagating information that may needed anywhere in a program,
but it quickly becomes dangerous if there is a lot of it about.

This kind of thing crops up in lots of places. So when thinking about when
things are good or bad, we should always ask “in what contexts” and “in what
doses”?
