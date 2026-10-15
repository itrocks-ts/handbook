# Framework changes

Apply [package versioning](#package-versioning) as soon as the first file of a package is modified.

Read the affected package's README and local instructions, then select the applicable conventions:

- Source or tests: [coding conventions](../framework-usage/coding-conventions.md).
- Markdown: [documentation conventions](documentation/markdown.md).
- README: [README content](documentation/readme.md).
- Description or keywords: [package metadata](documentation/package-metadata.md).
- Dependency configuration documentation: [dependency documentation](documentation/dependencies.md).
- Architecture or integration contract: select the relevant [architecture guide](architecture/README.md).

For a new package, read [structure and build](architecture/package-structure-and-build.md),
[boundaries](architecture/package-boundaries.md), [reuse](architecture/framework-reuse.md),
README content and package metadata. Read coding conventions only if adding source.

A local implementation change preserving existing contracts does not require architecture reading.

For setup, rebuilds, dependency reviews and releases, see [development tools](development-tools.md).
The full dependency audit is optional: consider it before a major release or run it at the developer's request.

## Package versioning

When modifying a framework package, update its `package.json` version as soon as the first file is changed.
Choose the highest level required by the development: patch for fixes or documentation, minor for backwards-compatible
features, major for breaking changes.

First inspect `git diff HEAD -- package.json` in that package's repository, covering staged and unstaged changes.
Compare the working version with `HEAD`: if it already contains an increment at the required level or higher, keep it.
Otherwise, increment the required component from the `HEAD` version and reset lower components to zero.
Do not increment again for each file or follow-up change within the same pending development.

Reassess the level when the scope changes. For example, with `1.2.3` at `HEAD`, a fix becomes `1.2.4`; if it grows into
a backwards-compatible feature, replace that pending version with `1.3.0`. An existing `1.3.0` or `2.0.0` already covers
a further patch-level change.
