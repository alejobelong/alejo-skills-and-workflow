# Domain Docs XML Shape

Use this XML shape for `docs/agents/domain.md`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<domain_docs>
  <purpose>Give Alejo skills one place to find project language before writing PRDs, SADs, issues, tests, or implementation names.</purpose>
  <conventions>
    <context_file>CONTEXT.xml</context_file>
    <context_map>CONTEXT-MAP.xml</context_map>
    <adr_files>docs/adr/*.xml</adr_files>
  </conventions>
  <creation_rule>alejo-questions creates or updates these docs when it resolves new terms or decisions.</creation_rule>
</domain_docs>
```
