---
name: alejo-issues
description: Break a PRD, prototype report, SAD, plan, spec, or existing issue into independently grabbable implementation issues on the project issue tracker using the thinnest possible behavior-first end-to-end vertical slices with self-contained minimal context and slice-owned code organization, avoiding horizontal layer/component tickets. Use when the user wants to convert planning context into issues, create implementation tickets, or break down work for agents.
---

# Alejo Issues

Break planning context into independently grabbable issues using behavior-first vertical slices.

The issue tracker and triage label vocabulary should have been provided in `AGENTS.md` and `docs/agents/`. Run `/setup-alejo-skills` if not.

## Process

### 1. Gather context

Work from whatever is already in the conversation context. Then inspect the Alejo repo instructions; relevant Linear Project Documents (`PRD`, `SAD`/`SAT`, `Q&A`, `CONTEXT.md`, `prototype.html`); local mirrors such as prototype reports in `docs/prototypes/`, latest Alejo Questions logs, `CONTEXT.md`, ADRs; and prior Alejo-skill outputs when they exist.

If the user passes an issue reference, such as an issue number, URL, or path, fetch it from the issue tracker and read its full body and comments.

### 2. Explore the codebase

If you have not already explored the codebase, inspect it enough to understand the current state of the code. Issue titles and descriptions should use the project's domain glossary vocabulary and respect SAD/ADR constraints in the area you are touching.

### 3. Draft vertical slices

Break the plan into vertical-slice issues. Each issue is a thin vertical slice that cuts through all relevant integration layers end to end, not a horizontal slice of one layer. Use prototype evidence to sharpen behavior, acceptance criteria, risks, and dependencies, but do not turn throwaway prototype code into implementation scope.

Start with the smallest user- or operator-observable happy path through the whole capability. Fold the minimum required parsing, validation, scheduling, adapter, storage, or setup work into that first behavior instead of making those things standalone blockers.

Slices may be `HITL` or `AFK`. `HITL` slices require human interaction, such as an architectural decision or design review. `AFK` slices can be implemented and merged without human interaction. Prefer `AFK` over `HITL` where possible.

Honor the SAD's code-organization rule. Each implementation issue should identify one owning feature/slice folder for the user-facing capability and keep slice-owned UI, API/route, data access, tests, and contracts together there. If the framework requires route/app files elsewhere, describe them as thin adapters into the slice-owned feature code. Do not create issues that imply catch-all `controllers/`, `services/`, or `repositories/` files mixing multiple capabilities.

For each slice, build a short self-contained context pack from only the relevant PRD, SAD, Q&A, `CONTEXT.md`, ADR, and prototype details. Include enough for a coding agent to implement the issue with normal codebase inspection, but not enough to re-read the whole planning stack. Source links prove provenance; they do not replace needed context. If a slice cannot be made self-contained, ask the user or mark it `HITL`.

Each `AFK` issue is also the compact run contract for `alejo-run` and Symphony. It must include acceptance criteria, verification surface, preconditions, dependencies, secret refs, quality attributes, BDD budget, readiness label/status, and code organization.

<vertical-slice-rules>

- Each slice title describes behavior and outcome, not a component being added. Avoid `Add`, `Build`, `Implement`, `Bootstrap`, or `Create <component>` titles unless the component is itself the user-facing product.
- Each slice has an externally observable outcome, such as a command result, UI/API/MCP behavior, persisted artifact, state change, issue comment, report, or pass/fail verdict.
- Each slice delivers a narrow but complete path through every relevant layer, such as interface, domain logic, storage, integrations, and tests.
- Each slice maps to one owning feature folder or existing feature area; shared code is limited to genuinely cross-cutting or multi-slice concerns.
- Each published issue contains only the necessary source context for that slice: product intent, architecture constraints, domain terms, prototype evidence, source refs, and run-contract fields.
- A completed slice is demoable or verifiable on its own by an agent that did not implement it.
- The first implementation slice should be the degenerate happy path through the whole capability. Preconditions needed for that path belong inside the first slice unless they require human judgment.
- Treat parsers, preflight validators, schedulers, artifact resolvers, scenario generators, adapters, schemas, migrations, and worktree setup as means, not slices, unless they are framed around an independently observable behavior.
- Surface additions must be stated as behavior on a real scenario, for example `Synthetic tester verifies one slice through the API surface`, not `Add API surface adapter`.
- Prefer many thin slices over few thick ones.
- Split thick slices by user role, scenario, happy path versus edge case, permission, state, data scope, or integration boundary.
- Mark a slice `HITL` when it hides an unresolved decision, tool choice, UX judgment, policy, ADR question, or language such as `likely`, `choose`, `decide`, `contradiction handling`, or `TBD`.

</vertical-slice-rules>

Before showing the user any proposed slice, run this gate:

- **Observable behavior**: What can a user, operator, or synthetic tester see after this slice is done?
- **Independent verification**: How can a separate agent prove the behavior works without reading private implementation intent?
- **Narrow completeness**: Is it one complete scenario, or a bundle of related capabilities?
- **No horizontal smell**: If the slice mainly says `before X`, `without Y`, `still does not run`, `only adds`, `prepares`, or `enables later`, fold it into the first behavior that uses it or defer it.
- **Code ownership**: Does the slice keep its UI/API/data/tests/contracts in one feature folder, with only thin framework adapters or justified shared code outside it?
- **Context sufficiency**: Could a coding agent implement this issue from the issue body plus codebase inspection, without opening PRD/SAD/Q&A/prototype docs to discover requirements?
- **Run contract**: Does the issue state surface, preconditions, dependencies, secret refs, quality attributes, BDD budget, and readiness label/status explicitly?
- **Dependency discipline**: Block only on prior observable behaviors or required human decisions, not on plumbing-only tickets.

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: `HITL` / `AFK`
- **Blocked by**: which other slices, if any, must complete first
- **User stories covered**: which user stories this addresses, if the source material has them
- **PRD/SAD/prototype references**: the source sections or prototype evidence that justify the slice, when available
- **Necessary context**: the minimal product, architecture, domain, and prototype facts the coding agent needs
- **Observable outcome**: the concrete behavior, artifact, state change, or verdict produced by the slice
- **Run contract**: surface, preconditions, dependencies, secrets refs, quality attributes, BDD budget, and readiness label/status
- **Expected code organization**: the owning feature folder and any thin framework adapters
- **Why it is a vertical slice**: the scenario boundary that keeps the slice independently grabbable without becoming a horizontal component ticket

Ask the user:

- Does the granularity feel right?
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- Are the correct slices marked as `HITL` and `AFK`?

Iterate until the user approves the breakdown.

### 5. Publish the issues to the issue tracker

For each approved slice, publish a new issue to the issue tracker. Use the issue body template below. Publish `AFK` slices with the `ready-for-agent` triage label. Publish `HITL` slices with `ready-for-human` and `hitl` when those labels exist; do not mark them `ready-for-agent` until the human decision is resolved.

Publish issues in dependency order, blockers first, so you can reference real issue identifiers in the "Blocked by" field.

Do not create Linear issues for PRDs, SAD/SATs, Q&A logs, `CONTEXT.md`, prototype HTML, or prototype reports. Those planning artifacts belong in Linear Project Documents; issues are only vertical slices or actionable follow-ups.

<issue-template>

## Parent

A reference to the parent issue on the issue tracker, if the source was an existing issue. Otherwise omit this section.

## What to build

A concise description of this vertical slice. Describe the end-to-end behavior, not layer-by-layer implementation.

Avoid detailed internal file paths or code snippets. They go stale fast. Exception: name the owning feature folder required by the SAD, and name thin framework adapter files only when the framework requires them. If a prototype produced a snippet that encodes a decision more precisely than prose can, such as a state machine, reducer, schema, or type shape, inline it here and briefly note that it came from a prototype. Trim it to the decision-rich parts. Do not include a working demo.

## Necessary context

- Product intent: {slice-specific PRD requirement or user story}
- Architecture constraints: {relevant SAD decisions, quality attributes, security, data, or ops constraints}
- Domain language: {required `CONTEXT.md`/Q&A terms or decisions}
- Prototype evidence: {relevant UI/state/interaction evidence, or "None relevant"}
- Source refs: {short PRD/SAD/Q&A/context/prototype section links for provenance}

Keep this section just sufficient. Do not paste whole planning docs, unrelated user stories, broad background, or context the coding agent can learn by inspecting the codebase.

## Code organization

- Slice-owned code lives under one feature folder: `features/<capability-slug>/` or the repo's equivalent feature area.
- Keep UI, API/route handling, data access, tests, and shared contracts for this behavior colocated in that slice.
- If route/app files must live elsewhere for framework reasons, keep them as thin adapters into the slice folder.
- Do not add mixed-capability `controllers`, `services`, or `repositories` ownership for this behavior.

## Run contract

- Surface: `api` / `ui` / `cli` / `mcp`
- Preconditions: {required state, data, config, user role, or "None"}
- Dependencies: {issue refs, or "None"}
- Secrets refs: {Doppler secret names only, or "None"}
- Quality attributes: {slice-relevant targets from the SAD, or "None beyond acceptance criteria"}
- BDD budget: {default 3 outer repair iterations unless the SAD says otherwise}
- Readiness label/status: `ready-for-agent` when published; `symphony-execution` only after `alejo-run` approval

## Acceptance criteria

- [ ] Externally verifiable behavior
- [ ] Data or storage effect, if relevant
- [ ] Security, quality, or test expectation from the PRD/SAD, if relevant

## Blocked by

- A reference to the blocking ticket, if any

Or "None - can start immediately" if no blockers.

</issue-template>

Do NOT close or modify any parent issue.
