# Contributing

## Adding a New Skill

1. Create a folder under the appropriate category: `<category>/<skill-name>/`
2. Write a `skill.md` with YAML frontmatter (`name`, `description`, `category`, `tags`)
3. Add a `references/` directory if the skill needs deep-dive documentation
4. Add the skill to the table in `README.md`
5. Open a PR

## Conventions

- **Folder names:** kebab-case (e.g., `ux-ui`, `nestjs-patterns`)
- **Language:** All content in English
- **Voice:** Imperative, agent-agnostic. Never reference specific agent tools (no "use Read tool", no "run /command")
- **Size:** `skill.md` under 500 lines. Offload depth to `references/`
- **Frontmatter:** Only 4 fields: `name`, `description`, `category`, `tags`

## Categories

| Directory | Discipline |
|-----------|-----------|
| `design/` | UX, UI, design systems |
| `backend/` | APIs, services, databases |
| `frontend/` | Web apps, components |
| `mobile/` | Flutter, native apps |
| `devops/` | CI/CD, infrastructure, containers |
| `testing/` | QA, test strategies |
| `documentation/` | Technical writing, specs |
| `strategy/` | Discovery, interviews, PRDs, project planning |

New categories can be added as top-level directories when needed.

## Quality Checklist

- [ ] `skill.md` has valid YAML frontmatter with `name`, `description`, `category`, `tags`
- [ ] Content is agent-agnostic (no tool-specific references)
- [ ] All content in English
- [ ] `skill.md` under 500 lines
- [ ] `README.md` table updated
- [ ] No secrets, API keys, or sensitive data in any file
