---
name: alejo-prd
description: Turn the current conversation context and codebase understanding into a short but complete product-focused PRD XML document, then create or update a Linear Project and its PRD.xml Project Document. Use when the user wants to create a PRD or product requirements document from the current context.
---

# Alejo PRD

This skill takes the current conversation context and codebase understanding and produces a short but complete product-focused PRD in XML. Do NOT interview the user; synthesize what you already know.

The Linear workspace/team/project conventions should have been provided in Linear Project Documents `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, and `alejo-workflow.md`. Run `/setup-alejo-skills` if not.

## Process

1. Read the Alejo setup docs from Linear Project Documents when available: `AGENTS.md`, `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, `WORKFLOW.md`, existing planning documents, and the latest Alejo Questions log named `Q&A.xml`. Treat old local `AGENTS.md`, `docs/agents/*`, or `WORKFLOW.md` files only as legacy mirrors, not canonical sources.

2. Explore the repo only enough to understand current product behavior, domain language, and user-facing constraints. Use the project's domain glossary vocabulary throughout the PRD, carry forward the resolved Alejo Questions Q&A summary, and respect product-relevant ADR constraints.

3. Synthesize the desired user experience: actors, journeys, functional requirements, outcomes, scope boundaries, success signals, risks, and open product questions.

Do not define modules, architecture, implementation strategy, file paths, APIs, schemas, tests, or code organization. Functional requirements describe user-visible capabilities and product behavior only. Technical details belong in SAD and Alejo Issues.

4. Write the PRD using the XML template below, then create or update a Linear Project for this product effort and publish the PRD to the Linear Project document named `PRD.xml`. Prefer Project Documents/Resources; use the project overview/detailed description only if Project Documents are unavailable in the active tooling. Do not create a PRD issue. Do not apply `ready-for-agent` to PRDs.

If Linear Project or Project Document details are missing, infer them from repo instructions and existing Linear links. Do not ask for confirmation before publishing to the inferred Linear destination. If Linear publishing is impossible with the available tools, report the blocker and provide the PRD in the conversation without creating a local substitute as the canonical artifact.

## Prioritized List Rule

For every PRD section that contains a list, keep the list short but complete:

- Put the top 3-5 most important items first and identify them as `Primary`.
- Include remaining relevant items after the primary items as `Additional`.
- Prefer 3 primary items; use 4 or 5 only when the source material clearly has more core concerns.
- Order primary items by user value, risk reduction, dependency importance, or product confidence, depending on the section.
- Do not bury the main user stories, experience details, acceptance signals, risks, or out-of-scope boundaries in a long undifferentiated list.
- Use XML elements for structure and CDATA for natural language, user-supplied text, and anything that might contain XML special characters.

<prd-template>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<prd title="{Title}">
  <problem_statement><![CDATA[{The problem the user is facing, from the user's perspective.}]]></problem_statement>
  <desired_experience><![CDATA[{The intended experience and outcome from the user's perspective. Keep this product-facing, not technical.}]]></desired_experience>
  <user_stories>
    <story priority="primary" order="1">
      <actor><![CDATA[{actor}]]></actor>
      <want><![CDATA[{feature}]]></want>
      <benefit><![CDATA[{benefit}]]></benefit>
      <sentence><![CDATA[As a {actor}, I want {feature}, so that {benefit}.]]></sentence>
    </story>
    <story priority="additional" order="{N}">
      <actor><![CDATA[{actor}]]></actor>
      <want><![CDATA[{feature}]]></want>
      <benefit><![CDATA[{benefit}]]></benefit>
      <sentence><![CDATA[As a {actor}, I want {feature}, so that {benefit}.]]></sentence>
    </story>
  </user_stories>
  <functional_requirements>
    <requirement priority="primary" order="1"><![CDATA[{User-visible capability or product behavior the system must provide.}]]></requirement>
    <requirement priority="additional" order="{N}"><![CDATA[{Additional user-visible capability or product behavior.}]]></requirement>
  </functional_requirements>
  <experience_notes>
    <note priority="primary" order="1"><![CDATA[{Key moment, user-visible state, tone, permission, role, or product constraint.}]]></note>
    <note priority="additional" order="{N}"><![CDATA[{Additional experience detail.}]]></note>
  </experience_notes>
  <acceptance_signals>
    <signal priority="primary" order="1"><![CDATA[{User-visible signal that the experience works.}]]></signal>
    <signal priority="additional" order="{N}"><![CDATA[{Additional observable outcome.}]]></signal>
  </acceptance_signals>
  <out_of_scope>
    <boundary priority="primary" order="1"><![CDATA[{Important out-of-scope boundary.}]]></boundary>
    <boundary priority="additional" order="{N}"><![CDATA[{Additional out-of-scope boundary.}]]></boundary>
  </out_of_scope>
  <further_notes>
    <note order="1"><![CDATA[{Any further note about the feature.}]]></note>
  </further_notes>
</prd>
```

</prd-template>
