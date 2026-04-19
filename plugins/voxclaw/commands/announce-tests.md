---
description: Condense the latest failing tests or build errors into one spoken update with VoxClaw.
---

Create one short spoken status update for the latest build or test result.

Guidelines:

- Lead with pass or fail.
- Mention the failing suite, subsystem, or error class.
- Do not read stack traces or long assertion text aloud.
- Keep the spoken summary to one sentence when possible.

Then run:

```bash
voxclaw-say "<spoken failure summary>"
```
