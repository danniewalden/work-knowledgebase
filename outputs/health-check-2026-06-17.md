# Wiki Health Check — 2026-06-17

Lint pass over the Work-knowledgebase wiki (per the Lint workflow in `CLAUDE.md`).
Scope: structural integrity, contradictions, stale claims, orphans, missing concept pages,
missing cross-references, and gaps worth filling next.

**Corpus:** 56 source pages · 43 entities · 52 concepts (+ index/overview/log).

> **Tooling caveat:** the Linux shell mount was serving *stale/partial copies* of several files
> during this pass (`watch-config.json` frozen at 9.7 KB; `index.md` truncated before the Concepts
> section; `agent-legibility.md` and `martin-dilger.md` missing some of today's edits). Structural
> findings below are taken from the **authoritative file-tool layer** and from the clean full-link
> scan run earlier today when files were fresh — not from the stale shell view. Items marked
> *(re-verify)* should be re-run once the shell mount catches up.

---

## 1. Structural integrity — PASS

- **Dangling wikilinks: 0.** The full-wiki scan (run when files were fresh) resolved every
  `[[link]]` to an existing page; today's new slugs all resolve. No edits since added links to
  non-existent pages (all new targets have pages).
- **Orphan pages: 0.** Every page has at least one inbound cross-reference beyond the catalogs.
  - *False positive to ignore:* a stale-mount run flagged `dilger-adding-perspectives-to-event-modeling`
    as "index/overview only" — the authoritative `martin-dilger` entity links it in both a bullet and
    the source-list footer. Not an orphan.
- **Raw provenance: intact.** Every `wiki/sources/*` page points at an existing `raw/` file.
- **Index completeness:** the authoritative `index.md` lists every page (the shell's "33 concepts
  missing" result is an artifact of a truncated mount copy). *(re-verify once mount is fresh)*

## 2. Contradictions — none material

- **"Keep aggregates small" (Atomic Object) vs. "kill the aggregate" (DCB).** Surfaced *as a
  framed counterpoint* on `event-sourcing`, not silently reconciled — consistent with the schema's
  "say so when sources conflict" rule. Good as-is.
- **"No worked multi-agent event model exists" (event-modeled-agent-design / overview).** Still
  accurate as written: it distinguishes *no independently-published* worked model from the KB's own
  in-house ones (`outputs/worked-event-model-*`). Internally consistent.

## 3. Stale claims / housekeeping

- **`watch-config.json` `candidate_primaries` — one is now satisfied.** "CodeScene peer-reviewed
  defect-risk study" was fulfilled on 2026-06-16 by ingesting the Borg/Tornhill FORGE-2026 paper
  (`raw/papers/borg-tornhill-code-for-machines-not-just-humans`). Recommend removing it from
  `candidate_primaries` (or marking it captured). The "Simon Wardley primary" entry is *partially*
  satisfied (Value Chains + Evolution filed) — narrow it to the still-wanted chapters.
- **Podcast cadence:** `eventmodeling.org` podcast tops at Ep. 46 (April); fine, just noting the
  feed has been quiet for the weekly watch.

## 4. Concepts mentioned but lacking their own page (candidates)

These appear in prose (not as dangling links, so no breakage) and may deserve promotion to concept
pages as the thread matures:

- **`ai-readable-code`** — used as a tag/term across `tornhill-clear-design-principles-agentic-age`
  and `agent-legibility`. Currently folded into `agent-legibility`; could become its own hub if more
  sources land. *Lowest-effort fix: keep as an alias of agent-legibility.*
- **`balanced-coupling`** — Khononov's named model (strength × distance × volatility), referenced in
  `vlad-khononov`, `business-capabilities`, and `agent-legibility`. Strong candidate for its own
  concept page once a primary (his book / a definitive article) is captured.
- **`behavior-driven-development` (BDD)** — invoked in the Dilger Agent Harness (GWT as the BDD
  feedback backbone). Minor; currently adequate under `event-modeling` / GWT discussion.

## 5. Missing cross-references (quick wins)

- `dynamic-consistency-boundaries` → add the **Atomic Object** "keep aggregates small / async
  projections" counterpoint (currently noted only on `event-sourcing` + `cqrs`).
- `ulrich-homann` ↔ `vlad-khononov` — both are the theory spine under `business-capabilities`
  (capability black-box + Balanced Coupling); cross-link them.
- `tornhill-clear-design-principles-agentic-age` ↔ `locality-of-reference` — CLEAR's "L" and "R"
  are locality; ensure the link is bidirectional.

## 6. Thin / stub pages to grow or retire

- **`yordis-prieto`** — still a stub (named by Dymitruk, no source captured). Either capture a
  Prieto source or leave flagged.
- **`dilger-hold-my-beer-engineer`** — teaser stub; superseded in substance by the richer Dilger
  posts now ingested. Consider folding/retiring.
- **`daniel-event-modeling-wardley-mapping`** — content limited by the unobtainable YouTube
  transcript; still the best available, leave as-is with the note.

## 7. Gaps a web search / next ingest could fill

- An **independently-published, worked multi-agent Event Model** (the standing open edge of
  `event-modeled-agent-design`).
- **Tornhill CLEAR follow-ups** — the "AR" posts (Avoid search luck, Reduce the edit surface) and the
  promised deeper "C" guidance, once published, complete the framework.
- A **Balanced Coupling primary** (Khononov's book or a definitive article) to ground the model
  beyond the "Golden Age of Modularity" opinion post.
- The **Dilger "Adding Perspectives" / Architect-Perspective → C4-from-the-model** follow-up if it
  ships — would strengthen the model-as-single-source claim.
- Remaining **Wardley** chapters (doctrine/gameplay/PST) and a BIZBOK-level capability-map treatment.

## 8. Suggested questions to investigate next

- Does the "spec is the source of truth, code is disposable" claim hold up against any *independent*
  production case (vs. practitioner assertion)? — the inverse of the Faros numbers.
- How does Khononov's Balanced Coupling (strength × distance × volatility) map onto the DCB / VSA /
  capability boundary debates already in the KB? A synthesis page could connect Thread 6's coupling
  voices (Homann, Goeleven, Fritzsche, Bogard, Khononov).
- Is there an emerging consensus definition of "AI-readable code" across Tornhill (CLEAR),
  Fritzsche (FC/IS), Miller (codebase-is-the-prompt), and OpenAI (legibility)? Worth a synthesis hub.

---

### Verdict

The wiki is **structurally healthy** — no dangling links, no orphans, complete index, intact raw
provenance. No contradictions beyond one explicitly-framed counterpoint. The actionable items are
small: trim one satisfied `candidate_primaries` entry, add ~3 cross-references, and decide whether
`balanced-coupling` / `ai-readable-code` graduate to their own concept pages as the design-for-agents
thread keeps growing.
