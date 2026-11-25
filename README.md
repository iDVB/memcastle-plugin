# Memcastle for Claude Code

Memcastle is your memory for AI agents: your **Personal** space and your team's **shared** space. This plugin
connects Claude Code to it.

The plugin adds:

- **The Memcastle MCP server** (`https://api.memcastle.com/mcp`): the `memory_*`, `collection_*` and `reminder_*`
  tools. The first tool call opens the Memcastle sign-in in your browser.
- **The `memory` skill** (`memcastle:memory`): when to recall, what to save, where to file it, and how to update,
  undo and stay safe. Claude Code loads it when a conversation needs it.

## Install

In Claude Code:

```
/plugin marketplace add iDVB/memcastle-plugin
/plugin install memcastle@memcastle
```

Then ask Claude something that needs your memory, for example "what's my coffee order?", and sign in when asked.

## Without the plugin

You can add only the server instead:

```sh
claude mcp add --transport http memcastle https://api.memcastle.com/mcp
```

Claude Code v2.1.331 and later load the same skill from the server. Other MCP clients can read it with the
`memory_guide` tool.

## About this repo

This repo is generated from the Memcastle source and published as is. Please open an issue rather than a pull request.
