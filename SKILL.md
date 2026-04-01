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
## {repository name}

- Summary 1
  - Work completed
- Summary 2
  - Follow-up or decision
```

Rules:

- Use the repository name as the `##` heading. Prefer the git repository root name or the current working directory name.
- Summaries must be brief and task-oriented.
- Capture outcomes, fixes, decisions, or investigations, not the full conversation.
- If the chat has continued across multiple days, summarize only the most recent roughly one day of work.
- Omit speculative side discussions unless they materially affected the work.
- After appending to the daily note, show the same Markdown content in the chat reply.

## Workflow

1. Review the current chat and identify the main items worth recording.
2. Limit the content to a few bullets that can be scanned quickly later.
3. Build Markdown with explicit `\n` newlines for the CLI argument.
4. Append it with `obsidian daily:append content="..."`.
5. Display the appended Markdown content in the chat so the user can review exactly what was recorded.

Example:

```sh
obsidian daily:append content="## obsidian-daily\n\n- Skill creation\n  - Added a SKILL.md to append chat summaries to the daily note\n- Summary rules\n  - Limited long-running chats to roughly the most recent day of work"
```

## CLI Notes

- `content` is required for `daily:append`.
- Use `\n` for multiline Markdown in the CLI argument.
- If the working directory is not the target vault, specify the vault explicitly before the command.

Example:

```sh
obsidian vault="My Vault" daily:append content="## repo\n\n- Summary\n  - Work completed"
```
