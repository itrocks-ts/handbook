# it.rocks handbook

Read the guide matching the task before making changes, then follow the documents it references.
Paths below are relative to this package.

- Use the framework in an application: [framework usage](docs/framework-usage/README.md).
- Modify or create framework packages: [framework changes](docs/framework-changes/README.md).
- Update instructions or conventions for AI agents: [agent conventions](docs/agent-conventions/README.md).

If a task spans several categories, read each applicable guide.

## Commits

- End every application or framework development task with proposed commit messages.
- Keep proposed and authored messages short and in English. Describe the behaviour change from the closest
  user perspective: user > functionality > developer. For purely technical changes, use simple and beginner-friendly
  developer language (KISS).
- Cover all pending changes in each repository; for multiple commits, list each commit's files and shared-file hunks.
- For changes generated or modified by agents or subagents, add one trailer identifying contributing AI identity:
  `AI-assisted-by: <Agent tool> <AI name> <version> <model> <reasoning level>`
  (e.g. `AI-assisted-by: Codex GPT 6.1 sol high`). Capitalise the tool name.
  Use the contributing agent's execution metadata: preserve the full model version, including minor/patch versions
  and variant (e.g. `gpt-6.1-sol` becomes `GPT 6.1 sol`), and the actual reasoning level.
  Do not infer these from the agent's self-description, a parent agent or a requested profile.
  Include only known fields; omit missing information without placeholders or explanatory comments.
  Keep human-only and AI-generated changes in separate commits where practical for targeted reviews.
