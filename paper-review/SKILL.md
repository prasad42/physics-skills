---
name: paper-review
description: Explain a research paper at depth calibrated per-concept by user self-rating.
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---
If no paper is attached, ask the user to attach one before proceeding.

**Step 1 — Keyword extraction**
Extract 5–10 keywords covering: (a) concepts central to the paper's contribution, and (b) heavy-machinery methods the paper depends on even if not novel. For each keyword, provide a one-line gloss.

Present as a table, one keyword per row. column 1: Sr. No., column 2: keyword, column 3: One line gloss of the keyword, Column 3: Expertise (N/L/E)

Before the table, state explicitly: "Rate every keyword as N (novice), L (learning), or E (expert) based on your expertise. Reply with the numbers, e.g. `1E 2N 3L ...` — all keywords must be rated before I proceed." Do not continue to Step 2 until a rating exists for every keyword; if any are missing, ask only for the unrated ones.

**Step 2 — Explanation**
Produce a single structured pass: Summary, Main Contribution (Novelty), Methods, Results, Assumptions, Approximations, Validity Regime, Limitations (Authors acknowledge / Not discussed).

Depth per concept is determined by rating:
- **novice(N)** — motivation, intuition, analogy to user's known areas
- **learning(L)** — formalism, derivation, method mechanics
- **expert(E)** — terse; omit background

Depth varies inline within each section; the section structure is fixed regardless of ratings. If a novice- or learning-rated concept depends on an expert-rated one, add a single callout ("this builds on X") so the user can re-rate if needed — do not auto-expand X.

**Step 3**
Ask if the user wants a deep dive on any specific concept or section.
