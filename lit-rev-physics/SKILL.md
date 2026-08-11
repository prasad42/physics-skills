---
name: lit-rev-physics
description: Expertise-calibrated literature review of a physics subfield — grill, retrieve, synthesize.
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Produce a thematic literature review of a physics topic, calibrated to what the user already knows. Every bibliography entry must trace to a retrieved source; never cite from priors. Run the steps in order; each gate below blocks its successors.

**Step 1 — Map the user's field model (grill)**
Before any retrieval, interrogate the user's mental model of the subfield by invoking the `socratic-physics` skill: treat their picture as a DAG, ask one question at a time, offer your own provisional answer each time, resolve dependencies before dependents. Retarget the object — elicit, don't demolish. Draw out: which results they take as settled, which approaches they consider live vs. dead, what they believe the open problems are, which standard methods they trust and where they suspect those methods fail. Push on unstated scope, competing framings, and gaps in their map.
This does triple duty: it seeds sharper search queries than the bare topic, exposes the expertise axes that set synthesis depth, and gives the eventual gap analysis a target to confirm, correct, or extend.
*Completion:* the user's field map is explicit enough to name its main themes and their stated open problems. State when reached.

**Step 2 — Seed retrieval**
Search alphaXiv (primary) for the topic, using query terms sharpened by Step 1. Fall back to `web_search` for published-version metadata (PRX/PRL/DOI), non-arXiv venues, and pre-arXiv literature. Identify the most central hits.

**Step 3 — Snowball (one round)**
From the central hits, pull references and forward citations. Add only nodes central to the topic; discard peripheral drift.
*Completion:* one snowball round done and the central set has stabilized — a round adding zero new central nodes — or the round is exhausted.

**Step 4 — Corpus approval gate**
Present the candidate corpus as a table: author-year, title, why-central, seminal/recent. Ask the user to approve, prune, or request another snowball round. Do not proceed to Step 5 until the user approves the set.

**Step 5 — Keyword rating (corpus-grounded)**
From the approved corpus, extract 5–10 themes and heavy-machinery methods that actually dominate it — which may differ from the Step 1 priors. One-line gloss each. Present as a table: Sr. No. | theme | gloss | Expertise (N/L/E).
State: "Rate every theme as N (novice), L (learning), or E (expert). Reply e.g. `1E 2N 3L …` — all must be rated before I proceed." Do not continue until every theme is rated; ask only for the unrated ones.

**Step 6 — Synthesis**
Write `lit_review_<topic>.md`. Thematic organization (by physical question / competing approach), not chronological or paper-by-paper. Fixed skeleton:
- **Landscape** — the themes and how they relate.
- **Per-theme synthesis** — results, competing approaches, consensus vs. contested. Depth set by that theme's rating: **N** — motivation, intuition, method mechanics; **L** — formalism and derivation sketch; **E** — terse, frontier and open problems only, omit background. The skeleton is fixed regardless of ratings.
- **Open problems / gaps** — confront the Step 1 priors against the corpus: which held, which were wrong, which extend. This is the section that earns the grill.
- **Annotated bibliography** — table, every entry traced to a retrieved source, tagged seminal/recent, arXiv ID + DOI where retrieved.

Prose per journal style; APS-style inline citations `[Author, PRX 2025]`. Close with a BibTeX-ready reference block for direct drop into a `.bib`.
*Completion:* file written, every theme covered at its rated depth, every citation traceable.
