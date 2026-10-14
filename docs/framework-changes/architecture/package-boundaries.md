# Package boundaries

Give each package one coherent responsibility and the smallest public contract its consumers need.
Domain and reusable infrastructure packages must remain independent of `@itrocks/framework` and concrete adapters.
The framework binds implementations and starts the application.

- Separate server and browser surfaces. Browser imports must not load Node.js APIs or CommonJS-only modules.
- Expose named exports through a facade or explicit subpaths.
- Reserve side-effect modules such as `build.js` for activation; ordinary API imports must not start servers or
  mutate global registries.
- Keep declarative routes, menus and other contributions package-local and additive; application overrides belong
  in application configuration.
- Keep tests and demos outside runtime entries.

For source layout and generated outputs, follow [structure and build](package-structure-and-build.md).
For dependency direction and extension choices, follow [reuse](framework-reuse.md).

References: `action/src/action.ts`, `framework/src/front/app.ts`, `list/src/front/build.ts`.
