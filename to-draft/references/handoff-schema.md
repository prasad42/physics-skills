# Draft handoff schema

Use this reference after the main workflow reaches **6. Write the handoff**. It applies to every handoff, whether the review is full or incremental. No section or field is optional because of the review mode.

Begin with compact YAML frontmatter containing `baseline_schema: 2`, `baseline_complete`, `created`, `source_root`, `source_commit`, `proposal_path`, `proposal_sha256`, `proposal_resolved_path`, `proposal_resolved_sha256`, `draft_target`, `receiving_task`, and `review_mode`. `proposal_path` identifies the authoritative entry, normally `notes/proposal.md`; the resolved fields identify its final target and equal the entry fields when no pointer is used. Set `baseline_complete: true` only when the body contains every baseline field required by the workflow; otherwise set it to `false`. Quote path and task values. These fields support metadata-only baseline discovery.

Use this body structure:

1. **Title and provenance**: creation timestamp with timezone; source repository path; full and short commit; commit date and subject; exact dirty state; proposal authority-entry path and hash; resolved proposal-target path and hash; draft path or destination; draft Git stamp when available. Mark dirty and untracked evidence provisional.
2. **Review baseline and delta**: full or incremental mode; compatible handoff path or full-review reason; prior and current source, proposal-entry, proposal-target, and draft stamps; exact added, modified, renamed, deleted, dirty, and untracked paths; affected claims; and claims carried forward. Record SHA-256 or a stable content-addressed identifier for every dependency not captured by the source commit and for every applicable policy file. Record the complete draft source, bibliography, and referenced asset input path set, identify which inputs the draft commit captures, and give SHA-256 for every uncaptured input.
3. **Receiving task and boundaries**: the exact draft objective, allowed workspace, and read/write boundary.
4. **Prioritized checklist**: flat Markdown checkboxes tagged `[AUTHOR]`, `[DRAFT]`, `[SOURCE]`, `[VERIFY]`, or `[BLOCKED]`. State dependencies and acceptance criteria.
5. **Executive editorial decisions**: concise confirmed outcomes.
6. **Claim ledger**: for every proposal and relevant draft claim, give disposition, draft destination, evidence class, exact scoped wording guidance, strongest repository evidence, literature support, caveats, conflicts, and its complete transitive dependency paths. Include runlogs, tests, data, artifacts, generators, scripts, code, manifests, analytical assumptions, and policy files that can change the conclusion. This ledger is the dependency map for the next invocation.
7. **Literature and novelty audit**: claim-to-source table stating what each primary source supports, what it does not support, whether the draft already cites it, its stable DOI or URL, and retrieval date. Record the coverage-check date and search scope for each literature-dependent claim so a later invocation can apply the freshness bounds. Add BibTeX-ready entries only for recommended additions.
8. **Section-by-section patch specification**: exact sections to add, revise, move, or remove. Supply draft-ready wording only where wording itself was confirmed during grilling.
9. **Figure and table matrix**: classify each item as **Ready**, **Needs editorial assembly**, **Needs source generation**, **Needs new evidence**, or **Omit/defer**. For ready items, provide exact artifact path, provenance, supported caption claims, and destination. For other items, provide a concrete task, workspace, dependencies, and acceptance criterion. Main-text placement requires an explicit editorial decision.
10. **Appendix and supplement decisions**.
11. **Omissions, inconclusive results, and future work**.
12. **Contradictions and unresolved risks**.
13. **Notes consulted**: include only materially important notes, with path, role, affected claims, provenance quality, and current status.
14. **Artifact manifest**: exact repository-relative paths and associated runlog goals or commits.
15. **Verification checklist**: checks the receiving agent or author must perform in the draft.
16. **First actions**: an ordered, minimal starting sequence for the receiving agent.

The handoff is cumulative and self-contained. Revalidate conclusions affected by the delta, carry forward unchanged conclusions with their provenance, and restate the complete current result so the reader never has to reconstruct it from earlier handoffs.
