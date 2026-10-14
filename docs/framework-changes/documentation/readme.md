# Package README content

Follow [documentation conventions](markdown.md) and review
[package metadata](package-metadata.md) alongside the README.

Document developer-facing usage and the current public contract. Move dependency binding and framework wiring to
[dependency documentation](dependencies.md), linked from the README.

## Opening

Start with these badges, replacing `<package>` with the unscoped package name:

```markdown
[![npm version](https://img.shields.io/npm/v/@itrocks/<package>?logo=npm)](https://www.npmjs.org/package/@itrocks/<package>)
[![npm downloads](https://img.shields.io/npm/dm/@itrocks/<package>)](https://www.npmjs.org/package/@itrocks/<package>)
[![GitHub](https://img.shields.io/github/last-commit/itrocks-ts/<package>?color=2dba4e&label=commit&logo=github)](https://github.com/itrocks-ts/<package>)
[![issues](https://img.shields.io/github/issues/itrocks-ts/<package>)](https://github.com/itrocks-ts/<package>/issues)
[![discord](https://img.shields.io/discord/1314141024020467782?color=7289da&label=discord&logo=discord&logoColor=white)](https://25.re/ditr)
```

Use the unscoped package name as the title, followed by the canonical description from package metadata.

## Content selection

Include only useful sections, in usage order:

- Actual prerequisites and installation: `npm i @itrocks/<package>`; use `--save-dev` for development tools.
- Required concepts or initialisation order, then the smallest complete usage example and observable result.
- Public API: signatures, defaults, return values, side effects and non-obvious constraints.
- Limitations or recurring mistakes where they help prevent misuse.

Document public exports except wiring-only exports, which belong in dependency documentation.
For decorators, explain targets, inheritance and omitted or `false` arguments.
For callbacks, specify the signature and invocation timing. For commands, describe inputs, filesystem or registry
changes, output, exit behaviour and any dry-run mode.

Examples must use actual exports, include necessary imports, use `await` for asynchronous calls and state filenames
when several files participate. Use fenced blocks with the appropriate language.

A dependency bundle lists its packages and their roles, states whether it exports runtime code and shows imports
from the owning packages. Browser packages show script and stylesheet imports plus dynamic DOM activation requirements.

Link the first useful mention of another package to its repository or relevant heading; use authoritative sources
for platform concepts. Check examples and API claims against source, exports and generated files, and remove obsolete
instructions with the corresponding implementation.
