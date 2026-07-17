# ORDER_FLOW

> TPS Pattern Specification — `docs/patterns/ORDER_FLOW.md`
> Version: 0.1.0 | Status: Draft

## Overview

Order Flow describes the end-to-end interaction pattern for placing,
confirming, and tracking a trade order. It covers the full lifecycle
from user intent through order entry, validation, submission, and
status feedback.

## Flow Diagram

[User Intent]
│
▼
[Order Entry Panel]
├─ Select Symbol
├─ Select Side (Buy / Sell)
├─ Set Quantity
├─ Set Price (Limit) or Market
└─ Set Order Type (Market / Limit / Stop)
│
▼
[Client-side Validation]
├─ Required fields filled?
├─ Quantity > 0?
├─ Price within circuit breaker range?
└─ Sufficient buying power / margin?
│
┌──┴──────────────────┐
│ Fail │ Pass
▼ ▼
[Inline Error] [Confirmation Dialog]
├─ Show order summary
├─ Show estimated cost
└─ [Confirm] / [Cancel]
│
▼
[API Submission]
├─ Loading state on button
└─ Disable form inputs
│
┌──────────┴──────────┐
│ Error │ Success
▼ ▼
[Toast: Failed] [Toast: Submitted]
[Re-enable Form] [Order appears in
Orders panel]
│
▼
[Order Status Updates]
├─ Pending
├─ Partial Fill
├─ Filled
└─ Cancelled / Rejected

## Steps

### 1. Symbol Selection
- User types symbol in search field or selects from Watchlist
- Chart and Orderbook update to reflect selected symbol
- Order Entry panel pre-fills symbol

### 2. Order Configuration
- Side: Buy (default) or Sell toggle
- Order Type: Market / Limit / Stop / Stop-Limit
- Quantity: numeric input with lot size validation
- Price: enabled only for non-Market order types
- Time in Force: Day / GTC / IOC / FOK

### 3. Validation
- Client-side: immediate inline error feedback
- Server-side: rejection reason surfaced in toast notification
- Buying power check: insufficient funds shown before submission

### 4. Confirmation
- Required for orders above a configurable size threshold
- Summary shows: Symbol, Side, Qty, Type, Est. Value, Account
- User must explicitly confirm; no auto-submit on Enter

### 5. Submission Feedback
- Button enters loading state; form locked during API call
- Success: green toast "Order submitted — #ORDER_ID"
- Error: red toast with rejection reason; form re-enabled

### 6. Status Tracking
- Order immediately visible in Orders panel with `Pending` status
- Status transitions push real-time updates via WebSocket
- Fill notifications appear as toast with partial/full fill details

## Error States

| Error | Display | Recovery |
|---|---|---|
| Insufficient funds | Inline below qty / price | Adjust quantity |
| Invalid price | Inline below price field | Re-enter valid price |
| Market closed | Toast notification | Review trading hours |
| API rejection | Toast with reason code | Correct and retry |
| Network timeout | Toast with retry button | Retry or refresh |

## Related Components

- `ORDER_ENTRY` — primary input surface
- `ORDERBOOK` — price reference for limit orders
- `TABLE` (Orders) — post-submission tracking
- `ALERTS` — fill and rejection notifications

## Accessibility

- Form submission available via keyboard (Enter on Confirm button)
- Error messages linked to inputs via `aria-describedby`
- Loading state announced via `aria-live="polite"`
- Confirmation dialog traps focus until dismissed

