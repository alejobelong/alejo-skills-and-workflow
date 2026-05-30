---
name: alejo-issues
description: Convert a PRD, prototype report, SAD, plan, spec, review gap, or existing issue into autonomous production-ready Linear implementation issues using thin vertical slices, self-contained XML run contracts, explicit provider and Doppler requirements, slice-owned code organization, and ready-for-agent publishing. Use when the user wants implementation tickets or issue breakdowns for agents.
---

# Alejo Issues

Create only production-ready Linear implementation issues. A fresh coding agent must be able to execute each issue from the Linear body plus normal codebase inspection.

Issues are for observable product behavior, not planning artifacts or horizontal setup. PRD.xml, SAD.xml/SAT.xml, Q&A.xml, CONTEXT.xml, prototype.xml, setup docs, and workflow docs belong in Linear Project Documents. Run `/setup-alejo-skills` if Linear Project Documents `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, or `WORKFLOW.md` are missing.

## Rules

- Every issue is one thin end-to-end vertical slice with an externally observable outcome.
- Every issue is self-contained: product intent, architecture constraints, domain terms, providers, Doppler secret names, dependencies, acceptance criteria, verification surface, BDD budget, and code ownership are in the XML body.
- Every provider or integration needed by the slice is named explicitly, including product, purpose, environment, API/SDK/webhook surface, and required Doppler secret names.
- Secrets are referenced only by Doppler environment variable names. Never include secret values.
- If a required provider, secret name, scope, UX choice, architecture choice, or dependency is undecided, ask the user a multiple-choice question with a recommended option before publishing.
- If required secret names are not already present in Doppler, finish by using `alejo-secrets` to give the user a Doppler-only setup guide. Do not mark the dependent issue `ready-for-agent` until secrets are present or the user explicitly chooses to publish it blocked on secrets.
- Production means real code wired to real providers, real storage, real routes/UI/CLI/MCP surfaces, and real tests. Mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, `NotImplemented`, TODO-only paths, and unwired UI are not valid implementation targets.

## Process

### 1. Gather Context

Use current conversation context first. Then inspect repo instructions, Linear Project Documents, local mirrors in `docs/questions/` and `docs/prototypes/`, ADR XML docs, prior Alejo outputs, and relevant existing Linear issues.

If the user passes an issue reference, fetch the issue body and comments before slicing.

### 2. Inspect The Codebase

Inspect enough code to understand the framework, feature folders, routes/UI, APIs, domain logic, storage, tests, config, env examples, provider adapters, deployment, and integration boundaries.

Use project glossary terms from CONTEXT.xml and respect SAD/ADR constraints. Prefer existing conventions over inventing new folders or abstractions.

### 3. Inventory Providers And Secrets

For each planned slice, identify every external or internal provider it depends on: APIs, SDKs, OAuth apps, webhooks, databases, queues, object storage, email/SMS, analytics, observability, CI/deploy services, MCP servers, and local production services.

For each provider, decide:

- Provider/product name.
- Slice purpose.
- Integration surface: API, SDK, webhook, CLI, MCP, database, queue, or local service.
- Environment: production, sandbox, staging, local, or test account.
- Required credential names in Doppler.
- Required scopes, permissions, webhook events, callback URLs, regions, models, plans, or billing constraints.

Use safe Doppler checks only, such as `command -v doppler`, `doppler --version`, or `doppler secrets --only-names`. Do not print secret values.

If a provider choice is ambiguous, ask before drafting issues. The question must be multiple choice, include a recommended option first, and explain the tradeoff in one sentence.

### 4. Draft Vertical Slices

Start with the smallest happy path through the whole capability. Fold required parsing, validation, adapters, schemas, migrations, schedulers, storage, provider wiring, and verification into the first observable behavior that needs them.

Do not create placeholder, research-only, component-only, provider-setup-only, migration-only, parser-only, route-only, or adapter-only issues. If a setup task has no observable user/operator/tester outcome, fold it into the slice that uses it.

Each slice should be narrow enough to complete independently but complete enough to be production behavior. Split thick work by user role, scenario, state, permission, data scope, integration boundary, or happy path versus edge case.

### 5. Build The XML Run Contract

Every issue must include:

- Product intent and source refs from PRD.xml, Q&A.xml, CONTEXT.xml, prototype.xml, SAD.xml/SAT.xml, and ADR XML docs.
- Observable outcome and acceptance criteria.
- Verification surface: `api`, `ui`, `cli`, or `mcp`.
- Provider definitions and Doppler secret refs.
- Preconditions, dependencies, quality attributes, and BDD budget.
- Production constraints that forbid mocks, fakes, stubs, placeholders, skipped tests, and unwired UI.
- Slice-owned code organization, including any thin framework adapters.

Use `type="AFK"` and `readiness="ready-for-agent"` only when all execution decisions are resolved and required Doppler secret names exist.

### 6. Gate Each Slice

Before showing or publishing an issue, verify:

- A user, operator, or synthetic tester can observe the result.
- A separate agent can prove it works from the issue plus code inspection.
- It is one complete scenario, not a bundle of capabilities.
- It has no unresolved decisions.
- Providers and Doppler secret names are explicit and verified or queued for `alejo-secrets`.
- The production constraints reject mocks, fakes, stubs, skipped tests, placeholders, TODO-only paths, and unwired UI.
- UI/API/data/tests/contracts stay in one owning feature area, with only thin framework adapters elsewhere.
- Blockers are only prior observable behavior issues or explicit human decisions.

### 7. Review With The User

Present the proposed issue set before publishing. For each slice, show:

- Title.
- Blocked by.
- User stories covered.
- Source refs.
- Necessary context.
- Providers and Doppler secret refs.
- Observable outcome.
- Run contract.
- Expected code organization.
- Why it is a vertical slice.

Ask whether the granularity, dependencies, provider choices, and slice boundaries are right. Iterate until approved.

### 8. Publish And Handle Secrets

Publish accepted issues in dependency order with the `ready-for-agent` triage label only when they pass the gate. If an accepted slice still lacks Doppler secrets, either keep it unpublished until secrets are added or publish it with the repo's human/blocker labels if the user explicitly asks.

At the end, list any missing Doppler secret names by provider and use `alejo-secrets` to produce the setup guide. Do not ask the user to paste secret values into Codex.

<issue-template>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<vertical_slice_issue type="AFK" readiness="ready-for-agent">
  <parent>{parent issue ref, or omit this element}</parent>
  <what_to_build><![CDATA[{End-to-end production behavior and outcome. Do not describe layer-by-layer implementation.}]]></what_to_build>
  <necessary_context>
    <product_intent><![CDATA[{slice-specific PRD.xml requirement or user story}]]></product_intent>
    <architecture_constraints><![CDATA[{relevant SAD.xml/SAT.xml decisions, ADRs, quality attributes, security, data, or ops constraints}]]></architecture_constraints>
    <domain_language><![CDATA[{required CONTEXT.xml/Q&A.xml terms or decisions}]]></domain_language>
    <prototype_evidence><![CDATA[{relevant UI/state/interaction evidence, or None relevant}]]></prototype_evidence>
    <source_refs><![CDATA[{short PRD.xml/SAD.xml/Q&A.xml/CONTEXT.xml/prototype.xml/ADR refs for provenance}]]></source_refs>
  </necessary_context>
  <providers>
    <provider name="{provider product or None}" purpose="{why this slice needs it}" environment="{production|sandbox|staging|local|test-account|none}" surface="{api|sdk|webhook|cli|mcp|database|queue|local-service|none}">
      <credential_refs><![CDATA[{Doppler secret names only, or None}]]></credential_refs>
      <requirements><![CDATA[{scopes, permissions, webhook events, callback URLs, regions, models, billing, or None}]]></requirements>
    </provider>
  </providers>
  <code_organization>
    <slice_owned_folder>features/{capability-slug}/</slice_owned_folder>
    <rule><![CDATA[Keep UI, API/route handling, data access, tests, provider adapters, and shared contracts for this behavior colocated in the slice.]]></rule>
    <framework_mapping><![CDATA[{Thin route/app adapters if the framework requires files elsewhere, or None.}]]></framework_mapping>
    <avoid><![CDATA[Do not add mixed-capability controllers, services, repositories, provider clients, or test utilities for this behavior.]]></avoid>
  </code_organization>
  <run_contract>
    <surface>{api|ui|cli|mcp}</surface>
    <preconditions><![CDATA[{required state, data, config, role, provider setup, or None}]]></preconditions>
    <dependencies><![CDATA[{issue refs, or None}]]></dependencies>
    <secrets_refs><![CDATA[{Doppler secret names verified by name-only check, or None}]]></secrets_refs>
    <quality_attributes><![CDATA[{slice-relevant targets from SAD.xml/SAT.xml, or None beyond acceptance criteria}]]></quality_attributes>
    <bdd_budget>{default 3 outer repair iterations unless SAD.xml/SAT.xml says otherwise}</bdd_budget>
    <readiness_label_status>ready-for-agent only after all decisions and Doppler secret names are resolved; symphony-execution only after alejo-run handoff</readiness_label_status>
  </run_contract>
  <production_constraints>
    <required><![CDATA[Use real production code paths, real provider SDKs/APIs or official sandbox/test accounts, real persistence, real UI/API/CLI/MCP wiring, and executable tests.]]></required>
    <invalid><![CDATA[Mocks, fake providers, stubbed SDK responses, placeholder code, skipped tests, disabled branches, NotImplemented, TODO-only paths, and unwired UI are not accepted.]]></invalid>
  </production_constraints>
  <acceptance_criteria>
    <criterion status="todo"><![CDATA[Externally verifiable behavior works through the declared surface.]]></criterion>
    <criterion status="todo"><![CDATA[Provider integration, storage effect, or state change is real and observable when relevant.]]></criterion>
    <criterion status="todo"><![CDATA[Security, quality, and test expectations from PRD.xml/SAD.xml/SAT.xml are satisfied.]]></criterion>
    <criterion status="todo"><![CDATA[No mocks, fake providers, stubbed SDK responses, placeholders, skipped tests, disabled branches, NotImplemented paths, TODO-only paths, or unwired UI remain.]]></criterion>
  </acceptance_criteria>
  <blocked_by><![CDATA[{blocking issue refs, or None - can start immediately}]]></blocked_by>
</vertical_slice_issue>
```

</issue-template>

Keep each XML issue body just sufficient. Do not paste whole planning docs, broad background, unrelated stories, stale file guesses, or code the agent can discover by inspecting the repo. Do not close or modify parent issues.
