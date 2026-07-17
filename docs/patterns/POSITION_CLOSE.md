# POSITION_CLOSE

> TPS Pattern Specification — `docs/patterns/POSITION_CLOSE.md`
> Version: 0.1.0 | Status: Draft

## Overview

Position Close describes the interaction pattern for closing an open
trading position. It is a destructive, financially consequential action
and therefore requires explicit user confirmation with a clear summary
of the expected outcome.

## Flow Diagram

[Position Table Row]
└─ User clicks [Close] button
│
▼
[Close Position Dialog]
├─ Symbol and side summary
├─ Current quantity to close (editable: full or partial)
├─ Estimated close price (last / market)
├─ Estimated P&L at close
└─ [Confirm Close] / [Cancel]
│
┌─────┴──────────────────────┐
│ Cancel │ Confirm
▼ ▼
[Dialog dismissed] [API: Submit close order]
[No change] ├─ Button loading state
└─ Dialog locked
│
┌──────────┴──────────┐
│ Error │ Success
▼ ▼
[Error toast] [Success toast]
[Dialog re-enabled] [Dialog closes]
[Position removed
or qty reduced]

## Close Types

| Type | Description |
|---|---|
| `full_close` | Close entire open quantity at market |
| `partial_close` | Close a user-specified portion of quantity |
| `close_at_limit` | Close at a specified limit price |

## Dialog Content

┌────────────────────────────────────────────┐
│ Close Position [✕] │
├────────────────────────────────────────────┤
│ AAPL · Long │
│ │
│ Quantity to Close [100] / 100 (Full) │
│ Order Type Market │
│ Est. Close Price $182.45 │
│ Est. P&L +$425.00 (2.39%) │
│ │
│ ⚠ Closing at market price. │
│ Actual fill may differ slightly. │
├────────────────────────────────────────────┤
│ [Cancel] [Confirm Close] │
└────────────────────────────────────────────┘

## Validation Rules

- Quantity must be between 1 and current open quantity
- Partial close quantity must respect lot size minimums
- Confirm Close button disabled if quantity is invalid

## Feedback States

| State | Display |
|---|---|
| Loading | Confirm button shows spinner; dialog locked |
| Success | Green toast "AAPL position closed"; dialog dismissed |
| Partial success | Toast "50 of 100 AAPL shares closed" |
| Error | Red toast with reason; dialog re-enabled for retry |

## Related Components

- `POSITION_TABLE` — entry point for Close action
- `ORDER_ENTRY` — alternative for manual close order construction
- `ORDER_FLOW` — shared submission and feedback pattern

## Accessibility

- Dialog has `role="dialog"` and `aria-modal="true"`
- Focus moves to dialog on open; returns to triggering row on close
- Escape key cancels and closes dialog
- Confirm button has `aria-label="Confirm close position for AAPL"`
- Estimated P&L includes visually hidden "profit" or "loss" for screen readers

