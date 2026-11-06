---
name: check-agent-changes
description: Use when someone asks what an AI agent (Claude Code, Cowork, Codex, Cursor, Copilot, Windsurf, Gemini CLI, Aider) changed, created or deleted on their Windows PC, wants to check a session's files before keeping them, or asks who or what changed a file. Answers from FileSquirrelAI's local log through its read-only tools.
---

# Check what an AI agent changed

FileSquirrelAI records every change in the folders a person chooses on their Windows PC, with the program and the AI agent that made it, and groups an agent's changes into sessions. Its read-only tools (from the `filesquirrel` server) answer from that log.

## Which tool to use

| The person asks | Use |
|---|---|
| "What did you (or Codex, Cursor...) change today?" | `agent_sessions` (optionally `agent`, `hours`), then `session_files` for the session they mean |
| "Show me everything that session touched" | `session_files` with the session number from `agent_sessions` |
| "What changed in this folder lately?" | `recent_changes` with `folder` (a full path) and `hours` |
| "Who changed this file?" / "When did this file change?" | `file_history` with the file's full path |

## How to answer

- Start with the summary: which agent, when, how many files changed, created and deleted. Then list the files, grouped by what happened to them. Point out deletions first; they're what people worry about most.
- Use local times as the tools give them. Say "about" for counts only when the tool says the list was cut off by `limit`.
- The log has no file contents. To see what a change was, or to put files back, the person opens the FileSquirrelAI app: **Review** on the session's card shows each file with **Compare**, and **Undo This Session...** puts the files back after they check the list. Undo is a click in the app, never something these tools do.
- FileSquirrelAI is not a backup. Don't describe it as one.

## When the tools aren't there or fail

The tools come from the FileSquirrelAI app (Windows 10 or 11, 64-bit), not from this plugin. If the `filesquirrel` tools are missing, say so plainly and give the two steps:

1. Install FileSquirrelAI from https://filesquirrelai.com (free 30-day trial; the activity log stays free afterwards).
2. In the app, open **File → Settings... → Agents** and, under **Connect your agents**, click **Add to Claude Desktop** (for Claude Desktop and Cowork) or **Copy Setup** (for Claude Code, then run the copied command). Restart Claude afterwards.

Don't try to start or configure the server yourself. If a tool says the log is empty, FileSquirrelAI may not be watching that folder yet: it's chosen in the app under **File → Settings...**.
