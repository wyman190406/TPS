# Grid System

## Overview

The TPS grid system supports the complex, multi-panel layouts characteristic of professional trading platforms. It is designed around panel-based composition, not page-based column grids.

---

## Layout Model

TPS uses a **panel composition model**, not a traditional 12-column grid.

Trading platforms are built from independently resizable, dockable panels — not fixed-column page layouts. The grid system must support:

- Horizontal and vertical panel splitting
- Independently scrollable panel regions
- Resizable panel dividers
- Panel minimize, maximize, and close
- Layout persistence per user

---

## Base Grid

When a column grid is needed (dashboards, reports, settings pages), TPS uses:

| Property | Value |
|----------|-------|
| Columns | 12 |
| Gutter | 8px (compact), 16px (comfortable) |
| Margin | 0px (panels are edge-to-edge by default) |
| Breakpoints | See below |

### Breakpoints

| Name | Min Width | Typical Context |
|------|-----------|----------------|
| `xs` | 0px | Mobile (limited TPS support) |
| `sm` | 600px | Single-panel mobile/tablet |
| `md` | 960px | Tablet / simplified terminal |
| `lg` | 1280px | Standard desktop |
| `xl` | 1600px | Wide desktop |
| `2xl` | 1920px | Full trading terminal |
| `3xl` | 2560px | Ultra-wide / multi-monitor |

---

## Panel Layout System

### Panel Units
Panels are defined by fractional units of available space:

1fr — one equal fraction
2fr — twice the space of 1fr
fixed: 320px — fixed-width panel (e.g., order entry)

### Standard Layout Templates

#### Classic Terminal (3-column)

[Chart 3fr] [Order Book 1fr] [Order Entry fixed:320px]

#### Research Layout (2-column)

[Chart + News 2fr] [Watchlist + Positions 1fr]

#### Full-Screen Chart

[Chart 1fr]
[Positions Bar fixed:180px]

---

## Panel Behavior Specifications

### Resizing
- Panel dividers must be draggable with a minimum handle size of 4px width / 100% height
- Minimum panel width: 200px
- Minimum panel height: 120px
- Resize must not cause layout reflow outside the affected panels

### Scrolling
- Each panel manages its own scroll context independently
- Panels must not propagate scroll events to parent containers (scroll trapping)
- Horizontal scroll in data tables must not trigger parent panel scroll

### Responsive Behavior
| Breakpoint | Behavior |
|-----------|---------|
| `lg` and above | Full multi-panel layout |
| `md` | Tabbed panel switching (panels stack behind tabs) |
| `sm` and below | Single active panel, swipe to switch |

---

## Z-Index Scale

| Layer | Token | Value | Usage |
|-------|-------|-------|-------|
| Base | `z-base` | 0 | Normal document flow |
| Raised | `z-raised` | 10 | Sticky headers, frozen columns |
| Dropdown | `z-dropdown` | 100 | Select menus, autocomplete |
| Overlay | `z-overlay` | 200 | Side panels, drawers |
| Modal | `z-modal` | 300 | Dialog boxes |
| Toast | `z-toast` | 400 | Notification toasts |
| Tooltip | `z-tooltip` | 500 | Hover tooltips |
| Critical | `z-critical` | 999 | Emergency alerts, session expiry |

