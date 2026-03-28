# Landing Interview Skill Design

A structured discovery interview skill for landing page projects. Guides conversation with the developer before starting a new landing page or auditing an existing one. Produces a PRD in Markdown.

## Goal

Eliminate guesswork from landing page projects. Every design decision should be grounded in strategy, audience understanding, and measurable objectives — captured in a PRD before any code or design work begins.

## File Structure

```
strategy/landing-interview/
├── skill.md                          # Flow, logic, modes, PRD template, output
└── references/
    ├── interview-questions.md        # Questions organized in 5 thematic blocks
    └── premium-checklist.md          # Quality criteria for validation
```

## Frontmatter

```yaml
---
name: landing-interview
description: >
  Structured discovery interview for landing page projects. Guides the conversation
  with the developer before starting a new landing page or auditing an existing one.
  Produces a PRD in Markdown. Use when the user mentions landing page, landing web,
  one-page site, or wants to plan/audit a conversion-focused website.
category: strategy
tags: [landing, interview, discovery, prd, audit, web, conversion]
---
```

## Modes

The skill supports two modes:

1. **New Project** — Discovery interview from scratch to define requirements
2. **Audit** — Review of an existing landing page, contrasting stated goals vs observed reality

The first question determines the mode: "Is this a new landing page project or an audit of an existing one?"

## Flow

### 1. Detect Mode

Ask whether this is a new project or an audit. If audit, ask if there is a URL available.

### 2. Inspect Landing (audit mode with URL only)

**Tool priority:**
1. Playwright CLI in headed mode (`npx playwright open <url>`) — preferred
2. Playwright MCP (`browser_navigate`, `browser_take_screenshot`)
3. Chrome DevTools MCP (`navigate_page`, `take_screenshot`)

**What to inspect:**
- Screenshot desktop (1440px) of hero/above the fold
- Screenshot mobile (375px) of hero
- Full page scroll on desktop
- Identify: visible CTAs, visual hierarchy, number of sections, perceived load speed

**How to use inspection:**
- Do NOT share a report to the developer immediately
- Use observations to ask sharper questions during the interview
- In the audit section of the PRD, include findings with screenshots as evidence
- Contrast what the developer says vs what was observed ("You mentioned a single CTA, but I see 4 different buttons competing above the fold")

**If no browser tool is available:**
- Inform: "I can't inspect the URL directly. Describe the current state of the landing or share screenshots."
- Continue with verbal interview

### 3. Interview by Blocks

Consult `references/interview-questions.md` for the questions in each block:

1. **Strategy & Goals** — audience, primary action, success metrics, user segments
2. **Structure & Hierarchy** — sitemap, message hierarchy, content status
3. **Design Direction** — brand assets, visual references, photography/graphics
4. **Technical & Performance** — platform/CMS, SEO, analytics, contact channels
5. **Launch & Post-launch** — training, support window, iteration plan

**Interview tone:** Conversational and challenging. Question vague or incomplete answers:
- "'Everyone' is not a target audience — who specifically?"
- "You listed 8 sections — which 3 are essential if we had to ship tomorrow?"
- "You said 'modern and clean' — everyone says that. What specifically should it NOT look like?"
- "Who will update the content after launch? If nobody, it'll go stale in 3 months."
- "Launch is day 1, not the finish line. What's the plan for week 2?"

One question at a time. Do not dump all questions from a block at once.

In audit mode: contrast developer answers with inspection observations.

### 4. Generate PRD

Compile all answers into a structured PRD. Ask the user where to save it (file path). Optionally publish as a GitHub issue if the user requests it.

### 5. Validate Against Premium Checklist

Consult `references/premium-checklist.md`. Verify the PRD covers all quality criteria. If areas are missing, flag them: "The PRD doesn't address [area]. Should we add a section for this or is it out of scope?"

## PRD Template

```markdown
# Landing Page PRD: [Project Name]

**Date:** YYYY-MM-DD
**Mode:** New Project | Audit
**Developer:** [name or handle]
**Status:** Draft

---

## 1. Overview

Brief description of the project and its context.

## 2. Target Audience

Who they are, what they know, how they arrive at the page.

## 3. Primary Objective

The One Thing — the single action we want users to take.

## 4. Success Metrics

Specific, measurable outcomes expected within 3 months.

## 5. Site Structure

| Section | Purpose | Priority |
|---------|---------|----------|
| Hero | ... | Must-have |
| ... | ... | ... |

### Message Hierarchy
- **Primary:** ...
- **Secondary:** ...
- **Tertiary:** ...

## 6. Design Direction

### Brand Assets
Logo, colors, typography — current status and decisions.

### Visual Style
References, mood, what it should NOT look like.

### Assets Needed
Custom graphics, photography, illustrations — with source/budget.

## 7. Technical Requirements

- **Platform/CMS:** ...
- **SEO:** Target keywords, heading structure, performance targets
- **Analytics:** Tools and key events to track
- **Contact channels:** ...

## 8. Launch Plan

- **Training:** Who, when, what
- **Support window:** Duration and scope
- **Iteration:** Measurement and improvement cycle

## 9. Audit Findings (only for audit mode)

### Current State
Screenshots and observations from site inspection.

### Issues Found
Prioritized list mapped to premium checklist areas.

### Recommendations
Specific actions to address each issue.

## 10. Premium Quality Checklist

- [ ] First impression / 50ms test
- [ ] Visual assets (custom, purposeful)
- [ ] Brand foundations (logo, colors, typography)
- [ ] Motion & interaction (subtle, accessible)
- [ ] Structure & conversion (clear journey, strong CTA)
- [ ] Client autonomy (self-manageable)
- [ ] Handover & support (planned)
```

Section 9 only appears in audit mode. Checklist items are checked based on what the PRD covers.

## Reference: Interview Questions (interview-questions.md)

5 blocks with mandatory questions and challenge prompts for vague answers. See Section 3 of the flow above for the full list.

## Reference: Premium Checklist (premium-checklist.md)

7 areas of quality validation:

1. **First Impression (50ms test)** — clear purpose, no template energy, trust signals
2. **Visual Assets** — custom/brand-aligned, purposeful, no decorative noise
3. **Brand Foundations** — professional logo, cohesive colors (2-3 max), sophisticated typography
4. **Motion & Interaction** — scroll-based animation, interactive feedback, no gimmicks, respects prefers-reduced-motion
5. **Structure & Conversion** — logical sitemap, clear journey, no decision paralysis, strong consistent CTA, SEO-ready
6. **Client Autonomy** — self-manageable, not fragile, built for longevity
7. **Handover & Support** — structured training, post-launch support window, clear expectations

## New Category

This skill introduces a new top-level category: `strategy/`. Must be added to:
- `CONTRIBUTING.md` categories table
- `README.md` skills index
