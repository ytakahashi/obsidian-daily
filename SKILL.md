---
name: obsidian-daily
description: Use this skill when you want to append a concise summary of the current AI chat to today's Obsidian daily note via the Obsidian CLI. It is for workflows that record recent coding or repository work into the daily note using `obsidian daily:append`.
---

# Obsidian Daily

Use this skill when the user wants the current chat summarized into today's Obsidian daily note.

## Goal

Append a short Markdown summary of the current chat to the daily note with `obsidian daily:append`.

Keep the summary compact. Do not write a long transcript.

## What to write

Format the appended content like this:

```md
\n### {repository name}

- Summary 1
  - Work completed
- Summary 2
  - Follow-up or decision

Agent: {agent name}
```

Rules:

- Start the appended content with a leading newline `\n`.
- Use the repository name as the `###` heading. Prefer the git repository root name or the current working directory name.
- Summaries must be brief and task-oriented.
- Capture outcomes, fixes, decisions, or investigations, not the full conversation.
- If the chat has continued across multiple days, summarize only the most recent roughly one day of work.
- Omit speculative side discussions unless they materially affected the work.
- Add a final line in the appended block that identifies which AI agent wrote it, for example `Agent: Codex`, `Agent: Claude Code`, `Agent: Antigravity`, or `Agent: Cursor`.
- After appending to the daily note, show the same Markdown content in the chat reply.

## Execution Rule

Construct the Markdown content as an exact string value.

The content must:

- start with `\n`
- use `### {repository name}` as the heading
- include only a concise summary of the recent work
- end with a final `Agent: {agent name}` line

Then call `obsidian daily:append` and pass that exact string as the `content` argument.

If the `obsidian` CLI command fails, hangs, or cannot be executed because the AI Agent is running in a restricted background environment without GUI access, do not attempt to write directly to the file. Instead, simply output the exact Markdown string in a code block in the chat response so the user can manually copy and paste it into their daily note.

Do not change the Markdown content to fit a specific shell example.
Use whatever argument passing or escaping mechanism is appropriate for the current execution environment so that the exact content is preserved.
The mechanism may vary by agent or shell. For example, an agent may use direct argument escaping, `printf`, or a temporary file, as long as the exact Markdown content is preserved.

## Workflow

1. Review the current chat and identify the main items worth recording.
2. Limit the content to a few bullets that can be scanned quickly later.
3. Add the current AI agent name as the final line, such as `Agent: Codex`, `Agent: Claude Code`, `Agent: Antigravity`, or `Agent: Cursor`.
4. Build the exact Markdown string, starting with a leading `\n`.
5. Call `obsidian daily:append` and pass that exact value as `content`.
6. Display the appended Markdown content in the chat so the user can review exactly what was recorded.
7. If the CLI command execution is unavailable or fails due to environment restrictions (e.g., hanging in a background process), explicitly state this to the user and present the Markdown content in a code block for manual copying.

Exact content example:

```md
\n### obsidian-daily

- Skill creation
  - Added a SKILL.md to append chat summaries to the daily note
- Summary rules
  - Limited long-running chats to roughly the most recent day of work
- Code update
  - Adjusted `README.md` and `SKILL.md` examples

Agent: Codex
```

One possible shell example:

```sh
obsidian daily:append content="\n### obsidian-daily\n\n- Skill creation\n  - Added a SKILL.md to append chat summaries to the daily note\n- Summary rules\n  - Limited long-running chats to roughly the most recent day of work\n- Code update\n  - Adjusted \`README.md\` and \`SKILL.md\` examples\n\nAgent: Codex"
```

## CLI Notes

- `content` is required for `daily:append`.
- Start `content` with `\n`.
- Preserve the exact Markdown content when passing it to `content`.
- Argument quoting and escaping are environment-specific. Choose a method that preserves the exact content in the current agent or shell.
- If the working directory is not the target vault, specify the vault explicitly before the command.

One possible shell example:

```sh
obsidian vault="My Vault" daily:append content="\n### repo\n\n- Summary\n  - Work completed\n\nAgent: Codex"
```
