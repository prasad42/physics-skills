---
name: socratic-physics
description: Stress-test a physics argument, model, or protocol by systematic Socratic questioning. Use when the user invokes grill-me for physics topics; when they ask to grill, interrogate, cross-examine, or stress-test a physics argument, draft, note, or idea; or when a shared understanding for a physics argument or project is needed.
---

Interrogate this physics argument, model, or numerical protocol by systematic Socratic questioning. Treat the argument as a dependency graph over its nodes — definitions, assumptions, derivation steps, approximation regimes, observable consequences, failure modes — where edges are genuine logical or physical dependencies (e.g. an approximation regime constrains which derivation steps are valid; a failure mode may force revision of an upstream assumption). Identify the dependencies between nodes and resolve each blocker before its dependents. Do not force a linear order where the structure is a DAG.

Ask one question at a time and wait for a response before continuing. For each question, state your own provisional answer — the physical assumption you would make, the regime you would assert, or the approximation you would invoke — and explain briefly why.

Push on:
- unstated limits: thermodynamic, weak-coupling, Markov/Born, large-N, continuum, etc.;
- operator-ordering and normal-ordering choices;
- averaging vs. trajectory-level claims; ensemble vs. single-microstate statements; ergodicity assumptions;
- boundary conditions and their effect on bulk claims;
- symmetry, gauge, and basis choices;
- regularization/renormalization scheme dependence;
- finite-size artifacts and scaling assumptions;
- any step where a physicist might write "it can be shown."

When an answer reveals an inconsistency mid-tree, flag it immediately, branch to resolve it, and only then return to the interrupted node. Do not defer inconsistencies to a final consolidation.

If a question can be answered by inspecting the codebase, do that instead of asking.

Continue until every leaf node of the dependency graph has been resolved or explicitly deferred by the user. State when this condition is met.
