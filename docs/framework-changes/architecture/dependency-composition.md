# Dependency composition

For the choice between direct import, injection, port and composition, read [reuse](framework-reuse.md).

Expose a small typed `Dependencies` contract with deterministic local defaults and one `*DependsOn`,
`set*Dependencies` or `init*` entry. Merge `Partial<Dependencies>` without erasing unspecified defaults.
When an existing function directly fulfils a dependency, preserve its name, parameter meaning and order so bootstrap
can bind it directly. Add an adapter only when values or semantics differ.

Bootstrap order: load layered configuration, install export composition, bind dependencies and transformer registries,
then start servers. Avoid import-time metadata reads that freeze configuration before binding.

Configuration merges in dependency order; application files override or extend it.
Use `config.compose` and `@itrocks/compose` for import-compatible exported class replacement or `@Uses` augmentation.
Keep replacement chains short and check order-dependent method and metadata resolution.
Do not use export composition for ordinary function dependencies or browser `Plugin<T>` for server injection.

References: `framework/src/dependencies.ts`, `framework/src/framework.ts`, `config/src/config.ts`,
`compose/src/compose.ts`.

## Module paths in YAML

Use `.` for the entry point of the package declaring `config.yaml`, as resolved by Node.js from `package.json`.
`'@'` is an alias for `.`. Use `':ExportName'` to select a named export directly from that entry point.
Use a `./` path for another script in the same application or package and a package specifier for an external module.
Point to the script that runs at runtime, such as a compiled file in `./cjs/` in a TypeScript package.

In file and module references, a single leading slash starts at `appDir`. Use two leading slashes to start at
the filesystem root, for example `//var/lib/ticket/sessions` for the directory `/var/lib/ticket/sessions`.
This applies to route destinations, both sides of `compose`, modules in `container.data`, `dataSource.engine`,
`container.file`, `session.path` and top-level paths read through `configPath()`, such as `dataPath`.
HTTP route keys and web asset URLs keep their URL semantics.

In `routes` and `compose`, omit `:ExportName` when the script exposes a single class and the short form resolves
to that class. Both resolvers prefer the default export. Without a default, routes select the first function or
class and composition selects the first runtime export. Name the export when the short form would be ambiguous
or select another value.

```yaml
compose:
  '@itrocks/mysql:Mysql': './cjs/maintains'
routes:
  /counter: .
```

The `@itrocks/custom-list` entry point exports `CustomList`, so its `config.yaml` can refer to it directly.

```yaml
routes:
  /custom-list: ':CustomList'
```
