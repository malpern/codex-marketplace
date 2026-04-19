# Codex Marketplace

Installable Codex plugins published by Michael Alpern.

This repository is a standalone Codex marketplace so users can add one remote source and install VoxClaw without depending on the internal layout of the main app repository.

## Included plugins

- `voxclaw`: voice output for Codex through the VoxClaw macOS app, local CLI, or local HTTP listener

## Intended install flow

In Codex:

```bash
codex marketplace add malpern/codex-marketplace
```

Then install the `voxclaw` plugin from that marketplace.

## Repository layout

```text
marketplace.json
plugins/
  voxclaw/
    .codex-plugin/plugin.json
    skills/
    scripts/
    README.md
```

## Status

This marketplace is ready for local and remote marketplace-based installation.

OpenAI's official self-serve submission flow for the public Codex Plugin Directory was not publicly open as of April 19, 2026, so this repository is designed for GitHub-hosted marketplace distribution first.
