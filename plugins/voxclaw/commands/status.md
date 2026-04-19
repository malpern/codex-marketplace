---
description: Check whether VoxClaw is reachable from Claude Code.
---

Check VoxClaw availability before trying to speak.

Run:

```bash
voxclaw-say --health
```

If health succeeds, report the healthy endpoint briefly.
If health fails, explain whether the likely issue is:

- VoxClaw not running locally
- the network listener is disabled
- a remote URL was not provided and no local CLI is installed
