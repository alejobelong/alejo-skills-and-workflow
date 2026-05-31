---
name: alejo-prd-v2
description: Compact Alejo PRD v2 workflow that turns the latest Alejo Q&A.xml, product context, and minimal repo evidence into a product-focused PRD.xml Linear Project Document. Use when the user wants a leaner Q&A-first PRD skill that publishes PRD.xml to Linear Project Documents.
---

# Alejo PRD v2

Create a short product-focused `PRD.xml` from what is already known. Do not interview the user. The latest Alejo `Q&A.xml` is the primary source.

## Sources

Read only what is needed, in this order:

1. `AGENTS.md`: general project context and source-of-truth map; read first for orientation only.
2. `Q&A.xml`: highest weight. Carry forward resolved questions, answers, recommendations, product snapshot, decisions, and open questions.
3. `CONTEXT.xml`: canonical domain language and relationships.
4. Current conversation: latest user intent and corrections.
5. Existing `PRD.xml`: preserve still-valid product decisions when updating.
6. `prototype.xml`: UX evidence and visible interaction details.
7. Code/repo evidence: current product behavior and constraints only.
8. ADR XML: product-visible constraints only.

Do not load `issue-tracker.md`, `triage-labels.md`, `alejo-workflow.md`, or `WORKFLOW.md` unless needed only to locate the Linear Project.

## Process

1. Resolve the Linear Project from current context, existing Linear links, or Linear tooling.
2. Read `AGENTS.md` for project orientation, then read `Q&A.xml` for product substance. If Q&A is missing, continue from the conversation but mark confidence lower.
3. Inspect only enough repo evidence to avoid false product claims.
4. Synthesize the desired user experience: users, value proposition, journeys, scope, acceptance signals, risks, and open questions.
5. Publish by creating or updating the Linear Project Document named `PRD.xml`.

If a writable Linear Project Document cannot be reached, report the blocker and stop. Do not create a PRD issue, project overview substitute, or local canonical file.

## Product Rules

- Stay product-facing: no modules, APIs, schemas, tests, file paths, or implementation plans.
- Use `CONTEXT.xml` terms.
- Treat Q&A answers as stronger than old PRDs, guesses, or code-adjacent assumptions.
- Keep lists short: 3 primary items first, then additional items only when useful.
- Use XML structure and CDATA for prose, evidence, quotes, and user text.

## PRD XML

```xml
<?xml version="1.0" encoding="UTF-8"?>
<prd title="{Title}">
  <source_summary>
    <primary_source>Q&amp;A.xml</primary_source>
    <confidence>{high|medium|low}</confidence>
    <notes><![CDATA[{Main Q&A decisions and any missing context.}]]></notes>
  </source_summary>
  <problem_statement><![CDATA[{User-facing problem.}]]></problem_statement>
  <desired_experience><![CDATA[{End-user experience and value proposition.}]]></desired_experience>
  <users>
    <user priority="primary" order="1"><![CDATA[{User/actor and context.}]]></user>
  </users>
  <user_stories>
    <story priority="primary" order="1">
      <actor><![CDATA[{actor}]]></actor>
      <want><![CDATA[{capability}]]></want>
      <benefit><![CDATA[{benefit}]]></benefit>
      <sentence><![CDATA[As a {actor}, I want {capability}, so that {benefit}.]]></sentence>
    </story>
  </user_stories>
  <experience_notes>
    <note priority="primary" order="1"><![CDATA[{Key user-visible behavior, state, tone, permission, or constraint.}]]></note>
  </experience_notes>
  <acceptance_signals>
    <signal priority="primary" order="1"><![CDATA[{Observable signal that the experience works.}]]></signal>
  </acceptance_signals>
  <scope>
    <in><![CDATA[{Included product behavior.}]]></in>
    <out><![CDATA[{Excluded product behavior.}]]></out>
  </scope>
  <risks_and_open_questions>
    <item><![CDATA[{Risk, unresolved question, or assumption.}]]></item>
  </risks_and_open_questions>
</prd>
```
