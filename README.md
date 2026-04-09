# obsidian-daily

`obsidian-daily` is an agent skill for appending a concise summary of the current AI chat to today's Obsidian daily note.

The skill is intended for repository work logs such as implementation, investigation, fixes, and decisions. It writes a short Markdown summary through the Obsidian CLI with `obsidian daily:append content="..."` instead of storing the full conversation. If the CLI cannot be executed (e.g. agent running in a background environment without GUI access), it falls back to outputting the Markdown block in the chat for the user to manually copy.

## Summary format

The appended content uses this structure:

```md
## {repository name}

- Summary 1
  - Work completed
- Summary 2
  - Follow-up or decision
```

The summary should stay compact. If a chat continues across multiple days, the skill should record only roughly the most recent day of work.

## Setup

This repository is expected to be used via a symbolic link:

```sh
ln -s /path/to/obsidian-daily ~/.agents/skills/obsidian-daily
```

Replace `/path/to/obsidian-daily` with the local checkout path of this repository.

## Requirements

- Obsidian CLI must be enabled and available.
- The target Obsidian vault should be the current working directory, or you should specify `vault=<name>` when running the CLI command.

See [SKILL.md](./SKILL.md) for the skill instructions used by the agent.
