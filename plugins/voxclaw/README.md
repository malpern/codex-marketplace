# VoxClaw Plugin

Installable Codex plugin for using VoxClaw as a voice output layer.

This same plugin directory also ships a Claude Code plugin manifest, slash commands, a subagent, and a PATH wrapper for `voxclaw-say`.

This plugin packages a reusable skill so Codex can:

- send text to a running VoxClaw listener over HTTP
- use a stable helper script instead of duplicating curl logic
- prefer a human-provided VoxClaw setup pointer when available
- fall back to the local `voxclaw` CLI when appropriate
- package workflow-specific speaking skills for coding sessions

The packaged skill is derived from the main VoxClaw project:
[VoxClaw SKILL.md](https://github.com/malpern/VoxClaw/blob/main/SKILL.md).

The plugin manifest in this marketplace follows the richer field set documented in OpenAI's Codex plugin build guide, including publisher metadata and install-surface `interface` fields.

## Runtime surfaces

Codex:

- skill-first workflow
- shared helper script
- marketplace installation through `codex marketplace add`

Claude Code:

- `.claude-plugin/plugin.json`
- slash commands such as `/voxclaw:say` and `/voxclaw:announce-tests`
- `spoken-update` subagent
- `voxclaw-say` exposed on `PATH` through `bin/`

## Helper script

Use the plugin helper as the default integration surface:

```bash
plugins/voxclaw/scripts/voxclaw-say "Build passed"
plugins/voxclaw/scripts/voxclaw-say --health
plugins/voxclaw/scripts/voxclaw-say --url http://192.168.1.50:4140/read "Hello from Codex"
plugins/voxclaw/scripts/voxclaw-say --voice nova --rate 1.2 "Heads up"
```

Behavior:

- If `--url` is provided, send to that `/read` endpoint.
- Else if local listener health passes on `localhost:4140`, send over HTTP.
- Else if the `voxclaw` CLI is installed, invoke the CLI directly.
- Else fail with a clear error.

The helper also accepts stdin:

```bash
printf '%s\n' "Task complete. Tests passed." | plugins/voxclaw/scripts/voxclaw-say
```

## Included skills

- `voxclaw`: general voice output
- `voxclaw-read-task-summary`: speak a short completion summary
- `voxclaw-read-test-failures`: speak a short failure summary

## Claude Code features

- `/voxclaw:say`
- `/voxclaw:status`
- `/voxclaw:announce-tests`
- `spoken-update` agent
- `voxclaw-say` available as a bare command while the plugin is enabled

## Demo and verification

- Demo guide: `plugins/voxclaw/DEMO.md`
- Smoke test: `plugins/voxclaw/scripts/smoke-test`
