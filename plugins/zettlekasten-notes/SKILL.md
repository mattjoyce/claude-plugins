---
name: zettelkasten-vault
description: Create and manage a Zettelkasten-style knowledge vault using Obsidian Flavored Markdown. Use this skill whenever the user wants to capture notes, ideas, research, meeting notes, or any knowledge in a structured way — especially when they mention "vault", "zettelkasten", "atomic notes", "zettels", "knowledge base", "second brain", "evergreen notes", "note-taking", or want to link ideas together. Always use this skill when creating .md files that should live in the vault, not just standalone markdown. Strongly prefer this skill over the generic obsidian-markdown skill when the intent is knowledge management rather than one-off document creation.
---

# Zettelkasten Vault Skill

This skill governs the creation and management of a personal knowledge vault using Zettelkasten principles within an Obsidian-compatible folder structure.

## Core Philosophy

The Zettelkasten method, pioneered by sociologist Niklas Luhmann, treats knowledge as a **web of atomic ideas**, not a hierarchy of documents.

Key principles to embody in every note:
- **Atomicity**: One idea per note. If you find yourself writing two ideas, split them.
- **Connectivity**: Every note should link to at least one other note. A note with no links is a dead end.
- **Own words**: Never copy-paste. Restate ideas in the author's voice — this is where understanding happens.
- **No categories**: Use tags and links instead of folders-as-categories. Let structure emerge.
- **Permanent notes**: Write as if explaining to a future self who has forgotten the context entirely.

---

## Vault Structure

Always create notes inside a `vault/` folder at the working directory root. Use this layout:

```
vault/
├── inbox/          # Fleeting notes — raw captures, not yet processed
├── notes/          # Permanent Zettels — atomic, linked, evergreen
├── literature/     # Literature notes — processed from a source
├── structure/      # Structure notes (MOCs) — index/map notes
└── assets/         # Images, attachments
```

Create the folder structure before creating any notes:
```bash
mkdir -p vault/{inbox,notes,literature,structure,assets}
```

---

## Note Types

### 1. Fleeting Note (`inbox/`)
Quick capture of a raw thought. Temporary — meant to be processed into a permanent note.

**Filename**: `YYYY-MM-DD-short-slug.md`

```yaml
---
type: fleeting
date: 2025-02-27
tags: [inbox]
---
```

### 2. Literature Note (`literature/`)
Processing a source (book, article, paper, video). Summarises in own words. One note per source.

**Filename**: `author-year-short-title.md` (e.g., `luhmann-1992-communicating-with-zettelkastens.md`)

```yaml
---
type: literature
title: "Communicating with Zettelkastens"
author: Niklas Luhmann
year: 1992
source: https://example.com/source
tags: [knowledge-management, systems]
related: []
---
```

### 3. Permanent Note / Zettel (`notes/`)
The core unit. One atomic idea, written to stand alone, linked richly.

**Filename**: Use a timestamp ID + slug: `YYYYMMDDHHII-slug.md` (e.g., `202502271430-links-are-first-class.md`)

The timestamp ID is the **unique identity** of the note — never change it.

```yaml
---
id: "202502271430"
type: permanent
title: "Links are first-class citizens in a Zettelkasten"
created: 2025-02-27
modified: 2025-02-27
tags: [zettelkasten, linking, knowledge-management]
related: ["[[202502271200-atomicity-principle]]", "[[202502271315-emergence-of-structure]]"]
status: evergreen
---
```

**Status values**: `seedling` (new, rough) → `budding` (developing) → `evergreen` (mature, stable)

### 4. Structure Note / MOC (`structure/`)
A Map of Content — an index note that gives navigation context for a cluster of ideas. Not a category; it's a curated lens.

**Filename**: `MOC-topic-name.md`

```yaml
---
type: structure
title: "MOC: Knowledge Management"
created: 2025-02-27
tags: [MOC, knowledge-management]
---
```

---

## Frontmatter Reference

### Required fields (all note types)
| Field | Description |
|-------|-------------|
| `type` | `fleeting` / `literature` / `permanent` / `structure` |
| `title` | Human-readable title |
| `created` | ISO date `YYYY-MM-DD` |
| `tags` | List of lowercase hyphenated tags |

### Permanent note additional fields
| Field | Description |
|-------|-------------|
| `id` | Timestamp `YYYYMMDDHHII` — immutable unique ID |
| `modified` | ISO date, updated on each edit |
| `related` | Wikilinks to related notes |
| `status` | `seedling` / `budding` / `evergreen` |

### Literature note additional fields
| Field | Description |
|-------|-------------|
| `author` | Author name(s) |
| `year` | Publication year |
| `source` | URL or citation string |

---

## Linking Rules

- **Always link when referencing another concept** that has or should have a note: `[[note-id-slug]]`
- Use **display text** for readability: `[[202502271430-links-are-first-class|links are first-class]]`
- Link to **headings** within a note when relevant: `[[202502271430-links-are-first-class#Why this matters]]`
- When creating a new note, **scan existing notes** and add backlinks from related ones
- Add new notes to a relevant **Structure/MOC note** if one exists

---

## Writing Guidelines

1. **Title is a claim or question**, not a label.
   - ✅ `"Atomic notes prevent knowledge silos"`
   - ❌ `"About atomic notes"`

2. **Body starts with the idea**, not with preamble or context.

3. **One heading level max** in a permanent note — if you need more, split the note.

4. **End every permanent note** with a `## Linked from` or `## See also` section listing related wikilinks.

5. **Tags describe what a note is about**, not what type of note it is (that's the `type` field).
   - ✅ `[knowledge-management, cognition]`
   - ❌ `[permanent-note, linked]`

---

## Workflow

When the user wants to **capture a new idea**:
1. Create a fleeting note in `inbox/` as a quick capture
2. Ask if they want to process it into a permanent note now or later

When the user wants to **process notes**:
1. Read the fleeting note
2. Identify the atomic idea(s) — split if needed
3. Write a permanent note in own words with a claim-title
4. Link to existing notes; create stubs for missing ones
5. Add to a relevant MOC if one exists

When the user wants to **capture from a source**:
1. Create a literature note in `literature/`
2. Extract key ideas as bullet points (in own words)
3. Spawn permanent notes for ideas worth keeping

---

## Example Permanent Note

```markdown
---
id: "202502271430"
type: permanent
title: "Connectivity is more valuable than completeness in a knowledge system"
created: 2025-02-27
modified: 2025-02-27
tags: [zettelkasten, linking, emergence]
related: ["[[202502271200-atomicity-principle]]", "[[202502271315-emergence-of-structure]]"]
status: seedling
---

A knowledge system with fewer, well-connected notes will surface more insight than one with many isolated notes. The value of a note is not in its content alone, but in the **relationships it participates in**.

This mirrors how memory works in the brain: recall is associative, not hierarchical. A note reached via three different paths is more likely to be retrieved — and more likely to spark unexpected connections — than one filed in the "right" folder.

> [!tip] Practical implication
> Before saving a new note, ask: *what does this connect to?* If the answer is nothing, the note isn't ready yet.

## See also

- [[202502271200-atomicity-principle|Atomicity prevents ideas from hiding inside each other]]
- [[202502271315-emergence-of-structure|Structure emerges from linking, not from planning]]
```
