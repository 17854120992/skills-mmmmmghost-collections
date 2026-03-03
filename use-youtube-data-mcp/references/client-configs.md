# Client Config Targets

Use this file to choose where to write MCP config.

## MCP Server Definition
- Name: `youtube-data`
- URL: `https://mkterswingman.com/mcp`
- Header: `Authorization: Bearer <API_KEY>`

## Candidate Paths

### Cursor
- macOS: `~/Library/Application Support/Cursor/User/globalStorage/rooveterinaryinc.roo-cline/settings/mcp_settings.json`
- Windows: `%APPDATA%\Cursor\User\globalStorage\rooveterinaryinc.roo-cline\settings\mcp_settings.json`
- Fallback check:
  - `~/.cursor/mcp.json`

### Codex
- `~/.codex/config.toml`
- `~/.codex/mcp.json`

### OpenCode
- `~/.config/opencode/mcp.json`
- `%APPDATA%\opencode\mcp.json`

### OpenClaw
- `~/.config/openclaw/mcp.json`
- `%APPDATA%\openclaw\mcp.json`

## Detection Heuristic
1. Prefer existing config files that already contain `mcp` or `servers`.
1. If multiple candidates exist, pick the one most recently modified.
1. If none exist, create the primary path for the detected client.

## Validation
After writing config:
1. Ensure JSON/TOML syntax is valid.
1. Ensure the API key is not empty.
1. Restart client if necessary.
