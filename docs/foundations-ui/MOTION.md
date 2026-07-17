# Motion & Animation

## Overview

Motion in trading interfaces serves a fundamentally different purpose than in consumer products. It communicates data change, system state, and operational feedback — not delight or brand personality.

**The default posture toward motion in TPS is restraint.**

---

## Core Principle

> Every animation must justify its existence by reducing cognitive load or communicating state. Animations that exist for aesthetics add latency and distraction.

---

## Motion Categories

### 1. Data Update Motion
Communicates that a value has changed.

| Change Type | Animation | Duration |
|-------------|-----------|----------|
| Price increase | Brief background flash → `color-positive` | 200ms |
| Price decrease | Brief background flash → `color-negative` | 200ms |
| Value neutral update | No animation | — |
| New row inserted | Fade in from 0 opacity | 150ms |
| Row removed | Fade out, collapse height | 150ms |

**Rule:** Flash animations for price changes must not persist beyond 500ms. Persistent color changes indicate staleness, not movement.

### 2. State Transition Motion
Communicates UI state changes.

| Transition | Animation | Duration |
|-----------|-----------|----------|
| Panel open | Slide in from edge | 200ms |
| Panel close | Slide out to edge | 150ms |
| Dropdown open | Fade in + slight scale from 0.97 | 150ms |
| Dropdown close | Fade out | 100ms |
| Tab switch | Cross-fade content | 150ms |
| Toast appear | Slide in from bottom-right | 200ms |
| Toast dismiss | Fade out + slide | 150ms |

### 3. Feedback Motion
Confirms user actions.

| Action | Feedback | Duration |
|--------|---------|----------|
| Order submitted | Submit button pulse | 300ms |
| Order filled | Row highlight flash | 500ms |
| Order rejected | Shake animation on form | 400ms |
| Error state | Shake + `color-critical` highlight | 400ms |

### 4. Loading States
Communicates system processing.

| State | Animation |
|-------|-----------|
| Data loading | Skeleton shimmer (left to right) |
| Order processing | Spinner in submit button |
| Chart loading | Skeleton bar chart |
| Connection retry | Progress indicator in status bar |

---

## Duration Scale

| Token | Value | Usage |
|-------|-------|-------|
| `duration-instant` | 0ms | Disabled motion mode |
| `duration-fast` | 100ms | Micro-interactions, hover |
| `duration-normal` | 150–200ms | Standard transitions |
| `duration-moderate` | 300ms | Panel transitions, feedback |
| `duration-slow` | 500ms | Complex state changes |

**Never exceed 500ms** for any animation in a trading interface.

---

## Easing Functions

| Token | Value | Usage |
|-------|-------|-------|
| `ease-standard` | `cubic-bezier(0.2, 0, 0, 1)` | Most transitions |
| `ease-decelerate` | `cubic-bezier(0, 0, 0, 1)` | Elements entering screen |
| `ease-accelerate` | `cubic-bezier(0.3, 0, 1, 1)` | Elements leaving screen |
| `ease-linear` | `linear` | Progress bars, timers |

---

## Reduced Motion

TPS-compliant products must respect `prefers-reduced-motion`.

When reduced motion is enabled:
- All decorative animations are disabled
- Data update flashes are replaced with instant color changes
- State transitions use instant cross-fades (opacity only, no transform)
- Loading states use static indicators instead of shimmer

```css
@media (prefers-reduced-motion: reduce) {
  /* All animations fall back to opacity-only or instant */
}

Prohibited Motion Patterns
❌ Parallax effects anywhere in the application
❌ Auto-playing animations not triggered by data or user action
❌ Bounce or elastic easing on data components
❌ Animations exceeding 500ms in trading-critical UI areas
❌ Simultaneous animations on more than 3 elements in the same viewport region
❌ Motion that shifts layout (causes reflow)

---

## 7️⃣ `docs/foundations-ui/ICONOGRAPHY.md`

```markdown
# Iconography

## Overview

Icons in TPS serve as functional signals — they encode state, action, and category information at a glance. Trading interfaces rely heavily on icons due to space constraints in dense layouts.

---

## Icon Requirements

All TPS icons must:

1. **Be recognizable at 12px** — The minimum size used in compact table views
2. **Have filled and outlined variants** — Filled = active/selected, Outlined = inactive/default
3. **Maintain consistent optical weight** — Stroke width 1.5px at 16px, scaled proportionally
4. **Not rely on color alone** — Shape must convey meaning independent of color

---

## Size Scale

| Token | Size | Usage |
|-------|------|-------|
| `icon-xs` | 12px | Inline table indicators, micro labels |
| `icon-sm` | 16px | Default UI icon size |
| `icon-md` | 20px | Navigation, toolbar |
| `icon-lg` | 24px | Header, prominent actions |
| `icon-xl` | 32px | Empty states, onboarding |

---

## Standard Icon Set

### Navigation & Layout
| Name | Usage |
|------|-------|
| `chart` | Chart panel |
| `orderbook` | Order book / depth |
| `positions` | Positions panel |
| `portfolio` | Portfolio view |
| `watchlist` | Watchlist |
| `news` | News feed |
| `settings` | Settings |
| `layout` | Layout manager |

### Order Actions
| Name | Usage |
|------|-------|
| `buy` | Buy / long action |
| `sell` | Sell / short action |
| `cancel-order` | Cancel a single order |
| `cancel-all` | Cancel all orders |
| `close-position` | Close position |
| `modify-order` | Edit order parameters |

### Order Status
| Name | Usage |
|------|-------|
| `order-pending` | Order staged, not submitted |
| `order-open` | Order submitted, awaiting fill |
| `order-partial` | Partially filled |
| `order-filled` | Fully filled |
| `order-cancelled` | Cancelled |
| `order-rejected` | Rejected by exchange |
| `order-expired` | Expired (time-in-force elapsed) |

### Market & Data
| Name | Usage |
|------|-------|
| `price-up` | Price increase indicator |
| `price-down` | Price decrease indicator |
| `price-unchanged` | No change |
| `volume` | Volume indicator |
| `alert` | Price alert |
| `alert-active` | Alert triggered |
| `connection-live` | Data feed connected |
| `connection-delayed` | Delayed data |
| `connection-lost` | Disconnected |

### Risk & Account
| Name | Usage |
|------|-------|
| `margin-safe` | Margin within limits |
| `margin-warning` | Margin approaching limit |
| `margin-critical` | Margin at critical level |
| `pnl-positive` | Positive P&L |
| `pnl-negative` | Negative P&L |
| `locked` | Feature locked / permission required |

### AI & Signals
| Name | Usage |
|------|-------|
| `ai-suggestion` | AI-generated content indicator |
| `signal` | Trading signal |
| `confidence-high` | High confidence indicator |
| `confidence-low` | Low confidence indicator |

---

## Icon + Label Pairing Rules

- Icons used without labels must have an accessible `aria-label` or `title`
- In compact layouts, icons may appear without labels if their meaning is established through consistent placement
- Critical action icons (cancel all orders, close position) must always appear with a label

---

## Prohibited Icon Patterns

- ❌ Using generic icons (hamburger menu, generic gear) for trading-specific functions
- ❌ Mixing icon styles (filled, outlined, rounded) within the same component
- ❌ Scaling icons below 12px
- ❌ Using icon opacity below 40% for any interactive element
- ❌ Rotating icons as a state indicator (e.g., spinning gear for loading — use a dedicated spinner)
