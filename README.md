# claude-plugins

Matt Joyce's Claude Code plugin collection — a marketplace of skills and tools for [Claude Code](https://claude.ai/claude-code).

Skills are installed via the Claude Code plugin system and live either in their own repos or as subdirectories of this monorepo.

## Plugins

| Name | Description | Category |
|------|-------------|----------|
| [kanban](https://github.com/mattjoyce/kanban-skill) | Markdown-based Kanban board — cards as `.md` files, no database, no server | productivity |
| [zettlekasten-notes](plugins/zettlekasten-notes/) | Zettelkasten-style knowledge vault using Obsidian Flavored Markdown | knowledge |

## Structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json      # Plugin registry
└── plugins/
    └── zettlekasten-notes/   # Single-file skills live here as subdirectories
        └── SKILL.md
```

Skills with scripts, assets, or complex structure get their own dedicated repos (e.g. `kanban-skill`). Simple single-file skills live directly in this monorepo under `plugins/`.

---

## Changelog

### 2026-02-27
- **Added** `zettlekasten-notes` skill — Zettelkasten knowledge vault with atomic notes, literature notes, permanent notes, and MOC structure notes

### 2026-02-27 (initial)
- **Created** plugin marketplace with `marketplace.json` registry format
- **Added** `kanban` plugin pointing to [mattjoyce/kanban-skill](https://github.com/mattjoyce/kanban-skill)
