---
name: alejo-consistency-propagation
description: Reconcile Alejo planning artifacts after any Context XML, Q&A XML, PRD project, prototype XML, SAD XML, ADR XML, WORKFLOW, secrets, or vertical-slice issue changes. Use when the user asks to run consistency propagation, verify completeness across Alejo documents, propagate a changed requirement or decision through the planning stack, or resolve differences between Context/Q&A/PRD/SAD/WORKFLOW/issues with human-approved choices.
---

# Alejo Consistency Propagation

Keep Alejo artifacts consistent by finding differences, asking the human what to do one difference at a time, and applying only approved changes.

## Source Order

Check artifacts in this order:

1. Foundation: current conversation, Linear Project Documents `CONTEXT.xml` and `Q&A.xml`, local `CONTEXT.xml`, ADR XML files in `docs/adr/`, and local resolved Q&A XML from `docs/questions/`.
2. Product: Linear Project document `PRD.xml` from the configured tracker/workspace.
3. Prototype: Linear Project document `prototype.xml` plus local prototype reports in `docs/prototypes/` when present.
4. Architecture: Linear Project document `SAD.xml`/`SAT.xml` plus local SAD mirrors in `docs/architecture/` when present.
5. Delivery: vertical-slice issues from the configured issue tracker.
6. Execution: repo `WORKFLOW.md`, `alejo-run` preflight expectations, and Symphony lane/readiness mappings.

Use repo instructions from `AGENTS.md` and `docs/agents/`. If they are missing or unclear, run or request `/setup-alejo-skills`.

## Workflow

### 1. Gather artifacts

Start from the changed artifact named by the user. If none is named, infer likely changes from the conversation, `git status`, modified Alejo docs, and relevant issue updates.

Read only the artifacts needed to compare the affected chain from Context/Q&A XML through PRD XML, prototype XML, SAD/SAT XML, delivery issues, and `WORKFLOW.md`.

### 2. Extract claims

List the meaningful claims from each artifact: domain language, product behavior, scope boundaries, architecture decisions, quality attributes, security or operations expectations, ADR constraints, issue coverage, acceptance criteria, verification surface, preconditions, dependencies, Doppler secret refs, BDD budget, readiness label/status, and slice-owned code organization.

Track each claim's source, artifact type, intended destinations, and whether it is present, missing, stale, contradicted, removed, or out of place.

### 3. Classify differences

Classify each found difference before asking the user:

- **Improvement**: Adding or clarifying it seems to improve consistency or completeness.
- **Removal**: It removes, narrows, deprecates, or weakens something previously accepted.
- **Contradiction**: Two artifacts cannot both be true.
- **Out of place**: It is true but belongs in a different artifact.
- **Ignore**: It does not belong elsewhere because of scope or abstraction level.

Do not edit yet.

### 4. Ask one decision at a time

Present one classified difference, recommend a choice, and wait for the user's answer before moving to the next difference. Use clear multiple choice like Alejo Questions.

Use this format:

```md
I found a {classification}: {short difference}.

Evidence:
- {source A}: {claim}
- {source B or missing destination}: {claim or gap}

What should I do?
A. {recommended action} (Recommended: {short reason})
B. Leave it unchanged ({short reason})
C. {alternative action} ({short reason})
D. Other / correction
```

For simple improvements, option A should usually be "Yes, add this to {destination}." For removals and contradictions, recommend the safest resolution based on the source order and current evidence, but still ask before editing.

### 5. Apply approved changes

After each user answer, immediately update the affected artifact(s), then continue with the next difference.

Keep edits minimal and artifact-appropriate:

- Linear Project document `CONTEXT.xml` and local `CONTEXT.xml`: stable domain terms and relationships only.
- Linear Project document `Q&A.xml`: resolved questions, recommendations, answers, evidence, and unresolved contradictions.
- Linear Project document `PRD.xml`: product behavior, user stories, experience notes, scope, and acceptance signals.
- Linear Project document `prototype.xml`: prototype HTML, UX evidence, reference notes, screenshots/links, and open UX/SAD/issues notes.
- Linear Project document `SAD.xml`/`SAT.xml`: architecture decisions, quality attributes, security, operations, and ADR links.
- Vertical-slice issues: XML behavior-first coverage, necessary context, acceptance criteria, surface, preconditions, dependencies/blockers, Doppler secret refs, quality attributes, BDD budget, readiness label/status, code organization, and source references.
- `WORKFLOW.md`: Symphony entry rules, issue contract, Doppler/name-only secret rules, lane mappings, and thread contract.

Do not create horizontal issues. Missing delivery work must become or update a behavior-first vertical slice.

If `alejo-secrets` confirms, renames, adds, or removes a Doppler secret name after issues exist, treat that as a delivery inconsistency and ask whether to propagate the exact name-only change back to every affected Linear issue before `alejo-run`.

When applying changes to XML artifacts or XML issue contracts, preserve valid XML, update the smallest relevant element, and wrap user-supplied prose or evidence in CDATA.

### 6. Finish

When all differences are resolved or deferred, give a concise summary of:

- Decisions applied.
- Artifacts or issues changed.
- Differences the user chose to leave unchanged.
- Any unresolved decisions still waiting on the human.
