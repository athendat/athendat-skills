# UX Strategy Reference

Design decisions rooted in cognitive psychology and behavioral science. These principles explain *why* certain patterns work and guide decision-making when no specific rule exists.

## Table of Contents
1. Cognitive Fluency
2. The Halo Effect (First 50ms)
3. Peak-End Rule
4. Reducing Cognitive Load
5. Flow Design Patterns
6. Error Handling Philosophy
7. Onboarding Strategy
8. Trust & Credibility Signals
9. B2B SaaS-Specific Patterns

---

## 1. Cognitive Fluency

**The principle:** Information that is easy to process feels more trustworthy, more beautiful, and more true. This is not a metaphor — it is a measurable cognitive bias.

**Application:**
- High-contrast text on clean backgrounds → feels more credible
- Consistent spacing and alignment → feels more professional
- Familiar patterns (navigation in expected places) → feels safer
- Readable font at comfortable size → feels more persuasive

**Anti-patterns to eliminate:**
- Walls of text without visual hierarchy
- Inconsistent alignment between similar elements
- Novel navigation patterns that require learning
- Low contrast or decorative fonts in body text
- Competing visual elements at the same hierarchy level

**Test:** Show someone the screen for 5 seconds, then take it away. Ask them what it's for and what they'd do first. If they can't answer both, cognitive fluency is broken.

---

## 2. The Halo Effect (First 50ms)

**The principle:** Users form a lasting quality judgment about the entire product within the first ~50 milliseconds of seeing the interface. This judgment persists even when later evidence contradicts it (they'll forgive bugs in a beautiful app, but distrust features in an ugly one).

**Where it matters most:**
- Hero section of landing pages
- Login/splash screen of apps
- Dashboard first-load state
- First screen of onboarding
- Email templates (the preview pane moment)

**How to win the 50ms test:**

1. **Visual hierarchy is instantly clear** — One dominant element, clear reading path
2. **Typography feels premium** — Tight heading spacing, generous body text
3. **Color is intentional** — One accent color with purpose, not a rainbow
4. **Space is generous** — Crowded layouts signal low quality
5. **Imagery is crisp** — No blurry, stretched, or generic stock photos

**For BALANC specifically:** The dashboard first-load is the 50ms moment. Show a clean, organized overview with clear data hierarchy. Never show an empty or loading state as the first impression — use optimistic rendering or skeleton screens.

---

## 3. Peak-End Rule

**The principle:** People judge an experience not by its average, but by its most intense moment (peak) and its final moment (end). A painful 20-minute process with a delightful ending is remembered more fondly than a smooth 5-minute process with an abrupt end.

**Designing peak moments:**
- Celebration after completing a complex form or first setup
- Satisfying animation when a report generates successfully
- Confetti or visual delight when hitting a milestone (first sale in BALANC, etc.)
- Smart summary showing what the user just accomplished

**Designing strong endings:**
- Order/process confirmation with clear next steps
- Success state with a summary of what happened
- Smooth transition to the next logical task
- Never end on an error or ambiguous state

**Peak-End mapping exercise:**
For each critical flow (onboarding, checkout, report generation), identify:
1. Where is the user's effort highest? (potential pain peak — mitigate this)
2. Where can we insert delight? (positive peak — amplify this)
3. What is the very last thing they see? (end — make it satisfying)

---

## 4. Reducing Cognitive Load

**The principle:** Working memory holds ~4 chunks of information. Every decision, every label to read, every option to evaluate uses a chunk. When you exceed capacity, the user feels overwhelmed and either makes mistakes or abandons.

### Strategies

**Progressive Disclosure:**
Show only what's needed now. Hide advanced options behind "More options" or secondary panels. BALANC's configuration screens especially benefit from this — show essentials first, details on demand.

**Smart Defaults:**
Pre-fill fields with the most common choice. For ATHENDAT clients: default currency, default tax rate, default date format based on locale. Every pre-filled field is one less decision.

**Chunking:**
Break long forms into logical steps (wizard pattern). Show progress. Each step should have a clear focus: "Step 2: Payment Details" not "Step 2: Continue".

**Recognition over Recall:**
Show options instead of asking users to type from memory. Autocomplete, recent items, favorites — anything that reduces the need to remember.

**Consistent Patterns:**
Once a user learns that "blue button = primary action", never break that pattern. Consistency across screens eliminates re-learning.

### Cognitive Load Audit

For any screen, count:
- Number of distinct actions available → aim for 1 primary + 2-3 secondary max
- Number of text blocks to read → can any be replaced with icons or shorter labels?
- Number of input fields visible → can any be deferred or auto-filled?
- Number of navigation options → can you reduce or group?

If the total exceeds 7 visible decision points, the screen likely needs simplification.

---

## 5. Flow Design Patterns

### Linear Flows (Setup, Checkout, Onboarding)

```
Step indicator (show progress)
    ↓
Clear step title (what we're doing now)
    ↓
Minimal inputs (only what's needed for THIS step)
    ↓
Primary action (clear label: "Continue to Payment", not just "Next")
    ↓
Back option (always available, preserves state)
```

### Hub-and-Spoke (Dashboards, Admin)

```
Central overview (hub) — summary of all areas
    ↓
Drill into specific area (spoke) — full detail
    ↓
Quick action from detail → returns to hub with updated state
```

For BALANC dashboards: The hub shows KPIs and alerts. Each widget is a spoke entrance. The user should always be able to return to hub with one action.

### Search-First (Large Catalogs, Inventories)

```
Prominent search bar (auto-suggest enabled)
    ↓
Filtered results (facets visible, active filters shown as chips)
    ↓
Quick-view detail (panel or modal, not full navigation)
    ↓
Action from detail (edit, add to cart, assign)
```

For HelarteApp and inventory management: Prioritize search over browsing when catalogs exceed ~50 items.

---

## 6. Error Handling Philosophy

Errors are not just technical events — they are emotional moments. Handle them with empathy.

### Error Prevention (Best)
- Validate inline as the user types (not only on submit)
- Disable impossible actions (grayed button with tooltip explaining why)
- Use constrained inputs (date picker instead of free text for dates)
- Auto-format inputs (phone numbers, currency amounts)

### Error Communication (When Prevention Fails)
- **Say what went wrong** — in human language, not error codes
- **Say why** — "This email is already registered" not "Validation error"
- **Say how to fix it** — "Try signing in instead" or "Check the format: DD/MM/YYYY"
- **Place the message near the problem** — inline with the field, not in a banner at the top
- **Use gentle visual treatment** — red accent + icon, not aggressive red background

### Error Recovery
- Never clear the form on error — preserve all user input
- For destructive actions: confirmation dialog with clear consequences
- Undo > Confirm: When possible, let the action happen with undo option rather than asking for confirmation before (less disruptive to flow)

### Offline Errors (Critical for ATHENDAT)
- Show sync status in a non-intrusive but persistent location
- Queue failed actions and retry automatically
- Show "Saved locally — will sync when online" messages
- Never show a generic "No connection" error — explain what still works

---

## 7. Onboarding Strategy

### First-Run Experience

The first 3 minutes determine whether a user adopts or abandons the product.

**Rules:**
1. Value within 60 seconds — show the user something useful immediately, even with minimal setup
2. Maximum 3 setup steps before first value moment
3. Pre-fill everything possible from signup data or reasonable defaults
4. Show, don't tell — interactive walkthroughs > video tutorials > text documentation
5. Allow skip — never trap users in onboarding

### Empty State Onboarding

When a section has no data yet, the empty state IS the onboarding for that feature:
- Short explanation of what goes here
- One clear CTA to add first item
- Optional: sample/demo data to show what it looks like populated

### Progressive Onboarding

Don't teach everything at once. Reveal tips contextually:
- First time opening reports → brief tooltip explaining key metrics
- First time creating an invoice → highlight shortcuts after completion
- After 5 logins → suggest advanced features they haven't tried

---

## 8. Trust & Credibility Signals

For B2B SaaS and fintech products, trust is the primary conversion factor.

### Visual Trust Signals
- Clean, professional typography (see UI Technical reference)
- Consistent, polished interface (no visual bugs)
- Clear data security indicators (lock icons, encryption badges)
- Professional error handling (see above)

### Informational Trust
- Transparent pricing (no hidden fees)
- Clear data policies (where is my data, who can see it)
- Audit trails visible to users (who changed what, when)
- Real-time sync indicators (the user knows their data is safe)

### Social Trust
- Client logos / testimonials on landing pages
- Usage metrics ("12,000 invoices processed this month")
- Active development signals (changelog, version numbers)

---

## 9. B2B SaaS-Specific Patterns

### Dashboard Design (BALANC)

**Priority hierarchy for B2B dashboards:**
1. Alerts/actions needed (what requires my attention NOW)
2. Key metrics trend (are things getting better or worse)
3. Recent activity (what happened since I last checked)
4. Quick actions (most common tasks)

**Anti-patterns:**
- Dashboard as feature showcase (showing everything the product can do)
- Vanity metrics without context (a number means nothing without trend or comparison)
- Static dashboards (same layout for all users regardless of role)

### Multi-Tenant Considerations
- Clear tenant/company indicator (always visible, never ambiguous)
- Role-based UI: hide options the user can't use (don't just disable them)
- Audit-friendly: show who did what, with timestamps

### Data-Heavy Interfaces
- Default to filtered/sorted views (not "show everything")
- Bulk actions for repetitive tasks
- Export capabilities for every data table
- Saved views / filters for power users
- Keyboard shortcuts for frequent operations (document and make discoverable)

### POS-Specific (SUNMI / Point of Sale)
- Minimal steps to complete a transaction
- Large touch targets, fat-finger proof
- High contrast for variable lighting (bright sun, dim store)
- Clear audio/visual feedback for payment success/failure
- Offline mode with prominent sync status
- No onboarding screens at POS — the device should be usable immediately
