# Package structure and build

Preserve an existing package's layout unless migrating it. For new packages, use kebab-case filenames and one concern
per file. Author runtime files in `src/`; never hand-edit generated JS, declarations, CSS or copied assets.

## Layout by surface

- Backend: `src/*.ts` → `cjs/`, with a root export and optional subpaths. Reference: `required`.
- Backend with templates: HTML → `cjs/`; SCSS and assets → `css/`. Reference: `action`.
- Mixed: backend in `src/`, browser in `src/front/`; browser outputs at package root. Reference: `list`.
- Browser-only: ES modules published as root subpaths. Reference: `xtarget`.
- CSS-only: SCSS partials and entries in `css/`. Reference: `ux-core`.
- Metadata or documentation only: no TypeScript configuration or runtime entry.

Keep owning HTML, SCSS and assets beside their source; tests in `test/`; declarative contributions in `config.yaml`.
Name the facade after the package unless `index.ts` is the intended public entry.
Use `build.ts` for browser registration and `transformers.ts` for transformer registration.
Use separate CJS/ESM builds only when consumers require both; reference `route`.

## Compiler and publication

Start from the closest reference package and remove unused options.
Backend defaults: strict checking, declarations, `module: nodenext`, `rootDir: src`, `outDir: cjs`, source maps,
consistent casing and skipped library checking. Add Node types or legacy decorators only when needed.
Exclude `src/front` from the backend build. Mixed browser builds extend the base configuration with `module: esnext`,
`target: es2022`, no source maps and the intended public output directory.
Use `@itrocks/prepare-module` where compiled browser subpaths must be copied to the root.

Package metadata includes author, description, keywords, homepage, license, scoped name, repository and version.
Start an unreleased package at `0.0.1`; do not bump existing versions incidentally.
Use `itrocks-ts/<package>` for the repository and keep the license consistent with `LICENSE`.

- Runtime imports belong in `dependencies`; internal packages use `latest`.
- Build and test tools belong in `devDependencies`; use optional dependencies only for optional integrations.
- Set `engines.node` to the project baseline for Node.js runtime packages.
- Declare the public entry with `exports`; browser packages may expose published subpaths.
- Use a positive `files` allowlist. Publish only existing files; exclude maps unless deliberately required.
- Copy HTML and assets explicitly; compile SCSS with `--no-source-map`.
- For Node tests, use `npm run build && node --test --test-isolation=none test/*.test.js`.

When moving a public file, update layout, compiler settings, exports, files, build, examples and tests together.
Run the applicable build and tests, then `npm pack --dry-run` to check the published files.

See [package metadata](../documentation/package-metadata.md) and [README content](../documentation/readme.md).
