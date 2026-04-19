---
name: voxclaw
description: Give your agent a voice. Send text to a Mac running VoxClaw and hear it spoken aloud with OpenAI neural voices or Apple TTS.
homepage: https://github.com/malpern/VoxClaw
metadata: {"requires":{"bins":["curl"]}}
---

# VoxClaw

Use this skill when the user wants audible output from Codex or another agent.

VoxClaw runs on macOS as a menu bar app and can speak text through:

- the local `voxclaw` CLI
- the `voxclaw://read?text=...` URL scheme
- the HTTP listener, usually on port `4140`

## Preferred flow

If the human provides a VoxClaw setup pointer, use the provided `health_url` and `speak_url` directly.

Connection order:

1. Use `plugins/voxclaw/scripts/voxclaw-say --health` when working in this repo.
2. If a pointer is available, pass its `speak_url` or `health_url` to the helper.
3. Otherwise let the helper probe `http://localhost:4140/status`.
4. The helper falls back to the local `voxclaw` CLI when needed.

Never guess a `.local` hostname if the user already supplied a numeric LAN IP.

## Preferred command

Default to the helper script instead of open-coded `curl`:

```bash
plugins/voxclaw/scripts/voxclaw-say "Hello from Codex"
plugins/voxclaw/scripts/voxclaw-say --health
plugins/voxclaw/scripts/voxclaw-say --url http://192.168.1.50:4140/read "Deployment complete"
plugins/voxclaw/scripts/voxclaw-say --voice nova --rate 1.2 "Build failed"
plugins/voxclaw/scripts/voxclaw-say --instructions "Read warmly" "Welcome back"
```

## HTTP API

Health check:

```bash
curl -sS http://localhost:4140/status
```

Speak text:

```bash
curl -X POST http://localhost:4140/read \
  -H 'Content-Type: application/json' \
  -d '{"text":"Hello from Codex"}'
```

Optional fields:

- `voice`
- `rate`
- `instructions`

## CLI fallback

When VoxClaw is installed locally and the task is on the same Mac, the CLI is often the simplest path:

```bash
voxclaw "Hello from Codex"
```

Useful variants:

```bash
voxclaw --clipboard
voxclaw --file article.txt
voxclaw --voice nova "Build passed"
voxclaw --rate 1.3 "Build passed"
voxclaw --instructions "Read warmly" "Deployment complete"
voxclaw --send "Hello"   # send to an already running listener
voxclaw --status
```

## User experience guidance

- Audio leads, visuals follow.
- Do not trigger the overlay before audio is ready.
- Keep spoken summaries concise unless the user asks for full narration.

## Error handling

- If `/status` fails locally, tell the user VoxClaw is not running or the listener is disabled.
- If local status works but remote status fails, treat it as a network or firewall issue.
- If the user has no OpenAI API key configured, Apple TTS still works.
