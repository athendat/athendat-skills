# UI Technical Reference

Detailed implementation guidelines for building ATHENDAT interfaces with precision.

## Table of Contents
1. Grid System Deep Dive
2. Typography Mastery
3. Color System Implementation
4. Component Patterns
5. Dark Mode Implementation
6. Responsive Strategy
7. Animation & Motion
8. Accessibility Essentials

---

## 1. Grid System Deep Dive

### The 4pt System

Every dimension in the interface — margins, padding, widths, heights, gaps, border-radius — is a multiple of 4. This creates a subconscious rhythm that users perceive as "polished" without knowing why.

**Why 4 and not 8?** The 4pt base gives you finer control (4, 8, 12, 16...) while 8pt can feel too coarse for dense data interfaces like BALANC. Use 8pt as the primary increment and 4pt for fine adjustments.

**Common spacing patterns:**

```
Inline spacing (between icon and label):        8px
Input padding:                                   12px vertical, 16px horizontal
Card padding:                                    16px (compact) / 24px (comfortable)
Stack gap (form fields):                         16px
Section gap:                                     32px - 48px
Page margin (desktop):                           24px - 64px
Page margin (mobile):                            16px
```

### Layout Grids

**Desktop (>1024px):** 12-column grid, 24px gutters, max-width 1280px centered.
**Tablet (768-1024px):** 8-column grid, 16px gutters.
**Mobile (<768px):** 4-column grid, 16px gutters, 16px outer margins.

For dense admin dashboards (BALANC), consider a 24-column micro-grid to handle complex table layouts and sidebar combinations.

### White Space as Design Tool

White space is not "empty" — it is an active design element that:
- Creates hierarchy (more space = higher importance)
- Reduces cognitive load (breathing room between groups)
- Signals premium quality (cheap designs cram everything together)

**Rule of thumb:** When in doubt, add more space, not less. Then selectively tighten where density is needed (data tables, toolbars).

---

## 2. Typography Mastery

### Heading Treatment

Negative letter-spacing on headings (-2% to -3%) creates a tighter, more editorial feel. This subtle technique separates amateur from professional typography.

```css
h1 {
  font-size: 40px;
  line-height: 1.1;
  letter-spacing: -0.03em;
  font-weight: 700;
}

h2 {
  font-size: 28px;
  line-height: 1.2;
  letter-spacing: -0.02em;
  font-weight: 600;
}
```

### Body Text Rules

- Line-height: 1.5 for body text (never less than 1.4)
- Maximum line width: 65-75 characters (use `max-width: 65ch`)
- Paragraph spacing: equal to line-height (typically 24px for 16px/1.5 body)

### Type Scale Discipline

Limit yourself to **6 sizes maximum** across the entire product. More sizes create visual noise and make the system harder to maintain.

If you need to differentiate without adding sizes, use:
- Font weight (400 vs 600)
- Color/opacity (primary vs secondary text)
- Case transformation (uppercase for labels at small sizes)

### Font Selection Guide

| Product Type | Recommended Approach |
|---|---|
| BALANC (data-heavy SaaS) | Geometric sans-serif (e.g., DM Sans, Plus Jakarta Sans). Clean, high x-height for readability at small sizes. |
| HelarteApp (consumer-facing) | Humanist sans-serif with personality. Slightly rounded terminals feel approachable. |
| POS interfaces | High legibility is paramount. Test at arm's length. Avoid thin weights. |
| Landing pages | Pair a distinctive display font (headings) with a clean body font. |

---

## 3. Color System Implementation

### Semantic Color Palette Structure

Define colors in three layers:

```
Layer 1 — Primitives:     Raw color values (blue-500: #3B82F6)
Layer 2 — Semantics:      Role-based aliases (color-primary: var(--blue-500))
Layer 3 — Components:     Specific usage (btn-primary-bg: var(--color-primary))
```

This three-layer approach means you can swap entire themes by changing Layer 2 without touching component code.

### State Colors

Each semantic color needs a full state palette:

```
--color-primary:          #3B82F6   (default)
--color-primary-hover:    #2563EB   (10% darker)
--color-primary-active:   #1D4ED8   (20% darker)
--color-primary-subtle:   #EFF6FF   (background tint, 5-10% opacity)
--color-primary-border:   #93C5FD   (lighter variant for borders)
```

### Accessible Color Pairs

Always define foreground + background pairs. Never assume a color works on all backgrounds.

```
✅ --color-error-bg: #FEF2F2;  --color-error-text: #991B1B;  (contrast 7.2:1)
❌ --color-error: #EF4444 on white background;                 (contrast 3.9:1 — FAILS)
```

---

## 4. Component Patterns

### Buttons

Three tiers, visually distinct:

```
Primary:    Filled, brand color. One per visible area (the main action).
Secondary:  Outlined or muted fill. Supporting actions.
Tertiary:   Text-only or ghost. Least important / cancel / back.
```

Minimum touch target: **44x44px** (48x48 for POS/SUNMI).
Minimum horizontal padding: **16px** (24px for primary buttons).
Border-radius: **8px** (consistent across all buttons).

### Form Inputs

- Label always visible (never placeholder-only — it disappears on focus)
- Error messages appear below the field, not in tooltips
- Group related fields visually (address block, payment block)
- Use `autocomplete` attributes for browser autofill
- Floating labels are acceptable if they maintain readability in filled state

### Cards

- Consistent border-radius (12px for cards, 8px for inner elements)
- Elevation via subtle shadow OR border, not both
- Clear content hierarchy: image → title → description → action
- Hover state: slight elevation increase or border color change

### Data Tables (critical for BALANC)

- Row height: 48px minimum, 56px comfortable
- Horizontal padding: 16px per cell
- Header: visually distinct (background color or weight), sticky on scroll
- Zebra striping OR subtle horizontal borders, not both
- Sort indicators always visible on sortable columns
- Row hover: subtle background highlight
- Selection: checkbox column, highlight selected rows

### Empty States

Never show a blank screen. Empty states are UX opportunities:
- Illustration or icon (relevant, not generic)
- Clear message: what this area will contain
- Primary action: CTA to populate the state
- Keep it encouraging, not clinical

---

## 5. Dark Mode Implementation

### Chromatic Elevation Model

Instead of shadows (which don't read well on dark surfaces), use brightness layers:

```
Level 0 — Page background:     #0F0F11  (darkest)
Level 1 — Card/panel:          #1A1A1E  (+4% brightness)
Level 2 — Dropdown/modal:      #242428  (+4% more)
Level 3 — Tooltip/popover:     #2E2E33  (+4% more)
```

### Text Opacity Hierarchy

```
Primary text:    rgba(255, 255, 255, 0.87)
Secondary text:  rgba(255, 255, 255, 0.60)
Disabled text:   rgba(255, 255, 255, 0.38)
Placeholder:     rgba(255, 255, 255, 0.30)
```

### Color Adjustments for Dark Mode

- Desaturate brand colors by 10-15%
- Increase lightness of accent colors so they pop against dark backgrounds
- Swap semantic backgrounds: error-bg from light red to dark muted red
- Borders: Use rgba(255,255,255, 0.12) instead of gray values (adapts to any surface)

### Progressive Blur

For overlays and backdrop effects, use layered blur instead of solid opacity:

```css
.overlay {
  background: linear-gradient(
    to bottom,
    rgba(15, 15, 17, 0.0) 0%,
    rgba(15, 15, 17, 0.8) 40%,
    rgba(15, 15, 17, 0.95) 100%
  );
  backdrop-filter: blur(8px);
}
```

This creates a natural depth transition, especially for text over images.

---

## 6. Responsive Strategy

### Breakpoints

```
Mobile:          < 640px    (single column, stack everything)
Tablet:          640-1024px (2 columns, collapsible sidebars)
Desktop:         1024-1440px (full layout)
Wide:            > 1440px   (constrain content, expand margins)
```

### Mobile-First Priorities

1. Content hierarchy must work in single column before expanding
2. Touch targets: 44px minimum (48px for primary actions)
3. Thumb zone: Place primary actions in bottom third of screen
4. Avoid hover-dependent interactions entirely on mobile
5. Form fields: Full width, stack vertically, generous spacing

---

## 7. Animation & Motion

### Timing Defaults

```
Micro (state change):     100-150ms   ease-out
Small (expand/collapse):  200-250ms   ease-in-out
Medium (panel/modal):     300-350ms   ease-in-out
Large (page transition):  400-500ms   ease-in-out
```

### Easing Functions

```css
--ease-standard:   cubic-bezier(0.4, 0.0, 0.2, 1);    /* most interactions */
--ease-decelerate: cubic-bezier(0.0, 0.0, 0.2, 1);    /* entering elements */
--ease-accelerate: cubic-bezier(0.4, 0.0, 1, 1);      /* exiting elements */
--ease-spring:     cubic-bezier(0.34, 1.56, 0.64, 1);  /* playful bounce */
```

### Motion Principles

- **Meaningful**: Animation should convey spatial relationships (where something came from / goes to)
- **Functional**: Loading, success, error states benefit from animation. Decorative loops do not.
- **Subtle**: If you notice the animation consciously, it's probably too much. The user should feel it, not see it.
- **Respect preferences**: Always honor `prefers-reduced-motion` — replace animations with instant transitions.

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 8. Accessibility Essentials

These are not optional — they are baseline requirements for all ATHENDAT products.

### Minimum Requirements (WCAG AA)

- **Color contrast**: 4.5:1 for normal text, 3:1 for large text and UI components
- **Focus indicators**: Visible on all interactive elements (never `outline: none` without replacement)
- **Keyboard navigation**: All interactive elements reachable and operable via keyboard
- **Labels**: Every form input has an associated `<label>` (or `aria-label`)
- **Alt text**: Every meaningful image has descriptive alt text
- **Heading hierarchy**: Logical h1 → h2 → h3 structure (no skipping levels)
- **Touch targets**: 44x44px minimum

### Testing Checklist

- [ ] Tab through the entire page — is the order logical?
- [ ] Can you complete the primary task using only keyboard?
- [ ] Run axe or Lighthouse accessibility audit (aim for 0 critical errors)
- [ ] Test with screen reader (VoiceOver / NVDA) on key flows
- [ ] Verify color contrast with browser DevTools or WebAIM checker
- [ ] Test at 200% zoom — does layout break?
