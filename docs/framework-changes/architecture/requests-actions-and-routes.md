# Requests, actions and routes

Keep transport-neutral data in `request-response`, URL interpretation in `action-request` and adapter details in the
server adapter.

Pipeline: adapter request → `action-request.Request` → route resolution → format method on an action → generic response.
The URL shape is `/route[/ids][/action][/format]`; the request resolves the domain type and lazily loads objects.
Default operations: collection `GET` → `list`, identified `GET` → `output`, `POST` → `save`, `DELETE` → `delete`.
Declare explicit routes for other operations.

- Configure destinations as module paths with optional `:ExportName`.
- Use `@Route` for reusable action identity and link generation.
- Extend `Action<T>` for format-specific operations (`html`, `json`, etc.); share domain work below those methods.
- Return `htmlResponse`, `htmlTemplateResponse` or `jsonResponse`, not adapter-specific responses.
- Use `@Need('object', alternative)` or `@Need('Store', alternative)` for structural prerequisites;
  authorisation and business validation remain explicit logic.
- Use the request's resolved type and objects, or `DataSource`; do not reparse identifiers in each action.

`@Actions` declares available operations. `ActionFlow(from, to, definition)` and the action repository describe UI links
(caption, target, CSS, template); they do not register HTTP routes.
Check missing objects/stores, multiple identifiers, format negotiation and error statuses when changing the pipeline.

References: `action-request/src/action-request.ts`, `route/src/routes.ts`, `action/src/action.ts`,
`action/src/repository.ts`, `framework/src/main.ts`.
