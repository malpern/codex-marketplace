# VoxClaw Plugin Demo

This plugin is meant to give Codex a stable voice-output surface during coding work.

## What to try

Health check:

```bash
plugins/voxclaw/scripts/voxclaw-say --health
```

Speak a direct message:

```bash
plugins/voxclaw/scripts/voxclaw-say "Task complete. Tests passed."
```

Pipe a generated summary:

```bash
printf '%s\n' "Build failed. The parser tests are failing after the networking changes." | \
  plugins/voxclaw/scripts/voxclaw-say
```

Use a remote VoxClaw listener:

```bash
plugins/voxclaw/scripts/voxclaw-say \
  --url http://192.168.1.50:4140/read \
  --voice nova \
  --rate 1.2 \
  "Deployment complete."
```

## Agent patterns

Use `voxclaw-read-task-summary` when finishing work:

```text
Summarize the completed work in 1 to 3 spoken sentences, then send it through plugins/voxclaw/scripts/voxclaw-say.
```

Use `voxclaw-read-test-failures` when verification fails:

```text
Condense the failing tests into one short spoken sentence and send it through plugins/voxclaw/scripts/voxclaw-say.
```

## Notes on manifest confidence

As of April 19, 2026, OpenAI's Codex docs explicitly document a richer `plugin.json` example including `version`, `author`, `repository`, `license`, `keywords`, `skills`, and extended `interface` metadata. This marketplace uses that richer shape for VoxClaw.
