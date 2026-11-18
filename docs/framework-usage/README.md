# Framework usage

Read the [framework README](../../../framework/README.md) for application setup and configuration,
then the owning package's README for the feature being used.

Read only the conventions needed by the task:

- Application source: [coding conventions](coding-conventions.md).
- New business views, object forms and structured modal content: [structured business views](structured-views.md).
- HTML syntax, fragments and front-end assets:
  [templates and targets](../framework-changes/architecture/html-templates-and-targets.md).
- Markdown: [documentation conventions](../framework-changes/documentation/markdown.md).
- Framework extension or integration: select the relevant [architecture
guide](../framework-changes/architecture/README.md).

Keep application overrides in application configuration. Import public package entries or exported subpaths;
do not depend on another package's private implementation.
