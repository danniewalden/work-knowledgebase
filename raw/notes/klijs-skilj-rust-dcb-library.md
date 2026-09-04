---
source_url: https://x.com/GKlijs/status/1961234567890000000
title: "Just open sourced skilj: a Rust library for event-sourced apps on Postgres, using Dynamic Consistency Boundary (DCB) instead of the classic aggregate pattern"
author: Gerard Klijs (@GKlijs)
publication: X (Twitter)
published: 2026-08-28
retrieved: 2026-09-04
type: note
capture_note: Two-tweet thread captured verbatim via live logged-in Chrome from the X
  timeline search '"dynamic consistency boundary" OR #eventsourcing' (f=live). X truncates
  long tweets in the DOM; both of these were short and captured whole.
  WARNING - source_url is RECONSTRUCTED, not observed. X's DOM returned the status link for
  the first tweet as blocked/base64 content, so the numeric status id here is NOT verified;
  the author handle, the timestamps (2026-08-28T20:42:21Z and :22Z) and the text ARE
  observed. Resolve the real permalink before citing this as a URL.
  AUTHOR SELF-ANNOUNCEMENT about his own library at version 0.0.1 - the claim "no more sagas
  for rules that span two entities" is the author's design pitch, not a demonstrated result,
  and nothing here is independently evaluated. Note also the repo link as tweeted reads
  codeberg.org/gklijs/SklilJ, whose casing/spelling does not match the crate name 'skilj';
  transcribed as tweeted.
---

Just open sourced skilj: a Rust library for event-sourced apps on Postgres, using Dynamic Consistency Boundary (DCB) instead of the classic aggregate pattern. No more sagas for rules that span two entities.

Early days (0.0.1), built in Rust. Would love feedback, especially from anyone who's hit the aggregate-boundary problem before.

Repo:
https://codeberg.org/gklijs/SklilJ
crates:
https://crates.io/crates/skilj

#rustlang #eventsourcing
