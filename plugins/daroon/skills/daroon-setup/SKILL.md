---
name: daroon-setup
description: Set up or repair Daroon's local workspace pointer and workspace boilerplate. Use when ~/.daroon/current is missing, broken, not a directory, lacks DAROON.md, or the user asks to initialize, link, relink, verify, or repair Daroon setup.
---

# Daroon Setup

This skill is the setup and repair layer for Daroon. It exists so the normal `daroon`, `daroon-capture`, and `daroon-curate` skills can assume a stable workspace pointer at `~/.daroon/current`.

## Desired Outcome

Daroon is ready when:
- `~/.daroon/current` exists as a symlink to the active Daroon workspace.
- The resolved workspace contains `DAROON.md`.
- The workspace contains the expected Daroon directories.
- The user understands what was created, repaired, or left unchanged.

## Agent Behavior

When setup is missing or broken, explain that Daroon is not set up yet or the workspace pointer needs repair.

Help the user choose a workspace path. On macOS, recommend `~/Library/Mobile Documents/com~apple~CloudDocs/Daroon` because iCloud Drive can sync the workspace across Apple devices, but accept any custom path the user chooses.

Before changing anything, inspect the current state and summarize the intended outcome: the workspace path, missing files or directories to create, and whether `~/.daroon/current` will be created or relinked.

Missing boilerplate should get created additively. Existing file, directory, or symlink should not get overwritten unless the user explicitly approves that exact replacement.

If `~/.daroon/current` already exists but is not a symlink, treat it as a setup issue and ask before changing it.

After setup or repair, verify the desired outcome and hand control back to `daroon`.

## Workspace Boilerplate

### Default Workspace Structure

```text
DAROON.md
logs/
projects/
projects/archive/
people/
people/archive/
topics/
topics/archive/
sources/
sources/archive/
```

### Default `DAROON.md` Boilerplate

```markdown
# Daroon

Status: active

## What This Is

Daroon is a private, local-first knowledge base shared between a person and their AI agents.
It keeps durable context portable, inspectable, searchable, and useful across chats, tools, repos, and time.

## Active Pointers

### People

### Projects

### Topics

### Sources And Logs

- `logs/`
- `sources/`
```

## Safety Rules

- Prefer an explicit user-provided workspace path over guessing.
- Do not invent a new canonical workspace path silently.
- Do not overwrite existing Daroon files.
- Do not replace an existing symlink, file, or directory without explicit approval.
- If `DAROON.md` exists, leave it unchanged unless the user asks to edit it.
- Treat repair as additive by default: create missing pieces, relink only with approval, and report anything unusual.
