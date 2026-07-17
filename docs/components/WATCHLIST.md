# Watchlist Component

## Overview

The Watchlist component provides a compact, scannable list of instruments with live price data. It is the primary instrument navigation surface for traders monitoring multiple assets.

---

## Component Anatomy

┌─────────────────────────────────────────────────┐
│ Watchlist [+ Add] [⋮ Menu] │
├──────────┬──────────┬────────┬──────────────────┤
│ Symbol │ Price │ Change │ Change % │
├──────────┼──────────┼────────┼──────────────────┤
│ AAPL │ 153.40 │ +2.20 │ +1.45% ████░░ │
│ TSLA │ 248.20 │ -3.60 │ -1.43% ░░██░░ │
│ NVDA │ 875.10 │ +12.40 │ +1.44% ███░░░ │
│ BTC/USD │ 42,150 │ -150 │ -0.35% ░█░░░░ │
└──────────┴──────────┴────────┴──────────────────┘

---

## Required Columns (Default)

| Column | Description | Update Frequency |
|--------|-------------|-----------------|
| Symbol | Ticker + optional name | Static |
| Price | Last traded price | Live |
| Change | Absolute change from previous close | Live |
| Change % | Percentage change from previous close | Live |

## Optional Columns

| Column | Description |
|--------|-------------|
| Bid | Best bid price |
| Ask | Best ask price |
| Volume | Current session volume |
| High | Session high |
| Low | Session low |
| Open | Session open price |
| Market Cap | (Equities) |
| Funding Rate | (Crypto perpetuals) |

---

## Price Update Behavior

- Price increases: flash `color-positive` for 200ms
- Price decreases: flash `color-negative` for 200ms
- Change column always reflects direction vs. previous close
- Positive change: `color-positive`, `+` prefix
- Negative change: `color-negative`, `−` prefix
- Unchanged: `color-neutral`

---

## Sparkline (Optional)

A mini 1D price chart per row:
- Width: 60–80px
- Height: matches row height minus 4px padding
- Bullish trend: `color-positive` line
- Bearish trend: `color-negative` line
- No axes, no labels — indication only

---

## Interaction

| Interaction | Action |
|-------------|--------|
| Click row | Load instrument in chart + order entry |
| Right-click row | Context menu (Add alert, Trade, Info, Remove) |
| Drag row | Reorder within watchlist |
| Double-click symbol | Edit symbol (replace with search) |

---

## Multiple Watchlists

- Users may create multiple named watchlists
- Watchlist tabs displayed at top of component
- Maximum recommended: 10 watchlists
- Active watchlist tab highlighted

---

## Add Instrument

Clicking [+ Add]:
- Opens inline search at bottom of list
- Typeahead search by ticker or name
- Press Enter or click result to add
- Escape to cancel

---

## Empty State

┌────────────────────────────┐
│ No instruments added │
│ [+ Add your first symbol] │
└────────────────────────────┘

---

## Performance

- Must handle 200+ instruments without scroll performance degradation
- Use virtualized rendering for lists > 50 rows
- Price updates must not cause list scroll position to reset

---

## Accessibility

- List uses `role="grid"` pattern
- Price updates announced via `aria-live="off"` by default (too frequent)
- A "summary update" at configurable interval available via `aria-live="polite"`
- Row context menu accessible via keyboard (`Shift+F10` or `Menu` key)

---

## Prohibited Patterns

- ❌ Reordering rows by price change during a session (disrupts muscle memory)
- ❌ Removing instruments from watchlist on accidental click
- ❌ Displaying price in wrong currency for the instrument
- ❌ Auto-scrolling watchlist to follow a selected instrument

