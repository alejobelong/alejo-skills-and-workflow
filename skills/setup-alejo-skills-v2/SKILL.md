---
name: setup-alejo-skills-v2
description: Compact Alejo Setup v2 workflow for configuring a repo with GitHub, a Linear Project, v2 Alejo Linear Project Documents, Doppler-safe defaults, and a repo-owned Symphony WORKFLOW.md without local setup-doc mirrors. Use when a repo should be prepared for the Alejo v2 skill stack.
---

# Setup Alejo Skills v2

Set up a repo for the Alejo v2 stack. Resolve Git, resolve Linear, publish setup documents to Linear Project Documents, write the repo-owned `WORKFLOW.md`, and mirror that workflow to Linear.

Do not create local canonical planning files. Do not create local `AGENTS.md` or `docs/agents/*` setup mirrors. The only required repo setup file is `WORKFLOW.md`, because Symphony consumes it.

## Use When

- A repo is starting the Alejo v2 flow.
- Alejo v2 skills cannot find Git, Linear Project Documents, Linear lanes, Doppler expectations, or `WORKFLOW.md`.
- A repo still has old generated local Alejo setup docs that should be migrated to Linear.

## Process

1. Inspect the repo and tools:
   - `git status --short --branch`, `git remote -v`, and `.git/config`;
   - `gh auth status` if GitHub setup is needed;
   - existing `WORKFLOW.md`, `AGENTS.md`, `CLAUDE.md`, and `docs/agents/*`;
   - Linear connector/MCP, Linear CLI, or Linear API/SDK access;
   - existing Linear project links in repo instructions, issues, branches, or safe tool output.

2. Resolve GitHub.
   - Use an existing usable remote when present.
   - If no usable remote exists, ask whether to use an existing repo or create a new one.
   - For an existing repo, ask for the remote URL only if it is not discoverable.
   - For a new repo, suggest a lowercase hyphenated name from the folder/project name and ask the user to confirm before creating it.
   - On confirmation, initialize Git if needed, create the GitHub repo, set `origin`, use `main`, and push after setup is complete.

3. Resolve the Linear Project.
   - Use an existing discoverable Linear Project when present.
   - If none is discoverable, ask whether to use an existing Linear Project or create a new one.
   - For an existing project, ask for the project URL only if tooling cannot resolve it.
   - For a new project, suggest a clear project name from the repo/folder and ask the user to confirm before creating it.
   - Prefer the Linear connector/MCP. Otherwise use a Linear CLI if installed, then the Linear API/SDK.
   - If no Linear write access is available, stop. Do not create local placeholder docs.

4. Publish Linear Project Documents.
   - Create or update these setup documents in Linear only:
     - `AGENTS.md`
     - `issue-tracker.md`
     - `triage-labels.md`
     - `alejo-workflow.md`
     - `WORKFLOW.md` mirror
   - Use the bundled templates in `references/` and replace repo/project values.
   - Preserve useful old generated local setup content by migrating it into Linear, then remove generated local setup copies. If a local file appears human-authored or unrelated to Alejo setup, leave it and report it for review.

5. Write the repo `WORKFLOW.md`.
   - Use `references/workflow-template.md` as the default Symphony contract.
   - If a repo `WORKFLOW.md` already exists, compare it before overwriting. Preserve intentional repo-specific runtime commands, project slug, lanes, and artifact sinks unless they conflict with Alejo v2.
   - Mirror the exact final repo `WORKFLOW.md` to the Linear Project Document named `WORKFLOW.md`.

6. Apply Alejo v2 defaults.
   - Linear Project Documents own setup docs and planning artifacts.
   - Repo `WORKFLOW.md` owns the Symphony runtime contract; the Linear `WORKFLOW.md` document is a mirror.
   - Linear issues are only vertical-slice implementation contracts and actionable follow-ups.
   - Doppler owns secret values. Linear and repo files may contain secret names only.
   - Statuses: `Needs Triage`, `Needs Info`, `Ready for Human`, `Ready for Agent`, `Night Shift Queued`, `In Night Shift`, `Done`, `Won't Fix`.
   - Labels: `vertical-slice`, `hitl`, `sad-follow-up`, `surface:api`, `surface:ui`, `surface:cli`, `surface:mcp`, `secrets-required`.
   - Only humans move issues to `Done`; `alejo-run-v2` leaves clean work in `Ready for Human`.

## Document Templates

- `references/agents.md` -> Linear `AGENTS.md`
- `references/issue-tracker-linear.md` -> Linear `issue-tracker.md`
- `references/triage-labels.md` -> Linear `triage-labels.md`
- `references/alejo-workflow.md` -> Linear `alejo-workflow.md`
- `references/workflow-template.md` -> repo `WORKFLOW.md` and Linear `WORKFLOW.md`

Planning documents are created later by their skills: `Q&A.xml`, `CONTEXT.xml`, `PRD.xml`, `prototype.xml`, `SAD.xml`, ADR XML, and vertical-slice Linear issues.

## Finish

Report the Git remote, Linear Project, Linear documents created or updated, repo `WORKFLOW.md` result, local generated setup docs removed, and any blockers.

End with this compact onboarding:

```md
## Alejo v2 Onboarding

1. `$setup-alejo-skills-v2` connects GitHub, resolves or creates the Linear Project, publishes setup docs to Linear, writes repo `WORKFLOW.md`, and mirrors it to Linear.
2. `$alejo-questions-v2` clarifies product experience, value proposition, domain language, and decisions. Output: `Q&A.xml`, `CONTEXT.xml`, and ADR XML when needed.
3. `$alejo-prd-v2` turns the latest Q&A into `PRD.xml`.
4. `$alejo-prototype` creates UI evidence when visuals reduce uncertainty. Output: `prototype.xml`.
5. `$alejo-sad-v2` creates `SAD.xml` from PRD, Q&A, CONTEXT, prototype evidence, ADRs, providers, and repo architecture.
6. `$alejo-issues-v2` creates self-contained production-ready vertical-slice Linear issues with XML run contracts.
7. `$alejo-secrets-v2` resolves provider resources and Doppler names without exposing secret values.
8. `$alejo-consistency-propagation-v2` reads selected documents line by line, classifies drift, and propagates approved changes.
9. `$alejo-run-v2` drives ready issues through Symphony, BDD verification, and fresh `alejo-review`; clean work stops in `Ready for Human`.
10. `$alejo-review` contrarian-checks the built system against the planning stack before a human moves work to `Done`.
```
