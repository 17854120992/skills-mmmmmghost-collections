---
name: use-youtube-data-mcp
description: Configure and use the hosted YouTube Data MCP end-to-end with minimal user input. Use when users want the agent to automatically set up MCP server config (Windows/macOS, Cursor/Codex/OpenClaw/OpenCode), request API key at setup time, run post-install capability discovery (`tools/list` and `get_patch_notes`), self-update this skill from GitHub, and install helper skills for document/spreadsheet I/O.
---

# Use YouTube Data MCP

## Workflow

1. Run self-update check for this skill.
1. Ask user for API key only when missing.
1. Detect client and OS, then write MCP config.
1. Install helper skills (`doc`, `spreadsheet`, and user-provided extra skill URLs).
1. Verify MCP connectivity and run capability discovery:
   - `tools/list`
   - `get_patch_notes`
1. Explain to user how to use current MCP abilities in plain language.

## Step 1: Self Update
- Try updating this skill directly from GitHub path:
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo 17854120992/mcp_youtube_data \
  --path skills/use-youtube-data-mcp \
  --method auto
```
- If the repo is private and no credential exists, continue with current local skill and tell user to provide GitHub token or switch to a public skill repo.

## Step 2: Ask For API Key
- If API key is not already provided in env or config, ask user once:
  - `Please provide your MCP API key for https://mkterswingman.com`
- Never echo full key in logs; mask with prefix/suffix in outputs.

## Step 3: Configure MCP Client
- Read [references/client-configs.md](references/client-configs.md).
- Detect environment and patch the matching MCP config file.
- Register this server using:
  - URL: `https://mkterswingman.com/mcp`
  - Header: `Authorization: Bearer <API_KEY>`
  - Transport: Streamable HTTP (or tool-specific equivalent)

## Step 4: Install Helper Skills
- Install helper skills directly:
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills --path skills/.curated/doc --method auto

python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo openai/skills --path skills/.curated/spreadsheet --method auto
```
- Optional extra skills:
```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/anthropics/skills/tree/main/skills/docx --method auto

python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/anthropics/skills/tree/main/skills/xlsx --method auto

python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --url https://github.com/anthropics/skills/tree/main/skills/pptx --method auto
```
- Remind user to restart Codex after skill install/update.

## Step 5: Post-Install Capability Discovery
- Immediately call:
  - `tools/list`
  - `get_patch_notes`
- Summarize:
  - Newest features and limits
  - Which tools support batch input
  - Recommended usage patterns for the current release

## Step 6: User Briefing Template
- Tell user:
  - Besides subtitle fetching, most tools support batch inputs.
  - User can paste multiple links directly in chat.
  - User can also provide Excel/CSV/DOCX for link extraction.
  - Results can be written back to local DOCX/Excel with helper skills.

## Notes
- Keep subtitle mode as single-video per request unless project rules change.
- If a client config path is uncertain, scan candidate config files and pick the one that already contains MCP settings first.
- After changing client config, remind user to restart the client if required.
