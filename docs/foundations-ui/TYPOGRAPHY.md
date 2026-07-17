# Typography

## Overview

TPS typography is optimized for dense, data-rich trading interfaces. Readability at small sizes, tabular number rendering, and clear hierarchy are the primary requirements.

---

## Font Selection Criteria

Trading interfaces have specific typographic requirements that general-purpose fonts may not meet:

1. **Tabular figures** — Numbers must align vertically in tables and lists
2. **Legibility at 10–12px** — Labels, ticks, and metadata render at small sizes
3. **Clear 0/O and 1/l/I disambiguation** — Critical for ticker symbols and order IDs
4. **Extended character support** — Currency symbols, mathematical operators, Greek letters (options Greeks)

---

## Recommended Font Stacks

### Primary (UI Text)

font-family-primary: "Inter", "SF Pro Text", system-ui, -apple-system, sans-serif;

### Monospace (Data & Code)

font-family-mono: "JetBrains Mono", "Fira Code", "SF Mono", "Consolas", monospace;

Monospace fonts are required for:
- Price displays
- Order IDs and reference numbers
- Quantity fields
- P&L values
- Any column of numbers requiring vertical alignment

---

## Type Scale

| Token | Size | Line Height | Weight | Usage |
|-------|------|-------------|--------|-------|
| `text-2xs` | 10px | 14px | 400 | Chart axis labels, micro metadata |
| `text-xs` | 11px | 16px | 400 | Table cell secondary data |
| `text-sm` | 12px | 18px | 400 | Default table text, labels |
| `text-base` | 14px | 20px | 400 | Body text, form inputs |
| `text-md` | 16px | 24px | 500 | Section labels, nav items |
| `text-lg` | 18px | 28px | 600 | Panel titles |
| `text-xl` | 22px | 32px | 600 | Primary price display |
| `text-2xl` | 28px | 36px | 700 | Hero price, large P&L |
| `text-3xl` | 36px | 44px | 700 | Dashboard headline metrics |

---

## Font Weight Usage

| Weight | Token | Usage |
|--------|-------|-------|
| 400 | `weight-regular` | Default body and data |
| 500 | `weight-medium` | Labels, nav, secondary emphasis |
| 600 | `weight-semibold` | Headings, active states |
| 700 | `weight-bold` | Critical values, headline metrics |

**Avoid weights below 400** in trading interfaces. Thin and light weights reduce legibility for data at small sizes.

---

## Numeric Formatting Rules

### Tabular Figures
All price, quantity, and financial value displays must use tabular (monospaced) figures:
```css
font-variant-numeric: tabular-nums;

Decimal Alignment
In columns containing decimal numbers, decimal points must align vertically.

Sign Display
Positive values: display + prefix in P&L contexts, omit in price contexts
Negative values: always display − (minus sign, U+2212), not - (hyphen)
Large Number Formatting
Value	Display
1000	1,000
1000000	1,000,000 or 1M (context-dependent)
0.00001	0.00001 (never scientific notation in price display)
Prohibited Patterns
❌ Using proportional figures for any tabular data
❌ Rendering prices in italic style
❌ Using text-shadow on data displays
❌ Applying letter-spacing to numeric strings
❌ Using font sizes below 10px for any visible content
❌ Mixing font families within a single data column

---

## 3️⃣ `docs/foundations-ui/SPACING.md`

```markdown
# Spacing System

## Overview

TPS uses a density-first spacing system. Unlike consumer-oriented design systems that default to generous whitespace, TPS defaults to compact spacing that maximizes information density — the primary requirement of professional trading interfaces.

---

## Base Unit

The TPS base spacing unit is **4px**.

All spacing values are multiples of this base unit.

---

## Spacing Scale

| Token | Value | Usage |
|-------|-------|-------|
| `space-0` | 0px | Reset, flush alignment |
| `space-1` | 4px | Micro gaps, icon padding |
| `space-2` | 8px | Cell padding, tight component spacing |
| `space-3` | 12px | Default component internal spacing |
| `space-4` | 16px | Standard section spacing |
| `space-5` | 20px | Comfortable form spacing |
| `space-6` | 24px | Panel padding default |
| `space-8` | 32px | Section separators |
| `space-10` | 40px | Large section gaps |
| `space-12` | 48px | Page-level spacing |
| `space-16` | 64px | Hero/header spacing |

---

## Density Modes

TPS defines three density presets:

### Compact (Default)
Optimized for maximum data density. Used in professional terminal layouts.

| Element | Value |
|---------|-------|
| Table row height | 28px |
| Cell padding (vertical) | `space-1` (4px) |
| Cell padding (horizontal) | `space-2` (8px) |
| Panel padding | `space-3` (12px) |
| Form field height | 32px |

### Comfortable
Balanced density for hybrid consumer/professional products.

| Element | Value |
|---------|-------|
| Table row height | 36px |
| Cell padding (vertical) | `space-2` (8px) |
| Cell padding (horizontal) | `space-3` (12px) |
| Panel padding | `space-4` (16px) |
| Form field height | 40px |

### Spacious
For onboarding flows, dashboards, and consumer-facing trading products.

| Element | Value |
|---------|-------|
| Table row height | 48px |
| Cell padding (vertical) | `space-3` (12px) |
| Cell padding (horizontal) | `space-4` (16px) |
| Panel padding | `space-6` (24px) |
| Form field height | 48px |

---

## Component-Specific Rules

### Tables & Data Grids
- Minimum row height: **24px** (absolute floor for accessibility)
- Column header padding must be equal to or greater than cell padding
- Frozen column dividers use `border-strong`

### Form Controls
- Minimum touch target: **32px** height (compact), **44px** (comfortable/spacious)
- Label-to-input gap: `space-1` (4px) in compact, `space-2` (8px) otherwise
- Input-to-input gap: `space-2` (8px) in compact, `space-3` (12px) otherwise

### Panels & Cards
- Panels must have consistent padding on all four sides
- Nested panels reduce padding by one scale step

---

## Spacing Anti-Patterns

- ❌ Using arbitrary pixel values not on the spacing scale
- ❌ Using `margin: auto` for vertical centering in data rows
- ❌ Inconsistent padding between visually grouped components
- ❌ Applying spacious-mode padding in compact-mode layouts
