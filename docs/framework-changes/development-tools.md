# Development tools

Use [`@itrocks/dev`](../../../dev/README.md) from the application root to work on the framework packages installed
under `node_modules/@itrocks/`. Install it with `npm i --save-dev @itrocks/dev`.
The package owns the commands and operational procedures; this guide explains when to use them.

## Choose an operation

- **Start editing framework sources, or refresh local checkouts:** use `npx vcs-modules`. It replaces npm distributions
  with Git checkouts, updates existing repositories, builds packages in dependency order and configures WebStorm.
  It can install dependencies and replace package directories; inspect its output for skipped repositories or builds.
  It skips pulling repositories with pending work. Use it when setting up or refreshing the environment.
- **Rebuild while editing:** use `npx wsbuild`. Keep it running while changing package TypeScript, styles or assets.
  For a single build, run the affected package's `npm run build`; run its applicable tests separately.
- **Understand package order, missing installed packages or cycles:** use `npx dependency-levels`. It reads internal
  declarations across all dependency sections and prints levels and blocked packages. This checks the declared graph;
  use the source audit below to check whether declarations match actual use.
- **Review available dependency upgrades:** use `npx check-majors`. It queries npm and reports major/minor upgrades.
  Use `npx check-majors upgrade` when choosing to update package manifests; this does not install the new dependencies.
  Review the resulting changes, then install, build and test as appropriate for the update.
- **Review packages ready to publish:** use `npx it-publish --dry`. It compares local and registry versions without
  publishing. After completing the intended builds, tests and version changes, use `npx it-publish` when publication
  is requested. It publishes packages whose local version is ahead; it does not build them or change their manifests.
- **Review dependency correctness:** ask an agent to run the [dependency audit](../../../dev/docs/dependency-audit.md).
  The procedure uses scripts for inventory and comparisons, then targeted review for ambiguous cases, assets and
  typings. Scripts, temporary configurations and reports belong in `<application-root>/tmp/`.

All commands accept `--help`. Check the [command documentation](../../../dev/README.md#commands) for detailed behaviour.

## Before a major release

Consider a full dependency audit before a major release, particularly after changes spanning several packages.
The developer decides when to run it; a full audit is not required for every framework package edit.
Between releases, it can also help investigate dependency failures or check a deliberate dependency cleanup.

Review audit findings, apply the intended corrections, then repeat the relevant comparisons and type checks.
Build and test the release packages, review `npx it-publish --dry`, and publish when requested.
Keep dependency upgrades separate when they are not part of the release scope.

## Guidance for agents

Select the operation matching the developer's request and existing authorisation. For a routine source change,
build and test the affected packages; run the full dependency audit when requested or recommend it for a major release.
Follow the procedure in `@itrocks/dev` rather than maintaining a separate audit implementation in this handbook.
