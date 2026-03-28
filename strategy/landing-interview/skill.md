---
name: landing-interview
description: >
  Structured discovery interview for landing page projects. Guides the conversation
  with the developer before starting a new landing page or auditing an existing one.
  Produces a PRD in Markdown. Use when the user mentions landing page, landing web,
  one-page site, or wants to plan, brief, or audit a conversion-focused website.
category: strategy
tags: [landing, interview, discovery, prd, audit, web, conversion]
---

# Landing Page Discovery Interview

Strategy precedes design. The goal is to eliminate guesswork and ground every decision in purpose, audience, and measurable outcomes.

This skill interviews the developer working on the landing page and produces a PRD before any code or design work begins.

## Detect Mode

Start by asking: **"Is this a new landing page project or an audit of an existing one?"**

If audit, ask if there is a URL available for inspection.

## Inspect Landing (Audit Mode with URL)

When a URL is provided, inspect the landing before starting the interview.

**Tool priority:**
1. Playwright CLI in headed mode (`npx playwright open <url>`)
2. Playwright MCP (`browser_navigate`, `browser_take_screenshot`)
3. Chrome DevTools MCP (`navigate_page`, `take_screenshot`)

**What to capture:**
- Desktop screenshot (1440px) of hero/above the fold
- Mobile screenshot (375px) of hero
- Full page scroll on desktop
- Note: visible CTAs, visual hierarchy, section count, perceived load speed

**How to use observations:**
- Do not share a report immediately — use findings to ask sharper questions
- Contrast developer answers with what was observed during inspection
- Include findings with screenshots in the audit section of the PRD

If no browser tool is available, inform the developer and continue with verbal description or shared screenshots.

## Interview

Consult `references/interview-questions.md` for the full question set.

**Rules:**
- One question at a time. Never dump an entire block at once.
- Conversational and challenging tone. Push back on vague answers:
  - "'Everyone' is not a target audience — who specifically?"
  - "You listed 8 sections — which 3 are essential if we had to ship tomorrow?"
  - "'Modern and clean' — everyone says that. What specifically should it NOT look like?"
  - "Who will update the content after launch? If nobody, it goes stale in 3 months."
  - "Launch is day 1, not the finish line. What's the plan for week 2?"
- In audit mode, contrast answers with inspection observations.

**Interview blocks:**
1. Strategy & Goals
2. Structure & Hierarchy
3. Design Direction
4. Technical & Performance
5. Launch & Post-launch

## Generate PRD

After the interview, compile all answers into a PRD using the template below.

- Ask the developer where to save the file (directory path)
- Optionally publish as a GitHub issue if requested

## Validate Against Premium Checklist

Consult `references/premium-checklist.md`. Verify the PRD covers all 7 quality areas. If any area is missing, flag it: "The PRD doesn't address [area]. Should we add a section or is it out of scope?"

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

## 9. Audit Findings (audit mode only)

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
