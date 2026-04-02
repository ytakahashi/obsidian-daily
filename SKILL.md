---
name: obsidian-daily
description: Use this skill when you want to append a concise summary of the current AI chat to today's Obsidian daily note via the Obsidian CLI. It is for workflows that record recent coding or repository work into the daily note using `obsidian daily:append`.
---

# Obsidian Daily

Use this skill when the user wants the current chat summarized into today's Obsidian daily note.

## Goal

Append a short Markdown summary of the current chat to the daily note with:

```sh
obsidian daily:append content="..."
```

Keep the summary compact. Do not write a long transcript.

## What to write

Format the appended content like this:

```md
\n### {repository name}

- Summary 1
  - Work completed
- Summary 2
  - Follow-up or decision
```

Rules:

- Start the appended content with a leading newline `\n`.
- Use the repository name as the `###` heading. Prefer the git repository root name or the current working directory name.
- Summaries must be brief and task-oriented.
- Capture outcomes, fixes, decisions, or investigations, not the full conversation.
- If the chat has continued across multiple days, summarize only the most recent roughly one day of work.
- Omit speculative side discussions unless they materially affected the work.
- After appending to the daily note, show the same Markdown content in the chat reply.

## Workflow

1. Review the current chat and identify the main items worth recording.
2. Limit the content to a few bullets that can be scanned quickly later.
3. Build Markdown with explicit `\n` newlines for the CLI argument, starting with a leading `\n`.
4. Append it with `obsidian daily:append content="..."`.
5. Display the appended Markdown content in the chat so the user can review exactly what was recorded.

Example:

```sh
obsidian daily:append content="\n### obsidian-daily\n\n- Skill creation\n  - Added a SKILL.md to append chat summaries to the daily note\n- Summary rules\n  - Limited long-running chats to roughly the most recent day of work"
```

If the content contains backticks or other special characters that the shell may interpret, assign the value to `OBSIDIAN_DAILY_CONTENT` first and pass it by reference. Use single quotes for the common case:

```sh
OBSIDIAN_DAILY_CONTENT='\n### obsidian-daily\n\n- Fixed `someFunc` bug\n  - Root cause identified'
obsidian daily:append content="$OBSIDIAN_DAILY_CONTENT"
```

If the content also contains single quotes or becomes hard to escape, use a quoted heredoc:

```sh
OBSIDIAN_DAILY_CONTENT="$(cat <<'EOF'
\n### obsidian-daily

- Fixed `someFunc` bug
  - Root cause identified
EOF
)"
obsidian daily:append content="$OBSIDIAN_DAILY_CONTENT"
```

## CLI Notes

- `content` is required for `daily:append`.
- Start `content` with `\n`.
- Use `\n` for multiline Markdown in the CLI argument.
- If the content contains backticks or other shell-special characters, assign the value to `OBSIDIAN_DAILY_CONTENT` with single quotes and pass it as `content="$OBSIDIAN_DAILY_CONTENT"` to avoid shell interpretation.
- If the content also contains single quotes or becomes hard to escape, use a quoted heredoc.
- If the working directory is not the target vault, specify the vault explicitly before the command.

Example:

```sh
obsidian vault="My Vault" daily:append content="\n### repo\n\n- Summary\n  - Work completed"
```
