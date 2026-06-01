# AGENTS.md Linear Project Document Shape

Use this XML shape for the Linear Project Document `AGENTS.md`. Replace every bracketed value before publishing. If a non-required value is unknown, omit that element instead of writing a placeholder.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_repo name="{Project Name}">
  <setup>
    <github>{repo URL}</github>
    <linear_project name="{project name}" url="{project URL}" />
    <linear_team name="{team name}" key="{team key}" />
    <source_of_truth>Linear Project Documents own Alejo setup docs, workflow docs, and planning artifacts.</source_of_truth>
    <no_local_copies>Do not maintain repo-local AGENTS.md, docs/agents/*, or WORKFLOW.md copies.</no_local_copies>
    <issue_home>Linear issues are only for vertical-slice implementation and actionable follow-ups.</issue_home>
    <secrets>Secret values belong in Doppler, never in repo files, Linear docs, or Linear issue bodies.</secrets>
    <workflow_pointer>Read alejo-workflow.md for the Alejo skill lifecycle. Read WORKFLOW.md for Symphony execution.</workflow_pointer>
  </setup>
  <canonical_sources>
    <source name="GitHub" purpose="Project code, ADR XML files, and implementation history." />
    <source name="Linear Project Documents" purpose="Alejo setup docs, workflow docs, and planning artifacts." />
    <source name="Linear issues" purpose="Vertical-slice implementation contracts and actionable follow-ups." />
    <source name="Doppler" purpose="Secret values and environment-backed runtime configuration." />
  </canonical_sources>
  <linear_documents>
    <document name="AGENTS.md" purpose="Repo onboarding and Alejo source-of-truth map." />
    <document name="issue-tracker.md" purpose="Linear Project, Project Documents, issue contract, and Symphony handoff." />
    <document name="triage-labels.md" purpose="Linear statuses and issue labels." />
    <document name="alejo-workflow.md" purpose="Planning-to-Symphony workflow." />
    <document name="WORKFLOW.md" purpose="Symphony execution workflow." />
    <document name="Q&amp;A.xml" purpose="Questions, decisions, and product clarity." />
    <document name="CONTEXT.xml" purpose="Project glossary, domain language, and shared context." />
    <document name="PRD.xml" purpose="Product intent and user value." />
    <document name="prototype.xml" purpose="UI evidence and prototype notes." />
    <document name="SAD.xml" alternate="SAT.xml" purpose="Architecture and implementation plan." />
  </linear_documents>
</alejo_repo>
```
