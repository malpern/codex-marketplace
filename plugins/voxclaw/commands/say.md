---
description: Speak a short message or spoken summary aloud with VoxClaw.
argument-hint: "[message]"
---

Use VoxClaw to produce audible output.

Behavior:

- If the user provided arguments to this command, treat them as the text to speak.
- Otherwise, produce a concise 1 to 3 sentence spoken summary of the current state.
- Prefer outcomes, blockers, and verification status over file-by-file detail.
- Keep the spoken text natural and short.

Then run:

```bash
voxclaw-say "<text to speak>"
```

If the listener is unavailable, explain the failure briefly and suggest checking VoxClaw or running `/voxclaw:status`.
