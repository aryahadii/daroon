---
name: daroon-capture
description: Capture future-useful context into Daroon during normal chat and project work. Use for lightweight continuity logs, source pointers, decisions, plans, preferences, and open loops that should be available to future agents.
---

# Daroon Capture

Capture new context when it is likely to help a future agent continue the user's work without forcing it into canon too early.

## Workspace

Default Daroon workspace root: `~/.daroon/current`.

Use the workspace map `DAROON.md` for placement. If it does not specify a capture convention, default to dated entries under `logs/` and source pointers or snapshots under source-specific folders such as `sources/`.

## Knowledge Base Shape

Capture works at Daroon's raw and recent-continuity layer. Keep the structure dynamic, but preserve these boundaries:

- Logs are low-threshold chronological continuity: what changed, what was decided, what remains open, and what source pointers matter.
- Maintained directories hold more structured knowledge such as project, person, topic, or source pages.
- Source directories preserve source material, snapshots, exports, or pointers that future curation may need.

## Default Behavior

- Capture lightweight logs, not polished canon.
- Preserve source boundaries and uncertainty.
- Keep entries concise and dated.
- Prefer routing pointers over duplicating large source material.
- Do not curate stable pages here; use `daroon-curate` for that.

## Good Capture Candidates

- New project direction or constraint.
- A decision the user accepted.
- A preference that should affect future work.
- An open loop or follow-up the user may expect continuity on.
- A source artifact that future curation should know exists.
