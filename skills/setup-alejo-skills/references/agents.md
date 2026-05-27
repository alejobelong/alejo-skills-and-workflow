# AGENTS.md XML Shape

Use this XML shape for the repo root `AGENTS.md`. Replace every bracketed value before writing. If a non-required value is unknown, omit that element instead of writing a placeholder.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_repo name="{Project Name}">
  <setup>
    <github>{repo URL}</github>
    <linear_project name="{project name}" url="{project URL}" />
    <linear_team name="{team name}" key="{team key}" />
    <artifact_home>Planning artifacts live in Linear Project Documents: Q&amp;A.xml, CONTEXT.xml, PRD.xml, prototype.xml, SAD.xml/SAT.xml.</artifact_home>
    <issue_home>Linear issues are only for vertical-slice implementation and actionable follow-ups.</issue_home>
    <workflow>WORKFLOW.md is the Symphony execution contract for approved issues.</workflow>
    <secrets>Secret values belong in Doppler, never in repo files or Linear issue bodies.</secrets>
  </setup>
  <skill_flow>
    <skill order="1" name="$setup-alejo-skills">Rerun only when Git, Linear, or setup docs are missing.</skill>
    <skill order="2" name="$alejo-questions">Clarify domain language, product questions, and trade-offs.</skill>
    <skill order="3" name="$alejo-prd">Publish product intent and user value to Linear.</skill>
    <skill order="4" name="$alejo-prototype">Publish UI evidence or a throwaway HTML prototype when useful.</skill>
    <skill order="5" name="$alejo-sad">Publish architecture for non-trivial implementation.</skill>
    <skill order="6" name="$alejo-issues">Create behavior-first vertical-slice Linear issues.</skill>
    <skill order="7" name="$alejo-secrets">Provide Doppler setup steps for required secrets.</skill>
    <skill order="8" name="$alejo-consistency-propagation">Reconcile changed artifacts and issue contracts.</skill>
    <skill order="9" name="$alejo-run">Preflight ready issues and hand approved work to Symphony.</skill>
  </skill_flow>
  <repo_references>
    <reference path="docs/agents/issue-tracker.md">Linear Project, Project Documents, issue contract, Symphony handoff.</reference>
    <reference path="docs/agents/triage-labels.md">Linear statuses and issue labels.</reference>
    <reference path="docs/agents/domain.md">Glossary, context map, and ADR conventions.</reference>
    <reference path="docs/agents/alejo-workflow.md">Planning-to-Symphony workflow.</reference>
    <reference path="WORKFLOW.md">Symphony execution workflow.</reference>
  </repo_references>
</alejo_repo>
```
