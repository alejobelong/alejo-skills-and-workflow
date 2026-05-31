---
name: setup-alejo-skills
description: Use when a repo needs Alejo skill setup, when `/setup-alejo-skills` is requested, or when Alejo skills are missing Git repo setup, Linear Project setup, or Linear Project Documents for AGENTS.md, issue-tracker.md, triage-labels.md, alejo-workflow.md, WORKFLOW.md, and Alejo XML artifacts.
---

# Setup Alejo Skills

Configure a repo for the Alejo skill suite. Set up Git first, then Linear, then publish the setup and workflow documents into Linear Project Documents. Do not maintain local copies of Alejo setup docs.

## When To Use

Run this once at the start of a repo, or anytime Alejo skills cannot find Git, a Linear Project, required Linear Project Documents, or the Symphony workflow.

## Workflow

1. Explore the repo and tools:
   - `git status --short --branch`
   - `git remote -v` and `.git/config`
   - `gh auth status` when GitHub setup is needed
   - existing `AGENTS.md`, `CLAUDE.md`, `WORKFLOW.md`, and `docs/agents/*` only to migrate old local setup docs into Linear
   - `CONTEXT.xml`, `CONTEXT-MAP.xml`, and `docs/adr/`
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

   - On confirmation, initialize Git if needed, create the remote repo with the active GitHub account, set `origin`, use `main`, and push after setup is complete.

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
   - If Codex has no Linear write access, stop and say Linear access must be connected before setup can finish. Do not fall back to local placeholder files.

4. Publish Linear Project Documents.
   - Required setup documents:
     - `AGENTS.md`
     - `issue-tracker.md`
     - `triage-labels.md`
     - `alejo-workflow.md`
     - `WORKFLOW.md`
   - Required planning documents, created later by the relevant skills when content exists:
     - `Q&A.xml`
     - `CONTEXT.xml`
     - `PRD.xml`
     - `prototype.xml`
     - `SAD.xml` or `SAT.xml`
   - Use the templates in `references/` and insert resolved repo-specific values: GitHub remote, Linear Project name and URL, Linear team, access method, and Project Document URLs when available.
   - Create or update the documents in Linear Project Documents only. Do not write `AGENTS.md`, `docs/agents/*`, or `WORKFLOW.md` into the repo as local copies.
   - If old local generated setup docs already exist, migrate any useful content into the Linear Project Documents, then remove the local generated copies. If a local file may contain human-authored content unrelated to Alejo setup, ask before deleting it.
   - A resolved Linear Project is required. Do not write Linear project placeholders.

5. Apply these defaults:
   - Linear Project Documents hold all Alejo setup docs, workflow docs, and planning artifacts.
   - Linear issues hold only vertical slices and actionable follow-ups.
   - Readiness/execution use Linear workflow statuses: `Needs Triage`, `Needs Info`, `Ready for Agent`, `Night Shift Queued`, `In Night Shift`, `Done`, `Won't Fix`.
   - Labels classify issues only: `vertical-slice`, `sad-follow-up`, `surface:*`, `secrets-required`.
   - Use one root `CONTEXT.xml` Project Document unless the repo already has a `CONTEXT-MAP.xml` pattern.
   - Secret values belong in Doppler, never in repo files, Linear docs, or Linear issue bodies.

## Document Shapes

Use these bundled templates as the source text for Linear Project Documents:

- `references/agents.md` -> `AGENTS.md`
- `references/issue-tracker-linear.md` -> `issue-tracker.md`
- `references/triage-labels.md` -> `triage-labels.md`
- `references/alejo-workflow.md` -> `alejo-workflow.md`
- `references/symphony-workflow.md` -> `WORKFLOW.md`

`AGENTS.md` is the repo onboarding and source-of-truth map, but it lives in Linear. It must point every Alejo skill to Linear Project Documents, Linear issues, GitHub, and Doppler instead of local setup docs.

## Finish

Report:

- Git remote used or created.
- Linear Project used or created.
- Linear Project Documents created or updated.
- Local generated setup docs removed, if any.
- Any local docs left in place because they appeared human-authored and need user review.

End with this onboarding:

```md
## Alejo Onboarding

Use Alejo in this order for new software work:

1. `$setup-alejo-skills`
   Run once per repo. It connects Git, creates or connects the Linear Project, and publishes AGENTS.md, issue-tracker.md, triage-labels.md, alejo-workflow.md, and WORKFLOW.md as Linear Project Documents.

2. `$alejo-questions`
   Use when the idea, domain language, scope, or decisions need sharpening. Output: Q&A.xml and CONTEXT.xml in the Linear Project.

3. `$alejo-prd`
   Use when product intent is clear enough to describe user value. Output: PRD.xml in the Linear Project.

4. `$alejo-prototype`
   Use when UI references, screenshots, or a throwaway HTML prototype would reduce uncertainty. Output: prototype.xml in the Linear Project.

5. `$alejo-sad`
   Use before non-trivial implementation. It turns PRD/prototype/context into architecture. Output: SAD.xml or SAT.xml in the Linear Project.

6. `$alejo-issues`
   Use after PRD/SAD to create behavior-first vertical-slice Linear issues. These issues are the implementation contracts.

7. `$alejo-secrets`
   Use when issues need API keys, credentials, tokens, provider resources, or env vars. Output: Doppler setup or recovery steps in chat; never secret values in files.

8. `$alejo-consistency-propagation`
   Use after any Linear Project Document, issue, secret-name, or workflow change. It keeps Linear Project Documents and issues aligned.

9. `$alejo-run`
   Use only when ready Linear issues should go to Symphony. It preflights issue contracts, moves passing issues into the Symphony execution lane, launches the documented workflow, and iterates without approval prompts.

10. `$alejo-review`
   Use after implementation to compare the built codebase against Linear Project Documents and issues. Output: a prioritized gap list for a fully running system.

If humans will implement manually, stop after `$alejo-issues` plus any needed `$alejo-secrets`. If Symphony should implement, continue to `$alejo-run`.
```
