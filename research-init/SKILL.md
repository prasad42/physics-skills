---
name: research-init
description: Bootstrap a proposal-led scientific research repository.
argument-hint: "[target repository path]"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Initialize a scientific research repository around this evidence chain:

`proposal -> codebase -> runlog/tests/notes -> /to-draft -> external draft`

This is a gated initializer, not a research run. Inspect and design before
writing. Preserve existing content, stay safe in dirty worktrees, and leave
scientific code, simulations, tests, package installation, environment creation,
and the external draft untouched.

## 1. Establish the target

Use the supplied path, or the current working directory when none was supplied.
Resolve it to an absolute path. Read every applicable `AGENTS.md`, then inspect
the target's files, Git state, existing proposal and workflow documents,
language manifests, environment definitions, and test conventions.

Classify the target as a new repository or adoption of an existing repository.
Treat any meaningful existing content as adoption; ask when the classification
is ambiguous. Present the absolute path and classification and obtain
confirmation before continuing.

If `.git/` is absent, ask whether Git initialization is permitted. Ask
separately whether an initialization commit is permitted. Git presence never
implies commit permission.

Completion: the confirmed target, mode, exact initial Git status, and Git
authority are known without changing the target.

## 2. Establish scientific intent

Search `notes/` case-insensitively for exactly named proposal files in Markdown,
TeX, or PDF form, including `proposal.md`, `Proposal.tex`, and `Proposal.pdf`.
Also reconcile any proposal candidate outside `notes/` found during target
inspection; ask whether it is authoritative rather than creating a competing
proposal.

- If exactly one exists, ask whether it remains authoritative and preserve it.
- If several exist, require the user to select the authoritative proposal.
- If the authoritative proposal is not `notes/proposal.md`, propose a short
  `notes/proposal.md` pointer containing its path, format, and confirmation date.
- If revision is needed, stop initialization and recommend a separate proposal
  revision task. This initializer never revises, translates, renames, or
  overwrites an existing proposal.

When no proposal exists, perform a focused primary-source check before making
claims about novelty, priority, or a literature gap. Retrieve sources rather
than citing from memory; record stable DOI or URLs and retrieval dates. Keep
concise claim-linked anchors in the proposal. Propose a separate literature note
only when the analysis would bloat the proposal.

Load the `grilling` skill and work the complete scientific-intent design tree in
rounds. Ask only decisions; inspect the repository and literature for facts.
Settle every applicable branch:

- Motivation and context.
- Research gap.
- Questions and hypotheses.
- Intended claims and evidentiary thresholds.
- Model, assumptions, and validity regime.
- Observables, methods, and planned analyses.
- Expected interpretations and conditional outcomes.
- Deliverables, figures, and tables.
- Draft scope and target audience or venue.
- Literature anchors.
- Exclusions and deferred work.

Mark genuinely unresolved items instead of inventing answers. For a new
proposal, when the frontier is empty, present the complete proposed
`notes/proposal.md` and request explicit confirmation. For an existing
authoritative proposal, present the proposed pointer when one is needed and
confirm that the proposal still enumerates the intended claims, scope, and
deliverables. Partial approvals do not open the write gate.

Completion: one authoritative proposal is confirmed, and any new proposal or
pointer has complete approved text but has not yet been written.

## 3. Design the repository

Use this baseline:

```text
AGENTS.md
notes/
  README.md
  proposal.md
  draft-handoffs/
runlog/
  README.md
  GOAL_TEMPLATE.md
  HANDOFF_TEMPLATE.md
  planned/
  active/
  finished/
  deprecated/
  handoffs/
tests/
  README.md
  legacy/unmapped/
```

Use minimal placeholder files only when empty directories must be tracked. Do
not create example goals or results.

### Role boundaries

- `notes/proposal.md` is the authoritative scientific intent or a pointer to it.
- `runlog/` is the chronological, authoritative lifecycle record for goals.
- `tests/` holds reproducible goal-linked validation and evidence.
- Other notes hold analytical derivations, literature work, meeting decisions,
  or scientific synthesis; identify each note's role and provenance in its title
  or opening metadata rather than enforcing speculative subdirectories.
- `runlog/handoffs/` carries session continuation context.
- `notes/draft-handoffs/` carries `/to-draft` outputs to a separate draft
  workspace.

`notes/README.md` must explain these boundaries and the full evidence chain.
The external draft remains separate. Mention `/to-draft` in `AGENTS.md` only
when draft work is requested.

### Scientific and execution contracts

When adopting an existing scientific repository, preserve its authoritative
scope document, such as `project_summary.md`, and require it to be read before
changing claims, acceptance criteria, or deferred work. Do not let a goal,
test, or draft note silently broaden that scope.

If scientific or numerical validation fails, the active goal must record the
exact reproduction, first divergence, residual and tolerance evidence,
diagnosis class (algebraic, instrument or fixture, numerical, physical, or
resource), corrective revision, rerun result, and remaining scope before work
continues.

When the repository has an execution contract, preserve it as the authority
for commands. Its design should cover explicit runtime and worker approval,
the confirmed host and environment, shell-first interactive tmux launches,
unbuffered visible progress, clean approved revisions, complete provenance,
and cleanup of owned sessions. A remote launch that depends on inherited PATH
must be replaced by the target's confirmed absolute executable and explicit
shell procedure. Use Git for all repository synchronization and transfer of
tracked files; do not substitute `scp` for Git-based revision or repository
transfer. When the target designates a compute host, keep planning, code,
documentation, and runlog edits on the control machine; use the compute host
only for approved simulations and artifact generation, plus the required Git
push of approved generated artifacts afterward. Pull those artifacts onto the
control machine with Git.

### Runlog contract

`runlog/README.md` is the lifecycle index and detailed source of truth. A goal
starts only after plan approval at `planned/YYYYMMDD-goal-N.md`, where `N` is the
next unused number for that date. Its identifier never changes. Move the same
file to `active/` when work starts, `finished/` with completed results, or
`deprecated/` with a reason and successor when applicable. Synchronize the
index on every transition.

Every goal contains title, state, created and updated dates, goal, code/artifacts,
plan, evidence/results, and next action. Consult active and planned goals during
normal work; consult finished or deprecated goals for history, provenance,
review, or contradictions. When commits are authorized, commit each lifecycle
transition with its related code or results; otherwise report it as uncommitted.
Never infer commit or push authority from repository access.

Keep one runlog goal per primary agent session. Before changing goals, update
the current goal's evidence, blockers, and next action, then stop. A continuation
handoff records the goal ID, repository state, settled decisions, evidence,
blockers, and exact next action without duplicating the goal's full history.

### Evidence contract

Goal-specific validation belongs at the immutable path
`tests/YYYYMMDD/goal-N/`, linked from the goal's `Code / Artifacts` section.
Keep validation scripts, notebooks, compact reproducible inputs, metadata,
summaries, and reviewable artifacts together there. The path does not move with
the goal's lifecycle state.

Large canonical data may live elsewhere, but link it through provenance
manifests containing parameters, seeds, code revision, environment, hashes where
practical, and generation commands. Preserve historical standalone work under
`tests/legacy/unmapped/` until a goal explicitly adopts it.

When figures are in scope, preserve the repository's figure contract and require
it before rendering. Goal-local validation and review figures, including
PNG/PDF pairs and provenance, belong under the immutable
`tests/YYYYMMDD/goal-N/figures/` path. A top-level `figures/` path is a
promotion target only when the goal explicitly approves a canonical or
publication-facing output. Record the selected physical layout, source data,
command, code revision, and validation of the resulting figure artifacts.

### Agent instructions and environment

Keep `AGENTS.md` short and behavioral, not a repository summary. Give strong
conditional pointers to `notes/proposal.md`, `runlog/README.md`, and
`tests/README.md`; state the one-goal-per-session boundary and only confirmed
environment commands. Require explicit user approval before pruning tmux
sessions or panes after a goal is marked finished. Put detailed lifecycle and
evidence rules in their READMEs.

Remain language-neutral when inspection does not establish the language; ask
which language the codebase will use. For Python, ask whether to adopt an
existing environment definition or propose a project-specific one. Environment
files belong in the manifest, but creating an environment or installing
packages requires separate work and approval after initialization.

Completion: every baseline path has proposed content or a deliberate compatible
existing source of truth, with no duplicated or conflicting authority.

## 4. Present the exact manifest

Classify every baseline and optional path as `create`, `already compatible`,
`merge proposed`, `conflict`, or `skip`. Preserve all existing content. For each
creation or merge, show the complete proposed text or exact patch. Show Git
initialization, staging, and commit actions separately.

A conflicting proposal, lifecycle, test, notes, environment, or `AGENTS.md`
convention blocks that item until the user decides. Do not treat unrelated dirty
changes as conflicts and do not include them in proposed Git actions.

Request explicit confirmation of the complete manifest. Immediately before
writing, re-read every existing manifest path and Git status. If anything has
changed, recompute the affected manifest and obtain confirmation again.
Resolve every manifest path and reject a symlink or traversal that would write
outside the confirmed target. Treat a symlinked baseline path as a conflict
requiring an in-repository regular-file or directory destination.

Completion: the user has confirmed the current exact manifest, including every
merge, conflict resolution, and Git action.

## 5. Apply safely

Apply only confirmed manifest actions. Never overwrite an existing proposal.
Preserve unrelated files and dirty changes. Initialize Git only when approved.
If a commit was approved, stage only confirmed manifest paths and use
non-interactive Git commands. Inspect attributes and configured filters for
those paths before staging; leave the changes uncommitted if staging can execute
external code. Disable repository hooks and commit signing for the initialization
commit so approval cannot trigger unrelated execution.

Run no scientific code, simulations, tests, analyses, or artifact generation,
package installation, or environment creation during initialization.

Completion: every approved action is applied and no unapproved path changed.

## 6. Verify

Inspect the resulting files and verify:

- The confirmed proposal or pointer exists unchanged at `notes/proposal.md`.
- Required directories, indexes, templates, and context pointers exist.
- Internal links resolve and lifecycle examples agree across documents.
- Runlog goals and immutable test paths use the same identifier convention.
- Pre-existing dirty paths and their content were preserved.
- Git actions stayed within granted authority.
- No prohibited execution occurred.

Perform a second dry-run inspection using the same classification and manifest
rules. Success requires no remaining required changes. Report every created or
modified path, Git action, and unresolved conflict. A skipped conflict means the
repository is only partially initialized; state that rather than claiming full
success.

Completion: verification passes and the second dry run is idempotent.
