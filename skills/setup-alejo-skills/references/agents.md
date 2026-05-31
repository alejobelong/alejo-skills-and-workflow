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
  </setup>
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
  <skill_flow>
    <skill order="1" name="$setup-alejo-skills">Connect Git and Linear; publish setup docs into Linear Project Documents.</skill>
    <skill order="2" name="$alejo-questions">Clarify domain language, product questions, and trade-offs.</skill>
    <skill order="3" name="$alejo-prd">Publish product intent and user value to Linear.</skill>
    <skill order="4" name="$alejo-prototype">Publish UI evidence or a throwaway HTML prototype when useful.</skill>
    <skill order="5" name="$alejo-sad">Publish architecture for non-trivial implementation.</skill>
    <skill order="6" name="$alejo-issues">Create behavior-first vertical-slice Linear issues.</skill>
    <skill order="7" name="$alejo-secrets">Recover or set up Doppler secrets and provider resources.</skill>
    <skill order="8" name="$alejo-consistency-propagation">Reconcile changed artifacts and issue contracts.</skill>
    <skill order="9" name="$alejo-run">Autonomously preflight, queue, launch, and drive ready issues through Symphony.</skill>
    <skill order="10" name="$alejo-review">Audit built code against Alejo documents and issues.</skill>
  </skill_flow>
</alejo_repo>
```
