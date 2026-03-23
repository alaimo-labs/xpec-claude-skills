# Xpec Skills

Claude Code plugin for working with [Xpec.ai](https://xpec.ai) product specifications.

## What's included

### Skills (cross-agent compatible)

| Skill            | Description                                           |
| ---------------- | ----------------------------------------------------- |
| `spec-discovery` | How to find and browse specifications                 |
| `spec-sections`  | How to read and interpret spec sections progressively |
| `spec-workflow`  | How to manage spec status and notes                   |

All skills follow the [Agent Skills](https://agentskills.io) open standard and work with Claude Code, Gemini CLI, Cursor, Codex CLI, and other compatible tools.

### Commands (Claude Code only)

| Command                    | Description                                                                        |
| -------------------------- | ---------------------------------------------------------------------------------- |
| `/xpec:implement [spec]`   | Full implementation workflow: discover spec, read sections, code, record decisions |
| `/xpec:review-spec [spec]` | Review a spec for completeness and clarity before implementation                   |

## Setup

### 1. Install the plugin

```bash
claude /plugin install https://github.com/alaimo-labs/xpec-claude-skills
```

### 2. Connect your project to Xpec

Each project connects to its own Xpec product. Add a `.claude/.mcp.json` file to your project root:

```json
{
  "mcpServers": {
    "xpec": {
      "type": "url",
      "url": "https://mcp.xpec.ai/v1/mcp",
      "headers": {
        "Authorization": "Bearer xpec_your_product_api_key",
        "X-Product-ID": "your_product_id"
      }
    }
  }
}
```

> **Tip:** Add `.claude/.mcp.json` to `.gitignore` if you don't want to share credentials across the team. Alternatively, commit the file with placeholder values and let each developer override locally.

You can find your Product ID and Product API Key in the Your Product > Settings > API Keys section in Xpec.

### Local development

```bash
claude --plugin-dir ./xpec-claude-skills
```

## How it works

The plugin teaches AI agents how to interact with Xpec specifications through MCP tools:

1. **Progressive discovery** — List specs first, then read only the sections you need
2. **Task-driven reading** — Match sections to the task (implementing? read user stories. Designing? read wireframes)
3. **Living documentation** — Keep specs updated with status changes and implementation notes

## License

MIT
