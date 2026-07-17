# Market Depth Component

## Overview

The Market Depth component (also known as Order Book or DOM — Depth of Market) displays the aggregated buy and sell orders at each price level for a given instrument. It is one of the most information-dense components in a trading interface.

---

## Component Variants

### Variant A: Stacked Order Book
Traditional two-panel layout with asks on top and bids below, separated by the spread.

┌─────────────────────────────┐
│ Price Size Total │ ← Ask side (sell orders)
│ 42,200.00 1.240 8.420 │ (color-negative tint)
│ 42,150.00 0.800 7.180 │
│ 42,100.00 2.340 6.380 │
│ 42,050.00 0.540 4.040 │
├──────── Spread: $50 ────────┤
│ 42,000.00 1.200 3.500 │ ← Bid side (buy orders)
│ 41,950.00 0.840 2.300 │ (color-positive tint)
│ 41,900.00 0.760 1.460 │
│ 41,850.00 0.700 0.700 │
└─────────────────────────────┘

### Variant B: Side-by-Side Order Book
Bids and asks displayed in parallel columns.

┌──────────────┬──────────────┐
│ BID │ ASK │
├──────────────┼──────────────┤
│ Size Price │ Price Size │
│ 1.200 42,000 │ 42,050 0.540 │
│ 0.840 41,950 │ 42,100 2.340 │
│ 0.760 41,900 │ 42,150 0.800 │
└──────────────┴──────────────┘

### Variant C: Ladder / DOM
Vertically centered on mid price, with order placement by clicking.

┌──────┬──────────┬──────┬───────┐
│ Bid │ Price │ Ask │ Vol │
├──────┼──────────┼──────┼───────┤
│ │ 42,200 │ 1.24 │ ████ │
│ │ 42,150 │ 0.80 │ ██ │
│ │ 42,100 │ 2.34 │ █████ │
│ │ 42,050 │ 0.54 │ █ │
├──────┼──────────┼──────┼───────┤
│ 1.20 │ 42,000 │ │ ████ │ ← Mid / Last price
├──────┼──────────┼──────┼───────┤
│ 0.84 │ 41,950 │ │ ███ │
│ 0.76 │ 41,900 │ │ ██ │
└──────┴──────────┴──────┴───────┘

---

## Data Requirements

Each row must display:
- **Price level** — In instrument precision, tabular alignment
- **Size / Quantity** — Total quantity at this price level
- **Cumulative total** — Running total from best price to this level
- **Depth bar** — Visual bar proportional to size (optional, recommended)

---

## Visual Encoding

### Depth Bars
- Bid bars: `color-positive` at 20–30% opacity, fill left-to-right
- Ask bars: `color-negative` at 20–30% opacity, fill right-to-left
- Bar width proportional to size relative to maximum visible size
- Bars must not obscure text

### Size Changes
- Size increase at a level: brief `color-positive` flash
- Size decrease at a level: brief `color-negative` flash
- New level appearance: fade in
- Level disappearance: fade out + row collapse

### Own Orders
User's own resting orders at a price level must be:
- Visually distinguished (different background, border, or icon)
- Labeled with order quantity separate from total market quantity

---

## Spread Display

Between the best bid and best ask:
- Display spread in price terms: `$50.00`
- Display spread in percentage: `0.12%`
- Display spread in ticks: `10 ticks`
- Minimum display: price + percentage

---

## Interaction

### Click to Trade (Ladder variant)
- Click on bid side: place buy limit order at that price
- Click on ask side: place sell limit order at that price
- Click must pre-fill order entry panel, not auto-submit
- If "one-click trading" is enabled (explicit user setting), submit directly with confirmation toast

### Hover Behavior
- Hovering a row highlights it and shows row total
- Tooltip displays: level price, size, cumulative volume, cumulative % of visible book

### Scroll / Zoom
- Scroll to adjust visible price range
- Center button to re-center on mid price
- Configurable number of levels displayed (5, 10, 20, 50)

---

## Update Performance

- Order book updates typically arrive at 10–100ms intervals
- DOM must batch updates and render at 60fps maximum
- Rapid size changes must not cause visual flickering
- Row positions must not shift during updates (stable layout)

---

## Accessibility

- Order book must be navigable via keyboard (arrow keys through rows)
- Each row must announce price, bid/ask side, and size to screen readers
- Live region updates must be `aria-live="off"` by default (too frequent for announcement)
- A summary widget showing best bid, best ask, and spread must use `aria-live="polite"`

---

## Prohibited Patterns

- ❌ Auto-submitting orders on click without explicit one-click trading setting
- ❌ Displaying size in base currency when quote currency is standard for the instrument
- ❌ Removing rows from view while user is hovering or has keyboard focus on them
- ❌ Showing cumulative depth from the wrong direction
