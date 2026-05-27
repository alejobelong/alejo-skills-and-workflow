# Alejo Questions Session Log XML Format

Create one XML file at the end of each Alejo Questions session.

Default path:

```text
docs/questions/YYYY-MM-DD-<topic-slug>.xml
```

## Template

```xml
<?xml version="1.0" encoding="UTF-8"?>
<alejo_questions topic="{Topic}" status="{complete|stopped_early|blocked}">
  <metadata>
    <date>{YYYY-MM-DD}</date>
    <repository>{repo name or path}</repository>
    <plan_under_review><![CDATA[{short summary or link/path}]]></plan_under_review>
    <context_docs_touched>{files or None}</context_docs_touched>
    <adrs_created_or_updated>{files or None}</adrs_created_or_updated>
  </metadata>
  <session_summary><![CDATA[{Brief summary of what changed in the shared understanding.}]]></session_summary>
  <questions_and_answers>
    <qa number="1">
      <question><![CDATA[{Question}]]></question>
      <recommended_answer><![CDATA[{recommendation given before asking}]]></recommended_answer>
      <user_answer><![CDATA[{user's answer, correction, or confirmation}]]></user_answer>
      <evidence_checked><![CDATA[{code/docs inspected, or None}]]></evidence_checked>
      <resolution><![CDATA[{settled answer, contradiction, or open point}]]></resolution>
      <docs_updated>{files changed, or None}</docs_updated>
    </qa>
    <qa number="2">
      <question><![CDATA[{Question}]]></question>
      <recommended_answer><![CDATA[{recommendation}]]></recommended_answer>
      <user_answer><![CDATA[{answer}]]></user_answer>
      <evidence_checked><![CDATA[{evidence}]]></evidence_checked>
      <resolution><![CDATA[{resolution}]]></resolution>
      <docs_updated>{files}</docs_updated>
    </qa>
  </questions_and_answers>
  <resolved_language>
    <term name="{Term}"><![CDATA[{definition or relationship resolved during the session}]]></term>
  </resolved_language>
  <decisions>
    <decision adr="{ADR link if one was created}"><![CDATA[{Decision made}]]></decision>
  </decisions>
  <open_questions>
    <open_question owner="{owner if known}"><![CDATA[{Question that remains unresolved and next step}]]></open_question>
  </open_questions>
  <follow_ups>
    <follow_up><![CDATA[{Documentation, code, test, or planning action to take next}]]></follow_up>
  </follow_ups>
</alejo_questions>
```

## Rules

- Record every visible question asked during the session with its sequential question number.
- Preserve the same question number used in the live Alejo Questions prompt.
- Preserve the recommendation that accompanied each question.
- Capture the user's actual answer or correction.
- Link to files when evidence came from code or docs.
- Mark unresolved contradictions directly instead of smoothing them over.
- Do not include hidden reasoning or private deliberation.
- Use CDATA for user-supplied prose, quotes, code-like text, and evidence snippets.
