# Dependency composition

For the choice between direct import, injection, port and composition, read [reuse](framework-reuse.md).

Expose a small typed `Dependencies` contract with deterministic local defaults and one `*DependsOn`,
`set*Dependencies` or `init*` entry. Merge `Partial<Dependencies>` without erasing unspecified defaults.
When an existing function directly fulfils a dependency, preserve its name, parameter meaning and order so bootstrap
can bind it directly. Add an adapter only when values or semantics differ.

Bootstrap order: load layered configuration, install export composition, bind dependencies and transformer registries,
then start servers. Avoid import-time metadata reads that freeze configuration before binding.

Configuration merges in dependency order; application files override or extend it.
Relative paths belong to the configuration file declaring them.
Use `config.compose` and `@itrocks/compose` for import-compatible exported class replacement or `@Uses` augmentation.
Keep replacement chains short and check order-dependent method and metadata resolution.
Do not use export composition for ordinary function dependencies or browser `Plugin<T>` for server injection.

References: `framework/src/dependencies.ts`, `framework/src/framework.ts`, `config/src/config.ts`,
`compose/src/compose.ts`.
