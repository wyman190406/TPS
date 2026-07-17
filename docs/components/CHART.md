# Chart Component

## Overview

The Chart component is the primary data visualization surface in a trading interface. It displays price action, volume, and technical indicators over time.

---

## Chart Types

### Candlestick Chart (Primary)
The default and most widely used chart type for professional trading.

- Each candle represents OHLC data for a time period
- Bullish candle (close > open): `color-positive` fill
- Bearish candle (close < open): `color-negative` fill
- Doji (close = open): neutral `border-default` outline
- Wick extends to high and low

### Bar Chart (OHLC)
Alternative to candlestick for users preferring minimal visual weight.

### Line Chart
Connects closing prices. Used for performance comparison and reference lines.

### Area Chart
Line chart with filled area below. Used for portfolio value over time.

### Heikin-Ashi
Smoothed candlestick variant. Must be clearly labeled to avoid confusion with standard OHLC.

---

## Timeframes

Standard timeframe options:

| Category | Options |
|----------|---------|
| Intraday | 1s, 5s, 15s, 30s, 1m, 3m, 5m, 15m, 30m |
| Daily | 1h, 2h, 4h, 6h, 12h, 1D |
| Weekly+ | 1W, 1M, 3M, 1Y |

Active timeframe must be clearly indicated in the toolbar.

---

## Chart Toolbar

Required toolbar elements:

| Element | Description |
|---------|-------------|
| Symbol search | Current symbol display + click to change |
| Timeframe selector | Current timeframe + quick-select buttons |
| Chart type selector | Candlestick, bar, line, area |
| Indicators button | Open indicator panel |
| Drawing tools | Trendline, horizontal line, Fibonacci, text |
| Layout save | Save current indicator/drawing configuration |
| Fullscreen toggle | Expand chart to full panel |
| Settings | Chart visual settings |

---

## Price Axis

- Displayed on the right side by default (configurable to left)
- Auto-scales to fit visible price range
- Current price always visible with a label
- Label format matches instrument precision
- User-draggable to manually set scale
- Double-click to reset auto-scale

### Price Line
- Current last price: `text-primary` label with `surface-elevated` background
- Bid price: optional, `color-positive` dashed line
- Ask price: optional, `color-negative` dashed line
- Open price for session: `color-neutral` dashed line
- User's positions: `color-info` solid line with entry price label

---

## Time Axis

- Displayed at the bottom
- Auto-formats based on timeframe (HH:MM for intraday, MMM DD for daily+)
- Draggable to scroll history
- Pinch/scroll to zoom time range

---

## Crosshair

When cursor is on chart:
- Vertical line: current time
- Horizontal line: current price
- OHLCV data for the hovered candle in top-left corner
- Price label on price axis at crosshair position
- Time label on time axis at crosshair position

---

## Volume Panel

Displayed as a sub-panel below the main chart:
- Bar chart per period
- Bullish volume: `color-positive` at 60% opacity
- Bearish volume: `color-negative` at 60% opacity
- Volume MA overlay: `color-info` line
- Height: 20–25% of main chart height by default

---

## Technical Indicators

### Overlay Indicators (on main chart)
- Moving Averages (SMA, EMA, WMA)
- Bollinger Bands
- VWAP
- Ichimoku Cloud
- Parabolic SAR

### Panel Indicators (sub-panels below chart)
- RSI
- MACD
- Stochastic
- ATR
- OBV

Each indicator must:
- Display its name and parameters in the panel header
- Provide a settings icon to modify parameters
- Provide a close (×) button to remove
- Use `viz-0X` color tokens from the color system

---

## Drawing Tools

| Tool | Behavior |
|------|---------|
| Trendline | Click start + click end, drag to adjust |
| Horizontal line | Click to place at price level |
| Rectangle | Click-drag to draw region |
| Fibonacci Retracement | Click high + click low |
| Text annotation | Click to place, type to edit |

Drawing tools persist across timeframe changes on the same symbol.

---

## Performance Requirements

| Metric | Requirement |
|--------|------------|
| Initial render | < 500ms for 500 candles |
| Scroll / zoom | 60fps maintained |
| Live candle update | < 16ms render time |
| Indicator calculation | Non-blocking (Web Worker) |
| Historical data load | Seamless infinite scroll |

---

## Accessibility

- Chart must provide a data table view as an accessible alternative
- Current price and direction must be announced via `aria-live="polite"` at configurable intervals
- Drawing tools must be keyboard operable
- Chart region must have `role="img"` with descriptive `aria-label`

---

## Prohibited Patterns

- ❌ Blocking order entry interaction while chart is loading
- ❌ Using non-standard OHLC coloring without explicit user configuration
- ❌ Auto-scaling in a way that hides the current price off-screen
- ❌ Performing indicator calculations on the main thread
