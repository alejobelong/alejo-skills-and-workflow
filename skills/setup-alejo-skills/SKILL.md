---
name: setup-alejo-skills
description: Use when a repo needs Alejo skill setup, when `/setup-alejo-skills` is requested, or when Alejo skills are missing Git repo setup, Linear Project setup, AGENTS.md, docs/agents, or WORKFLOW.md.
---

# Setup Alejo Skills

Configure a repo for the Alejo skill suite. Set up Git first, then Linear. Ask only for the Git repo choice and the Linear Project choice when needed. Write a short, clear `AGENTS.md` that explains how to use the stack in this repo.

## When To Use

Run this once at the start of a repo, or anytime Alejo skills cannot find Git, Linear Project, `AGENTS.md`, `docs/agents/*`, domain docs, or `WORKFLOW.md` setup.

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
   - Replace any old setup block such as `## Agent skills`, `## Alejo Setup`, or `## Alejo Onboarding` with the current `AGENTS.md` shape.
   - `AGENTS.md` must be the short repo onboarding and source-of-truth map, not just a list of doc links.
   - Write `docs/agents/issue-tracker.md`.
   - Write `docs/agents/triage-labels.md`.
   - Write `docs/agents/domain.md`.
   - Write `docs/agents/alejo-workflow.md`.
   - Write or update root `WORKFLOW.md` for Symphony.

Use the templates in `references/`. Insert resolved repo-specific values: GitHub remote, Linear Project name and URL, Linear team, access method, and Project Document URLs when available. A resolved Linear Project is required; do not write Linear project placeholders.

## AGENTS.md Shape

Use [agents.md](./references/agents.md) as the shape for `AGENTS.md`. Replace every bracketed value before writing. If a non-required value is unknown, omit that line instead of writing a placeholder.

Keep the generated `AGENTS.md` short. It should contain:

- project title
- resolved GitHub repo
- resolved Linear Project and team
- where each artifact lives
- short skill flow
- links to `docs/agents/*` and `WORKFLOW.md`

Do not call `docs/agents/*` "Agent skills"; those are setup reference docs.

Minimal generated shape:

```md
# <Project Name>

This repo uses the Alejo skill suite.

## Alejo Setup

- GitHub: <repo URL>
- Linear Project: <project name> - <project URL>
- Linear team: <team name> (<team key>)
- Planning artifacts live in Linear Project Documents: `Q&A`, `CONTEXT.md`, `PRD`, `prototype.html`, `SAD`/`SAT`.
- Linear issues are only for vertical-slice implementation and actionable follow-ups.
- `WORKFLOW.md` is the Symphony execution contract for approved issues.
- Secret values belong in Doppler, never in repo files or Linear issue bodies.

## Skill Flow

1. `$setup-alejo-skills`: rerun only when Git, Linear, or setup docs are missing.
2. `$alejo-questions`: clarify domain language, product questions, and trade-offs.
3. `$alejo-prd`: publish product intent and user value to Linear.
4. `$alejo-prototype`: publish UI evidence or a throwaway HTML prototype when useful.
5. `$alejo-sad`: publish architecture for non-trivial implementation.
6. `$alejo-issues`: create behavior-first vertical-slice Linear issues.
7. `$alejo-secrets`: provide Doppler setup steps for required secrets.
8. `$alejo-consistency-propagation`: reconcile changed artifacts and issue contracts.
9. `$alejo-run`: preflight ready issues and hand approved work to Symphony.

## Repo References

- `docs/agents/issue-tracker.md`: Linear Project, Project Documents, issue contract, Symphony handoff.
- `docs/agents/triage-labels.md`: Linear statuses and issue labels.
- `docs/agents/domain.md`: glossary, context map, and ADR conventions.
- `docs/agents/alejo-workflow.md`: planning-to-Symphony workflow.
- `WORKFLOW.md`: Symphony execution workflow.
```

## Finish

Report the files written, Git remote used or created, and Linear Project used or created.

End with this onboarding:

```md
## Alejo Onboarding

Use Alejo in this order for new software work:

1. `$setup-alejo-skills`
   Run once per repo. It connects Git, creates or connects the Linear Project, writes `AGENTS.md`, `docs/agents/*`, and `WORKFLOW.md`.

2. `$alejo-questions`
   Use when the idea, domain language, scope, or decisions need sharpening. Output: `Q&A` and `CONTEXT.md` in the Linear Project.

3. `$alejo-prd`
   Use when product intent is clear enough to describe user value. Output: `PRD` in the Linear Project.

4. `$alejo-prototype`
   Use when UI references, screenshots, or a throwaway HTML prototype would reduce uncertainty. Output: `prototype.html` in the Linear Project.

5. `$alejo-sad`
   Use before non-trivial implementation. It turns PRD/prototype/context into architecture. Output: `SAD` or `SAT` in the Linear Project.

6. `$alejo-issues`
   Use after PRD/SAD to create behavior-first vertical-slice Linear issues. These issues are the implementation contracts.

7. `$alejo-secrets`
   Use when issues need API keys, credentials, tokens, or env vars. Output: Doppler setup steps in chat; never secret values in files.

8. `$alejo-consistency-propagation`
   Use after any PRD, SAD/SAT, Q&A, context, prototype, issue, secret-name, or `WORKFLOW.md` change. It keeps Linear Project Documents and issues aligned.

9. `$alejo-run`
   Use only when ready Linear issues should go to Symphony. It preflights issue contracts, asks for approval, and moves approved issues into the Symphony execution lane.

If humans will implement manually, stop after `$alejo-issues` plus any needed `$alejo-secrets`. If Symphony should implement, continue to `$alejo-run`.
```

## Templates

- `references/issue-tracker-linear.md`
- `references/triage-labels.md`
- `references/domain.md`
- `references/alejo-workflow.md`
- `references/symphony-workflow.md`
- `references/agents.md`
