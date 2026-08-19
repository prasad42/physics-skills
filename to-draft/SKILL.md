---
name: to-draft
description: Prepare a proposal-led, evidence-backed handoff for creating or updating a scientific draft.
argument-hint: "[draft path, new-draft destination, or intended draft task]"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Prepare a self-contained handoff after substantial work in a scientific codebase. The handoff is both an evidence-backed patch specification for a draft-writing agent and a human-readable editorial task list. Inspect and reconcile the proposal, draft, notes, runlogs, tests, artifacts, code, Git state, and primary literature; then grill the user on publication decisions before writing anything.

This workflow is read-only except for the two outputs explicitly allowed below:

- Create `notes/proposal.md` only when no proposal exists and the user approves the complete proposed text.
- Create one final handoff under `notes/draft-handoffs/` after the user confirms the complete editorial decision recap.

The external draft workspace is always read-only. Treat missing verification as a limitation or task, not permission to run Python, simulations, tests, analyses, figure generation, draft compilation, or source-repository edits.

## 1. Establish the workspaces

Read every applicable `AGENTS.md` from the source repository hierarchy before inspecting scientific content. Identify the source repository root and record:

- Absolute path.
- Creation time with timezone.
- Full and short `HEAD`, commit date, and subject.
- Exact `git status --short` output.

Resolve the draft mode before it becomes a dependency:

- If the user supplied a readable draft path, use update mode.
- If the user supplied an unreadable path, ask for a corrected or mounted path.
- If no draft path was supplied, ask whether to prepare a new draft at a named destination or update an existing draft at a readable path.

For an existing draft, read its source and bibliography inputs. If it is in a Git repository, record that repository's absolute path, `HEAD`, commit metadata, and dirty state. For new-draft mode, record the intended destination and target format. Write nothing there.

Completion: source provenance and one unambiguous draft mode are established.

## 2. Establish scientific intent

Search `notes/` case-insensitively for exactly named proposal files in Markdown, TeX, or PDF form, such as `proposal.md`, `Proposal.tex`, or `Proposal.pdf`.

- If exactly one proposal exists, read it as the authoritative statement of scientific intent and direction.
- If multiple proposals exist, ask the user to select the authoritative one.
- Keep an existing proposal read-only. If it no longer reflects the user's intent, ask whether proposal revision should occur separately before this workflow continues.
- Do not use `project_summary.md` as a current-state authority.

If no proposal exists, bootstrap one through this gated branch:

1. Extract a provisional scientific proposal from `project_summary.md` when available, then the draft, README, relevant runlogs, notes, and repository evidence. These are seeds, not authority.
2. Perform a preliminary primary-literature audit sufficient to test the proposed motivation, gap, and novelty. Retrieve sources; do not cite from memory.
3. Load the `grilling` skill and interview the user about scientific intent, claim policy, scope, target audience or venue, and deliverables. Work the full design-tree frontier in rounds.
4. Present the complete proposed document and request explicit confirmation.
5. After confirmation, create `notes/proposal.md` with: motivation and context; research gap; questions and hypotheses; intended claims and evidentiary thresholds; model and assumptions; observables and methods; intended analyses; expected interpretations and conditional outcomes; draft scope and target audience or venue; planned figures and tables; literature anchors; exclusions and deferred work.
6. Restart the normal reconciliation using the approved proposal.

If the user declines, requests revisions, or withholds proposal confirmation, remain read-only and continue the proposal grilling only when the user is ready.

Existing proposals retain their format. A generated proposal is Markdown because it is searchable, diffable, and directly consumable by agents.

Completion: one authoritative proposal exists and every intended claim, scope boundary, and target deliverable can be enumerated.

## 3. Build the evidence map

Inventory every file under `notes/`. Always read the proposal and read every note materially connected to a proposal claim, draft claim, runlog result, analytical issue, editorial decision, or literature question. Classify notes by role rather than trusting their directory:

- Analytical derivations must expose assumptions and trace to supporting calculations where applicable.
- Numerical claims must trace to runlogs, immutable tests, data, or artifacts.
- Literature claims must trace to retrieved primary papers.
- Meeting notes carry author intent, subject to the current grilling.
- Previous draft handoffs carry earlier editorial decisions and unfinished tasks; revalidate their scientific conclusions against current evidence.
- Untraceable claims remain explicitly unverified.

Read the repository's runlog index and lifecycle rules first. For every proposal claim and every relevant draft claim, follow claim-led provenance through all material finished, active, planned, and deprecated goals:

- Finished goals supply completed conclusions.
- Active evidence is provisional.
- Planned goals establish unresolved dependencies, not results.
- Deprecated goals establish invalidity, supersession, or provenance, not current support.

Follow each relevant goal into its linked immutable tests, scripts, result files, figures, data manifests, commits, and code. Inspect existing images and PDFs when their visual content affects publication suitability. Read code only where needed to verify implementation facts, conventions, or artifact generation. Inventory first, then read relevant material deeply; do not substitute a broad historical summary for claim-level provenance.

Use this authority order when sources conflict:

1. User decisions from the current grilling.
2. Reproducible immutable tests and artifacts.
3. Finished runlog conclusions.
4. Active runlog evidence, marked provisional.
5. Current code and manifests for implementation facts.
6. Verified analytical and literature notes.
7. Proposal for scientific intent.
8. Existing draft for text requiring reconciliation.
9. Historical handoffs and `project_summary.md`.

File dates alone do not settle scientific conflicts. Resolve conflicts from primary evidence where possible and reserve unresolved interpretations for the grilling.

Classify each claim as one of: **Established analytically**, **Numerically supported**, **Preliminary**, **Inconclusive**, **Superseded/invalid**, **Planned but unexecuted**, **Editorial decision**, or **Open interpretation**.

Completion: every proposal claim and relevant draft claim has a status, strongest available evidence, caveats, contradictions, and unresolved publication decisions.

## 4. Audit the literature

Before editorial grilling, perform a focused literature audit for the claims identified above. This is a draft-facing audit, not a general thematic review.

1. Read relevant repository literature notes and follow their citations to retrieved primary papers.
2. For every literature-dependent claim, check direct precedents, seminal context, recent competing results, and novelty or priority risk.
3. Check freshness. Search externally when repository coverage is missing, stale relative to the handoff, or used to assert novelty or priority.
4. Verify bibliographic metadata, record a stable DOI or URL and retrieval date, and separate what each source supports from what it does not support.
5. Identify citations already present in the draft and BibTeX entries that the patch specification should add.

Keep the audit in the final handoff rather than creating a separate literature note. Every citation must trace to a retrieved source; flag an unresolved literature gap instead of filling it from memory.

Completion: every literature-dependent included claim has traceable primary support or an explicit unresolved gap, and novelty language has been tested against the retrieved corpus.

## 5. Grill publication decisions

Load the `grilling` skill and work the design tree in rounds. Ask only genuine publication decisions and unresolved conflicts; do not ask the user for facts available from the workspaces or literature. Give a recommended answer with every question.

Settle, where relevant:

- Include, omit, defer, or future work.
- Main text, appendix, supplement, or discussion-only placement.
- Exact evidentiary strength, scope, and caveat.
- Relationship to current draft wording and structure.
- Figure and table selection, assembly, generation task, or omission.
- Analytical interpretation and literature framing.
- Treatment of inconclusive, superseded, invalid, active, or dirty evidence.
- Conflicts among proposal, draft, notes, runlogs, tests, artifacts, code, and literature.

The user may resolve a missing analysis by omission, caveat, or future-work treatment. Record source-repository work separately from draft work; the receiving draft agent receives no implied authority to execute it.

When the frontier is empty, present a complete recap of all editorial decisions, open items, and assumptions. Request explicit confirmation that shared understanding is complete. Do not write the handoff before confirmation. If the user declines, requests revisions, or withholds confirmation, remain read-only, report the blocked gate, and continue the grilling only when the user is ready.

Completion: every claim and deliverable has a publication disposition, every resolvable conflict is settled, and the user has confirmed the complete recap.

## 6. Write the handoff

Create `notes/draft-handoffs/` if needed. Write exactly one self-contained file named:

`YYYYMMDD-HHMM-<source-short-sha>-<slug>.md`

Derive a short filesystem-safe slug from the confirmed draft task. Never overwrite an existing handoff; if the name already exists, append the next unused numeric suffix such as `-2`. Use repository-relative paths for source artifacts and record the absolute source repository path once in provenance. Include the external draft's absolute path because it belongs to another workspace.

Use this structure:

1. **Title and provenance**: creation timestamp with timezone; source repository path; full and short commit; commit date and subject; exact dirty state; proposal path and content hash; draft path or destination; draft Git stamp when available. Mark dirty and untracked evidence provisional.
2. **Receiving task and boundaries**: the exact draft objective, allowed workspace, and read/write boundary.
3. **Prioritized checklist**: flat Markdown checkboxes tagged `[AUTHOR]`, `[DRAFT]`, `[SOURCE]`, `[VERIFY]`, or `[BLOCKED]`. State dependencies and acceptance criteria.
4. **Executive editorial decisions**: concise confirmed outcomes.
5. **Claim ledger**: for every proposal and relevant draft claim, give disposition, draft destination, evidence class, exact scoped wording guidance, strongest repository evidence, literature support, caveats, and conflicts.
6. **Literature and novelty audit**: claim-to-source table stating what each primary source supports, what it does not support, whether the draft already cites it, its stable DOI or URL, and retrieval date. Add BibTeX-ready entries only for recommended additions.
7. **Section-by-section patch specification**: exact sections to add, revise, move, or remove. Supply draft-ready wording only where wording itself was confirmed during grilling.
8. **Figure and table matrix**: classify each item as **Ready**, **Needs editorial assembly**, **Needs source generation**, **Needs new evidence**, or **Omit/defer**. For ready items, provide exact artifact path, provenance, supported caption claims, and destination. For other items, provide a concrete task, workspace, dependencies, and acceptance criterion. Main-text placement requires an explicit editorial decision.
9. **Appendix and supplement decisions**.
10. **Omissions, inconclusive results, and future work**.
11. **Contradictions and unresolved risks**.
12. **Notes consulted**: include only materially important notes, with path, role, affected claims, provenance quality, and current status.
13. **Artifact manifest**: exact repository-relative paths and associated runlog goals or commits.
14. **Verification checklist**: checks the receiving agent or author must perform in the draft.
15. **First actions**: an ordered, minimal starting sequence for the receiving agent.

The handoff is cumulative and must stand alone. Consult previous handoffs for decisions, but revalidate and restate all current conclusions rather than requiring the reader to reconstruct them.

## Completion gate

Finish only when all conditions hold:

- Every proposal claim has an include, omit, defer, or future-work disposition.
- Every relevant existing draft claim is retained, changed, moved, or removed.
- Every included empirical claim points to repository evidence.
- Every included literature-dependent claim points to retrieved primary literature.
- Active, dirty, and untracked evidence is visibly provisional.
- Superseded and invalid evidence is excluded from current support.
- Every relevant figure and table has a source or a concrete task and intended destination.
- Every contradiction is resolved or explicitly marked open by the user.
- The user confirmed the complete decision recap.
- The timestamped, SHA-stamped handoff exists and is human-readable as a task list without sacrificing claim-level provenance.

Report the created proposal path, if any, and final handoff path. Report open or blocked items succinctly. Do not modify the draft.
