# CLAUDE.md — 飞书渠道伙伴资讯 & 培训推送 Skill

This file provides guidance to Claude Code when working with this repository.

## Project Overview

This is a **lark-cli custom skill** for Feishu (Lark) channel sales managers. It automates:
1. **Daily content collection** — Real-time web search for SaaS industry news + Feishu product updates
2. **Push management** — Generate formatted daily digests and push to partner groups via lark-im
3. **Knowledge base** — Archive all content to Feishu Wiki for search and reuse

## Architecture

```
User (Natural Language Commands)
    │
    ▼
AI Agent (reads SKILL.md)
    │
    ├── 模块0: WebSearch/WebFetch → auto-collect real-time news/updates
    ├── 模块1: lark-wiki → archive and classify content
    ├── 模块2: lark-im   → push to partner groups
    └── 模块3: lark-docs → search knowledge base
```

## Key Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Core skill file — the AI agent's instruction manual |
| `README.md` | Human-readable project overview |
| `test_data.md` | Test scenarios for skill validation |
| `config_template.md` | First-time setup configuration reference |

## Skill Deployment

The skill is deployed to `~/.claude/skills/lark-channel-sales-content/SKILL.md`.
After editing `SKILL.md`, sync with:
```bash
cp SKILL.md ~/.claude/skills/lark-channel-sales-content/SKILL.md
```

## Prerequisites

- lark-cli installed and configured (`lark-cli config init`)
- Feishu app with required scopes (see config_template.md)
- Feishu Wiki space for knowledge base storage
- Feishu IM chat groups for partner push delivery

## Related Skills

- `lark-channel-sales` — Data analysis for partner performance grading and KPI monitoring
- `lark-wiki` — Feishu Wiki space and node management
- `lark-im` — Feishu instant messaging
- `lark-shared` — lark-cli auth and setup
