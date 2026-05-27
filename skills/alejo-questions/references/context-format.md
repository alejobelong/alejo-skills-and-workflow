# CONTEXT.xml Format

Use `CONTEXT.xml` as a glossary for project-specific domain language.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<context name="{Context Name}">
  <responsibility><![CDATA[{One or two sentences explaining what this context is responsible for.}]]></responsibility>
  <language>
    <term canonical="{Canonical Term}">
      <definition><![CDATA[{One-sentence definition of what the term is.}]]></definition>
      <avoid><![CDATA[{near-synonyms or ambiguous aliases}]]></avoid>
    </term>
  </language>
  <relationships>
    <relationship><![CDATA[An {Entity} {relationship} one or more {Other Entities}.]]></relationship>
    <relationship><![CDATA[A {Thing} belongs to exactly one {Owner}.]]></relationship>
  </relationships>
  <example_dialogue>
    <turn speaker="developer"><![CDATA[{A realistic question using the canonical terms.}]]></turn>
    <turn speaker="domain_expert"><![CDATA[{A short answer that clarifies boundaries between terms.}]]></turn>
  </example_dialogue>
  <flagged_ambiguities>
    <ambiguity word="{ambiguous word}">
      <meaning><![CDATA[{Concept A}]]></meaning>
      <meaning><![CDATA[{Concept B}]]></meaning>
      <resolution><![CDATA[{decision}]]></resolution>
    </ambiguity>
  </flagged_ambiguities>
</context>
```

## Rules

- Pick one canonical term when multiple words compete for the same concept.
- Define what the term is, not how the code implements it.
- Keep definitions to one sentence.
- Show important relationships and cardinality when known.
- Include only domain-specific concepts, not general programming concepts.
- Group terms with sub-elements only when natural clusters emerge.
- Keep stale ambiguity notes only when they help future readers avoid repeating the confusion.
- Use CDATA for natural language so domain terms cannot be confused with XML structure.

## Context Maps

For multi-context repos, maintain a root `CONTEXT-MAP.xml` that points to each context's glossary:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<context_map>
  <contexts>
    <context name="Ordering" path="./src/ordering/CONTEXT.xml"><![CDATA[receives and tracks orders]]></context>
    <context name="Billing" path="./src/billing/CONTEXT.xml"><![CDATA[issues invoices and records payments]]></context>
  </contexts>
  <relationships>
    <relationship from="Ordering" to="Billing"><![CDATA[Ordering emits events that Billing consumes.]]></relationship>
  </relationships>
</context_map>
```
