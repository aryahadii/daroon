---
name: bear
description: Access Bear app notes. Use when the user asks to search, read, create, append, edit, tag, open, archive, restore, or otherwise work with Bear notes.
---

# Bear

This plugin connects Codex to Bear through Bear's official `bearcli mcp-server`. The MCP server is the source of truth for note operations; this skill is the behavior layer that keeps personal notes work careful, searchable, and useful.

## Default Behavior

- Prefer Bear MCP tools over shelling out to `bearcli`.
- Search or read before writing unless the user explicitly asks to create a new note.
- Use note IDs after lookup whenever possible; titles can be case-insensitive and ambiguous.
- Keep generated notes concise, source-aware, and easy to scan.
- Do not use Bear as a dumping ground. If the note belongs somewhere specific, use the user's requested title and tags.
- Do not bulk list note content unless the user clearly asks for broad discovery.
- Encrypted note content is not available through BearCLI. Say this plainly if a read fails for that reason.

## Safety Rules

Ask for confirmation before:

- `overwrite_note`
- `trash_note`
- `archive_note`
- `delete_tag`
- `rename_tag`
- `delete_attachment`
- broad tag changes across many notes
- edits that may remove attachment references
- any operation that touches more than five notes

For `overwrite_note`, always read the note first and pass the returned `contentHash` as `baseHash`. Treat a hash mismatch as a real conflict: reread, summarize the difference, and ask how to proceed.

For `edit_note`, prefer exact local replacements over full overwrites. Use small atomic edits and verify the changed metadata returned by the tool.

For appending, prefer `append_to_note` over `overwrite_note`. Append at the end unless the user asks for a top update.

## MCP Tool Map

Read and search:

- `get_note`
- `read_note_content`
- `list_notes`
- `search_notes`
- `search_in_note`
- `list_tags`
- `list_pins`
- `list_attachments`
- `read_attachment`

Create and add:

- `create_note`
- `append_to_note`
- `add_tags`
- `add_pins`

Edit and replace:

- `edit_note`
- `overwrite_note`

Open in Bear:

- `open_note`

Move and restore:

- `archive_note`
- `trash_note`
- `restore_note`

Global tag operations:

- `rename_tag`
- `delete_tag`

Remove:

- `remove_tags`
- `remove_pins`
- `delete_attachment`

## Search Guidance

Use Bear search syntax in `search_notes`:

- plain text terms
- quoted exact phrases
- `#tag`
- `!#tag` for exact tag
- `#*/tag` for subtags
- `@title`
- `@today`, `@yesterday`, `@lastXdays`
- `@todo`, `@done`, `@task`
- `@pinned`
- `@images`, `@files`, `@attachments`, `@code`
- `@locked`, `@empty`, `@untitled`, `@wikilinks`, `@backlinks`, `@ocr`

Start with narrow searches. Use `limit` and `includeContent=false` for initial discovery, then read specific notes.

## Common Workflows

Find notes about a topic:

1. Call `search_notes` with a narrow query and a modest `limit`.
2. Inspect titles, tags, and match counts.
3. Read only the best candidates with `read_note_content` or `get_note` with `includeContent=true`.

Create a note from conversation:

1. Choose a clear title.
2. Use the user's requested tags, or `codex/inbox` if none are given.
3. Call `create_note` with `ifNotExists=true` when the title is meant to be unique.
4. Return the title, ID, and tags.

Append an update:

1. Search for the target note.
2. Confirm the intended note if there are multiple plausible matches.
3. Call `append_to_note`.
4. Briefly summarize what was appended.

Rewrite a note:

1. Read the note with metadata and content.
2. Draft the replacement.
3. Ask for confirmation.
4. Call `overwrite_note` with `baseHash`.
5. Mention any changed title, tags, attachment count, or location.
