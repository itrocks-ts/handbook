# Framework changes

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
