# Contributing to ATHENDAT Claude Skills

## Creating a New Skill

### 1. Plan

Before writing, answer:
- **What** should Claude be able to do with this skill?
- **When** should it trigger? (list specific phrases, contexts, keywords)
- **What's the output?** (code, documents, analysis, design specs...)
- **Who benefits?** (developers, designers, clients, sales team...)

### 2. Structure

```
skills/<skill-name>/
├── SKILL.md              # Required — main instructions
├── references/           # Optional — deep docs loaded on demand
│   ├── topic-a.md
│   └── topic-b.md
├── scripts/              # Optional — automation code
└── assets/               # Optional — templates, images, fonts
```

### 3. Write the SKILL.md

**Required YAML frontmatter:**

```yaml
---
name: skill-name
description: >
  What the skill does and when to trigger it. Be specific and slightly
  "pushy" — Claude tends to under-trigger skills, so include edge cases
  and alternative phrasings that should activate this skill.
---
```

**Body guidelines:**
- Use imperative voice ("Use 4pt grid spacing" not "You should use 4pt grid spacing")
- Explain *why* when the reason isn't obvious — Claude follows reasoning better than blind rules
- Keep SKILL.md under 500 lines; offload depth to `references/`
- Include a decision table if the skill covers multiple scenarios
- Add an output format template so results are consistent

### 4. Language

All skill content must be written in **English**. This ensures:
- Consistent behavior regardless of conversation language
- Better triggering accuracy (Claude's skill matching works best in English)
- Reusability across teams and projects

### 5. Test

Run at least 3 realistic prompts with the skill active:
- A simple case (happy path)
- An edge case (ambiguous or complex request)
- A triggering test (does Claude activate the skill from natural language?)

### 6. Package & PR

```bash
# Package
cd skills/<skill-name>
zip -r ../../dist/<skill-name>.skill .

# Commit
git add skills/<skill-name> dist/<skill-name>.skill
git commit -m "feat(skills): add <skill-name>"
```

Open a PR with:
- Skill name and purpose
- Example prompts and expected behavior
- Any dependencies or stack requirements

## Updating an Existing Skill

1. Edit the source files under `skills/<skill-name>/`
2. Re-package to `dist/`
3. Bump version in SKILL.md description if significant changes
4. PR with changelog of what changed and why

## Naming Conventions

- Skill folder: `kebab-case` (e.g., `ath-ux-ui-design`)
- Prefix with `ath-` for ATHENDAT-specific skills
- No prefix for generic/reusable skills
- Reference files: `kebab-case.md` describing the topic (e.g., `ui-technical.md`)

## Quality Checklist

- [ ] SKILL.md has valid YAML frontmatter with `name` and `description`
- [ ] Description is specific enough to trigger correctly
- [ ] Body is under 500 lines (depth offloaded to references)
- [ ] All content is in English
- [ ] Tested with 3+ real prompts
- [ ] Packaged `.skill` file in `dist/`
- [ ] No secrets, API keys, or sensitive data in any file
