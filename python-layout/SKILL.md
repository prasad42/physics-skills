---
name: python-layout
description: Make an existing Python repository installable without changing its behavior.
argument-hint: "[target repository path]"
disable-model-invocation: true
metadata:
  opencode/autoinvoke: false
---

Make an existing Python repository installable. Establish package metadata and
an importable package boundary while preserving runtime behavior, scientific
results, data formats, cache identity, and supported commands.

## 1. Inspect the repository

Resolve the supplied path, or the current directory, to an absolute path. Read
applicable `AGENTS.md` files and follow the repository's governance, approval,
execution, and evidence rules. Inspect Git status, Python and environment
manifests, tests, documentation, and supported commands. Record dirty paths and
preserve unrelated work. Treat commits, dependency installation, and environment
creation as separate permissions.

Inventory tracked Python files and their consumers. Trace imports and commands,
including notebooks, schedulers, and external callers documented in the
repository. Identify coupling to the repository root, current working directory,
`sys.path`, sibling imports, import-time side effects, multiprocessing,
serialized qualified names, package resources, and installed metadata.

Completion: the current package boundary, supported commands, consumers, dirty
paths, and compatibility risks are known.

## 2. Design the smallest package boundary

Prefer the smallest coherent change that makes the project installable. Reuse a
working package layout; otherwise normally place reusable code under
`src/<import_package>/` and keep command orchestration outside the package or
behind explicit entry points.

Settle:

- distribution and import-package names;
- supported Python versions, build backend, and `pyproject.toml` metadata;
- package discovery and intended public imports;
- one version source;
- runtime dependencies confirmed by imports and existing environment evidence;
- supported script, module, and console-entry-point commands;
- package-resource, repository-data, configuration, and output path rules;
- compatibility required by named consumers or persisted representations.

Use public package imports from entry points. Keep argument parsing, process-pool
creation, simulation, analysis, and plotting behind an explicit main path. Add a
compatibility wrapper only for a concrete consumer and give it a testable
removal condition.

Define validation before editing. Include metadata inspection, installation or
wheel construction, import from outside the repository, every supported entry
point, and existing deterministic tests relevant to moved code. Add path,
serialization, cache, or multiprocessing regressions for risks found during
inspection.

Completion: every affected file and consumer maps to the proposed package
boundary, and packaging, compatibility, and validation decisions are settled.

## 3. Approve the manifest

Present the design and an exact path manifest using `move`, `create`, `edit`,
`retain`, `delete after move`, `conflict`, or `skip`. Show metadata, import,
entry-point, test, and command-documentation changes. Treat dirty overlap and
unknown consumers as conflicts. Obtain explicit approval before writing.

Immediately before editing, re-read affected files and Git status. Recompute and
reapprove changed manifest items. Keep all destinations inside the confirmed
repository.

Completion: the current design and complete path manifest are approved.

## 4. Apply the package migration

Use history-preserving moves for tracked files. Apply only approved changes and
update imports, resource lookups, commands, and their documentation together.
Keep numerical methods, defaults, random behavior, schemas, caches, figures, and
scientific artifacts unchanged. Keep dependency upgrades, broad cleanup, and
unrelated formatting outside this migration.

Completion: every approved path and consumer reflects the package design, with
unrelated work and behavior preserved.

## 5. Validate installability

Before Python execution or package installation, follow the repository's
approval and environment rules and give the user the expected runtime. Use the
confirmed environment and avoid dependency resolution or upgrades unless
separately approved.

Run the approved checks, including:

- build and installed-metadata inspection;
- package import from outside the repository root;
- smoke tests for supported commands and entry points;
- relevant deterministic tests and identified compatibility regressions;
- searches for stale imports, commands, and moved paths.

Record exact commands and results where repository governance requires it.
Inspect the final diff and confirm that unrelated files and generated scientific
artifacts did not change. Commit only with explicit authority.

Completion: a clean environment can install the project, import its public
package outside the repository root, and run every supported command covered by
the approved validation plan.
