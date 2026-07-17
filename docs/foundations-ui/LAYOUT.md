# Layout Patterns

## Overview

This document defines the standard layout patterns for TPS-compliant trading interfaces. Layouts are compositional — they describe how panels, toolbars, and regions are organized, not the content within them.

---

## Application Shell

Every TPS-compliant trading application must include these shell regions:

┌─────────────────────────────────────────────┐
│ Global Header Bar │ fixed height: 48px (compact) / 56px (comfortable)
├──────┬──────────────────────────────┬────────┤
│ │ │ │
│ Side │ Main Content │ Side │
│ Nav │ Region │ Panel │
│ │ │ │
├──────┴──────────────────────────────┴────────┤
│ Status / Footer Bar │ fixed height: 24px (compact) / 32px (comfortable)
└─────────────────────────────────────────────┘

### Global Header Bar
- Application logo / product name
- Global instrument search
- Account selector
- Connection status indicator
- Notifications
- User menu

### Status / Footer Bar
- Market session status
- Data feed connection status
- Last data update timestamp
- System latency indicator

---

## Standard Layout Patterns

### LP-01: Classic Trading Terminal

Best for: Active traders, equities, crypto spot

┌──────────────────────┬───────────┬────────────┐
│ │ │ │
│ Chart │ Order │ Order │
│ │ Book │ Entry │
│ │ │ │
├──────────────────────┴───────────┤ │
│ Positions / Orders │ │
└──────────────────────────────────┴────────────┘

### LP-02: Research Terminal

Best for: Analysts, longer-timeframe traders

┌─────────────────────────┬──────────────────────┐
│ │ Watchlist │
│ Chart + TA ├──────────────────────┤
│ │ News Feed │
├─────────────────────────┴──────────────────────┤
│ Positions / Portfolio Summary │
└─────────────────────────────────────────────────┘

### LP-03: Options Trader Layout

Best for: Options flow, multi-leg strategies

┌──────────────┬─────────────────────────────────┐
│ Underlying │ Options Chain │
│ Chart ├─────────────────────────────────┤
│ │ Greeks Dashboard │
├──────────────┴─────────────────────────────────┤
│ Positions + P&L │
└────────────────────────────────────────────────┘

### LP-04: Portfolio Dashboard

Best for: Portfolio managers, account overview

┌──────────────────────────────────────────────┐
│ Performance Summary │
├──────────────┬───────────────────────────────┤
│ Allocation │ Open Positions Table │
│ Chart ├───────────────────────────────┤
│ │ Recent Activity │
└──────────────┴───────────────────────────────┘

---

## Panel Hierarchy Rules

1. **Chart panel** is the primary content region. It should receive the largest available space in layouts where it is present.
2. **Order entry** must always be fully visible without scrolling when the application is at its intended minimum resolution.
3. **Positions / order status** must not be hidden behind tabs in professional layouts.
4. **Navigation** is secondary to data. Nav elements must not compete visually with market data.

---

## Toolbar Placement

| Toolbar Type | Position | Notes |
|-------------|---------|-------|
| Chart toolbar | Top of chart panel | Symbol, timeframe, indicators |
| Drawing toolbar | Left of chart panel | TradingView convention |
| Order entry toolbar | Top of order entry panel | Order type selector |
| Table toolbar | Top of table | Filter, search, column config |

---

## Responsive Layout Transitions

| Width | Layout Behavior |
|-------|----------------|
| ≥ 1600px | Full multi-panel terminal |
| 1280–1599px | Reduced panels, order book may collapse |
| 960–1279px | Two-column layout, tabbed secondary panels |
| < 960px | Single panel with bottom navigation |

---

## Layout Persistence

TPS-compliant products must:
- Save user layout configurations per account
- Support named layout presets ("Scalping", "Research", "Overview")
- Restore previous layout on session start
- Provide a "Reset to Default" action
