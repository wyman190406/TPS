# Color System

## Overview

The TPS color system is designed for professional trading environments. It prioritizes information clarity, extended-session eye comfort, and accessibility over aesthetic preference.

---

## Design Constraints

- **Dark theme is the default.** Light theme is a supported variant, not the primary target.
- **Color is never the sole carrier of information.** All color-coded states must have a secondary signal.
- **Color-blind safety is required.** All critical color pairs must pass simulation for Deuteranopia, Protanopia, and Tritanopia.

---

## Color Roles

### Semantic Colors

| Role | Purpose | Dark Default | Light Default |
|------|---------|-------------|---------------|
| `color-positive` | Price up, profit, buy | `#26A69A` | `#00897B` |
| `color-negative` | Price down, loss, sell | `#EF5350` | `#E53935` |
| `color-neutral` | Unchanged, no direction | `#9E9E9E` | `#757575` |
| `color-warning` | Risk alerts, margin warnings | `#FFA726` | `#F57C00` |
| `color-critical` | Liquidation risk, system errors | `#FF1744` | `#D50000` |
| `color-info` | General information, AI suggestions | `#42A5F5` | `#1E88E5` |

### Surface Colors

| Role | Purpose | Dark Default | Light Default |
|------|---------|-------------|---------------|
| `surface-base` | App background | `#0F0F0F` | `#FAFAFA` |
| `surface-panel` | Panel / card background | `#1A1A1A` | `#FFFFFF` |
| `surface-elevated` | Dropdowns, modals | `#242424` | `#F5F5F5` |
| `surface-overlay` | Tooltips, popovers | `#2E2E2E` | `#EEEEEE` |
| `surface-interactive` | Hover state background | `#333333` | `#E0E0E0` |

### Border Colors

| Role | Purpose | Dark Default | Light Default |
|------|---------|-------------|---------------|
| `border-subtle` | Dividers, panel edges | `#2A2A2A` | `#E0E0E0` |
| `border-default` | Input outlines | `#3D3D3D` | `#BDBDBD` |
| `border-strong` | Focus rings, active states | `#616161` | `#757575` |

### Text Colors

| Role | Purpose | Dark Default | Light Default |
|------|---------|-------------|---------------|
| `text-primary` | Main content | `#E8E8E8` | `#212121` |
| `text-secondary` | Labels, metadata | `#9E9E9E` | `#616161` |
| `text-disabled` | Inactive elements | `#4A4A4A` | `#BDBDBD` |
| `text-inverse` | Text on colored backgrounds | `#0F0F0F` | `#FFFFFF` |

---

## Buy / Sell Convention

TPS defaults to the global convention:

| Direction | Color Token | Dark Value | Light Value |
|-----------|-------------|-----------|-------------|
| **Buy / Long / Up** | `color-positive` | `#26A69A` (teal-green) | `#00897B` |
| **Sell / Short / Down** | `color-negative` | `#EF5350` (red) | `#E53935` |

### Regional Override
Some markets use reversed conventions (e.g., red = up in certain Asian markets). TPS-compliant products must support a buy/sell color swap configuration without modifying the semantic token names.

---

## Data Visualization Colors

For charts and multi-series data:

viz-01: #42A5F5 (blue)
viz-02: #FFA726 (amber)
viz-03: #AB47BC (purple)
viz-04: #26A69A (teal)
viz-05: #EF5350 (red)
viz-06: #66BB6A (green)
viz-07: #EC407A (pink)
viz-08: #78909C (blue-grey)

All visualization colors must maintain a minimum contrast ratio of 3:1 against `surface-panel`.

---

## Staleness & Connection States

| State | Color Token | Behavior |
|-------|-------------|----------|
| Live | `color-positive` | Steady |
| Delayed | `color-warning` | Steady |
| Stale (>5s) | `color-warning` | Pulsing |
| Disconnected | `color-negative` | Pulsing |
| Unknown | `color-neutral` | Steady |

---

## Accessibility Requirements

- All text on surfaces must meet **WCAG 2.1 AA** (4.5:1 for normal text, 3:1 for large text)
- `color-positive` and `color-negative` must be distinguishable under Deuteranopia simulation
- Critical alerts must use `color-critical` combined with an icon, never color alone

---

## Prohibited Patterns

- ❌ Using raw hex values in component code — always reference tokens
- ❌ Creating new semantic colors without TPS specification review
- ❌ Using `color-positive` / `color-negative` for non-directional purposes
- ❌ Applying opacity to `color-critical` in a way that reduces it below AA contrast
