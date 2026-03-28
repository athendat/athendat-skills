# ATHENDAT Skills Repository Redesign

Convert the current Claude-specific skills repo into an agent-agnostic, category-organized skills library for ATHENDAT.

## Goals

- Agent-agnostic: compatible with Claude Code, Gemini CLI, Cursor, Windsurf, GitHub Copilot, Codex, and any future agent
- Organized by discipline (not by product or tech stack)
- Easy to extend: adding a skill = creating a folder + writing Markdown
- No build step, no packaging, no scripts

## Repository Structure

```
athendat-skills/
├── README.md
├── CONTRIBUTING.md
├── .gitignore
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
│
├── design/
│   └── ux-ui/
│       ├── skill.md
│       └── references/
│           ├── ui-technical.md
│           └── ux-strategy.md
│
├── backend/
├── frontend/
├── mobile/
├── devops/
├── testing/
└── documentation/
```

- Each discipline is a top-level directory
- Each skill is a subdirectory within its discipline
- Empty categories are NOT created until they have at least one skill
- `dist/` is eliminated (no packaging)
- `skills/` as a single container directory is eliminated

## Skill Format

### File: `skill.md`

YAML frontmatter with exactly 4 fields:

```yaml
---
name: skill-name
description: >
  What the skill does. Be specific.
category: design
tags: [tag1, tag2, tag3]
---
```

### Content Rules

- Markdown pure, no proprietary extensions
- Imperative voice, agent-agnostic language
- Never reference specific agent tools ("Read tool", "Write tool", "/command")
- Use neutral phrasing: "Consult `references/file.md`" not "Read `references/file.md`"
- Under 500 lines; offload depth to `references/`
- All content in English
- List reference files with descriptions in a table when present

### References

Optional `references/` subdirectory with supporting `.md` files. These contain deep-dive documentation that the main `skill.md` points to.

## README.md

Serves as the central index:

- Table of all skills grouped by category
- Tech stack context block (ATHENDAT's stack for reference)
- Usage section with brief, concrete instructions per agent:
  - Claude Code: add as skill or reference
  - Cursor/Windsurf: add to rules
  - GitHub Copilot: reference in .github/copilot-instructions.md
  - Gemini CLI: reference in GEMINI.md
  - Any agent: paste or reference the content
- Link to CONTRIBUTING.md

## CONTRIBUTING.md

Simplified for manual workflow:

- Step-by-step: create folder, write skill.md, add references, update README table, open PR
- Conventions: kebab-case folders, English, imperative voice, agent-agnostic
- Category table as reference
- Quality checklist (frontmatter valid, agent-agnostic, English, under 500 lines, README updated)
- No packaging/build steps

## Migration of Existing Skill

### `ath-ux-ui-design` -> `design/ux-ui`

- Move from `skills/ath-ux-ui-design/` to `design/ux-ui/`
- Rename `SKILL.md` to `skill.md`
- Update frontmatter to new 4-field format
- Replace agent-specific language ("Read `references/...`" -> "Consult `references/...`")
- Move references as-is (content is already agent-agnostic)
- Delete `dist/ath-ux-ui-design.skill`

## What Gets Deleted

- `dist/` directory and its contents
- `skills/` directory (replaced by category directories)

## What Gets Updated

- `README.md` — full rewrite to new format
- `CONTRIBUTING.md` — simplified, no packaging references
- `.gitignore` — remove dist-related comments
- `.github/PULL_REQUEST_TEMPLATE.md` — remove `.skill` packaging references
