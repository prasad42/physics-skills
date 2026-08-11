# physics-skills

A small collection of reusable AI agent skills, leaning toward physics and research work. Each top-level folder is one skill, defined by its `SKILL.md` (plus any supporting files). Install a folder into your agent's skills directory or upload it to a chat surface and it becomes a `/command` you can invoke.

## The skills

| Skill | What it does | Best on |
|-------|--------------|---------|
| [grill-me](./grill-me/) † | Interviews you relentlessly about a plan or design, one question at a time, until you reach shared understanding. | CLI agent |
| [grilling](./grilling/) | Interviews across a decision tree in dependency-aware rounds. | CLI agent |
| [find-skills](./find-skills/) | Finds and evaluates installable agent skills. | CLI agent |
| [socratic-physics](./socratic-physics/) | Stress-tests a physics argument, model, or numerical protocol via systematic Socratic questioning over its dependency graph. | Either (leans Chat) |
| [handoff](./handoff/) † | Compacts the current conversation into a handoff document a fresh agent can pick up. | CLI agent |
| [lit-rev-physics](./lit-rev-physics/) | Expertise-calibrated literature review of a physics subfield: grills your field model, retrieves and snowballs a corpus via alphaXiv, then synthesizes a thematic write-up. | CLI agent |
| [paper-review](./paper-review/) | Explains a research paper at a depth calibrated per-concept by your own N/L/E self-rating. | Chat |
| [project-summary](./project-summary/) | Interviews you about a research draft to build or refresh a `project_summary.md`, plus a suggested Claude-Project custom-instructions block. | CLI agent (+ a claude.ai Project) |
| [research](./research/) | Researches a question against primary sources and saves a cited repository note. | CLI agent |
| [teach](./teach/) † | Teaches a topic statefully across sessions, using a workspace of missions, lessons, and learning records. | CLI agent |
| [writing-for-agents](./writing-for-agents/) | Guides writing and editing skills and agent instruction files. | Either |

† Copied from [mattpocock/skills](https://github.com/mattpocock/skills) (MIT). See [THIRD_PARTY_NOTICES.md](./THIRD_PARTY_NOTICES.md).

## Installing skills

A skill is just a folder containing a `SKILL.md`, so the **same folder works on every agent** — you only need to put it where your agent looks for skills.

### Option 1: Quick install (npx)

```bash
npx skills add prasad42/physics-skills
```

The [skills CLI](https://skills.sh) detects your agent (Claude Code, opencode, Codex, Cursor, etc.) and installs the skills to the right location. Run with `--list` to see available skills first, or add `--skill <name>` to install a single one.

### Option 2: Manual install (CLI agents)

Copy a skill folder into your agent's skills directory:

- Personal (available in every project):
  ```
  ~/.agents/skills/<name>/
  ```
- Project-scoped (committed with git):
  ```
  <project>/.agents/skills/<name>/
  ```

Example — install `paper-review` as a personal skill:

```bash
cp -r paper-review ~/.agents/skills/paper-review
```

Most agents also look in `.claude/skills/` and `.opencode/skills/` — use whichever matches your agent.

Invoke a skill by name with `/<skill-name>` (e.g. `/paper-review`).

### Option 3: Chat surfaces (claude.ai, etc.)

1. Zip the individual skill folder, with `SKILL.md` at the root of the archive (e.g. `paper-review.zip` containing `SKILL.md` and any supporting files).
2. In claude.ai, go to **Settings → Capabilities → Skills** and upload the zip.
3. In a chat, invoke the skill by referencing it or selecting it from the skills menu.

Exact menu labels change over time — see your chat platform's documentation for the authoritative steps.

## Chat vs. CLI agent

The "Best on" column above is a recommendation, not a hard rule — most skills technically run on either surface. The split follows what each skill needs:

- **CLI agent** for the filesystem-heavy skills — `teach`, `handoff`, `project-summary`, `grill-me`, and `lit-rev-physics` — which read or write files, maintain a workspace, or explore a codebase to answer their own questions.
- **Either** for `writing-for-agents`, a reference for agent-facing documents.
- **Chat** for the attach-and-reason skills — `paper-review` (easiest place to attach a PDF) and `socratic-physics` (pure reasoning, no files needed).

`project-summary` is a hybrid: run it in a CLI agent so it can write `project_summary.md`, then paste its suggested custom-instructions block into the matching claude.ai Project.
