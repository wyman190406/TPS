# SYMBOL_SEARCH

> TPS Pattern Specification — `docs/patterns/SYMBOL_SEARCH.md`
> Version: 0.1.0 | Status: Draft

## Overview

Symbol Search is the universal pattern for locating and selecting a
trading instrument. It appears as an overlay or inline component,
triggered from multiple surfaces including the chart toolbar, order
entry panel, and watchlist management.

## Flow Diagram

[Trigger: user activates search]
├─ Keyboard shortcut (e.g. /)
├─ Click on symbol chip in chart toolbar
├─ Click [+ Add Symbol] in Watchlist
└─ Click symbol field in Order Entry
│
▼
[Search Overlay / Inline Panel opens]
└─ Input auto-focused
│
▼
[User types query]
├─ Debounce: 150ms
├─ API: search by ticker + company name
└─ Results list updates in real time
│
▼
[Results List]
├─ Each row: Ticker · Company Name · Exchange · Type
├─ First result auto-highlighted
└─ Arrow keys navigate; Enter selects
│
▼
[Symbol Selected]
├─ Context action executed:
│ ├─ Chart: symbol updated, data reloaded
│ ├─ Order Entry: symbol field filled
│ └─ Watchlist: symbol added to active list
└─ Overlay/panel closes

## Search Result Row

┌─────────────────────────────────────────────────┐
│ AAPL Apple Inc. NASDAQ STK │
│ AAPL.HK Apple Inc. (HK ADR) HKEX STK │
│ AAPLW Apple Warrant OTC WRT │
└─────────────────────────────────────────────────┘

## Result Metadata

| Field | Description |
|---|---|
| `ticker` | Exchange ticker symbol |
| `name` | Full company / instrument name |
| `exchange` | Listing exchange |
| `type` | Instrument type: STK / ETF / FUT / OPT / FX / CRYPTO |
| `currency` | Trading currency |

## States

| State | Description |
|---|---|
| `idle` | Input empty, recent searches shown |
| `searching` | Debounce active or API request in flight |
| `results` | One or more matches returned |
| `no_results` | Query returned zero results |
| `error` | Search API unavailable |

## Recent Searches

- Up to 10 most recently selected symbols shown when input is empty
- Recent searches persisted to localStorage
- Individual entry removable via `✕`; "Clear all" option available

## Keyboard Navigation

| Key | Action |
|---|---|
| `↑` / `↓` | Navigate result rows |
| `Enter` | Select highlighted result |
| `Escape` | Close overlay, return focus to trigger |
| `/` | Open symbol search from anywhere (global shortcut) |

## Related Components

- `INPUT` — underlying search field
- `WATCHLIST_MANAGEMENT` — add symbol flow
- `ORDER_ENTRY` — symbol field integration
- `CANDLESTICK` — chart symbol change

## Accessibility

- Overlay has `role="dialog"` with `aria-label="Symbol Search"`
- Input has `role="combobox"` with `aria-expanded` and `aria-autocomplete="list"`
- Results list has `role="listbox"`; each row `role="option"`
- Screen reader announces result count on update: "5 results for AAPL"
- No-results state has `aria-live="polite"` announcement

