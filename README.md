# Codex Marketplace

Installable Codex plugins published by Michael Alpern.

This repository is a standalone Codex marketplace so users can add one remote source and install VoxClaw without depending on the internal layout of the main app repository.

The main VoxClaw app, screenshots, releases, and website-linked product docs live in [malpern/VoxClaw](https://github.com/malpern/VoxClaw).

Website: [voxclaw.com](https://voxclaw.com/)

## Included plugins

- `voxclaw`: voice output for Codex through the VoxClaw macOS app, local CLI, or local HTTP listener

## Install

Codex:

```bash
codex marketplace add malpern/codex-marketplace
```

Claude Code:

```bash
claude plugin marketplace add malpern/codex-marketplace
```

## Repo boundary

Use this repository for:

- Codex marketplace metadata
- Claude Code marketplace metadata
- plugin packaging
- install docs for agent runtimes

Use [`malpern/VoxClaw`](https://github.com/malpern/VoxClaw) for:

- app source code
- screenshots and product presentation
- releases
- broader end-user usage docs

## Intended install flow

In Codex:

```bash
codex marketplace add malpern/codex-marketplace
```

Then install the `voxclaw` plugin from that marketplace.

In Claude Code:

```bash
/plugin marketplace add malpern/codex-marketplace
/plugin install voxclaw@malpern-marketplace
```

## Repository layout

```text
marketplace.json
.claude-plugin/
  marketplace.json
plugins/
  voxclaw/
    .claude-plugin/plugin.json
    .codex-plugin/plugin.json
    agents/
    bin/
    commands/
    skills/
    scripts/
    README.md
```

## Status

This marketplace is ready for local and remote marketplace-based installation.

OpenAI's official self-serve submission flow for the public Codex Plugin Directory was not publicly open as of April 19, 2026, so this repository is designed for GitHub-hosted marketplace distribution first.
