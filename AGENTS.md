# it.rocks handbook

Read the guide matching the task before making changes, then follow the documents it references.
Paths below are relative to this package.

- Use the framework in an application: [framework usage](docs/framework-usage/README.md).
- Modify or create framework packages: [framework changes](docs/framework-changes/README.md).
- Update instructions or conventions for AI agents: [agent conventions](docs/agent-conventions/README.md).

If a task spans several categories, read each applicable guide.

## Development task completion

End every development task on an application or framework package with a proposed commit message.
Write proposed and authored commit messages in English for every development task.
Keep it as short and concise as possible. Wherever possible, describe the change from the application or package
user's perspective, using wording they can understand.
Before writing it, inspect each affected Git repository's status and complete pending diff, including
staged, unstaged and untracked files, to account for work already in progress.

Group related changes into atomic commits. If the pending changes warrant several commits, propose a short message
for each and list the files to include, identifying the relevant hunks when a file spans several commits.
Keep proposals separate for distinct repositories and cover all changes assigned to each commit.
Proposing messages does not authorise creating commits.
