# Orders Component

## Overview

The Orders component displays the user's active and historical orders. It allows traders to monitor order status, modify open orders, and cancel pending orders.

---

## Tabs

The Orders component is organized into tabs:

| Tab | Content |
|-----|---------|
| **Open Orders** | Submitted, pending, partially filled orders |
| **Order History** | Completed, cancelled, rejected, expired orders |
| **Conditional Orders** | Stop orders, alerts-triggered orders (if supported) |

Default view: Open Orders tab.

---

## Open Orders Table

### Required Columns

| Column | Description |
|--------|-------------|
| Time | Order submission timestamp (HH:MM:SS) |
| Symbol | Instrument ticker |
| Type | Market, Limit, Stop, Stop-Limit |
| Direction | Buy / Sell |
| Quantity | Total order quantity |
| Filled | Quantity filled so far |
| Price | Limit price (or "Market") |
| Status | Open, Partial, Pending Cancel |
| TIF | Time-in-Force |
| Actions | Modify, Cancel |

---

## Order Status Display

| Status | Badge Color | Icon | Description |
|--------|------------|------|-------------|
| Pending Submit | `color-neutral` | `order-pending` | Staged, not yet sent |
| Open | `color-info` | `order-open` | Submitted, awaiting fill |
| Partial | `color-warning` | `order-partial` | Partially filled |
| Filled | `color-positive` | `order-filled` | Fully executed |
| Cancelled | `color-neutral` | `order-cancelled` | Cancelled by user |
| Rejected | `color-negative` | `order-rejected` | Rejected by exchange |
| Expired | `color-neutral` | `order-expired` | TIF elapsed |
| Pending Cancel | `color-warning` | `order-pending` | Cancel submitted |

All statuses must display badge + icon + text label. Never color alone.

---

## Order History Table

Adds columns:
- **Fill Price** — Actual execution price (volume-weighted for partial fills)
- **Fill Time** — Timestamp of final fill or cancellation
- **Rejection Reason** — Plain-language reason for rejected orders

---

## Modify Order

Clicking "Modify" on an open order:
- Opens an inline edit row (preferred) or side panel
- Editable fields: Price, Quantity, TIF
- Non-editable fields: Symbol, Direction, Type (to change these, cancel and re-enter)
- "Save Changes" submits the modification
- "Cancel Edit" dismisses without changes

---

## Cancel Order

Single order cancel:
- Inline confirmation in the row: "Cancel this order? [Yes] [No]"
- Default focus on [No]
- Row shows "Pending Cancel" status until server confirms

Cancel All Orders:
- Modal confirmation listing count and estimated value of orders to be cancelled
- Default focus on [Keep Orders]
- Requires explicit click on [Cancel All Orders] button

---

## Real-Time Updates

Orders table must reflect real-time updates:
- New order appears at top of Open Orders
- Partial fill updates Filled quantity in real-time
- Full fill moves order to Order History (with animation)
- Rejection immediately moves order to history with rejection reason
- Cancel confirmation removes from Open Orders

---

## Empty States

| Tab | Empty Message |
|-----|--------------|
| Open Orders | "No open orders. Orders you place will appear here." |
| Order History | "No order history. Completed orders will appear here." |

---

## Filtering & Search

- Filter by: Symbol, Direction (Buy/Sell), Type, Status
- Date range picker for Order History
- Search by Order ID or Symbol
- Export to CSV (Order History only)

---

## Accessibility

- Status changes must trigger `aria-live="polite"` announcements
- Order rejection must trigger `aria-live="assertive"` announcement with reason
- Cancel confirmation must trap focus within confirmation area
- Modify row must move focus to first editable field

---

## Prohibited Patterns

- ❌ Showing a success state before server acknowledgement
- ❌ Silently discarding an order modification if the request fails
- ❌ Auto-cancelling orders on session end without user consent
- ❌ Displaying "Filled" status for partial fills
