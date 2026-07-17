# LAYOUT_WORKSPACE

> TPS Pattern Specification — `docs/patterns/LAYOUT_WORKSPACE.md`
> Version: 0.1.0 | Status: Draft

## Overview

Layout Workspace defines the top-level spatial organization of a
professional trading platform. It establishes how panels are arranged,
resized, and persisted, enabling traders to create efficient, personalized
multi-panel environments.

## Default Layout (Desktop)

┌─────────────────────────────────────────────────────────────────┐
│ HEADER: Logo · Symbol Search · Account · Notifications │
├───────────┬─────────────────────────────┬───────────────────────┤
│ │ │ │
│ WATCHLIST │ CHART │ ORDER BOOK │
│ │ (Primary Panel) │ │
│ │ ├───────────────────────┤
│ │ │ ORDER ENTRY │
│ │ │ │
├───────────┴─────────────────────────────┴───────────────────────┤
│ BOTTOM TABS: Positions │ Orders │ Trade History │ Alerts │
└─────────────────────────────────────────────────────────────────┘

## Panel Zones

| Zone | Default Component | Resizable | Collapsible |
|---|---|---|---|
| Header | Global toolbar | No | No |
| Left Sidebar | Watchlist | Yes (width) | Yes |
| Main | Chart | Yes | No |
| Right Sidebar | Orderbook + Order Entry | Yes (width) | Yes |
| Bottom Panel | Positions / Orders tabs | Yes (height) | Yes |

## Layout Behaviors

### Panel Resizing
- Drag dividers between panels to resize
- Min/max constraints enforced per panel (e.g. sidebar min 200px)
- Double-click divider to reset panel to default size
- Resize cursors indicate direction

### Panel Collapsing
- Sidebar collapse button (◀ / ▶) toggles hidden state
- Collapsed panel shows icon-only rail or hides completely
- Bottom panel collapse slides down; toggle via chevron or keyboard

### Layout Persistence
- Current panel sizes and collapsed states saved to localStorage
- Layout auto-restored on next session
- "Reset Layout" option in workspace settings

### Multi-Window Support
- Any panel can be popped out to an independent browser window
- Popped-out windows remain synchronized via shared WebSocket
- Window state persisted per user session

## Responsive Breakpoints

| Breakpoint | Layout Behavior |
|---|---|
| `≥ 1440px` | Full multi-panel default layout |
| `1024–1439px` | Right sidebar auto-collapsed; toggle available |
| `768–1023px` | Single-column: chart full width; panels in tab switcher |
| `< 768px` | Mobile layout: bottom sheet panels; chart focus mode |

## Layout Presets

| Preset | Description |
|---|---|
| `default` | Chart + Watchlist + Orderbook + Order Entry |
| `chart_focus` | Full-screen chart, all sidebars collapsed |
| `trading` | Order Entry prominent; compact chart |
| `research` | Wide chart + Watchlist; no Order Entry |

Users can save and name custom presets.

## Related Components

- `CANDLESTICK` — primary chart panel content
- `WATCHLIST` — left sidebar content
- `ORDERBOOK` — right sidebar upper content
- `ORDER_ENTRY` — right sidebar lower content
- `POSITION_TABLE` — bottom panel tab content

## Accessibility

- Panel dividers have `role="separator"` with `aria-orientation`
- Dividers focusable and operable via arrow keys
- Collapsed panels announce state: `aria-expanded="false"`
- Layout preset switcher accessible via keyboard and screen reader
- Focus management: panel collapse does not lose keyboard focus

