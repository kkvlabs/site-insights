# Other MCP clients

Site Insights by KKV Labs is a standard remote MCP server (Streamable HTTP) with OAuth sign in. Any app that adds remote servers by link and signs you in itself can use it. You do not need mcp-remote, a proxy or a pasted token.

```
https://insights.kkvlabs.com/mcp
```

| App | Basis |
|---|---|
| Claude (web, desktop, mobile) | Tested by us. Guide: [claude.md](claude.md) |
| ChatGPT (chatgpt.com on the web) | Tested by us with Plus, 18 Nov 2026. Guide: [chatgpt.md](chatgpt.md) |
| Claude Code | Tested by us, 18 Nov 2026. Guide: [claude-code.md](claude-code.md) |
| Cursor | Cursor docs, 18 Nov 2026 |
| OpenAI Codex (CLI and IDE) | OpenAI Codex docs, 18 Nov 2026 |
| Zed | Zed docs, 18 Nov 2026 |
| Goose | Goose docs, 18 Nov 2026 |

The four apps below are confirmed against their official docs only. We have not tested them end to end. If something does not work, email support@kkvlabs.com.

After you sign in in any app, switch on the sites the assistant may read at https://insights.kkvlabs.com/account.

## Cursor

Add this to `~/.cursor/mcp.json`, then sign in when Cursor asks.

```json
{ "mcpServers": { "site-insights": { "url": "https://insights.kkvlabs.com/mcp" } } }
```

Docs: https://cursor.com/docs/context/mcp

## OpenAI Codex (CLI and IDE)

Add this to `~/.codex/config.toml`, then run `codex mcp login site_insights`.

```toml
[mcp_servers.site_insights]
url = "https://insights.kkvlabs.com/mcp"
```

Docs: https://developers.openai.com/codex/mcp

## Zed

Settings, then AI, then MCP Servers, then Add Server, then Add Remote Server. Or add this to `settings.json`:

```json
"context_servers": { "site-insights": { "url": "https://insights.kkvlabs.com/mcp" } }
```

Docs: https://zed.dev/docs/ai/mcp

## Goose

Run `goose configure`, choose Add Extension, then Remote Extension (Streamable HTTP), and paste the link.

Docs: https://goose-docs.ai/docs/getting-started/using-extensions

## Not listed yet

VS Code with Copilot, Windsurf, Cline and Gemini CLI are left out because their docs do not confirm sign in with no extra setup. Raycast and LibreChat are left out until their callback addresses are checked against our server. They will be added only after a check.

[Back to README](../README.md)
