---
name: setup-alejo-skills
description: Use when a repo needs Alejo skill setup, when `/setup-alejo-skills` is requested, or when Alejo skills are missing Git repo setup, Linear Project setup, tracker, triage, domain, or workflow docs.
---

# Setup Alejo Skills

Configure a repo for the Alejo skill suite. Set up Git first, then Linear. Ask only for the Git repo choice and the Linear Project choice when needed.

## Workflow

1. Explore the repo:
   - `git status --short --branch`
   - `git remote -v` and `.git/config`
   - `gh auth status` when GitHub setup is needed
   - `AGENTS.md` or `CLAUDE.md`
   - `docs/agents/`
   - `CONTEXT.md`, `CONTEXT-MAP.md`, and `docs/adr/`
   - Linear connector/MCP, installed Linear CLI, or Linear API/SDK access
   - existing Linear URLs or safe Linear tooling output

2. Resolve the Git repo.
   - If a usable Git remote already exists, use it.
   - If the repo has no usable remote, ask exactly:

```text
Should I use an existing Git repo or create a new one?
```

   - If using an existing repo, ask for the Git remote URL if it is not already discoverable.
   - If creating a new repo, suggest a lowercase hyphenated name from the project/folder name and ask exactly:

```text
I suggest `<repo-name>`. Should I create this GitHub repo?
```

   - On confirmation, initialize Git if needed, create the remote repo with the active GitHub account, set `origin`, use `main`, and push after setup files are written.

3. Resolve the Linear Project.
   - If a Linear Project is already discoverable, use it.
   - If no project is discoverable, ask exactly:

```text
Should I use an existing Linear Project or create a new one?
```

   - If using an existing project, ask for the Linear Project URL if it is not already discoverable.
   - If creating a new project, suggest a clear project name from the Git repo/folder name and ask exactly:

```text
I suggest `<project-name>`. Should I create this Linear Project?
```

   - Use the discovered/default Linear team. If no team is discoverable, ask which Linear team should own the project.
   - On confirmation, create the Linear Project from Codex. Prefer a Linear connector/MCP. Otherwise use an installed Linear CLI if it supports project creation. Otherwise use Linear's API/SDK.
   - If Codex has no Linear write access, stop and say Linear access must be connected before setup can finish. Do not fall back to placeholders.

4. Apply these defaults:
   - Linear Project Documents hold `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, and `prototype.html`.
   - Linear issues hold only vertical slices and actionable follow-ups.
   - Readiness/execution use Linear workflow statuses: `Needs Triage`, `Needs Info`, `Ready for Human`, `Ready for Agent`, `Night Shift Queued`, `In Night Shift`, `Done`, `Won't Fix`.
   - Labels classify issues only: `vertical-slice`, `hitl`, `sad-follow-up`, `surface:*`, `secrets-required`.
   - Use one root `CONTEXT.md` unless the repo already has `CONTEXT-MAP.md`.

5. Write the setup files directly:
   - Update `AGENTS.md`; if absent, update `CLAUDE.md`; if both are absent, create `AGENTS.md`.
   - Update one existing `## Agent skills` block in place, or add it if missing.
   - Write `docs/agents/issue-tracker.md`.
   - Write `docs/agents/triage-labels.md`.
   - Write `docs/agents/domain.md`.
   - Write `docs/agents/alejo-workflow.md`.
   - Write or update root `WORKFLOW.md` for Symphony.

Use the templates in `references/`. A resolved Linear Project is required; do not write Linear project placeholders.

## Agent Skills Block

```md
## Agent skills

### Issue tracker
Linear Project and issue setup. See `docs/agents/issue-tracker.md`.

### Triage labels
Linear workflow statuses and issue labels. See `docs/agents/triage-labels.md`.

### Domain docs
Domain glossary setup. See `docs/agents/domain.md`.

### Alejo workflow
Linear Project Documents for planning artifacts; Linear issues for slices. See `docs/agents/alejo-workflow.md`.
```

## Finish

Report the files written, Git remote used or created, and Linear Project used or created.

End with this short onboarding:

```md
## Alejo Onboarding

1. `$setup-alejo-skills` configures the repo.
2. `$alejo-questions` resolves domain language and Q&A.
3. `$alejo-prd` publishes `PRD` to the Linear Project.
4. `$alejo-prototype` publishes `prototype.html` when UI evidence helps.
5. `$alejo-sad` publishes `SAD`/`SAT`.
6. `$alejo-issues` creates vertical-slice Linear issues.
7. `$alejo-secrets` gives Doppler setup steps when needed.
8. `$alejo-consistency-propagation` keeps artifacts and issues aligned.
9. `$alejo-run` moves approved ready issues into the Symphony execution lane.
```

## Templates

- `references/issue-tracker-linear.md`
- `references/triage-labels.md`
- `references/domain.md`
- `references/alejo-workflow.md`
- `references/symphony-workflow.md`
