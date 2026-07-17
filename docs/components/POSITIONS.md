# Positions Component

## Overview

The Positions component displays the user's currently open trading positions. It is a critical risk management surface — traders rely on it to monitor exposure, P&L, and margin status in real time.

---

## Component Anatomy

┌──────┬──────────┬──────┬───────┬────────────┬────────────┬──────────────┬──────────┐
│ Sym │ Direction│ Qty │ Entry │ Mark Price │ Unreal P&L │ Margin Used │ Actions │
├──────┼──────────┼──────┼───────┼────────────┼────────────┼──────────────┼──────────┤
│ AAPL │ Long │ 100 │151.20 │ 153.40 │ +$220.00 │ $2,280.00 │ [Close] │
│ TSLA │ Short │ 50 │245.80 │ 248.20 │ -$120.00 │ $1,848.00 │ [Close] │
└──────┴──────────┴──────┴───────┴────────────┴────────────┴──────────────┴──────────┘

---

## Required Columns

| Column | Description | Format |
|--------|-------------|--------|
| Symbol | Instrument ticker | Uppercase, monospace |
| Direction | Long / Short | Label + color |
| Quantity | Position size | Instrument lot precision |
| Entry Price | Average entry price | Instrument price precision |
| Mark Price | Current reference price | Instrument price precision, live update |
| Unrealized P&L | Open profit/loss | Currency, `+`/`-` prefix, color-coded |
| Realized P&L | Closed profit from partial closes | Currency, `+`/`-` prefix |
| P&L % | Percentage return | 2dp, `+`/`-` prefix, color-coded |
| Margin Used | Collateral allocated to position | Currency |
| Liq. Price | Liquidation price (leveraged only) | Instrument price precision, color warning |
| Actions | Close, Modify | Button group |

All columns are visible by default. Users may hide non-critical columns in comfortable/spacious modes.

---

## Direction Display

| Direction | Color | Icon | Label |
|-----------|-------|------|-------|
| Long | `color-positive` | `arrow-up` | "Long" |
| Short | `color-negative` | `arrow-down` | "Short" |
| Flat | `color-neutral` | `dash` | "Flat" |

---

## P&L Display

- Positive P&L: `color-positive`, `+` prefix
- Negative P&L: `color-negative`, `−` prefix
- Zero: `color-neutral`, no prefix
- Currency symbol always displayed
- Real-time updates must use the flash animation pattern (see Motion spec)

---

## Liquidation Price Warning

When mark price is within a configurable threshold of liquidation price:

| Proximity | Treatment |
|-----------|-----------|
| > 20% away | Standard display |
| 10–20% away | `color-warning` on liq. price cell |
| < 10% away | `color-critical` + `margin-critical` icon + row highlight |
| < 5% away | `color-critical` + persistent banner above table |

---

## Summary Row

A pinned summary row at the top or bottom of the table:

Total Positions: 2 Unrealized P&L: +$100.00 Margin Used: $4,128.00

- Updates in real-time
- P&L color follows direction
- Clickable to expand full portfolio summary

---

## Actions

### Close Position Button
- Displays "Close" for each position row
- Clicking opens an inline confirmation:

Close 100 AAPL Long at market?
[Cancel] [Confirm Close]

  ```
- Confirm focus defaults to [Cancel]

### Modify Position
- Opens order modification panel for stop-loss / take-profit adjustment
- Does not open a new order form

### Close All Positions
- Available as a toolbar button above the table
- Requires modal confirmation listing all positions to be closed
- Confirm focus defaults to [Cancel]

---

## Empty State

When no positions are open:

```
┌────────────────────────────────┐
│ [positions icon] │
│ No open positions │
│ Your open trades will │
│ appear here. │
└────────────────────────────────┘

---

## Filtering & Sorting

- Sort by any column (click header)
- Filter by: Symbol, Direction, P&L positive/negative
- Search by symbol
- Filter state persists per session

---

## Accessibility

- Table uses `role="grid"` with proper `role="columnheader"` and `role="gridcell"`
- P&L values must include direction in accessible label ("Positive two hundred twenty dollars" not just "+$220")
- Liquidation warnings must use `role="alert"` when entering critical proximity
- Close button must include position context in accessible label ("Close AAPL Long position")

---

## Prohibited Patterns

- ❌ Auto-closing positions without explicit user confirmation
- ❌ Hiding unrealized P&L behind a toggle by default
- ❌ Displaying P&L without indicating whether it is realized or unrealized
- ❌ Removing a position row immediately on close submission (wait for server confirmation)
