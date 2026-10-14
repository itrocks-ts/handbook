# HTML templates and targets

Render valid standalone HTML and identify the fragment for asynchronous navigation.
The action prepares a small named data context and owns business decisions.

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

Match block delimiters exactly. Keep selectors, attributes and action names consistent with browser and SCSS contracts.
Verify direct navigation and fragment insertion.

References: `template/src/template.ts`, `template-insight/src/template.ts`, `edit/src/edit.html`,
`xtarget/src/begin-end.ts`, `xtarget/src/composite.ts`.
