# ATHENDAT Skills

Reusable skill modules for AI coding agents. Agent-agnostic, organized by discipline.

## Skills

### Design

| Skill | Description | Tags |
|-------|-------------|------|
| [ux-ui](design/ux-ui/) | UX/UI design system combining technical precision (4pt grid, typography, color semantics) with cognitive psychology (fluency, halo effect, peak-end rule) for premium interfaces. | angular, flutter, ui, ux, accessibility, design-system |

### Backend

_No skills yet._

### Frontend

_No skills yet._

### Mobile

_No skills yet._

### DevOps

_No skills yet._

### Testing

_No skills yet._

### Documentation

_No skills yet._

## Tech Stack Context

These skills are designed around ATHENDAT's core stack:

- **Backend:** NestJS, C#
- **Frontend:** Angular
- **Mobile:** Flutter
- **Database:** MongoDB
- **Infrastructure:** Docker, APISIX, Redis, RabbitMQ, Hashicorp Vault, Appwrite
- **Hardware:** SUNMI POS devices
- **Maps:** Mapbox

## Usage

These skills are plain Markdown files. Point your AI coding agent to the relevant `skill.md` file:

- **Claude Code:** Add as a skill or include the path in your project context
- **Cursor / Windsurf:** Add the `skill.md` path to your rules or context files
- **GitHub Copilot:** Reference in `.github/copilot-instructions.md` or include in chat context
- **Gemini CLI:** Reference in `GEMINI.md` or add to context files
- **Any other agent:** Paste or reference the `skill.md` content directly

Each skill's `skill.md` is self-contained. If it has a `references/` directory, the main file will indicate when to consult those deeper documents.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on creating and submitting new skills.

## License

Internal use — ATHENDAT S.R.L. All rights reserved.
