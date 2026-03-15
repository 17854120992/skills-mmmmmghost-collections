# web-research-subagent

Delegate web search to a dedicated subagent and return only concise, source-backed findings to the main agent.

## What It Solves

- Prevents context pollution from raw search dumps
- Enforces citation-first outputs
- Keeps only decision-useful facts in the main thread

## Core Contract

The research subagent returns exactly:

1. Answer
2. Key Findings (3-7 bullets)
3. Evidence (claim + source URL + date)
4. Assumptions and Gaps
5. Confidence (high/medium/low)

## Files

- `SKILL.md`
- `agents/openai.yaml`
- `references/subagent_prompt_template.md`
- `references/client-adapters.md`
- `references/AGENTS.template.md`

## Cross-Client Use

For non-Codex clients (Cursor / Claude Code / OpenCode), reuse:

- `references/subagent_prompt_template.md`
- `references/AGENTS.template.md`
- `references/client-adapters.md`
