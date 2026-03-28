# Skills Repo Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Convert the Claude-specific skills repo into an agent-agnostic, category-organized skills library.

**Architecture:** Flat category directories at the repo root, each containing skill subdirectories with `skill.md` + optional `references/`. No build step, no packaging. README as central index.

**Tech Stack:** Markdown, YAML frontmatter, Git.

---

### Task 1: Create new directory structure and move references

**Files:**
- Create: `design/ux-ui/skill.md` (placeholder, will be written in Task 2)
- Move: `skills/ath-ux-ui-design/references/ui-technical.md` -> `design/ux-ui/references/ui-technical.md`
- Move: `skills/ath-ux-ui-design/references/ux-strategy.md` -> `design/ux-ui/references/ux-strategy.md`

- [ ] **Step 1: Create the directory structure**

```bash
mkdir -p design/ux-ui/references
```

- [ ] **Step 2: Copy reference files to new location**

The reference files are already agent-agnostic (pure design knowledge). Copy them as-is:

```bash
cp skills/ath-ux-ui-design/references/ui-technical.md design/ux-ui/references/ui-technical.md
cp skills/ath-ux-ui-design/references/ux-strategy.md design/ux-ui/references/ux-strategy.md
```

- [ ] **Step 3: Verify files copied correctly**

```bash
diff skills/ath-ux-ui-design/references/ui-technical.md design/ux-ui/references/ui-technical.md
diff skills/ath-ux-ui-design/references/ux-strategy.md design/ux-ui/references/ux-strategy.md
```

Expected: no output (files are identical).

- [ ] **Step 4: Commit**

```bash
git add design/ux-ui/references/
git commit -m "refactor: create design/ux-ui structure and copy reference files"
```

---

### Task 2: Write agent-agnostic skill.md

**Files:**
- Create: `design/ux-ui/skill.md`

- [ ] **Step 1: Write the new skill.md**

Write `design/ux-ui/skill.md` with the following content. Key changes from the original `SKILL.md`:
- New 4-field YAML frontmatter (name, description, category, tags)
- "Read `references/...`" changed to "Consult `references/...`"
- Quick Decision table updated with neutral language
- Output Format section uses neutral "Implementation" instead of agent-specific phrasing
- No references to any agent's tools or commands

```markdown
---
name: ux-ui
description: >
  UX/UI design system and guidelines for ATHENDAT products (BALANC, HelarteApp, and client projects).
  Combines technical UI precision (4pt grid, typography scale, color semantics, interaction states)
  with cognitive psychology principles (fluency, halo effect, peak-end rule) to produce premium
  digital experiences. Use this skill whenever designing, reviewing, critiquing, or improving any
  UI component, screen, layout, flow, wireframe, mockup, or design system — including landing pages,
  dashboards, forms, mobile screens, web apps, admin panels, POS interfaces, or any user-facing
  element. Also applies for UX audits, accessibility reviews, dark mode implementation, design tokens,
  component libraries, or feedback on visual hierarchy, spacing, or interaction patterns.
category: design
tags: [angular, flutter, ui, ux, accessibility, design-system, dark-mode, pos, mobile, web]
---

# UX/UI Design System

Premium design methodology for ATHENDAT products. Every interface must feel intentional, reduce cognitive load, and guide users toward their goals with minimal friction.

This skill operates at two levels: **technical execution** (UI) and **behavioral strategy** (UX). Consult both before designing anything.

## Quick Decision: Which Reference to Consult

Before starting, determine what you need:

| Task | Reference |
|------|-----------|
| Building/reviewing components, layouts, spacing, typography, colors, dark mode | `references/ui-technical.md` |
| Designing flows, onboarding, forms, error handling, empty states, user journeys | `references/ux-strategy.md` |
| Full screen or feature design | **Both references** |

## Core Principles

These three principles override any specific rule when they conflict:

1. **Cognitive Fluency First** — If a user has to think about how to use the interface, the design has failed. Every element must feel predictable and self-evident. Prioritize recognition over recall.

2. **The 50ms Verdict** — Users form quality judgments in ~50ms (the Halo Effect). The hero section, first screen, or initial state of any component sets the perceived quality of the entire product. Invest disproportionate effort here.

3. **Peak-End Memory** — Users remember experiences by their best moment (peak delight) and the final interaction (end). Design at least one moment of micro-delight per flow, and make the completion state feel rewarding.

## Design Tokens — ATHENDAT Defaults

When no project-specific design system exists, use these defaults. They are calibrated for B2B SaaS interfaces (BALANC, HelarteApp) and can be overridden per-project.

### Spacing (4pt Grid)

All spacing and sizing values must be multiples of 4. This is non-negotiable.

```
--space-xs:   4px    (tight inline elements)
--space-sm:   8px    (related elements)
--space-md:   16px   (default component padding)
--space-lg:   24px   (section gaps)
--space-xl:   32px   (major section separation)
--space-2xl:  48px   (page-level breathing room)
--space-3xl:  64px   (hero/landing sections)
```

### Typography Scale

Limit to 6 sizes maximum. Tighter letter-spacing on headings creates a more professional, editorial feel.

```
--text-xs:    12px / 1.5    (captions, labels)
--text-sm:    14px / 1.5    (secondary text, table data)
--text-base:  16px / 1.5    (body text)
--text-lg:    20px / 1.4    (subheadings, card titles)
--text-xl:    28px / 1.2    (section headings)      letter-spacing: -0.02em
--text-2xl:   40px / 1.1    (hero/page titles)       letter-spacing: -0.03em
```

### Color Semantics

Color communicates function, not decoration. Every color must have a semantic role.

```
Primary    -> Brand action (main CTA, active navigation)
Secondary  -> Supporting actions (secondary buttons, links)
Success    -> Confirmation, completion (green family)
Warning    -> Caution, attention needed (amber family)
Error      -> Failure, destructive action (red family)
Info       -> Neutral guidance (blue family)
Neutral    -> Backgrounds, borders, disabled states (gray scale)
```

Always provide a minimum contrast ratio of **4.5:1** for text and **3:1** for interactive elements (WCAG AA).

### Interaction States

Every interactive element must define all five states. Missing states feel broken.

```
Default   -> Resting appearance
Hover     -> Subtle elevation or color shift (desktop)
Focus     -> Visible ring/outline for keyboard navigation (accessibility)
Active    -> Pressed/engaged feedback (scale or darken)
Disabled  -> Reduced opacity (0.5) + cursor: not-allowed
```

## Dark Mode Rules

Dark mode is not "invert colors." Follow chromatic elevation:

- **Never use pure black** (`#000`). Base background: `#0F0F11` to `#1A1A1E`.
- **Layered elevation**: Each layer above the base gets slightly lighter (+2-4% brightness per level). This creates depth without shadows.
- **Reduce saturation**: Vibrant colors that work on light backgrounds become harsh on dark. Desaturate by 10-15%.
- **Text hierarchy**: Primary text at 87% white opacity, secondary at 60%, disabled at 38%.

## Micro-Interactions Checklist

Add micro-interactions at these friction points (prioritize top 3 per flow):

- Button press: brief scale + color feedback (100-150ms)
- Form field focus: smooth border/label animation
- Successful action: checkmark morph or subtle celebration
- Loading states: skeleton screens over spinners (feels faster)
- Copy to clipboard: tooltip confirmation with checkmark
- Toggle/switch: spring physics animation
- Navigation transition: directional slide matching hierarchy
- Error appearance: gentle shake + red accent (not aggressive)

## Output Format

When designing a component, screen, or flow, structure the output as:

```
## [Component/Screen Name]

### Context
Who uses this, when, and why.

### Design Decisions
Key choices made and their rationale (tie to UX principles).

### Specifications
- Layout grid and spacing
- Typography choices
- Color usage
- Interaction states
- Responsive behavior

### Implementation
Working code (HTML/CSS, Angular, Flutter, or other — match the project stack).

### Checklist
- [ ] 4pt grid respected
- [ ] Hero/first impression optimized (50ms test)
- [ ] All interactive states defined
- [ ] Cognitive load minimized
- [ ] Visual hierarchy guides to CTA
- [ ] Dark mode compatible
- [ ] Accessible (WCAG AA minimum)
- [ ] At least one micro-delight moment
```

## Platform-Specific Notes

- **Angular (BALANC web)**: Use Angular Material or custom component library. Prefer CSS custom properties for theming. Implement OnPush change detection for animation-heavy components.
- **Flutter (mobile apps)**: Use Material 3 with custom theme extensions. Respect platform conventions (iOS/Android) while maintaining brand identity. Use `AnimatedContainer` and `Hero` transitions.
- **POS/SUNMI devices**: Design for limited screen real estate and touch-first interaction. Larger touch targets (48px minimum). High contrast for varied lighting conditions.
- **Offline-first interfaces**: Always show sync status. Design optimistic UI patterns — show success immediately, reconcile in background. Make offline state obvious but not alarming.
```

- [ ] **Step 2: Verify line count is under 500**

```bash
wc -l design/ux-ui/skill.md
```

Expected: under 500 lines.

- [ ] **Step 3: Commit**

```bash
git add design/ux-ui/skill.md
git commit -m "feat: add agent-agnostic ux-ui skill.md"
```

---

### Task 3: Rewrite README.md

**Files:**
- Modify: `README.md` (full rewrite)

- [ ] **Step 1: Write the new README.md**

```markdown
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
- **GitHub Copilot:** Add the `skill.md` path to your workspace instructions or include it directly in chat context
- **Gemini CLI:** Add the `skill.md` path to your Gemini configuration or include it in your context files
- **Any other agent:** Paste or reference the `skill.md` content directly

Each skill's `skill.md` is self-contained. If it has a `references/` directory, the main file will indicate when to consult those deeper documents.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on creating and submitting new skills.

## License

This project is licensed under the MIT License – see [LICENSE](LICENSE) for details.
```

- [ ] **Step 2: Commit**

```bash
git add README.md
git commit -m "docs: rewrite README for agent-agnostic skills library"
```

---

### Task 4: Rewrite CONTRIBUTING.md

**Files:**
- Modify: `CONTRIBUTING.md` (full rewrite)

- [ ] **Step 1: Write the new CONTRIBUTING.md**

```markdown
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

New categories can be added as top-level directories when needed.

## Quality Checklist

- [ ] `skill.md` has valid YAML frontmatter with `name`, `description`, `category`, `tags`
- [ ] Content is agent-agnostic (no tool-specific references)
- [ ] All content in English
- [ ] `skill.md` under 500 lines
- [ ] `README.md` table updated
- [ ] No secrets, API keys, or sensitive data in any file
```

- [ ] **Step 2: Commit**

```bash
git add CONTRIBUTING.md
git commit -m "docs: rewrite CONTRIBUTING for agent-agnostic workflow"
```

---

### Task 5: Update .gitignore and PR template

**Files:**
- Modify: `.gitignore`
- Modify: `.github/PULL_REQUEST_TEMPLATE.md`

- [ ] **Step 1: Update .gitignore**

Remove the `dist/`-related comment at the bottom. The new `.gitignore`:

```
# OS
.DS_Store
Thumbs.db

# IDE
.vscode/
.idea/
*.swp
*.swo

# Node (if any scripts use it)
node_modules/
package-lock.json

# Python (if any scripts use it)
__pycache__/
*.pyc
.venv/
venv/

# Temp/workspace files
*-workspace/
iteration-*/
eval-*/
feedback.json
```

- [ ] **Step 2: Update PR template**

Replace `.github/PULL_REQUEST_TEMPLATE.md` with:

```markdown
## Skill Change

**Skill:** `<category>/<skill-name>/`
**Type:** New Skill / Update / Fix

### What does this skill do?
<!-- Brief description -->

### When should it be used?
<!-- List 3-5 scenarios where this skill applies -->

1.
2.
3.

### Checklist

- [ ] `skill.md` has valid YAML frontmatter (`name`, `description`, `category`, `tags`)
- [ ] Content is agent-agnostic (no tool-specific references)
- [ ] All content in English
- [ ] `skill.md` under 500 lines
- [ ] `README.md` table updated

### Notes
<!-- Any context, tradeoffs, or known limitations -->
```

- [ ] **Step 3: Commit**

```bash
git add .gitignore .github/PULL_REQUEST_TEMPLATE.md
git commit -m "chore: update gitignore and PR template for new repo structure"
```

---

### Task 6: Delete old files and directories

**Files:**
- Delete: `dist/ath-ux-ui-design.skill`
- Delete: `dist/` (directory)
- Delete: `skills/ath-ux-ui-design/SKILL.md`
- Delete: `skills/ath-ux-ui-design/references/ui-technical.md`
- Delete: `skills/ath-ux-ui-design/references/ux-strategy.md`
- Delete: `skills/` (directory)

- [ ] **Step 1: Remove old directories**

```bash
git rm -r dist/
git rm -r skills/
```

- [ ] **Step 2: Verify new structure is correct**

```bash
find . -not -path './.git/*' -not -path './docs/*' -type f | sort
```

Expected output:
```
./.github/PULL_REQUEST_TEMPLATE.md
./.gitignore
./CONTRIBUTING.md
./README.md
./design/ux-ui/references/ui-technical.md
./design/ux-ui/references/ux-strategy.md
./design/ux-ui/skill.md
```

- [ ] **Step 3: Commit**

```bash
git commit -m "refactor: remove old skills/ and dist/ directories"
```

---

### Task 7: Final verification

- [ ] **Step 1: Verify all YAML frontmatter is valid**

Check that `design/ux-ui/skill.md` starts with valid YAML frontmatter containing all 4 required fields (`name`, `description`, `category`, `tags`).

- [ ] **Step 2: Verify skill.md is under 500 lines**

```bash
wc -l design/ux-ui/skill.md
```

Expected: under 500.

- [ ] **Step 3: Verify no agent-specific language remains**

Search for agent-specific terms in the skill file:

```bash
grep -i -E "Read tool|Write tool|Grep tool|Bash tool|claude code|use the .* tool" design/ux-ui/skill.md
```

Expected: no output (no matches).

- [ ] **Step 4: Review git log**

```bash
git log --oneline
```

Expected: clean history with the commits from Tasks 1-6.
