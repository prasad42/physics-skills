---
name: workflow
description: Choose the next workflow for a repository task.
metadata:
  opencode/autoinvoke: false
---

# Workflow router

Use only the context supplied by the user; make one routing decision, then stop.

- New or ungoverned research repository, or an adoption audit: recommend `@research-init`.
- Existing Python repository that must become installable: recommend `@python-layout`.
- Ordinary scientific implementation or analysis: recommend the repository Goal loop.
- Manuscript evidence reconciliation: recommend `@to-draft`.
- Session continuation: recommend `@handoff` when available.

Tell the user the recommended next invocation and give a one-sentence reason. If the supplied context cannot distinguish branches, ask one concise clarifying question instead. Remain read-only: perform no inspection, edits, commands, child-skill invocations, or authority claims.

Completion criterion: exactly one recommendation with one reason, or exactly one clarifying question, is returned and no work is performed.
