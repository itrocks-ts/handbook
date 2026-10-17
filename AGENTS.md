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
- For changes generated or modified by agents or subagents, add an `AI-assisted-by` trailer for each distinct
  contributing agent identity:
  `AI-assisted-by: <Agent tool> <tool version> <AI name> <AI version> <model variant> <reasoning level>`
  (e.g. `AI-assisted-by: Codex 0.162.0-alpha.17.2 GPT 6.1 sol medium`). Capitalise the tool name.
- Before proposing or authoring any commit, **read the contributing session's actual metadata or tool logs**.
  This lookup is mandatory even when the system prompt provides a generic model name. Preserve the full tool version,
  non-zero AI minor/patch versions, model variant and actual reasoning level; never infer them from defaults or examples.
  For Codex, locate the session log using `CODEX_THREAD_ID` or `CODEX_SESSION_ID` under `$CODEX_HOME/sessions`
  (default `~/.codex/sessions`). Read `session_meta.cli_version` and the contributing turns' `turn_context.model`
  and `turn_context.effort`. Inspect each subagent's own session when it contributed changes.
- Omit a field only after checking the corresponding metadata/logs and finding it unavailable. Never shorten a known
  `gpt-6.1-sol` to `GPT-6`, or omit a known reasoning level. After committing, read back the stored commit message and
  verify every trailer against the retrieved metadata. Keep unrelated log contents out of commit messages.
- Keep human-only and AI-generated changes in separate commits where practical for targeted reviews.
