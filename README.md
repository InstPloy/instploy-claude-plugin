# InstPloy Claude Plugin

Claude Code / Claude.ai marketplace that ships the InstPloy plugin.

> Cursor: https://github.com/InstPloy/instploy-cursor-plugin  
> ChatGPT: https://github.com/InstPloy/instploy-chatgpt-plugin

## Repo layout

```text
.
├── .claude-plugin/marketplace.json
└── plugins/instploy/
    ├── .claude-plugin/plugin.json
    ├── .mcp.json
    ├── commands/connect-instploy.md
    └── skills/instploy-mcp/SKILL.md
```

## Install marketplace

```bash
claude plugin marketplace add InstPloy/instploy-claude-plugin
```

Or:

```text
/plugin marketplace add InstPloy/instploy-claude-plugin
```

Then install:

```bash
claude plugin install instploy@instploy-claude-plugin
```

On enable, set:

| Option | Maps to JSON |
|--------|----------------|
| InstPloy MCP URL (`instploy_url`) | `instploy.url` |
| Authorization Bearer token (`instploy_token`) | token from `headers.Authorization` |

## Paste JSON in chat

```text
/instploy:connect-instploy
```

## Local test

```bash
claude --plugin-dir ./plugins/instploy
```

## Your InstPloy JSON

```json
"instploy": {
  "url": "https://YOUR_INSTANCE.instploy.com/instploy/manager/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_TOKEN_HERE"
  }
}
```

## Security

- Never commit real Bearer tokens
- Plugin files only contain placeholders / instructions
