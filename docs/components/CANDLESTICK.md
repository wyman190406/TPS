# CANDLESTICK

> TPS Component Specification — `docs/components/CANDLESTICK.md`
> Version: 0.1.0 | Status: Draft

## Overview

Candlestick is the primary price chart component for trading platforms.
It renders OHLC (Open, High, Low, Close) data as candlestick bars with
optional overlays, volume bars, and technical indicators.

## Anatomy

┌──────────────────────────────────────────────────┐
│ AAPL · 1D [1m][5m][15m][1H][1D][1W] │
│ │
│ 185 ──┬──────────────────────────────── ██ │
│ │ ██ ████ │
│ 182 ──┤ ██ ██ ████ ████ │
│ │ ████ ████ ██ ████ ████ │
│ 179 ──┤ ██████ ████ ████ █████ ██ │
│ │ ████ ████ ████ ████ │
│ 176 ──┴────────────────────────────────────── │
│ Feb Mar Apr May │
│ ▁▂▃▄▄▅▅▆▆▅▄▅▆▇▇▆▅▄▃▄▅▆▇▇▆▅ ← Volume Bars │
└──────────────────────────────────────────────────┘

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `symbol` | `string` | — | Instrument symbol |
| `data` | `OHLCVBar[]` | `[]` | OHLCV data array |
| `interval` | `Interval` | `'1D'` | Active time interval |
| `intervals` | `Interval[]` | See below | Available interval options |
| `showVolume` | `boolean` | `true` | Render volume bars below chart |
| `showGrid` | `boolean` | `true` | Show background grid lines |
| `showCrosshair` | `boolean` | `true` | Show crosshair on hover |
| `overlays` | `Overlay[]` | `[]` | Technical indicator overlays (MA, BB, etc.) |
| `theme` | `'dark' \| 'light'` | `'dark'` | Color theme |
| `height` | `number` | `400` | Chart height in pixels |

## Data Types

```typescript
interface OHLCVBar {
  time: number;      // Unix timestamp (seconds)
  open: number;
  high: number;
  low: number;
  close: number;
  volume: number;
}

type Interval = '1m' | '5m' | '15m' | '30m' | '1H' | '4H' | '1D' | '1W' | '1M';

interface Overlay {
  type: 'MA' | 'EMA' | 'BB' | 'VWAP';
  period?: number;
  color?: string;
}

**States**
 State	Description
 loading	Fetching historical data
 streaming	Receiving real-time bar updates
 error	Data fetch failed
 empty	No data for selected interval
**Behavior**
 ·Bullish candle (close ≥ open): filled with color.price.up
 ·Bearish candle (close < open): filled with color.price.down
 ·Wick extends from high to low
 ·Mouse hover shows crosshair with OHLCV tooltip
 ·Scroll to zoom; drag to pan
 ·Last bar auto-scrolls to right edge on new data
 ·Volume bars inherit candle color at reduced opacity
**Color Tokens**
 Token	Usage
 color.price.up	Bullish candle body and wick
 color.price.down	Bearish candle body and wick
 color.chart.volume	Volume bar fill
 color.chart.grid	Background grid lines
 color.chart.crosshair	Crosshair lines
 color.surface.panel	Chart background
**Accessibility**
 ·Chart region has role="img" and aria-label describing symbol and interval
 ·Keyboard arrow keys shift visible range left/right
 ·Screen reader announces last close price on symbol change

---

## 2️⃣ `docs/components/ORDERBOOK.md`

```markdown
# ORDERBOOK

> TPS Component Specification — `docs/components/ORDERBOOK.md`
> Version: 0.1.0 | Status: Draft

## Overview

Orderbook displays the Level 2 bid/ask order book for a trading instrument.
It shows aggregated price levels, sizes, cumulative depth, and updates in
real time. Traders use it to assess market liquidity and identify support
or resistance zones.

## Anatomy
┌─────────────────────────────────────┐
│ Order Book [0.01 ▾] │
├──────────┬────────────┬─────────────┤
│ Count │ Size │ Bid │
│ 9 │ 2,800 │ 182.45 ███ │
│ 6 │ 1,500 │ 182.44 ██ │
│ 4 │ 900 │ 182.43 █ │
├──────────┴────────────┴─────────────┤
│ Spread 0.02 (0.01%) │
├──────────┬────────────┬─────────────┤
│ Ask │ Size │ Count │
│ 182.47 │ 3,200 │ 11 ███ │
│ 182.48 │ 5,100 │ 18 ██████ │
│ 182.49 │ 1,400 │ 5 █ │
└──────────┴────────────┴─────────────┘

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `bids` | `BookLevel[]` | `[]` | Bid levels (descending price) |
| `asks` | `BookLevel[]` | `[]` | Ask levels (ascending price) |
| `grouping` | `number` | `0.01` | Price grouping increment |
| `groupingOptions` | `number[]` | `[0.01, 0.05, 0.1, 0.5, 1]` | Available grouping options |
| `maxRows` | `number` | `15` | Max visible rows per side |
| `showCount` | `boolean` | `true` | Show order count column |
| `showDepthBar` | `boolean` | `true` | Show cumulative depth bar |
| `onPriceClick` | `(price: number) => void` | — | Callback when a price row is clicked |

## Data Types

```typescript
interface BookLevel {
  price: number;
  size: number;
  count?: number;
  cumulative?: number;
}

**States**
 State	Description
 loading	Connecting to order book feed
 active	Receiving live updates
 stale	Feed timeout, data may be outdated
 empty	No order book data available
**Behavior**
 ·Bids sorted descending by price; asks sorted ascending
 ·Spread row always centered between best bid and best ask
 ·Depth bars proportional to cumulative size relative to visible window max
 ·Row size changes flash: increase → color.price.up, decrease → color.price.down
 ·Clicking a price row fires onPriceClick to pre-fill order entry
 ·Grouping selector aggregates levels within each price bucket
**Color Tokens**
 Token	Usage
 color.price.bid	Bid price text and depth bar
 color.price.ask	Ask price text and depth bar
 color.price.up	Size increase flash
 color.price.down	Size decrease flash
 color.surface.panel	Component background
 color.text.secondary	Count and size text
 color.border.divider	Spread row separator
**Accessibility**
 ·Component has aria-label="Order Book"
 ·Bid section: aria-label="Bids"; Ask section: aria-label="Asks"
 ·Spread row has role="separator" and aria-label with spread value
 ·Live updates announced via aria-live="polite" at reduced frequency

---

## 3️⃣ `docs/components/POSITION_TABLE.md`

```markdown
# POSITION_TABLE

> TPS Component Specification — `docs/components/POSITION_TABLE.md`
> Version: 0.1.0 | Status: Draft

## Overview

Position Table displays the user's open positions across all instruments.
Each row shows the instrument, direction, quantity, average cost, current
price, unrealized P&L, and quick-action controls.

## Anatomy

┌──────────────────────────────────────────────────────────────────────┐
│ Positions (4) [Collapse All] │
├──────────┬────────┬────────┬──────────┬──────────┬────────┬─────────┤
│ Symbol │ Side │ Qty │ Avg Cost │ Last │ P&L │ Action │
├──────────┼────────┼────────┼──────────┼──────────┼────────┼─────────┤
│ AAPL │ Long │ 100 │ 178.20 │ 182.45 │+$425 ▲ │[Close] │
│ TSLA │ Long │ 50 │ 245.00 │ 238.10 │ -$345 ▼│[Close] │
│ NVDA │ Short │ 20 │ 485.00 │ 490.30 │ -$106 ▼│[Close] │
│ MSFT │ Long │ 75 │ 415.80 │ 419.50 │+$278 ▲ │[Close] │
├──────────┴────────┴────────┴──────────┴──────────┼────────┴─────────┤
│ Total: │+$252 │
└───────────────────────────────────────────────────┴──────────────────┘

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `positions` | `Position[]` | `[]` | Array of open position objects |
| `showTotal` | `boolean` | `true` | Show total unrealized P&L footer |
| `onClose` | `(positionId: string) => void` | — | Callback for close position action |
| `onRowClick` | `(position: Position) => void` | — | Callback when a row is clicked |
| `currency` | `string` | `'USD'` | Display currency for P&L |
| `loading` | `boolean` | `false` | Show skeleton loading state |

## Data Types

```typescript
interface Position {
  id: string;
  symbol: string;
  side: 'Long' | 'Short';
  quantity: number;
  averageCost: number;
  lastPrice: number;
  unrealizedPnl: number;
  unrealizedPnlPct: number;
  currency: string;
}

**States**
 State	Description
 loading	Fetching position data
 populated	One or more positions displayed
 empty	No open positions
 error	Failed to load positions
**Behavior**
 ·P&L positive: color.price.up with upward arrow indicator
 ·P&L negative: color.price.down with downward arrow indicator
 ·Last price updates in real time; cell flashes on change
 ·Close button triggers confirmation dialog before executing
 ·Row click emits onRowClick for detail panel or chart focus
 ·Total row recalculates on every position update
**Color Tokens**
 Token	Usage
 color.price.up	Positive P&L text
 color.price.down	Negative P&L text
 color.surface.panel	Table background
 color.surface.row.hover	Row hover highlight
 color.text.primary	Symbol, quantity, price
 color.text.secondary	Column headers
 color.border.divider	Row separators
**Accessibility**
 ·Table has role="table" with aria-label="Open Positions"
 ·Each row has aria-label summarizing symbol, side, and P&L
 ·Close button has aria-label="Close [symbol] position"
 ·P&L values include visually hidden text for screen readers ("profit" / "loss")

---

## 4️⃣ `docs/components/BUTTON.md`

```markdown
# BUTTON

> TPS Component Specification — `docs/components/BUTTON.md`
> Version: 0.1.0 | Status: Draft

## Overview

Button is the foundational interactive control for triggering actions.
It supports multiple variants, sizes, and states, and is used across
all surfaces — toolbars, forms, dialogs, and data tables.

## Anatomy

┌──────────────────────────┐
│ [Icon] Label │ ← Primary Button
└──────────────────────────┘

┌──────────────────────────┐
│ [Icon] Label │ ← Secondary (Outlined)
└──────────────────────────┘

[Icon] Label ← Ghost / Text Button

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `label` | `string` | — | Button text |
| `variant` | `'primary' \| 'secondary' \| 'ghost' \| 'danger'` | `'primary'` | Visual style variant |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | Button size |
| `icon` | `ReactNode` | — | Optional leading icon |
| `iconPosition` | `'left' \| 'right'` | `'left'` | Icon placement |
| `disabled` | `boolean` | `false` | Disable interaction |
| `loading` | `boolean` | `false` | Show loading spinner, disable click |
| `fullWidth` | `boolean` | `false` | Stretch to container width |
| `onClick` | `() => void` | — | Click handler |

## Variants

| Variant | Usage |
|---|---|
| `primary` | Main CTA — submit order, confirm action |
| `secondary` | Supporting action — cancel, reset |
| `ghost` | Low-emphasis — toolbar controls, filters |
| `danger` | Destructive action — close position, cancel order |

## Sizes

| Size | Height | Font Size | Padding (H) |
|---|---|---|---|
| `sm` | 28px | 12px | 10px |
| `md` | 36px | 14px | 14px |
| `lg` | 44px | 16px | 18px |

## States

| State | Description |
|---|---|
| `default` | Ready for interaction |
| `hover` | Cursor over button |
| `active` | Button pressed |
| `focus` | Keyboard focus visible |
| `loading` | Async action in progress |
| `disabled` | Not interactive |

## Behavior

- Loading state replaces label with spinner; width is preserved
- Disabled state prevents all pointer and keyboard events
- Focus ring appears on keyboard navigation only (not on mouse click)
- Danger variant requires single click; no additional confirmation built in

## Color Tokens

| Token | Usage |
|---|---|
| `color.action.primary` | Primary button background |
| `color.action.primaryHover` | Primary hover background |
| `color.action.danger` | Danger button background |
| `color.action.ghost` | Ghost button text |
| `color.text.onAction` | Button label on colored background |
| `color.border.button` | Secondary button border |

## Accessibility

- `role="button"` (native `<button>` element preferred)
- `aria-disabled="true"` when disabled
- `aria-busy="true"` when loading
- Minimum touch target size: 44×44px
- Focus visible outline: 2px `color.focus.ring` offset 2px


