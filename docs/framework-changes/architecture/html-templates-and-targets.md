# HTML templates and targets

Render valid standalone HTML and identify the fragment for asynchronous navigation.
The action prepares a small named data context and owns business decisions.

## Authoring and validation

Author page and fragment markup in HTML templates. Server actions prepare data; browser code enhances the rendered DOM.
Do not assemble view markup in TypeScript strings or construct entire views with DOM creation calls.

The rendered standalone document and the DOM after fragment insertion must pass the
[W3C Nu HTML Checker](https://validator.w3.org/nu/). Validate rendered output, with template expressions resolved,
including conditional branches and representative dynamic values. Check source templates for valid HTML structure too.
Use standard HTML and permitted ARIA attributes; application-specific metadata belongs in `data-*` attributes.
Do not invent bare attributes or rely on the browser silently repairing invalid nesting.
Context-dependent composite fragments can be enclosed in a `<template>` outside `BEGIN`/`END` to keep their standalone
document valid without inserting that wrapper into the live DOM.

## Expressions

- `{property.path}` reads a path; a non-class function is called on its owner.
- `{?property}` or `{property?}` suppresses the attribute contribution or block when falsy.
- `<!--items-->...<!--end-->` renders a truthy value once or iterates it with each item as context.
- `{./file.html}` includes a relative template with the current context.
- `{{template}}` resolves an included template path from data.
- `{@display}`, `{@output}`, `{@route}` read decorator semantics.
- `{%property.name}`, `{%orderedProperties}` traverse reflected metadata.

Use `data-if="{condition}" ... data-end` for several conditional attributes.
`template-insight` translates literal text; use `.tr` for data-derived strings needing translation.
Use `app://(expression)` for application URLs in `action`, `formaction`, `href`, `location` and `src`.

## Fragments and assets

- `<!--BEGIN-->` and `<!--END-->` delimit the asynchronous response fragment.
- `<!--#selector-->...<!--#end-->` updates a target; several target blocks may coexist.
- Target modes: `:content` (default), `:replace`, `:before`, `:after`, `:prepend`, `:append`, `:auto`.
- Reuse application-owned targets such as `main` and `#notifications:prepend`.

Keep language, title and required assets in the full document. Client navigation updates the title and imports missing
head styles/scripts without duplicating URLs. Includes retain asset dependencies; relative links become application
paths, with `node_modules/@itrocks` served as `/@itrocks/...` and other dependencies as `/lib/...`.

Declare template-specific CSS with `<link rel="stylesheet">` and JavaScript with `<script type="module" src="...">`
in that template's `<head>`, outside `BEGIN`/`END` when appropriate. These fragment markers do not prevent the framework
from processing the head: `xtarget` loads the declared assets when the HTML is first used and avoids duplicates.
Prefer these declarations over application-wide imports or script-driven asset loading.
Keep only shared application infrastructure and necessary context detection in the application entry.
When no HTML template owns an optional integration, load it at the relevant context and document why it is needed.
Framework adapters belong to the framework; importing a reusable package must not implicitly bind it to the framework.

Match block delimiters exactly. Keep selectors, attributes and action names consistent with browser and SCSS contracts.
Verify direct navigation and fragment insertion.

References: `template/src/template.ts`, `template-insight/src/template.ts`, `edit/src/edit.html`,
`xtarget/src/begin-end.ts`, `xtarget/src/composite.ts`.
