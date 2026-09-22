---
name: research-init
description: Bootstrap a proposal-led scientific research repository.
argument-hint: "[target repository path]"
disable-model-invocation: true
---

# Research repository initializer

Build this evidence chain:

`proposal -> codebase -> runlog/tests/notes -> @to-draft -> external draft`

This is a gated initializer, not a research run. Inspect and design before
writing. Preserve existing content and dirty worktrees. Leave scientific code,
executable tests, simulations, analyses, package installation, environment
creation, and the external draft untouched.

## 1. Target gate

Use the supplied target or the current directory and resolve it absolutely.
Read every applicable `AGENTS.md`. Inspect the target's files, Git state,
proposal and workflow documents, language manifests, environment definitions,
and test conventions.

Classify the target:

- **New**: no meaningful existing content.
- **Adoption**: any meaningful existing content. Preserve compatible paths and
  conventions. If governance already satisfies this contract, report a clean
  audit and stop instead of rewriting it.

Ask when classification is ambiguous. Present the absolute path and
classification for confirmation. If `.git/` is absent, ask separately for Git
initialization and for an initialization commit. Repository access and Git
presence grant neither commit nor push authority.

**Gate:** the user has confirmed the target and mode; the exact initial Git
status and Git authority are recorded; the target is unchanged.

## 2. Scientific-intent gate

Search `notes/` case-insensitively for exactly named proposal files in Markdown,
TeX, or PDF form, including `proposal.md`, `Proposal.tex`, and `Proposal.pdf`.
Reconcile proposal candidates found elsewhere during inspection.

- One candidate: ask whether it remains authoritative.
- Several candidates: require the user to choose one.
- Authoritative file outside `notes/proposal.md`: propose a short
  `notes/proposal.md` pointer recording its path, format, and confirmation date.
- Revision required: stop and recommend a separate revision task. Preserve the
  existing proposal without translating, renaming, or overwriting it.

This initializer alone may create the proposal or pointer; later workflows defer
proposal creation here.

When no proposal exists, retrieve primary sources before asserting novelty,
priority, or a literature gap. Record stable DOI or URLs and retrieval dates;
keep claim-linked anchors concise. Propose a separate literature note only when
the necessary analysis would bloat the proposal.

Load `grilling` and settle the scientific-intent frontier in rounds. Ask only
for decisions; inspect the repository and literature for facts. Cover every
applicable branch:

- motivation, context, and research gap;
- questions, hypotheses, intended claims, and evidentiary thresholds;
- model, assumptions, and validity regime;
- observables, methods, and planned analyses;
- expected interpretations and conditional outcomes;
- deliverables, figures, and tables;
- draft scope, audience or venue, and literature anchors;
- exclusions and deferred work.

Mark unresolved items explicitly. For a new proposal, present the complete
proposed `notes/proposal.md` only after the frontier is empty, then request
explicit approval. For an existing proposal, present any required pointer and
confirm that the proposal still covers the intended claims, scope, and
deliverables. Partial approval keeps the gate closed.

**Gate:** one authoritative proposal is confirmed; any new proposal or pointer
has complete approved text and remains unwritten.

## 3. Repository-design gate

Before proposing baseline file contents, read
[`references/default-manifest.md`](references/default-manifest.md). Use its
canonical templates for new repositories and as the comparison baseline in
adoption mode. Substitute confirmed values, select only applicable conditional
blocks, and expose every adaptation in the exact manifest.

### New-repository baseline

```text
AGENTS.md
README.md
FIGURES.md
notes/
  README.md
  proposal.md
  draft-handoffs/
runlog/
  README.md
  GOAL_TEMPLATE.md
  planned/
  active/
  finished/
  deprecated/
tests/
  README.md
  unit/
  integration/
  evidence/
  legacy/unmapped/
```

In adoption mode, preserve compatible existing paths. Do not add `tests/unit/`
or `tests/integration/` merely to match the baseline. A future-governance
boundary may leave every historical goal and evidence path unchanged. Track
empty directories only with minimal placeholders. Create no example goals or
results. Use `@python-layout` as a separate task when an existing Python
repository must become installable.

New goal and evidence directory names use only `GNNNN`; do not add dates to
their names. Preserve dated legacy paths unchanged in adoption mode.

### Authority map

- `notes/proposal.md`: authoritative scientific intent or pointer.
- `runlog/`: chronological goal lifecycle and authoritative status.
- `tests/unit/`, `tests/integration/`: live reusable tests.
- `tests/evidence/GNNNN/`: immutable evidence linked to goal `GNNNN`.
- Other notes: derivations, literature, meetings, and synthesis; identify role
  and provenance in the title or opening metadata.
- `notes/draft-handoffs/`: `@to-draft` output for the separate draft workspace.

Make `notes/README.md` explain this map and the full evidence chain. Keep the
external draft separate. Mention `@to-draft` in `AGENTS.md` only when draft work
is requested.

### Scope and failure contracts

In adoption mode, preserve the authoritative scope document, such as
`project_summary.md`, and require it before changing claims, acceptance
criteria, or deferred work. Goals, tests, and draft notes remain within that
scope.

Require an active goal to record every scientific or numerical validation
failure before work continues: exact reproduction, first divergence, residual
and tolerance evidence, diagnosis class (algebraic, instrument or fixture,
numerical, physical, or resource), corrective revision, rerun result, and
remaining scope.

### Execution contract

Ask whether this machine is the control host and Chandra the compute host. If
so, keep planning, code, documentation, and runlog edits on the control host;
reserve Chandra for approved simulations and artifact generation. Preserve the
existing command authority or propose `runlog/EXECUTION.md`.

The authority must specify:

- one explicit bounded execution-bundle approval rather than per-command
  prompts;
- the bundle's scientific scope, mutating commands, revision, parameters,
  seeds, outputs, runtime ceiling, and worker ceiling;
- bundled read-only preflight, synchronization, monitoring, verification, and
  provenance commands;
- cache-first checkpoints: when complete compatible raw caches can answer a
  request, prefer a bounded cache-only path with atomic per-unit outputs,
  exact input hashes, provenance, review-only partial labeling, and separate
  trajectory-resampling versus averaged-cache records; trajectory-producing
  units checkpoint every completed indexed trajectory through one parent writer
  and resume only validated missing indices;
- renewal triggers for changed scientific scope, revision, host or environment,
  parameters, outputs, runtime or worker bounds, or mutating actions;
- fail-safe instrument-only launch corrections may remain in the bundle only
  when no scientific work or data mutation began and every bound is unchanged;
- confirmed host and environment;
- long compute launches through shell-first interactive tmux with unbuffered
  visible progress;
- clean approved revisions and complete provenance;
- declaration and cleanup of every owned tmux session before the goal can move
  to `finished/`; any bundle that creates a session must name its exact cleanup
  command, and an unlisted session blocks completion;
- the confirmed absolute executable and explicit shell procedure when remote
  execution would otherwise inherit `PATH`;
- Git-only cross-host transfer of tracked files.

For a cross-host run, push the exact approved clean revision, verify that exact
revision and a clean Chandra checkout, commit and push only approved generated
artifacts there, and pull them onto the control host with Git. Record both
hosts, revisions, commands, worker counts, sessions, outputs, and post-transfer
verification. `scp` is not a repository or revision transfer mechanism.

### Runlog contract

Make `runlog/README.md` the lifecycle index and detailed authority. A goal starts
only after plan approval creates `planned/GNNNN.md`.

Allocate the smallest integer greater than every `GNNNN` found across all
lifecycle directories and the evidence root, using at least four digits. Create
the planned file without overwriting; if concurrency takes the ID, rescan. The
ID never changes. Move the same file to `active/`, `finished/`, or
`deprecated/`, and synchronize the index on every transition.

Every goal records its ID, title, state, created and updated dates, bounded
outcome, code/artifacts, plan, evidence/results, and exact next action. Commit a
transition with its related code or results only when authorized; otherwise
report it as uncommitted.

Normal work consults the index and relevant active or planned goal. Read
finished or deprecated goals for history, provenance, review, or contradiction
resolution.

Before allocation, compare scope and acceptance criteria with related goals:

- continue the matching active goal;
- reuse the matching planned goal;
- report no remaining work when a finished goal already satisfies the request;
- create a linked successor to extend or correct finished work;
- follow a deprecated goal's successor rather than reactivating it.

Topic overlap alone does not establish identity. Keep one goal per primary
session. Before switching, record evidence, blockers, and the exact next action,
then stop. When continuation needs a fresh agent session, ask the user to invoke
the user-invoked `@handoff` skill. It writes temporary session context outside
the repository; create no repository handoff template or handoff directory.

### Evidence and adoption boundary

Link immutable goal validation from the goal's `Code / Artifacts` section to
`tests/evidence/GNNNN/`. Keep its scripts, notebooks, compact reproducible
inputs, metadata, summaries, and reviewable artifacts together. The path remains
fixed through lifecycle transitions. Preserve historical goals and evidence at
their existing paths; retain unmapped standalone work under
`tests/legacy/unmapped/` until a goal adopts it.

An adopted repository may switch future work to `GNNNN` only with user approval.
First inventory every legacy active and planned goal. Close or deprecate
completed legacy work and represent continuing work with one linked `GNNNN`
successor; no work remains active in both systems. Mark the legacy index
historical through the boundary date and make `runlog/README.md` authoritative
from that date. Start at one greater than the largest existing `GNNNN` across
lifecycle and evidence paths, or `G0001`. Update `AGENTS.md`, README pointers,
runlog indexes and templates, and `tests/README.md` in one manifest. Move or
rename no historical file. Historical relocation, live-suite reorganization,
and identifier rewrites are separate tasks.

Large canonical data may live elsewhere when a provenance manifest links its
parameters, seeds, code revision, environment, generation command, and hashes
where practical.

### Figures, orientation, and agents

Preserve the figure contract or propose `FIGURES.md`. Default to APS styling
unless the proposal or user selects another venue. Select one- or two-column
physical width before rendering. Put goal-local PNG/PDF review pairs and
provenance under `tests/evidence/GNNNN/figures/`. Promote an output to top-level
`figures/` only when the goal explicitly approves a canonical or publication
artifact. Record physical layout, source data, command, code revision, and
artifact validation.

Keep `README.md` concise: link the proposal, lifecycle, evidence, and scope;
record setup and environment evidence; list supported commands; and map the
directories. Link discoverable manifests instead of copying them. In adoption
mode, merge only missing orientation into a compatible README.

Keep `AGENTS.md` short and behavioral. Give conditional pointers to
`notes/proposal.md`, `runlog/README.md`, `tests/README.md`, and, when present,
`runlog/EXECUTION.md` and `FIGURES.md`. State one goal per session and only
confirmed environment commands.

Include this later-session delegation gate: once an approved plan exists in its
planned goal file and implementation is ready, ask whether to delegate to `@executor`.
Goal approval alone is not delegation approval. On approval, dispatch the goal
path, repository instructions, exact scope, acceptance criteria, and all
execution and approval gates; then verify the actual changes and evidence. On
refusal, implement directly. The initializer itself stops before implementation.
Require explicit approval before pruning tmux sessions or panes after finish
unless cleanup was named in an approved execution bundle.

Remain language-neutral until inspection establishes the language. For Python,
ask whether to adopt an existing environment definition or propose a
project-specific one. Environment files may enter the manifest; creation and
package installation remain separate approved work.

**Gate:** every baseline path has proposed content or a deliberate compatible
authority, with no duplicated or conflicting source of truth.

## 4. Manifest gate

Classify every baseline and optional path as `create`, `already compatible`,
`merge proposed`, `conflict`, or `skip`. Preserve existing content. Show the
complete text or exact patch for every creation and merge. List Git
initialization, staging, and commit actions separately. Unrelated dirty changes
are neither conflicts nor proposed Git actions.

A conflict in proposal, lifecycle, tests, notes, environment, or `AGENTS.md`
blocks that item until the user decides. Request explicit approval of the whole
manifest.

Immediately before writing, reread every existing manifest path and Git status.
Recompute changed items and obtain approval again. Resolve every destination;
reject traversal and any symlink that would write outside the confirmed target.
A symlinked baseline path remains blocked until an in-repository regular-file or
directory destination is approved.

**Gate:** the user has approved the current exact manifest, every conflict
resolution, and each Git action.

## 5. Apply gate

Apply only approved manifest actions. Preserve unrelated files and dirty
changes. Never overwrite an existing proposal. Initialize Git only when
approved.

For an approved commit, inspect attributes and configured filters for every
staged path. Stage only manifest paths with non-interactive Git commands. If
staging can execute external code, leave the changes uncommitted. Disable
repository hooks and commit signing for the initialization commit.

Perform no scientific execution, simulation, test run, analysis, artifact
generation, package installation, or environment creation.

**Gate:** every approved action is applied and no unapproved path changed.

## 6. Verification gate

Verify all of the following:

- approved `notes/proposal.md` content or pointer exists unchanged;
- required directories, indexes, templates, and context pointers exist;
- internal links resolve and lifecycle examples agree;
- goal and immutable-evidence identifiers agree;
- pre-existing dirty content is preserved;
- Git actions stayed within authority;
- prohibited execution did not occur.

Repeat the inspection as a dry run using the same classification and manifest
rules. Success requires no remaining required change. Report every created or
modified path, Git action, and unresolved conflict. A skipped conflict means
partial initialization.

**Completion:** verification passes and the second dry run is idempotent.
