# 🧠 ATHENDAT Claude Skills

A centralized repository of reusable [Claude Skills](https://docs.anthropic.com) for ATHENDAT's product ecosystem. Skills are structured knowledge modules that enhance Claude's capabilities for specific tasks — from UI/UX design to document generation, code review, and beyond.

## What Are Skills?

Skills are `.skill` packages containing:
- A `SKILL.md` with instructions, patterns, and decision logic
- Optional `references/` for deep-dive documentation
- Optional `scripts/` for deterministic automation
- Optional `assets/` for templates, fonts, or other static files

When installed in Claude, skills trigger automatically based on context — giving Claude domain-specific expertise tailored to ATHENDAT's stack and workflows.

## Available Skills

| Skill | Description | Status |
|---|---|---|
| [`ath-ux-ui-design`](skills/ath-ux-ui-design/) | UX/UI design system combining technical precision (4pt grid, typography, color semantics) with cognitive psychology (fluency, halo effect, peak-end rule) for premium interfaces. | ✅ Ready |

## Tech Stack Context

These skills are designed around ATHENDAT's core stack:

- **Backend:** NestJS, C#
- **Frontend:** Angular
- **Mobile:** Flutter
- **Database:** MongoDB
- **Infrastructure:** Docker, APISIX, Redis, RabbitMQ, Hashicorp Vault, Appwrite
- **Hardware:** SUNMI POS devices
- **Maps:** Mapbox

## Installation

### In Claude.ai (UI)
1. Go to **Settings → Profile → Skills**
2. Upload the `.skill` file from the `dist/` folder

### Manual Build
```bash
# Package a skill from source
cd skills/<skill-name>
# Use the skill-creator packaging script or zip manually:
zip -r ../../dist/<skill-name>.skill .
```

## Repository Structure

```
claude-skills/
├── README.md
├── CONTRIBUTING.md
├── .gitignore
├── dist/                    # Packaged .skill files (ready to install)
├── skills/                  # Skill source files
│   └── <skill-name>/
│       ├── SKILL.md         # Main instructions (required)
│       ├── references/      # Deep-dive docs (loaded on demand)
│       ├── scripts/         # Automation scripts
│       └── assets/          # Templates, fonts, static files
└── .github/
    └── PULL_REQUEST_TEMPLATE.md
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on creating and submitting new skills.

**Quick start:**
1. Create a new folder under `skills/`
2. Write a `SKILL.md` with YAML frontmatter (`name`, `description`)
3. Add reference files if the skill needs deep-dive documentation
4. Test with real prompts in Claude
5. Package and add to `dist/`
6. Open a PR

## License

Internal use — ATHENDAT S.R.L. All rights reserved.
