---
name: alejo-prd
description: Turn the current conversation context and codebase understanding into a short but complete product-focused PRD, then create or update a Linear Project with that PRD. Use when the user wants to create a PRD or product requirements document from the current context.
---

# Alejo PRD

This skill takes the current conversation context and codebase understanding and produces a short but complete product-focused PRD. Do NOT interview the user; synthesize what you already know.

The Linear workspace/team/project conventions should have been provided in `AGENTS.md` and `docs/agents/`. Run `/setup-alejo-skills` if not.

## Process

1. Read the Alejo repo instructions if available: `AGENTS.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, `docs/agents/alejo-workflow.md`, and the latest Alejo Questions logs in `docs/questions/`.

2. Explore the repo only enough to understand current product behavior, domain language, and user-facing constraints. Use the project's domain glossary vocabulary throughout the PRD, carry forward the resolved Alejo Questions Q&A summary, and respect product-relevant ADR constraints.

3. Synthesize the desired user experience: actors, journeys, outcomes, scope boundaries, success signals, risks, and open product questions.

Do not define modules, architecture, implementation strategy, file paths, APIs, schemas, tests, or code organization. Those belong in SAD and Alejo Issues.

4. Write the PRD using the template below, then create or update a Linear Project for this product effort and add the PRD to the project description/overview/document area available in the repo's Linear tooling. Do not create a PRD issue. Do not apply `ready-for-agent` to PRDs.

If the available Linear tooling cannot create or update projects, stop and ask before falling back to any other artifact shape.

## Prioritized List Rule

For every PRD section that contains a list, keep the list short but complete:

- Put the top 3-5 most important items first and identify them as `Primary`.
- Include remaining relevant items after the primary items as `Additional`.
- Prefer 3 primary items; use 4 or 5 only when the source material clearly has more core concerns.
- Order primary items by user value, risk reduction, dependency importance, or product confidence, depending on the section.
- Do not bury the main user stories, experience details, acceptance signals, risks, or out-of-scope boundaries in a long undifferentiated list.

<prd-template>

## Problem Statement

The problem the user is facing, from the user's perspective.

## Desired Experience

The intended experience and outcome from the user's perspective. Keep this product-facing, not technical.

## User Stories

A prioritized numbered list of user stories. Put the top 3-5 primary user stories first, then include additional user stories needed for completeness. Each user story should use this format:

1. As a <actor>, I want a <feature>, so that <benefit>.

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending.
</user-story-example>

This list should be complete enough to cover the feature while staying concise. Avoid exhaustive permutations when one story can cover the behavior.

## Experience Notes

A prioritized list of product experience details: key moments, user-visible states, content tone, permissions or roles from the user's perspective, and constraints the user must feel in the product.

## Acceptance Signals

A prioritized list of user-visible signals that the experience works. Describe observable outcomes, not implementation tests or internal modules.

## Out of Scope

A concise prioritized list of the things that are out of scope for this PRD. Put the most important 3-5 boundaries first.

## Further Notes

Any further notes about the feature. Keep this short and prioritize the most important notes first when there is more than one.

</prd-template>
