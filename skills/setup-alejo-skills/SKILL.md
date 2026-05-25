---
name: setup-alejo-skills
description: Use when a repo needs one-shot Linear-default configuration for Alejo skills, when `/setup-alejo-skills` is requested, or when Alejo PRD/Issues are missing issue tracker, triage label, domain doc, Linear Project document, or artifact-location context.
---

# Setup Alejo Skills

Scaffold the per-repo configuration expected by the Alejo skill suite. This is an autopilot setup skill: explore, infer, apply the recommended Linear defaults, then write. Do not ask for confirmation before using the Linear defaults.

## Process

### 1. Explore

Read, do not assume:

- `git remote -v` and `.git/config` for GitHub/GitLab/other remotes, plus any Linear workspace/team/project hints in docs or environment.
- Root `AGENTS.md` and `CLAUDE.md`, especially any existing `## Agent skills` block.
- Root `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/adr/`, and context-local `docs/adr/`.
- `docs/agents/`, `docs/questions/`, `docs/prototypes/`, `docs/architecture/`, Doppler configuration hints, and `.scratch/prototypes/`.
- Existing Linear workspace, team, project, Project Documents, workflow statuses, and issue labels if Linear tooling is available and safe to query.

### 2. Apply Linear Defaults

Use Linear unless the user explicitly asks for another tracker or the repo already has unambiguous non-Linear Alejo instructions. Do not ask the user to choose the issue tracker, status mapping, label set, domain-doc mode, artifact paths, or Linear Project document policy.

Recommended Linear defaults:

- Linear Projects are the planning container for product work.
- Linear Project Documents/Resources are the canonical home for Alejo planning artifacts: `PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, and `prototype.html`.
- Linear issues are only for vertical-slice implementation work and actionable follow-ups. Do not create PRD, SAD/SAT, Q&A, context, or prototype issues.
- Workflow statuses carry readiness/execution: `Needs Triage`, `Needs Info`, `Ready for Human`, `Ready for Agent`, `Night Shift Queued`, `In Night Shift`, `Done`, `Won't Fix`.
- Labels classify issue type/surface only: `vertical-slice`, `hitl`, `sad-follow-up`, `surface:*`, and `secrets-required`.
- Domain docs use a single root `CONTEXT.md` unless a repo already has `CONTEXT-MAP.md` or obvious multiple bounded contexts.
- Local docs and `.scratch/prototypes/` may be temporary working copies, but the Linear Project Documents are the published source of truth for Alejo artifacts.

If Linear workspace/team/project details are not discoverable, still write the Alejo setup files with `TODO: fill Linear ...` placeholders and report those placeholders at the end. Do not block setup to ask for them.

### 3. Write Directly

Do not show a draft before editing. Use templates from `references/` and write:

- The `## Agent skills` block for `AGENTS.md` or `CLAUDE.md`.
- `docs/agents/issue-tracker.md`.
- `docs/agents/triage-labels.md`.
- `docs/agents/domain.md`.
- `docs/agents/alejo-workflow.md`.

Pick the file to edit:

- If `AGENTS.md` exists, edit it.
- Else if `CLAUDE.md` exists, edit it.
- If neither exists, create `AGENTS.md`.

Update an existing `## Agent skills` block in place. Do not duplicate it or overwrite surrounding user edits.

The block:

```md
## Agent skills

### Issue tracker
{one-line summary}. See `docs/agents/issue-tracker.md`.

### Triage labels
{one-line summary}. See `docs/agents/triage-labels.md`.

### Domain docs
{single-context or multi-context summary}. See `docs/agents/domain.md`.

### Alejo workflow
{one-line summary of Linear Project document artifact storage, Linear issue slice storage, and skill flow}. See `docs/agents/alejo-workflow.md`.
```

### 4. Done

Report the files written and which Alejo skills now read them: `alejo-questions`, `alejo-prd`, `alejo-prototype`, `alejo-sad`, `alejo-issues`, `alejo-secrets`, `alejo-run`, and `alejo-consistency-propagation`.

End with a short Alejo onboarding for building software. Derive it from the actual installed Alejo skills, not only from `docs/agents/alejo-workflow.md`, because the repo workflow doc may be stale.

Use this shape:

```md
## Alejo Onboarding

Expected path for new software work:
1. Required once per repo: `$setup-alejo-skills`.
2. Usually required for new product work: `$alejo-questions` to resolve domain language, decisions, ADRs, and Q&A, then publish `Q&A` and `CONTEXT.md` to the Linear Project.
3. Required for agent-ready product work: `$alejo-prd` to publish product intent as the Linear Project `PRD` document.
4. Optional after PRD, before SAD: `$alejo-prototype` when reference-driven UI evidence or a small disposable experiment can reduce uncertainty; publish the resulting `prototype.html` to the Linear Project.
5. Required for non-trivial implementation: `$alejo-sad` to turn requirements and prototype evidence into architecture, then publish `SAD`/`SAT` to the Linear Project.
6. Required before implementation agents: `$alejo-issues` to create behavior-first vertical slices.
7. Conditional: `$alejo-secrets` when slices need credentials, APIs, tokens, or env vars; it outputs a Doppler-only terminal guide and never writes secret values. If confirmed secret names change after issues exist, propagate the name-only change back to Linear issues before `$alejo-run`.
8. Anytime during day shift: `$alejo-consistency-propagation` after any artifact changes, contradictions, removals, secret-name changes, or scope drift. This is a day-shift skill only.
9. Optional autonomous execution path: `$alejo-run` after ready Linear issues; it preflights issue contracts, asks for approval, then moves approved issues into Symphony's execution lane.

If the user will implement manually, stop after approved issues plus any needed Doppler setup. If the user wants autonomous execution, continue through Alejo Run. Do not create a separate plan artifact. Night-shift skills for Symphony coding/testing threads are not defined yet and will be designed later.
```

## Templates

- `references/issue-tracker-github.md`
- `references/issue-tracker-gitlab.md`
- `references/issue-tracker-linear.md`
- `references/issue-tracker-local.md`
- `references/triage-labels.md`
- `references/domain.md`
- `references/alejo-workflow.md`
