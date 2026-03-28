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
