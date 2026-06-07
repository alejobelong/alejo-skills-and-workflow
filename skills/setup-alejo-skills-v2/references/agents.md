# AGENTS.md Linear Project Document Shape

Publish this XML as the Linear Project Document `AGENTS.md`. Replace bracketed values; omit unknown optional values instead of writing placeholders.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_repo name="{Project Name}" stack="v2">
  <setup>
    <github>{repo URL}</github>
    <linear_project name="{project name}" url="{project URL}" />
    <linear_team name="{team name}" key="{team key}" />
    <source_of_truth>Linear Project Documents own Alejo setup docs and planning artifacts. Repo WORKFLOW.md owns the Symphony runtime contract and is mirrored to Linear.</source_of_truth>
    <no_local_setup_mirrors>Do not maintain repo-local AGENTS.md or docs/agents/* generated setup copies.</no_local_setup_mirrors>
    <issue_home>Linear issues are only for vertical-slice implementation contracts and actionable follow-ups.</issue_home>
    <secrets>Doppler owns secret values. Linear and repo files may contain secret names only.</secrets>
  </setup>
  <canonical_sources>
    <source name="GitHub" purpose="Project code, repo WORKFLOW.md, ADR XML when stored in repo, branches, PRs, and implementation history." />
    <source name="Linear Project Documents" purpose="AGENTS.md, issue-tracker.md, triage-labels.md, alejo-workflow.md, WORKFLOW.md mirror, Q&amp;A.xml, CONTEXT.xml, PRD.xml, prototype.xml, SAD.xml, and ADR XML when published there." />
    <source name="Linear issues" purpose="Self-contained production-ready vertical-slice run contracts." />
    <source name="Doppler" purpose="Secret values and environment-backed runtime configuration." />
  </canonical_sources>
  <alejo_v2_skills>
    <skill name="setup-alejo-skills-v2" purpose="Repo, GitHub, Linear, setup docs, and WORKFLOW.md." />
    <skill name="alejo-questions-v2" purpose="Product clarity, Q&amp;A.xml, CONTEXT.xml, and decisions." />
    <skill name="alejo-prd-v2" purpose="PRD.xml." />
    <skill name="alejo-prototype" purpose="prototype.xml and UI evidence." />
    <skill name="alejo-sad-v2" purpose="SAD.xml architecture." />
    <skill name="alejo-issues-v2" purpose="Vertical-slice Linear implementation issues." />
    <skill name="alejo-secrets-v2" purpose="Provider resources and Doppler names." />
    <skill name="alejo-consistency-propagation-v2" purpose="Line-by-line drift detection and approved propagation." />
    <skill name="alejo-run-v2" purpose="Symphony execution, BDD verification, and review loop." />
    <skill name="alejo-review" purpose="Contrarian readiness review before Done." />
  </alejo_v2_skills>
</alejo_repo>
```
