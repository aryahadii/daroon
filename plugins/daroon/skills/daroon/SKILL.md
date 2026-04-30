---
name: daroon
description: Use Daroon as the user's private, local-first knowledge base shared across AI agents. Use when durable context about projects, people, topics, decisions, preferences, sources, plans, or open loops may improve the answer or work.
---

# Daroon

Daroon is a private, local-first knowledge base shared between the user and the AI agents that work with them. It is not just hidden agent memory. It is an inspectable workspace of ordinary files where the user and agents can store, review, import, search, update, and cite durable context.

Daroon is valuable because it lets any current or future agent ground work in the user's accumulated context across chats, tools, repos, products, and time, while keeping the user in control of the same knowledge. It should reduce repeated explanation, preserve decisions and open loops, connect work to source material, and make future agents useful faster.

## Workspace

Default Daroon workspace root: `~/.daroon/current`.

`~/.daroon/current` is expected to be a stable symlink to the active Daroon workspace. If the user explicitly points to a different Daroon workspace, use that path instead.

If `~/.daroon/current` is missing, broken, not a directory, or does not contain `DAROON.md`, tell the user that Daroon is not set up yet or the workspace pointer needs repair. Then use `daroon-setup` to help them create, recreate, relink, or fix it before normal Daroon lookup, capture, or curation.

## What Lives Here

The exact structure is user-adaptable and should be described by `DAROON.md`, the workspace map and index.

- `DAROON.md` holds the active map, routing index, and high-level state of the knowledge base.
- Logs hold low-threshold chronological continuity: recent work, decisions, changes, open loops, and pointers for future agents.
- Maintained pages hold higher-confidence knowledge about projects, people, topics, preferences, plans, and recurring context.
- Sources hold evidence, imports, snapshots, exports, references, or raw material that may be too large or early to promote directly.
- Archives preserve older or inactive material without crowding the active surface.

Daroon should grow from both ongoing work and deliberate imports: chats, project notes, digital exports, source snapshots, and other user-approved material. It should stay useful to both the user and agents, not become a passive dump.

## When To Use It

Use Daroon when prior context could materially improve the result, prevent stale assumptions, continue an ongoing thread, recover project state, explain what is known about a person or topic, or decide whether new context should be captured or curated.

Skip Daroon for trivial, self-contained tasks where durable context would not change the answer.

## Default Behavior

- Start from the workspace map `DAROON.md`, then follow the smallest relevant set of files.
- Prefer narrow file reads over broad scans.
- Treat maintained pages as stronger evidence for durable facts, logs as stronger evidence for recent continuity, and sources as evidence rather than automatic truth.
- Keep answers grounded in the files actually read.
- Do not expose private context unless it is relevant to the user's request.

## Capture And Curation

If the current task creates future-useful continuity, use `daroon-capture`.
If recent captured context has become stable enough for canon, use `daroon-curate`.
