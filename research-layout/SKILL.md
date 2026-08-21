---
name: research-layout
description: Refactor a scientific Python repository into a validated src package and scripts layout.
argument-hint: "[target repository path]"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Migrate an established scientific Python repository toward this separation:

`src/<package>/ -> reusable scientific and I/O code`

`scripts/ -> explicit simulation, analysis, and figure entry points`

This is a gated refactoring workflow, not a fixed scaffold. Preserve scientific
behavior, provenance, cache identity, and historical evidence. Patterns in other
repositories are evidence, not templates.

## 1. Establish authority and quiescence

Use the supplied path, or the current working directory when none was supplied.
Resolve it to an absolute path. Read every applicable `AGENTS.md`, the proposal
pointer, runlog index and relevant goals, test conventions, Git status, language
manifests, environment definitions, and user-facing execution documentation.

Confirm the target and Git authority. Record all existing dirty paths without
changing them. Never infer commit, dependency-installation, or environment-
creation permission from repository access.

Treat layout migration as its own runlog goal. If another goal is active, or a
running job, scheduler submission, notebook, external checkout, or downstream
automation may depend on current paths or imports, stop and arrange a goal
boundary or coordinated migration window. Do not mix migration into a scientific
production goal.

Completion: the target, governing workflow, Git authority, active consumers, and
safe migration window are known.

## 2. Inventory behavior before designing paths

Build a complete inventory of tracked Python files and their consumers. Classify
each file as one of:

- reusable model, algorithm, parameter, or I/O library;
- simulation producer;
- analysis or figure entry point;
- goal-linked validation or historical evidence;
- packaging or environment support;
- generated, cached, data, figure, notebook, or archival material.

Trace imports and invocation commands. Identify runtime behavior coupled to:

- repository-root or current-working-directory paths;
- `sys.path`, sibling imports, wildcard imports, or import-time side effects;
- multiprocessing importability and pickling;
- cache keys, serialized qualified names, schema or data versions;
- random seeds, configuration discovery, and environment variables;
- module execution, direct file execution, notebooks, schedulers, and external
  consumers;
- version lookup and installed-package metadata.

Use Git history and existing documentation when a file's role is unclear. Ask
the user only for decisions that inspection cannot settle. Do not move data,
figures, notebooks, caches, runlogs, notes, or immutable goal evidence merely to
make the tree look conventional.

Completion: every Python file and known invocation has a proposed role, and all
path-, import-, serialization-, and provenance-sensitive behavior is recorded.

## 3. Design the migration

Propose the smallest coherent target. The usual shape is:

```text
pyproject.toml
src/
  <import_package>/
    __init__.py
    ...
scripts/
  ...
```

Place reusable scientific logic under one import package. Keep `scripts/` as
thin orchestration over package APIs when practical; a script may remain larger
when splitting it would create unrelated scientific changes. Keep goal-specific
validation at its immutable evidence path rather than promoting it to `scripts/`.

Settle and present these decisions explicitly:

- distribution name, import-package name, and version source;
- build backend and manifest, preferring `pyproject.toml` for a new manifest;
- package discovery and intended public API;
- internal imports and supported invocation commands;
- whether any stable command deserves a console entry point;
- runtime versus development dependencies, based only on confirmed imports and
  existing environment evidence;
- repository-root, package-resource, data, output, and configuration path rules;
- cache/data compatibility and any required migration or version boundary;
- external consumers that require temporary compatibility imports.

Do not add compatibility shims speculatively. Require a concrete consumer,
persisted representation, or shipped command, and define the shim's removal
condition. Do not change numerical methods, defaults, parameter grids, random
number behavior, output schemas, cache identity, or figure semantics as part of
the layout refactor.

Define validation before editing. At minimum, cover import from outside the
repository root, package metadata, each supported entry point, path handling,
and representative deterministic scientific behavior. Add cache or serialization
regressions whenever the inventory found those risks.

Completion: one reviewable migration design maps every inventoried file and
consumer to a destination or deliberate non-action, with compatibility and
validation decisions settled.

## 4. Plan and approve the exact manifest

After the user approves the design, create the repository's next planned runlog
goal using its established template and identifier convention. Include every
moved or edited path, validation artifact, compatibility decision, and acceptance
criterion. Move the goal to active only when migration work begins, following
the repository's commit rules.

Present an exact manifest classifying each affected path as `move`, `create`,
`edit`, `retain`, `delete after move`, `conflict`, or `skip`. Show import and
entry-point changes, packaging metadata, tests, documentation, and Git actions.
Treat dirty overlap and ambiguous external consumers as conflicts. Obtain
explicit approval for the complete current manifest.

Immediately before writing, re-read affected paths and Git status. Recompute and
reapprove any manifest item that changed. Reject symlink or traversal targets
that escape the confirmed repository.

Completion: the runlog goal and exact current migration manifest are approved.

## 5. Apply the refactor

Use history-preserving moves when Git tracks the source. Apply only approved
changes and preserve unrelated work. Update imports, package-relative resource
lookups, launch documentation, and scheduler examples together with each move.
Keep entry points import-safe: argument parsing, process-pool creation, simulation,
and plotting belong behind an explicit main path.

Avoid opportunistic cleanup, formatting sweeps, dependency upgrades, scientific
changes, regenerated data, and regenerated figures. Do not install dependencies
or create an environment without separate permission. If a local editable or
wheel install is approved for validation, avoid resolving or upgrading
dependencies unless explicitly authorized.

Completion: every approved path and consumer reflects the target design, with no
unrelated or scientific behavior changes.

## 6. Validate and close the goal

Before any Python execution, follow the repository's prompt, environment,
progress-bar, worker-count, and long-run rules. Give a time estimate and obtain
permission. Ask for worker count before every parallelizable run. Never launch a
production simulation merely to validate packaging.

Run the approved validation matrix in the confirmed environment. Include:

- build or installation metadata inspection as applicable;
- package import from a directory outside the repository;
- supported script or entry-point smoke tests without production-scale work;
- existing deterministic unit and scientific regression tests;
- path, cache, serialization, multiprocessing, and figure regressions identified
  during inventory;
- a search for stale imports, old commands, and references to moved paths.

Record exact commands, environment, duration, and results in the active goal.
Distinguish failures caused by the migration from pre-existing failures. Fix only
in-scope migration regressions, then rerun the affected checks.

Inspect the final diff and verify that generated scientific artifacts and
unrelated dirty files did not change. Update the runlog index, move the same goal
file to finished only when all acceptance criteria pass, and commit only within
the user's granted authority. Otherwise leave the goal active with evidence,
blockers, and an exact next action.

Completion: the package works independently of repository-root import leakage,
all supported workflows use documented paths, scientific and provenance
regressions pass, and the runlog truthfully records the outcome.
