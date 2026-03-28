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

### Strategy

| Skill | Description | Tags |
|-------|-------------|------|
| [landing-interview](strategy/landing-interview/) | Structured discovery interview for landing page projects. Guides conversation with the developer before starting a new landing or auditing an existing one. Produces a PRD. | landing, interview, discovery, prd, audit, web, conversion |

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
- **GitHub Copilot:** Optionally reference it from a Copilot configuration file (for example `.github/copilot-instructions.md` that you create) or include it directly in chat context
- **Gemini CLI:** Optionally reference it from a Gemini configuration file (for example a `GEMINI.md` file you create) or add it to your context files
- **Any other agent:** Paste or reference the `skill.md` content directly

Each skill's `skill.md` is self-contained. If it has a `references/` directory, the main file will indicate when to consult those deeper documents.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on creating and submitting new skills.

## License

[MIT](LICENSE)
