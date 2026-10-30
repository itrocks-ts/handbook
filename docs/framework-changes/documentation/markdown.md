# Documentation conventions

Write in UK English. These rules apply to all Markdown; content requirements are routed by
[framework changes](../README.md).

## Content

Document the current state only. When updating or moving documentation, remove obsolete content and redirect stubs;
do not retain migration notices, previous behaviour or comparisons with earlier versions.

Organise package READMEs and supporting documentation in this order, including only applicable sections:

1. Normal usage and capabilities shared by it.rocks and other contexts.
2. Configuration, conventions and behaviour specific to integration with the it.rocks framework.
3. Usage outside the it.rocks framework: both standalone applications and integration with other frameworks,
   including manual setup and capabilities specific to those contexts.

Name context-specific sections explicitly. Keep manual setup and adapter wiring out of shared usage when it.rocks
already supplies them. Put dependency binding details in [dependency documentation](dependencies.md), linked from
the relevant context section.

## Formatting

- Limit source lines to 120 columns, including Markdown syntax. Only indivisible content such as URLs may exceed it.
- Wrap prose at natural phrase boundaries; keep code examples within the limit where syntax permits.
- Align table pipes with padding and size separator cells to their columns, preserving alignment markers.
- If a table exceeds the limit, shorten cells or split it. Realign it after edits.
- Use sentence case headings, one level-one title and hierarchical heading levels.
- Mark packages, symbols, commands, filenames and literal values with backticks.
- Link to existing explanations rather than repeating them. Use relative links within this documentation package.
