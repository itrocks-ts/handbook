# Framework reuse and extension

Search existing package names, exports, READMEs and source before creating infrastructure.
Reuse the narrowest public contract; import its public entry or exported subpath, never private files.

## Find the owner

- Model inspection: `reflect`, `property-type`, `property-default`, `class-type`.
- Semantics: existing decorators, otherwise `decorator` helpers.
- Class composition: `uses`; application export replacement: `compose`.
- Presentation: `class-view`, `property-view`, `list-properties`.
- Conversion: `transformer`, `core-transformers`, `data-to-object`.
- HTTP data: `request-response`, `core-responses`; URL/actions: `action-request`, `route`, `action`.
- Rendering: `template`, normally through `template-insight`.
- Storage/schema: `storage`, `store`, `schema`; concrete adapters remain outside domain code.
- Dynamic DOM: `build`; navigation/forms/assets: `xtarget`, `form-fetch`, `asset-loader`.
- Browser extensions: `plugin`; shared UI: `ux-core`, `action-bar`, `notifications`, `table`.

Use `business-pack` as the baseline for domain packages, `action-pack` for actions/views and `crud-pack` for standard
CRUD.
Import concrete APIs from their owners. Outside a documented pack, declare runtime owners directly rather than relying
on transitive dependencies.

## Select the extension

- Class/property fact: focused decorator and `*Of` accessor.
- Representation change: transformer.
- Behaviour supplied by a higher layer: typed `Dependencies`, defaults and `*DependsOn()` binding.
- Interchangeable stateful infrastructure: abstract port implemented by adapters.
- One-time registration: explicit `init*`, `set*` or side-effect `build` module.
- Optional browser host behaviour: `Plugin<T>`.
- Global exported class replacement/augmentation: configuration with `compose`/`Uses` at the composition root.

Use direct imports for stable lower-level contracts. Inject only where an import would create a cycle or point reusable
code towards framework, application, adapter or presentation code. Put ports where they are consumed, in domain terms.
Domain and reusable core must not import the framework or concrete server/database adapters.
For function dependencies, keep narrow typed contracts and deterministic defaults; for stateful lifecycles, prefer ports
and explicit construction. See [composition](dependency-composition.md) for binding and bootstrap rules.

References: `framework/src/dependencies.ts`, `core-transformers/src/core-transformers.ts`, `storage/src/data-source.ts`.
