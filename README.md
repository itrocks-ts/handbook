[![npm version](https://img.shields.io/npm/v/@itrocks/handbook?logo=npm)](https://www.npmjs.org/package/@itrocks/handbook)
[![npm downloads](https://img.shields.io/npm/dm/@itrocks/handbook)](https://www.npmjs.org/package/@itrocks/handbook)
[![GitHub](https://img.shields.io/github/last-commit/itrocks-ts/handbook?color=2dba4e&label=commit&logo=github)](https://github.com/itrocks-ts/handbook)
[![issues](https://img.shields.io/github/issues/itrocks-ts/handbook)](https://github.com/itrocks-ts/handbook/issues)
[![discord](https://img.shields.io/discord/1314141024020467782?color=7289da&label=discord&logo=discord&logoColor=white)](https://25.re/ditr)

# handbook

Provides framework usage and development guides for developers and AI agents.

## Installation

```bash
npm i --save-dev @itrocks/handbook
```

## Usage

Reference `node_modules/@itrocks/handbook/AGENTS.md` from the application's root `AGENTS.md`.
The [agent entry point](AGENTS.md) routes tasks to the relevant documentation.

Developers can start directly with [framework usage](docs/framework-usage/README.md),
[framework changes](docs/framework-changes/README.md) or [agent conventions](docs/agent-conventions/README.md).

This package contains documentation only and has no runtime API or build step.
Conventions live in this package. Framework usage and reference implementations link to the installed `@itrocks`
packages.

For package setup, builds, dependency checks and releases, use the
[development tools guide](docs/framework-changes/development-tools.md).

## Documentation layout

```text
docs/
├── framework-usage/
│   ├── README.md
│   └── coding-conventions.md
├── framework-changes/
│   ├── README.md
│   ├── development-tools.md
│   ├── architecture/
│   │   ├── README.md
│   │   └── topic-specific guides
│   └── documentation/
│       ├── dependencies.md
│       ├── markdown.md
│       ├── package-metadata.md
│       └── readme.md
└── agent-conventions/
    └── README.md
```
