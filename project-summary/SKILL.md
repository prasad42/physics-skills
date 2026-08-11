---
name: project-summary
description: Interview the user about a research draft or note or codebase or project_summary.md to write or update project_summary.md — the current-state physics companion to RUNLOG.md.
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Interview me about a draft or note to build or refresh `project_summary.md`: the standing, present-tense statement of what's claimed and assumed right now, as opposed to `RUNLOG.md`'s chronological record of what was run and when. Where RUNLOG narrates *how something changed*, `project_summary.md` states *what's true now* — it gets overwritten in place, never appended to.

## 1. Locate the target

Check the repo for an existing `project_summary.md`. If found, this is an update: read it in full before anything else — you'll be revising it, not starting over. If none exists, this is a fresh build.

## 2. Silent extraction pass

Read the draft or note the user is sharing — this is the primary source. Map it onto:

- **Core question(s)** — what the work is actually trying to answer.
- **Claims** — every distinguishable claim, and its evidentiary status (proven analytically, numerically supported and at what scale/statistics, conjectured, in progress).
- **Model/Assumptions** — the framework definition and the assumptions load-bearing for the claims above.

Secondarily, skim `RUNLOG.md`'s (if it exists) recent entries (all the entries after the current `project_summary.md` date) and relevant source files — not the draft — for two narrower facts:

- **Data Validity** — datasets or conventions currently flagged invalid or superseded in RUNLOG (present tense: what not to use right now, not the story of how it broke).
- **Codebase Conventions** — module/class naming, data directory layout: the minimal facts a future session needs to not misname something.

Do this internally. Don't narrate the pass to the user.

## 3. Find the real gaps

Flag only what's genuinely unresolved:

- A claim stated without precision — undefined notation, unclear scope, conflated with another claim.
- A claim with no stated evidentiary status.
- An assumption that's load-bearing but never stated.
- A missing or internally inconsistent core question.
- A claim at risk of being over-read, with no scope disclaimer.

A claim already precise and scoped in the draft needs no question.

## 4. Interview

Ask one question at a time, ordered: core question → claims → model/assumptions. Fold risk/scope questions in under the claim they qualify, rather than as a separate pass.

For each question, give your recommended resolution and ask for confirmation rather than asking open-ended — you can usually infer the likely answer, and confirming is faster than composing:

> "Claim 2's $p_c$ estimate is numerically supported (N=8, four $(p,p_2)$ combos) but not yet extrapolated to $N\to\infty$ — mark it 'numerical, finite-size' rather than 'established'?"

Treat answers as authoritative. Only follow up if one creates a new gap or contradicts another part of the draft. Stop once the structural gaps are resolved, not once every section is maximally elaborated — "in progress" or "open" are acceptable final answers.

## 5. Write project_summary.md

Sections, in order: **Core Question(s)**, **Claims** (with evidentiary status per claim), **Model/Assumptions**, **Data Validity**, **Codebase Conventions**. The existing structure of previous file needs to be ripped apart and matched with the following structure. 

- Add today's date.
- Preserve the draft's own notation, terminology, and claim names — don't rename or renumber into a generic scheme.
- Introduce nothing beyond what the draft states or the interview confirmed.
- Mark anything left genuinely unresolved inline as `*(open — not yet resolved)*` rather than silently resolving it.
- Data Validity and Codebase Conventions stay short — facts only, no RUNLOG-style narrative of how something broke or got fixed.

No commentary beyond flagging any items still marked open.
