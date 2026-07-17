# Order Entry Component

## Overview

The Order Entry component is the most critical interactive element in a trading interface. It is the primary mechanism through which users submit buy and sell instructions to the market. Errors in order entry have direct financial consequences.

---

## Component Anatomy

┌─────────────────────────────────────┐
│ [BUY] [SELL] │ ← Direction Toggle
├─────────────────────────────────────┤
│ Order Type: [Limit ▼] │ ← Order Type Selector
├─────────────────────────────────────┤
│ Price: [_42,150.00] │ ← Price Input
│ Quantity: [________0.01] │ ← Quantity Input
├─────────────────────────────────────┤
│ Time in Force: [Day ▼] │ ← TIF Selector
├─────────────────────────────────────┤
│ Est. Value: $421.50 │ ← Calculated Summary
│ Est. Fee: $0.42 │
│ Available: $10,420.00 │
├─────────────────────────────────────┤
│ [ Place Buy Order ] │ ← Submit Button
└─────────────────────────────────────┘

---

## States

### Direction States
| State | Visual Treatment |
|-------|----------------|
| Buy selected | Header background `color-positive`, button `color-positive` |
| Sell selected | Header background `color-negative`, button `color-negative` |

Direction state must be immediately obvious at a glance. Color + label + button text all change together.

### Order Type States
| Type | Required Fields |
|------|----------------|
| Market | Quantity only (price field hidden or disabled) |
| Limit | Price + Quantity |
| Stop | Stop Price + Quantity |
| Stop-Limit | Stop Price + Limit Price + Quantity |

Fields not applicable to the selected order type must be hidden, not merely disabled.

### Input Validation States
| State | Indicator |
|-------|-----------|
| Default | `border-default` |
| Focus | `border-strong` + focus ring |
| Valid | No change (avoid green — reserved for buy direction) |
| Error | `border-critical` + inline error message below field |
| Warning | `border-warning` + inline warning message |

### Submit Button States
| State | Appearance | Behavior |
|-------|-----------|---------|
| Idle (Buy) | `color-positive` background | Clickable |
| Idle (Sell) | `color-negative` background | Clickable |
| Submitting | Spinner + "Placing Order…" | Disabled |
| Success | Brief flash confirmation | Reset after 1.5s |
| Error | Shake animation + error message | Remain filled |
| Disabled | `surface-interactive`, muted text | Not clickable |

---

## Input Behavior

### Price Input
- Accepts decimal input per instrument tick size
- Increment/decrement via arrow keys (1 tick per press, 10 ticks with Shift)
- Scroll wheel supported when field is focused
- Must validate against instrument minimum/maximum price
- Must display in instrument's quote currency

### Quantity Input
- Accepts decimal input per instrument lot size
- Percentage buttons optional: [25%] [50%] [75%] [100%] of available balance
- Must validate against minimum and maximum order size
- Must display lot size hint below field

### Price Precision
- Display and accept exactly the precision defined by instrument tick size
- Never round displayed values in input fields
- Paste handling must strip non-numeric characters and validate precision

---

## Order Summary Panel

Must always display before submission:
- **Estimated order value** (price × quantity)
- **Estimated fee** (based on current fee tier)
- **Available balance / buying power**
- **Post-order balance** (available minus estimated value)

If any of these cannot be calculated, display "—" not zero.

---

## Confirmation Behavior

| Order Type | Confirmation Required | Method |
|-----------|----------------------|--------|
| Standard orders (< threshold) | No | Direct submit |
| Large orders (> user-defined threshold) | Yes | Inline confirm step |
| Close position | Yes | Inline confirm step |
| Cancel all orders | Yes | Modal confirmation |

Threshold for large order confirmation is user-configurable. Default: 10× average order size or 20% of available balance.

---

## Keyboard Behavior

| Key | Action |
|-----|--------|
| `Tab` | Move between fields in order |
| `Enter` (on submit button) | Submit order |
| `Escape` | Clear form / cancel staged order |
| `B` (global shortcut) | Focus order entry, set Buy |
| `S` (global shortcut) | Focus order entry, set Sell |
| `↑` / `↓` (in price field) | Increment / decrement by 1 tick |
| `Shift + ↑` / `↓` | Increment / decrement by 10 ticks |

---

## Accessibility

- Direction toggle must use `role="radiogroup"` with `role="radio"` for each option
- Order type selector must be a native `<select>` or ARIA combobox
- Submit button must announce result via `aria-live="assertive"`
- Error messages must be associated with their fields via `aria-describedby`
- Estimated value panel must update and be announced via `aria-live="polite"`

---

## Prohibited Patterns

- ❌ Auto-submitting order on Enter without explicit button focus
- ❌ Clearing form fields when order is rejected (retain values for correction)
- ❌ Displaying confirmation of submission before server acknowledgement
- ❌ Using the same button label for "Stage Order" and "Submit Order"
- ❌ Hiding the available balance from the order entry panel

