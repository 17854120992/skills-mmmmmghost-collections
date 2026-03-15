---
name: web-research-subagent
description: Delegate internet research to a subagent and relay only distilled, source-backed findings to the main agent. Use when web searching could flood context with noisy results, when the user asks for latest/current information, or when evidence links are required.
---

# Web Research Subagent

Use this skill to keep the main context clean: the subagent explores the web, then returns only decision-useful facts with citations.

For cross-client usage (Cursor/Claude Code/OpenCode), read:
- `references/client-adapters.md`
- `references/AGENTS.template.md`

## Workflow

### 1. Build a narrow research brief

Before delegating, define:

- Goal: what decision the main agent needs to make
- Scope: allowed domains, date range, locale, and required recency
- Output contract: max findings, citation format, and uncertainty notes

Keep the brief under 12 lines.

### 2. Delegate research to a subagent

Spawn one subagent dedicated to web research. Give it:

- The brief from Step 1
- A strict output format (see `references/subagent_prompt_template.md`)
- A requirement to provide source URLs for each claim

Do not pass unrelated implementation context.

### 3. Enforce context hygiene on return

When the subagent reports back:

- Keep only high-signal findings (usually 3-7 bullets)
- Drop repetitive details and generic background
- Preserve links, dates, and confidence notes
- Mark inference vs. source-stated facts

Never paste full search dumps into main context.

### 4. Integrate for the main task

Convert the research result into the minimum needed for action:

- Decision summary (what matters now)
- Evidence table (claim -> source link -> date)
- Known unknowns (what is still uncertain)

If confidence is low, run one targeted follow-up query instead of broad re-search.

## Output Contract (Required)

Require this exact structure from the subagent:

1. `Answer`
2. `Key Findings` (3-7 bullets)
3. `Evidence` (claim + URL + publish/update date)
4. `Assumptions and Gaps`
5. `Confidence` (`high`/`medium`/`low`)

Reject outputs that do not include URLs.

## Guardrails

- Prefer primary sources (official docs, standards, vendor pages, first-party announcements).
- Use secondary sources only when primary sources are missing, and label them.
- Quote sparingly; summarize in your own words.
- If multiple sources conflict, show both and explain which is more reliable.

## Quick Trigger Examples

- "Use this skill to research the latest API pricing and return only citations I need."
- "Delegate web search to a subagent; give me concise facts and links, no raw dumps."
- "Find current policy changes online and report only actionable deltas."
