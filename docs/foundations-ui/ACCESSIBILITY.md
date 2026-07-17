# Accessibility

## Overview

TPS accessibility standards ensure that professional trading interfaces are usable by the broadest possible range of users, including those with visual, motor, cognitive, and auditory differences.

Accessibility in TPS is a **specification requirement**, not a post-hoc consideration.

---

## Baseline Standard

TPS-compliant products must meet **WCAG 2.1 Level AA** as a minimum.

Trading-specific extensions defined in this document apply on top of WCAG 2.1 AA where the standard does not adequately address the domain.

---

## Visual Accessibility

### Contrast Requirements

| Context | Minimum Ratio | Notes |
|---------|--------------|-------|
| Normal text (< 18px) | 4.5:1 | WCAG AA |
| Large text (≥ 18px regular, ≥ 14px bold) | 3:1 | WCAG AA |
| UI components and states | 3:1 | WCAG AA |
| Price up/down colors | 3:1 against background | Plus secondary signal required |
| Data visualization | 3:1 between adjacent series | |

### Color Vision Deficiency

All critical information encoded in color must have a secondary signal:

| Information | Color Signal | Required Secondary Signal |
|-------------|-------------|--------------------------|
| Price direction | Green / Red | Arrow icon + `+`/`-` prefix |
| Order status | Color badge | Icon + text label |
| P&L positive/negative | Green / Red | `+`/`-` sign + icon |
| Alert level | Color | Icon + text severity label |
| Connection status | Color dot | Icon shape change |

### Text Sizing
- Users must be able to increase text size to 200% without loss of content or functionality
- Compact mode may require a density override when large text is active

---

## Keyboard Accessibility

### Global Requirements
- All interactive elements must be reachable and operable via keyboard
- Focus order must follow logical reading and interaction sequence
- Focus must never be trapped (except intentional modal dialogs)
- Focus indicator must be clearly visible (minimum 2px outline, 3:1 contrast)

### Trading-Specific Keyboard Requirements

| Action | Required Keyboard Support |
|--------|--------------------------|
| Place order | Full keyboard form completion + submit via Enter |
| Cancel order | Keyboard accessible cancel action per order row |
| Cancel all orders | Keyboard shortcut (configurable) |
| Navigate order book | Arrow key navigation through price levels |
| Switch panels | Tab / keyboard shortcut navigation |
| Open/close positions table | Keyboard accessible |

### Keyboard Shortcuts
- All keyboard shortcuts must be discoverable via a shortcut reference panel
- Shortcuts must not conflict with browser or OS reserved shortcuts by default
- Users must be able to customize shortcut bindings
- Shortcuts must be documented in the product help system

---

## Screen Reader Accessibility

### ARIA Requirements
- All custom components must implement appropriate ARIA roles
- Dynamic data updates (price changes, order fills) must use `aria-live` regions
- Alert severity must be communicated via `role="alert"` or `aria-live="assertive"`

### Live Region Policy

| Data Type | `aria-live` Setting | Notes |
|-----------|-------------------|-------|
| Price updates | `off` (default) | Constant announcement is disruptive |
| Order fill notification | `assertive` | Immediate announcement required |
| Order rejection | `assertive` | Immediate announcement required |
| Margin warning | `assertive` | Immediate announcement required |
| System status change | `polite` | Announce when user is idle |

### Screen Reader Labels
- Price columns must announce currency and instrument context, not just the number
- Percentage changes must include the `%` symbol in the accessible label
- Directional icons must have descriptive labels ("Price up 2.3%", not "arrow up")

---

## Motor Accessibility

### Touch Targets
| Density Mode | Minimum Touch Target |
|-------------|---------------------|
| Compact | 32×32px |
| Comfortable | 44×44px |
| Spacious | 44×44px |

### Pointer Precision
- Order entry fields must be operable with low-precision pointing (no pixel-precise targets for critical actions)
- Drag handles (panel resize, price ladder) must have a minimum grab area of 8px

### Timeout Extensions
- Session timeouts must provide a warning with at least 60 seconds to extend
- Time-limited actions must provide a mechanism to extend or disable the limit

---

## Cognitive Accessibility

### Error Messages
- Error messages must identify the specific field or action that caused the error
- Error messages must provide actionable guidance, not just state the error
- Order rejection messages must include the rejection reason code and plain-language explanation

### Confirmation Patterns
- Destructive actions (cancel all orders, close all positions) must require explicit confirmation
- Confirmation dialogs must clearly state the consequence of the action
- Default focus in confirmation dialogs must be on the cancel/safe action, not the destructive action

### Consistency
- Consistent component behavior across the application reduces cognitive load
- Deviations from established TPS patterns require documented justification

---

## Accessibility Testing Requirements

TPS-compliant products must include:

1. **Automated testing** — Integrated axe-core or equivalent in CI pipeline
2. **Manual keyboard testing** — Full user flow completable via keyboard only
3. **Screen reader testing** — Tested with NVDA + Chrome and VoiceOver + Safari
4. **Color contrast audit** — All text and UI component contrast verified
5. **Color blindness simulation** — All critical color encodings verified under Deuteranopia, Protanopia, Tritanopia

---

## Accessibility Anti-Patterns

- ❌ Using `outline: none` without providing an alternative focus indicator
- ❌ `aria-live="assertive"` on continuously updating price feeds
- ❌ Focus-trapping outside intentional modal dialogs
- ❌ Relying on hover to reveal critical information
- ❌ Using placeholder text as the only label for form fields
- ❌ Auto-refreshing content that cannot be paused or controlled by the user
