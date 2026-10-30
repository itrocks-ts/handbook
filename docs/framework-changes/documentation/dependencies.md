# Dependency documentation

For consumer-supplied dependencies, add `docs/dependencies.md` to the affected package and link it from its README.
Follow [documentation conventions](markdown.md).

Cover:

- Defaults and behaviour for each dependency.
- The functions or values supplied by it.rocks, with links to their owning package's documentation headings.
- Configuration showing how a consumer supplies it outside it.rocks.

Use `bind()` in [framework/src/dependencies.ts](../../../../framework/src/dependencies.ts) as the source of truth.
`src/framework.ts` calls it but does not define the bindings.
Describe the mapping without copying the framework implementation.
