# Client Adapters

This skill is Codex-native, but the core pattern is client-agnostic.

## Portable Core

Reuse these parts in any agent client:

- Research-subagent prompt template: `subagent_prompt_template.md`
- Structured return contract:
  1. Answer
  2. Key Findings (3-7 bullets)
  3. Evidence (claim + source URL + date)
  4. Assumptions and Gaps
  5. Confidence
- Context hygiene rule: no raw search dump in main thread/context

## Codex

- Place skill folder in `$CODEX_HOME/skills/`.
- Trigger by name: `web-research-subagent`.
- Optional: add a project `AGENTS.md` rule using `AGENTS.template.md`.

## Cursor / Claude Code / OpenCode

If the client does not support Codex skill metadata:

1. Copy `subagent_prompt_template.md` into your project docs.
2. Add an agent-routing policy (system prompt, project rule file, or workflow config):
   - For web search tasks, delegate to a dedicated research subagent.
   - Enforce structured return contract.
   - Forbid raw search logs in main context.
3. Keep a short "research brief" before delegation:
   - goal
   - scope
   - recency/date constraints
   - allowed domains (if any)

## Suggested Repo Integration

- Keep this skill as a folder in your skill collection.
- For non-Codex users, expose a "Prompt Pack" section in README that points to:
  - `references/subagent_prompt_template.md`
  - `references/AGENTS.template.md`
