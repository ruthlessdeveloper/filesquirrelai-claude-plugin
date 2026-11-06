# FileSquirrelAI plugin for Claude

Ask Claude what an AI agent changed on your Windows PC. This plugin connects Claude Code and Cowork to [FileSquirrelAI](https://filesquirrelai.com), a Windows app that records which program and which AI agent changes each file in the folders you choose, groups an agent's changes into sessions, and lets you review and undo a whole session.

With the plugin, you can ask things like:

- "What did you change in the last session?"
- "Did Codex delete anything in my project folder today?"
- "Who changed `C:\Projects\site\config.json`, and when?"

and Claude answers from FileSquirrelAI's log on your PC.

## What's in it

A skill, `check-agent-changes`, that tells Claude when to use FileSquirrelAI's tools and how to report what it finds.

The tools themselves come from the FileSquirrelAI app: its read-only MCP server, `FileSquirrel.Mcp.exe`, signed by DistillAI, which you connect to Claude from the app (see **Install**). The plugin doesn't start or configure any server.

The server has four tools, all read-only:

| Tool | What it returns |
|---|---|
| `agent_sessions` | Recent AI agent sessions: agent, start and end, folder, and how many files were changed, created and deleted |
| `session_files` | The files one session touched and what happened to each |
| `recent_changes` | The latest logged changes, with the program and agent behind each |
| `file_history` | Every logged change to one file |

The tools never change, restore or delete files, and they return no file contents. Undo is a click in the FileSquirrelAI app, after you review the list.

## Install

1. Install the FileSquirrelAI app from https://filesquirrelai.com.
2. Connect it to Claude: in the app, **File → Settings... → Agents**, under **Connect your agents**, click **Add to Claude Desktop** (Claude Desktop and Cowork) or **Copy Setup** (Claude Code, then run the copied command). Restart Claude.
3. Add this plugin. In Claude Code:

```
/plugin install filesquirrelai --marketplace ruthlessdeveloper/filesquirrelai-claude-plugin
```

## Requirements

- Windows 10 or 11, 64-bit.
- The FileSquirrelAI app, from https://filesquirrelai.com. Everything is free for a 30-day trial; after it the activity log and alerts stay free, and FileSquirrelAI Pro ($19 one-time for version 1.x) keeps new changes undoable.
- Claude Code, Claude Desktop or Cowork on your PC. Plain claude.ai chat in a browser can't reach programs on your PC, so there the skill loads but the tools don't.

## Privacy Policy

This plugin, and the FileSquirrelAI server it uses, run entirely on your PC.

- **Data collection:** the plugin collects nothing. The server reads FileSquirrelAI's local log (`C:\ProgramData\FileSquirrel`): file paths, times, the kind of change, and the program and agent that made it. No file contents.
- **Usage and storage:** results go only to the Claude app that asked, on your PC, as the answer to your question. Claude then handles them like anything else in your conversation, under Anthropic's own privacy terms. Nothing is stored by the plugin.
- **Third-party sharing:** none. The plugin and the server make no network connections and send nothing to DistillAI or anyone else.
- **Data retention:** the plugin keeps nothing. FileSquirrelAI's log stays on your PC for as long as you keep it; the app's settings say how long, and uninstalling offers to remove it.
- **Contact:** support@filesquirrelai.com.

FileSquirrelAI's full privacy policy: https://filesquirrelai.com/privacy/

## Support

Email support@filesquirrelai.com. FileSquirrelAI is published by DistillAI.

## License

The files in this repository are under the MIT License (see `LICENSE`). The FileSquirrelAI app is separate software with its own terms.
