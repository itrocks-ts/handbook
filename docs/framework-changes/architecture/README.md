# Architecture routing

Read only the guides for the contracts or responsibilities being changed. Combine guides when a task crosses boundaries.
A package is a published `@itrocks/*` module; `HasPlugins` and `Plugin<T>` refer specifically to browser extensions.

- Files, naming, metadata, outputs or build: [structure and build](package-structure-and-build.md).
- Responsibility, public API or server/browser separation: [boundaries](package-boundaries.md).
- Reuse, extension mechanism or port: [reuse](framework-reuse.md).
- Model, decorator, reflection or inheritance: [domain metadata](domain-model-and-metadata.md).
- Dependency binding, configuration or bootstrap: [composition](dependency-composition.md).
- Request, route, action, response or workflow: [actions and routes](requests-actions-and-routes.md).
- Conversion or view metadata: [transformations and views](transformations-and-views.md).
- Template, include, fragment or target: [HTML templates](html-templates-and-targets.md).
- DOM activation, navigation or browser plugin: [browser components](browser-components.md).
- Selector, UI state, stylesheet or asset: [SCSS and assets](scss-and-assets.md).
- Storage, relations, schema or database adapter: [persistence](persistence-and-schema.md).

Reference implementation paths in these guides are relative to `node_modules/@itrocks/`.
