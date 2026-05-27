# ADR XML Format

ADRs live in `docs/adr/` unless a context-local ADR directory already exists. Use sequential numbering:

```text
0001-short-slug.xml
0002-short-slug.xml
```

## Minimal Template

```xml
<?xml version="1.0" encoding="UTF-8"?>
<adr id="{0001}" status="accepted">
  <title>{Short Decision Title}</title>
  <context><![CDATA[{One to three sentences explaining the context.}]]></context>
  <decision><![CDATA[{The decision that was chosen.}]]></decision>
  <rationale><![CDATA[{Why this decision was chosen.}]]></rationale>
</adr>
```

That is enough for most ADRs. Add sections only when they preserve useful context.

## Optional Sections

```xml
<adr id="{0001}" status="accepted">
  <considered_options>
    <option id="A"><![CDATA[{Option A}]]></option>
    <option id="B"><![CDATA[{Option B}]]></option>
  </considered_options>
  <consequences>
    <consequence><![CDATA[{Non-obvious consequence}]]></consequence>
  </consequences>
</adr>
```

## When To Create One

Create an ADR only when all three conditions hold:

- The decision would be costly to reverse.
- The choice would surprise a future reader without context.
- The team chose between real alternatives with meaningful trade-offs.

Good ADR subjects include architecture boundaries, cross-context integration patterns, lock-in technology choices, deliberate deviations from common practice, and constraints invisible in the code.

Use CDATA for user-supplied language, code-like text, or quoted evidence.
