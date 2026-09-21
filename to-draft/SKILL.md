---
name: to-draft
description: Prepare a proposal-led, evidence-backed handoff for creating or updating a scientific draft.
argument-hint: "[draft path, new-draft destination, or intended draft task]"
metadata:
  opencode/autoinvoke: false
---

Prepare a self-contained handoff after substantial work in a scientific codebase. The handoff is both an evidence-backed patch specification for a draft-writing agent and a human-readable editorial task list. Build the first handoff from the full relevant evidence base; when a later invocation has a usable compatible baseline, build it from the delta. Then grill the user on publication decisions before writing anything.

This manuscript-facing workflow requires one existing authoritative proposal and is read-only except for one final handoff under `notes/draft-handoffs/`, written after the user confirms the complete editorial decision recap. It does not initialize a project or make Python code installable; use `@research-init` for initialization and `@python-layout` for packaging.

The external draft workspace is always read-only. Treat missing verification as a limitation or task, not permission to run Python, simulations, tests, analyses, figure generation, draft compilation, or source-repository edits.

## 1. Establish the workspaces and review mode

Read every applicable `AGENTS.md` from the source repository hierarchy before inspecting scientific content. Identify the source repository root and record:

- Absolute path.
- Creation time with timezone.
- Full and short `HEAD`, commit date, and subject.
- Exact `git status --short` output.

Resolve the draft mode before it becomes a dependency:

- If the user supplied a readable draft path, use update mode.
- If the user supplied an unreadable path, ask for a corrected or mounted path.
- If no draft path was supplied, ask whether to prepare a new draft at a named destination or update an existing draft at a readable path.

For an existing draft, identify its source, bibliography, and referenced asset inputs without reading their scientific content yet. If it is in a Git repository, record that repository's absolute path, `HEAD`, commit metadata, and dirty state. For new-draft mode, record the intended destination and target format. Write nothing there.

Locate exactly named proposal candidates under `notes/` without reading their
scientific contents, using the filename rules in step 2. If
`notes/proposal.md` exists, it is the authority entry and no other candidate may
replace it in this workflow. Otherwise ask the user to select among multiple
candidates and record the sole or selected authority entry. If no proposal
exists, stop and direct the user to `@research-init`; write nothing.

Read only enough of the authority entry to follow its explicit proposal
pointers to one resolved target. Reject a cycle, missing target, or path outside
the source repository. Record and hash both the authority entry and resolved
target, even when they are the same file; defer their scientific contents to
step 2.

Search `notes/draft-handoffs/` except its `README.md` for a prior handoff with the same absolute source repository, authoritative proposal entry and resolved target, and draft path or destination. Inspect only filenames and handoff frontmatter during discovery; do not open each cumulative body. Choose the newest matching handoff whose frontmatter declares the current `baseline_schema: 2` and `baseline_complete: true`. Ignore older schemas, incomplete baselines, and handoffs for other source or draft targets.

Choose one review mode:

- **Full**: no compatible handoff exists, or its baseline cannot establish what changed. Inspect the full relevant evidence base.
- **Incremental**: a compatible handoff has a usable baseline. Treat it as a cached evidence map and inspect the delta plus anything the delta invalidates.

For incremental review, read the compatible handoff once and extract its source commit, proposal entry and resolved-target hashes, hashes or immutable identifiers for dependencies outside that commit, draft Git stamp or input hashes, policy-file hashes, literature retrieval dates, and complete transitive claim dependencies. Build a metadata-first change set before opening scientific files:

1. Compare source commits with `git diff --name-status <prior-source-commit>..HEAD` and `git log --oneline <prior-source-commit>..HEAD`; add current staged, unstaged, and recursively enumerated untracked paths from `git status --short --untracked-files=all`.
2. Compare every dependency not captured by the prior source commit, including dirty, untracked, ignored, external, and mutable generated inputs, by SHA-256 or a stable content-addressed identifier. Include deleted paths.
3. Inventory the current draft source, bibliography, and referenced asset input paths and compare the full path set to detect additions and deletions. For a versioned draft, also compare its prior commit to current `HEAD` and add its current staged, unstaged, and recursively enumerated untracked paths. Compare recorded hashes for every dirty, ignored, external, or other input not captured by the draft commit.
4. Compare both proposal hashes and the source-policy hashes. Expand the changed set through the prior transitive dependencies, including runlogs, tests, data, artifacts, generators, scripts, code, manifests, analytical assumptions, and policy files. A changed conclusion also invalidates downstream claims, figures, tables, citations, and editorial decisions that depend on it.
5. Follow changed goals and manifests to relevant ignored artifacts. An ignored artifact without a provenance link is not evidence; flag it rather than silently adding it to a claim.

Read the compatible handoff and affected files, not unchanged evidence. Carry forward an unchanged claim only when its recorded dependency closure is complete, every dependency remains unchanged, and the prior handoff gives enough provenance to satisfy the current completion gate. A filename or modification time alone is not a reliable content baseline.

Fall back to full review when a prior source or draft commit is unavailable or not an ancestor; any required proposal, policy, non-commit dependency, draft, literature, or dependency field is absent; the proposal changed so broadly that affected claims cannot be bounded; the dependency closure is incomplete; or the user requests full revalidation. State the fallback reason.

After choosing the review mode, read every draft source and bibliography input in full mode. In incremental mode, read changed inputs and unchanged inputs required to reconcile affected claims; carry forward unaffected draft claims from the compatible handoff.

Compare the current receiving task and boundaries with the compatible handoff. A changed task does not invalidate an otherwise sound evidence baseline, but prior editorial decisions carry forward only within unchanged scope. Treat every newly in-scope claim absent from the prior ledger as affected and review its full provenance; fall back to full review when the new scope cannot be bounded from the prior claim map.

Completion: source provenance, one unambiguous draft mode, one review mode, and either a bounded delta or an explicit full-review reason are established.

## 2. Establish scientific intent

Use the case-insensitive proposal search completed in step 1. Exactly named Markdown, TeX, or PDF files such as `proposal.md`, `Proposal.tex`, or `Proposal.pdf` qualify.

- Use the authority entry and resolved target fixed in step 1. In incremental
  mode, carry forward the prior proposal map only when both hashes are unchanged;
  otherwise read the affected proposal content.
- Keep an existing proposal read-only. If it no longer reflects the user's intent, ask whether proposal revision should occur separately before this workflow continues.
- Follow an explicit pointer in the selected proposal. Do not treat
  `project_summary.md` as authoritative unless that proposal identifies it as
  the authority.

- Require the sole or user-selected proposal to already exist and remain read-only. If no proposal exists, stop and direct the user to `@research-init`; do not infer, bootstrap, create, or revise a proposal in this workflow.

Completion: one authoritative proposal exists and every intended claim, scope boundary, and target deliverable can be enumerated from current evidence or a valid carried-forward map.

## 3. Build the evidence map

In full mode, inventory every file under `notes/`, read the proposal, and read every note materially connected to a proposal claim, draft claim, runlog result, analytical issue, editorial decision, or literature question. In incremental mode, use the metadata-first change set from step 1: read changed notes and any unchanged note whose dependent claim was invalidated; carry forward other note classifications from the compatible handoff. Classify notes by role rather than trusting their directory:

- Analytical derivations must expose assumptions and trace to supporting calculations where applicable.
- Numerical claims must trace to runlogs, immutable tests, data, or artifacts.
- Literature claims must trace to retrieved primary papers.
- Meeting notes carry author intent, subject to the current grilling.
- The compatible prior handoff carries earlier editorial decisions and unfinished tasks; revalidate conclusions affected by the delta and preserve unchanged decisions for the current grilling.
- Untraceable claims remain explicitly unverified.

In full mode, read the repository's runlog index and lifecycle rules first. In incremental mode, reread them when they changed; otherwise use the rules recorded by the compatible handoff. Follow claim-led provenance through all material finished, active, planned, and deprecated goals in full mode. In incremental mode, inspect changed goals, lifecycle transitions, and unchanged goals reached through an invalidated dependency:

- Finished goals supply completed conclusions.
- Active evidence is provisional.
- Planned goals establish unresolved dependencies, not results.
- Deprecated goals establish invalidity, supersession, or provenance, not current support.

Follow each goal selected by the review mode into its linked immutable tests, scripts, result files, figures, data manifests, commits, and code. Resolve evidence locations from the repository's own policy and indexes (for example, read `tests/README.md` when it defines test evidence); record the exact paths in the handoff rather than imposing a universal directory or naming convention. Inspect existing images and PDFs when their visual content affects publication suitability. Read code only where needed to verify implementation facts, conventions, or artifact generation. Inventory first, then read relevant material deeply; do not substitute a broad historical summary for claim-level provenance or reopen unchanged evidence without an invalidated dependency.

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

Completion: every proposal claim and relevant draft claim has a current status, strongest available evidence, caveats, contradictions, and unresolved publication decisions; every carried-forward classification has unchanged dependencies.

## 4. Audit the literature

Before editorial grilling, perform a focused literature audit for the claims identified above. This is a draft-facing audit, not a general thematic review. In incremental mode, carry forward literature records for unchanged claims and retrieve sources only for affected claims, changed citations, unresolved prior gaps, novelty and priority coverage last checked more than 30 days ago, or other literature coverage last checked more than 180 days ago. Recheck novelty and priority on every submission or revision handoff regardless of age. During the audit, record the coverage-check date and search scope for each literature-dependent claim so the final handoff and next incremental review do not require reconstruction.

1. Read relevant repository literature notes and follow their citations to retrieved primary papers.
2. For every literature-dependent claim, check direct precedents, seminal context, recent competing results, and novelty or priority risk.
3. Check freshness. Search externally when repository coverage is missing, stale relative to the handoff, or used to assert novelty or priority.
4. Verify bibliographic metadata, record a stable DOI or URL and retrieval date, and separate what each source supports from what it does not support.
5. Identify citations already present in the draft and BibTeX entries that the patch specification should add.

Keep the audit in the final handoff rather than creating a separate literature note. Every citation must trace to a retrieved source; flag an unresolved literature gap instead of filling it from memory.

Completion: every literature-dependent included claim has traceable primary support or an explicit unresolved gap, and novelty language has been tested against the retrieved corpus.

## 5. Grill publication decisions

Load the `grilling` skill and work the design tree in rounds. In incremental mode, preserve confirmed decisions whose dependencies and task scope remain unchanged; reopen decisions introduced or invalidated by the evidence delta or changed receiving task. Ask only genuine publication decisions and unresolved conflicts; do not ask the user for facts available from the workspaces or literature. Give a recommended answer with every question.

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

Before writing, read the co-located [handoff schema](references/handoff-schema.md). It is required for every final handoff branch: use its frontmatter and all 16 sections, and do not omit a section because review mode is full or incremental. The schema carries the detailed output requirements; this file retains the workflow steps and completion gates.

The handoff is cumulative and must stand alone. Revalidate conclusions affected by the delta, carry forward unchanged conclusions with their provenance, and restate the complete current result so the reader never has to reconstruct it from earlier handoffs.

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
- Incremental review identifies every changed dependency, and every carried-forward claim traces to the compatible handoff and an unchanged complete dependency closure.
- The recorded commit stamps and hashes are sufficient for the next invocation to bound its delta; otherwise this handoff declares that the next review must be full.
- The user confirmed the complete decision recap.
- The timestamped, SHA-stamped handoff exists and is human-readable as a task list without sacrificing claim-level provenance.

Report the authoritative proposal path and final handoff path. Report open or blocked items succinctly. Do not modify the draft.
