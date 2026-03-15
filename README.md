# skills-mmmmmghost-collections

Practical agent skills with reusable workflows and references.

## Included Skills

- `use-youtube-data-mcp/`
- `web-research-subagent/`

## New: web-research-subagent

Purpose:
- Delegate web searching to a dedicated subagent.
- Return only concise, source-backed findings to the main agent.
- Reduce context pollution from raw search logs.

Key files:
- `web-research-subagent/SKILL.md`
- `web-research-subagent/references/subagent_prompt_template.md`
- `web-research-subagent/references/client-adapters.md`
- `web-research-subagent/references/AGENTS.template.md`

## Cross-Client Compatibility

Codex-native metadata is included (`SKILL.md`, `agents/openai.yaml`).

For other clients (Cursor / Claude Code / OpenCode), reuse:
- prompt template
- output contract
- routing policy template

See:
- `web-research-subagent/references/client-adapters.md`
