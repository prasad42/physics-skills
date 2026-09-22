# Canonical research-init manifest

Use these templates when `research-init` reaches the repository-design and
manifest gates. They are defaults for new repositories and an audit baseline
for adoption. Existing compatible authority wins.

## Substitution rules

Replace every `{{TOKEN}}` with a confirmed value before presenting the manifest.
Do not write unresolved tokens. Mark an unresolved decision as a manifest
conflict instead of inventing a value.

- `{{PROJECT_TITLE}}`: confirmed project title.
- `{{PROJECT_SUMMARY}}`: one-sentence orientation grounded in the proposal.
- `{{PROPOSAL_TARGET}}`: repository-relative authoritative proposal path.
- `{{PROPOSAL_FORMAT}}`: Markdown, TeX, or PDF.
- `{{CONFIRMATION_DATE}}`: ISO date on which the user confirms authority.
- `{{SCOPE_POINTER}}`: repository-relative scope document, when distinct from
  the proposal.
- `{{ENVIRONMENT_POINTER}}`: discoverable environment manifest or setup
  document.
- `{{SUPPORTED_COMMANDS}}`: only commands confirmed by repository inspection.
- `{{CONTROL_HOST}}`, `{{COMPUTE_HOST}}`, `{{ENVIRONMENT}}`, and
  `{{ABSOLUTE_EXECUTABLE}}`: confirmed execution values.

Blocks labelled **conditional** enter the manifest only when their condition is
confirmed. Omit the label from generated files.

## `AGENTS.md`

```markdown
# Repository instructions

Scientific intent: before changing questions, hypotheses, claims, acceptance
criteria, deliverables, or deferred work, read `notes/proposal.md` and the
authoritative document it identifies.

Scope: before changing the approved scope, read `{{SCOPE_POINTER}}`.

Goals: before planning, starting, continuing, switching, or closing work, read
`runlog/README.md` and the relevant planned or active goal. A primary session
works on one goal.

Evidence: before adding or changing reusable tests or goal evidence, read
`tests/README.md`.

Execution: before running code, simulations, analyses, tests, or artifact
generation, read `runlog/EXECUTION.md` and satisfy its approval gates.

Figures: before rendering or promoting a figure, read `FIGURES.md`.

Delegation: after an approved plan exists in `runlog/planned/GNNNN.md`, ask
whether to delegate implementation to `@executor`. Goal approval is not
delegation approval. Supply the executor with this file, the goal path, exact
scope, acceptance criteria, and every execution and provenance gate. The
primary agent verifies the actual changes and evidence.

Continuation: when a fresh agent session is needed, ask the user to invoke the
user-invoked `@handoff` skill. Session handoffs stay in the OS temporary
directory, outside this repository.

Failure provenance: before continuing after a scientific or numerical
validation failure, record its exact reproduction, first divergence,
residual/tolerance evidence, diagnosis class, corrective revision, rerun result,
and remaining scope in the active goal.

Cleanup: obtain explicit approval before pruning tmux sessions or panes after a
goal is finished.
```

Remove the `Scope`, `Execution`, or `Figures` paragraph only when the associated
document is deliberately absent. Include only confirmed environment commands;
detailed lifecycle and evidence rules belong in their dedicated documents.

## `README.md`

````markdown
# {{PROJECT_TITLE}}

{{PROJECT_SUMMARY}}

## Scientific authority

- Proposal: [`notes/proposal.md`](notes/proposal.md)
- Scope: [`{{SCOPE_POINTER}}`]({{SCOPE_POINTER}})

## Workflow

- Goal lifecycle and status: [`runlog/README.md`](runlog/README.md)
- Execution authority: [`runlog/EXECUTION.md`](runlog/EXECUTION.md)
- Tests and immutable evidence: [`tests/README.md`](tests/README.md)
- Figure contract: [`FIGURES.md`](FIGURES.md)
- Notes and draft handoffs: [`notes/README.md`](notes/README.md)

## Environment

See [`{{ENVIRONMENT_POINTER}}`]({{ENVIRONMENT_POINTER}}).

## Supported commands

{{SUPPORTED_COMMANDS}}

## Directory map

```text
notes/                 Scientific intent, analysis, and draft handoffs
runlog/                Goal lifecycle and execution authority
tests/unit/             Reusable unit tests
tests/integration/      Reusable integration tests
tests/evidence/GNNNN/   Immutable goal-linked evidence
tests/legacy/unmapped/  Preserved evidence not yet linked to a goal
```
````

Omit optional links rather than leaving placeholders. Point to manifests and
command help instead of copying setup details.

## `notes/proposal.md`

Use this pointer only when the authoritative proposal is elsewhere:

```markdown
# Proposal

The authoritative scientific proposal is
[`{{PROPOSAL_TARGET}}`]({{PROPOSAL_TARGET}}) ({{PROPOSAL_FORMAT}}), confirmed on
{{CONFIRMATION_DATE}}.

This file is a pointer. Scientific intent, scope, claims, acceptance criteria,
deliverables, and deferred work remain in the authoritative proposal.
```

When `notes/proposal.md` itself is authoritative, use the complete proposal text
approved at the scientific-intent gate instead of this pointer.

## `notes/README.md`

```markdown
# Notes

`notes/proposal.md` is the authoritative scientific intent or points to it. Read
it before changing questions, hypotheses, claims, acceptance criteria,
deliverables, or deferred work.

Other notes contain derivations, literature work, meeting decisions, or
scientific synthesis. Identify each note's role and provenance in its title or
opening metadata. Notes support the evidence record; they do not replace the
runlog or goal-linked validation.

The evidence chain is:

`proposal -> codebase -> runlog/tests/notes -> @to-draft -> external draft`

`runlog/` is the chronological authority for goal lifecycle and execution
provenance. `tests/` contains reusable validation and immutable goal evidence.
When draft work is requested, `@to-draft` outputs belong in
`notes/draft-handoffs/` for transfer to a separate draft workspace. The external
draft is maintained outside this repository.

For fresh-session continuation, ask the user to invoke `@handoff`; its temporary
session record does not belong in this repository.
```

## `runlog/GOAL_TEMPLATE.md`

```markdown
# GNNNN: Title

**State:** Planned
**Created:** YYYY-MM-DD
**Last updated:** YYYY-MM-DD
**Scope authority:** `notes/proposal.md`
**Predecessor:** None
**Successor:** None

## Goal

State one bounded outcome.

## Exclusions

- State adjacent work that this goal does not authorize.

## Code / Artifacts

- `tests/evidence/GNNNN/`

List every expected code, data, note, figure, and immutable evidence path.

## Settled Decisions

- Record approved choices that implementation must not reopen.

## Plan

1. List the approved implementation and evidence steps.

## Acceptance Criteria

- State checkable scientific, numerical, software, and artifact requirements.

## Stopping Conditions

- State failures, resource bounds, or observations that stop or narrow work.

## Execution and Approvals

- Execution required: Yes / No
- Approved host and environment: Pending / Not applicable
- Execution bundle: Pending / Not applicable
- Approved revision, session, runtime ceiling, and worker ceiling: Pending / Not applicable
- Commit authority: Not granted
- Push authority: Not granted

## Evidence / Results

### Commands and provenance

Record host, environment, exact command, runtime, worker count, session, code
revision, exit status, and output paths.

### Validation

Record results against each acceptance criterion and link immutable evidence.

### Failures

For each scientific or numerical failure, record the exact reproduction, first
divergence, residual/tolerance evidence, diagnosis class, corrective revision,
rerun result, and remaining scope. Write `None` when no failure occurred.

### Review

Record review findings, resolutions, and residual risks.

## Lifecycle Record

Record approved state transitions, cleanup, commits, and pushes.

## Next Action

State one exact next action or declare completion.
```

## `runlog/README.md`

```markdown
# Runlog

`runlog/` is the authoritative goal lifecycle and status index. A primary agent
session works on one goal.

## Goal identity

Use `GNNNN`, with at least four digits. Allocate the smallest integer greater
than every goal ID found in all lifecycle directories and
`tests/evidence/`. Never reuse an ID. The same file and identifier move through
the lifecycle; `tests/evidence/GNNNN/` never moves.

Before allocation, compare scope and acceptance criteria with related goals.
Continue a matching active goal, reuse a matching planned goal, follow a
deprecated goal's successor, or create a linked successor when extending or
correcting finished work.

## Lifecycle

1. After explicit plan approval, create `planned/GNNNN.md` from
   `GOAL_TEMPLATE.md` without overwriting an existing path, then update this
   index.
2. Ask separately whether implementation should be delegated to `@executor`.
3. When implementation begins, update the goal and move it to `active/`; update
   this index and commit the transition only when authorized.
4. When acceptance criteria pass, record evidence and review, then request any
   finish, cleanup, commit, and push authorities not already named in an
   approved execution bundle.
5. After finish approval, move the goal to `finished/`, update the goal and
   indexes, and perform only approved cleanup and Git actions.
6. For cancellation, invalidation, or supersession, record the reason and
   successor, obtain approval, then move the goal to `deprecated/` and update
   the indexes.

Before switching goals, record evidence, blockers, and the exact next action,
then stop. For a fresh-session continuation, ask the user to invoke the
user-invoked `@handoff` skill; its record stays in the OS temporary directory.

Normal work reads this index and the relevant active or planned goal. Consult
finished or deprecated goals for history, provenance, review, or contradiction
resolution.

Repository access grants no commit or push authority.

## Active

No active goals.

## Planned

No planned goals.

## Recently finished

No finished goals.
```

Maintain full finished and deprecated indexes in their lifecycle directories
only when repository scale makes separate indexes useful. Do not duplicate a
complete historical index in several files.

## `runlog/EXECUTION.md` — conditional distributed contract

Use this template when the user confirms a control-host/compute-host workflow.
Otherwise propose a smaller local execution contract with the same approval and
provenance fields.

```markdown
# Execution authority

This document governs simulations, analyses, tests, and artifact generation.
Planning, code, documentation, and runlog edits occur on `{{CONTROL_HOST}}`.
Approved simulations and artifact generation occur on `{{COMPUTE_HOST}}` in
`{{ENVIRONMENT}}` using `{{ABSOLUTE_EXECUTABLE}}`.

## Approval gate

Obtain one explicit approval for a bounded execution bundle, not for each shell
command. State its purpose, primary mutating commands, approved revision, host
and environment, parameters and seeds, outputs, runtime ceiling, worker ceiling,
the exact tmux session or pane names, and the cleanup command that is required
before the goal can finish. State whether it includes tracked artifact or
runlog commits, pushes, or synchronization.

The bundle includes routine read-only preflight, synchronization and cleanliness
checks, monitoring, verification, and provenance capture. It may include an
instrument-only launch correction after a fail-safe stop when no scientific work
or data mutation began and every declared bound remains unchanged. Record the
failure before retrying.

Renew approval when scientific scope, revision, host or environment, parameters
or seeds, outputs, runtime or worker bounds, or mutating actions change. Package
installation, environment mutation, destructive operations, and Git commit or
push remain outside the bundle unless named before approval. Cleanup of every
declared session is mandatory; omitting it from the bundle blocks completion
and requires renewed approval before cleanup.

Before moving the goal to `finished/`, capture the final panes, verify that the
scientific process and child workers have exited, terminate only the declared
sessions or panes, verify that none remain with `tmux list-sessions`, and record
the names, commands, timestamps, exit status, and zero-remaining result.

## Cache-first checkpoints

When a requested result can use complete compatible raw caches, choose a bounded
cache-only checkpoint or intermediate artifact path before launching an
unrelated long run.

For analyses with independent sources or cells:

1. Preflight the raw-cache inventory and declare each unit and its output path.
2. For a trajectory-producing unit, after every completed trajectory, have one
   parent writer atomically rewrite the same resumable NPZ with the completed
   row, trajectory index, depth axis, child-seed lineage, status, exact input
   hashes, revision, parameters, environment, and command provenance. Preserve
   row identity when workers finish out of order and resume only validated
   missing indices. For non-trajectory units, persist each completed unit
   atomically with the same provenance fields.
3. Serve requested partial results from persisted units without repeating
   completed work; label them `review-only` until the full acceptance contract
   passes.
4. Keep trajectory-resampling outputs and averaged-cache summaries in separate
   records and manifests.

The checkpoint is complete when every reported unit has an atomic output,
matching input hashes, and sufficient provenance for exact review or replay. A
trajectory unit is complete only when all M indexed rows are finite and present,
the seed lineage is complete, and the averaged cache is derived from that full
matrix.

## Pre-execution gate

1. On the control host, verify a clean worktree, fetch the configured remote,
   and record the exact approved revision.
2. Make that clean revision available through Git.
3. On the compute host, fetch through Git, check out the exact approved
   revision, and verify both the revision and a clean worktree.
4. Record both hosts and stop if either check fails.

Tracked repository and revision transfer uses Git. Large untracked canonical
data follows the repository's data contract and provenance manifests.

## Launch contract

Use an interactive tmux session or pane with a confirmed explicit shell
procedure. Invoke `{{ABSOLUTE_EXECUTABLE}}` without relying on inherited `PATH`.
Run unbuffered and expose elapsed time and ETA for long work. Verify visible
progress before reporting the job as running.

## Provenance

Record hostname, exact command, worker count, tmux session or pane, start and
end times, exit status, Git revision, environment versions, parameters, seeds,
and output paths in the active goal.

## Artifact return

On the compute host, commit and push only approved tracked artifacts. On the
control host, fetch and fast-forward through Git. Verify matching revisions and
clean worktrees on both hosts. Record the post-transfer result in the goal.

## Cleanup

After goal completion, list owned sessions and panes. Prune them when cleanup
was named in the approved execution bundle; otherwise obtain explicit approval.
Record the cleanup result.
```

Replace generic Git verbs with the repository's confirmed remote and branch
procedure. Add an explicit data-path rule when large canonical data remains
untracked. A remote procedure may not substitute file-copy transport for Git
revision transfer.

## `tests/README.md`

```markdown
# Tests and evidence

## Reusable tests

Live reusable tests belong in `tests/unit/` or `tests/integration/`. Document
only confirmed discovery and execution commands here.

## Immutable goal evidence

Each goal's immutable validation belongs at `tests/evidence/GNNNN/`, using the
same identifier as its runlog goal. The path does not move when the goal moves
between lifecycle states. Link it from the goal's `Code / Artifacts` section.

Keep goal-specific scripts, notebooks, compact reproducible inputs, metadata,
summaries, and reviewable artifacts together. Record parameters, seeds, code
revision, environment, generation commands, acceptance results, and hashes where
practical.

Goal-local validation and review figures, including PNG/PDF pairs and
provenance, belong in `tests/evidence/GNNNN/figures/`. Promote a figure to
top-level `figures/` only when the goal explicitly approves a canonical or
publication-facing artifact.

Large canonical data may live elsewhere when the evidence directory links a
provenance manifest identifying its location, parameters, seeds, revision,
environment, generation command, and hashes where practical.

`tests/legacy/unmapped/` preserves standalone historical evidence until a goal
explicitly adopts it. It is not part of routine test discovery.
```

## `FIGURES.md`

```markdown
# Figure contract

Use APS styling unless the authoritative proposal or user selects another
venue. Select the intended one-column or two-column physical width before
rendering.

Goal-local validation and review figures belong under
`tests/evidence/GNNNN/figures/` with PNG/PDF pairs and provenance. A top-level
`figures/` path is a promotion target only when the active goal explicitly
approves a canonical or publication-facing artifact.

For every rendered or promoted figure, record physical dimensions, source data,
generation command, code revision, output paths, and validation. Visual review
supplements rather than replaces numerical or structural checks.
```

## Empty-directory placeholders

When Git must track an otherwise empty baseline directory, propose an empty
`.gitkeep` only for that directory. Remove it when a substantive tracked file is
added. Do not create example goals, evidence, results, or session handoffs.
