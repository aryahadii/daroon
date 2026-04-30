<p align="center">
  <img src="plugins/daroon/assets/logo.png" alt="Daroon" width="180">
</p>

# Daroon

Daroon is a small kit of Codex skills and plugins for people who use AI agents every day and want those agents to work with durable, local-first personal context.

The goal is to make Codex, Claude Code, Claude Cowork, OpenCode, and similar tools more personable and more useful by giving them a clean way to read and maintain a user's own knowledge base: projects, people, topics, logs, sources, and open loops.

## Current Scope

- A Codex plugin marketplace for installing local-first agent skills and app connectors.
- Daroon skills for reading, capturing, and curating file-first personal context.
- A Bear plugin that connects Codex to Bear notes through Bear's first-party BearCLI MCP server.

## Codex

This repository is intended to work as a Codex marketplace source:

```bash
codex plugin marketplace add git@github.com:aryahadii/daroon.git
```

Available plugins:

- `daroon`: durable personal context skills for agents.
- `bear`: Bear note access through BearCLI MCP, with a conservative skill layer for note search, creation, and edits.

## License

MIT
