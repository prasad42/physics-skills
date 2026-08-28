---
name: paper-review
description: Explain a research paper at depth calibrated per-concept by user self-rating.
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---
If no paper is attached, ask the user to attach one before proceeding.
For every paper, generate a Markdown brief at `today's_date/Pub_date_YYYYMMDD_paper_brief_name_1stauthor_last_author.md`; use the arXiv submission date when no publication date is available.

**Step 1 — Keyword extraction**
Extract 5–10 keywords covering: (a) concepts central to the paper's contribution, and (b) heavy-machinery methods the paper depends on even if not novel. For each keyword, provide a one-line gloss.

Present as a table, one keyword per row. Column 1: Sr. No., column 2: keyword, column 3: One line gloss of the keyword, column 4: Expertise (N/L/E)

Before the table, state explicitly: "Rate every keyword as N (novice), L (learning), or E (expert) based on your expertise. Reply with the numbers, e.g. `1E 2N 3L ...` — all keywords must be rated before I proceed." Do not continue to Step 2 until a rating exists for every keyword; if any are missing, ask only for the unrated ones.

**Step 2 — Explanation**
Produce a single structured pass: Summary, Main Contribution (Novelty), Methods, Results, Assumptions, Approximations, Validity Regime, Limitations (Authors acknowledge / Not discussed).

Lead the pass with a concise **Main Concept** section that states the paper's central idea in plain language and connects the problem, method, and main conclusion. Include a **Key Equations** subsection with 3–4 equations central to the paper when equations are available. Render each equation as display LaTeX inside a `$$ ... $$` block; do not put equations in plain-text or code blocks. Define symbols immediately after each equation and cite the paper's equation number.

Include a **Main Plots** subsection with 3–4 central figures. Embed or link the paper's figures when available, identify each figure by number, and give a short interpretation that separates what is directly plotted from the authors' inference.

Depth per concept is determined by rating:
- **novice(N)** — motivation, intuition, analogy to user's known areas
- **learning(L)** — formalism, derivation, method mechanics
- **expert(E)** — terse; omit background

Depth varies inline within each section; the section structure is fixed regardless of ratings. If a novice- or learning-rated concept depends on an expert-rated one, add a single callout ("this builds on X") so the user can re-rate if needed — do not auto-expand X.

**Step 3**
Ask if the user wants a deep dive on any specific concept or section.

The review is complete only after the dated Markdown brief has been written with the required sections, legible equations, and interpreted key plots.
