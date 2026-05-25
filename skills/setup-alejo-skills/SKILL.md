---
name: setup-alejo-skills
description: Use when a repo needs configuration for Alejo skills, when `/setup-alejo-skills` is requested, or when Alejo PRD/Issues are missing issue tracker, triage label, domain doc, or artifact-location context.
---

# Setup Alejo Skills

Scaffold the per-repo configuration expected by the Alejo skill suite. This is prompt-driven: explore, present findings, confirm with the user, then write.

## Process

### 1. Explore

Read, do not assume:

- `git remote -v` and `.git/config` for GitHub/GitLab/other remotes, plus any Linear workspace/team/project hints in docs or environment.
- Root `AGENTS.md` and `CLAUDE.md`, especially any existing `## Agent skills` block.
- Root `CONTEXT.md`, `CONTEXT-MAP.md`, `docs/adr/`, and context-local `docs/adr/`.
- `docs/agents/`, `docs/questions/`, `docs/prototypes/`, `docs/architecture/`, Doppler configuration hints, and `.scratch/prototypes/`.
- Existing issue labels if the tracker CLI is available and safe to query.

### 2. Confirm Decisions

Summarize what exists and what is missing. Walk the user through these decisions one at a time with a short explainer, recommendation, and choices:

1. Issue tracker: GitHub, GitLab, Linear, local markdown under `.scratch/`, or other.
2. Triage/status mapping: map canonical readiness roles to actual tracker workflow statuses or labels. For Linear, recommend workflow statuses for readiness/execution (`Needs Triage`, `Needs Info`, `Ready for Human`, `Ready for Agent`, `Night Shift Queued`, `In Night Shift`, `Done`, `Won't Fix`) and labels only for issue classification (`vertical-slice`, `hitl`, `sad-follow-up`, `surface:*`, `secrets-required`). Do not recommend `prd` or `sad` issue labels when PRDs/SADs live as Projects/docs rather than issues.
3. Domain docs: single-context or multi-context.
4. Alejo artifact paths: recommend the defaults unless the repo already has a better convention.

### 3. Draft

Show the exact draft before editing:

- The `## Agent skills` block for `AGENTS.md` or `CLAUDE.md`.
- `docs/agents/issue-tracker.md`.
- `docs/agents/triage-labels.md`.
- `docs/agents/domain.md`.
- `docs/agents/alejo-workflow.md`.

Use templates from `references/`. For Linear, ask for workspace/team/project only if they are not already clear. For other issue trackers, write `issue-tracker.md` from the user's prose.

### 4. Write

Pick the file to edit:

- If `AGENTS.md` exists, edit it.
- Else if `CLAUDE.md` exists, edit it.
- If neither exists, ask which one to create; recommend `AGENTS.md` for Codex.

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
{one-line summary of artifact paths and skill flow}. See `docs/agents/alejo-workflow.md`.
```

### 5. Done

Report the files written and which Alejo skills now read them: `alejo-questions`, `alejo-prd`, `alejo-prototype`, `alejo-sad`, `alejo-issues`, `alejo-secrets`, `alejo-run`, and `alejo-consistency-propagation`.

End with a short Alejo onboarding for building software. Derive it from the actual installed Alejo skills, not only from `docs/agents/alejo-workflow.md`, because the repo workflow doc may be stale.

Use this shape:

```md
## Alejo Onboarding

Expected path for new software work:
1. Required once per repo: `$setup-alejo-skills`.
2. Usually required for new product work: `$alejo-questions` to resolve domain language, decisions, ADRs, and Q&A.
3. Required for agent-ready product work: `$alejo-prd` to publish product intent to a Linear Project.
4. Optional after PRD, before SAD: `$alejo-prototype` when reference-driven UI evidence or a small disposable experiment can reduce uncertainty.
5. Required for non-trivial implementation: `$alejo-sad` to turn requirements and prototype evidence into architecture.
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
