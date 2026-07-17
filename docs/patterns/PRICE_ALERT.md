# PRICE_ALERT

> TPS Pattern Specification — `docs/patterns/PRICE_ALERT.md`
> Version: 0.1.0 | Status: Draft

## Overview

Price Alert describes the interaction pattern for creating, managing,
and receiving price-triggered notifications. Users set threshold
conditions on instruments; the platform notifies them when conditions
are met.

## Flow Diagram

[User triggers alert creation]
├─ Via Chart context menu: "Set Alert at [price]"
├─ Via Watchlist row action: "Add Alert"
└─ Via Alerts panel: "+ New Alert"
│
▼
[Alert Configuration Form]
├─ Symbol (pre-filled from context)
├─ Condition: Price ≥ / ≤ / crosses
├─ Target Price (numeric input)
├─ Notification: In-app / Push / Email
└─ Expiry: Never / End of Day / Custom date
│
▼
[Validation]
├─ Target price in valid range?
└─ Duplicate alert check
│
▼
[Alert Saved]
├─ Confirmation toast
├─ Alert line drawn on Chart
└─ Alert appears in Alerts panel (Active)
│
▼
[Runtime: Condition Met]
├─ In-app: Toast + Alerts panel badge
├─ Push notification (if enabled)
└─ Alert status → Triggered
│
▼
[Post-Trigger Options]
├─ View instrument
├─ Place order
└─ Reset / Delete alert

## Alert Conditions

| Condition | Description |
|---|---|
| `price_gte` | Last price ≥ target |
| `price_lte` | Last price ≤ target |
| `price_crosses_up` | Price crosses target from below |
| `price_crosses_down` | Price crosses target from above |
| `pct_change_gte` | % change from open ≥ threshold |
| `volume_spike` | Volume exceeds N× average |

## States

| State | Description |
|---|---|
| `active` | Monitoring, condition not yet met |
| `triggered` | Condition met, notification sent |
| `expired` | Past expiry date without trigger |
| `paused` | User-disabled temporarily |

## Alert Panel Entry

┌─────────────────────────────────────────────────┐
│ 🔔 AAPL Price ≥ 185.00 [Edit] [✕] │
│ Active · Expires: End of Day │
├─────────────────────────────────────────────────┤
│ ⚡ TSLA Price crosses 240.00 [Edit] [✕] │
│ Triggered 14:32 · In-app notified │
└─────────────────────────────────────────────────┘

## Notification Design

- In-app toast appears at top-right, persists 8 seconds
- Toast includes: Symbol, condition summary, current price, [View] CTA
- Alerts panel badge shows count of unread triggered alerts
- Triggered alert row highlighted until user acknowledges

## Related Components

- `CANDLESTICK` — alert price line overlay on chart
- `ALERTS` — alert management panel
- `INPUT` — target price entry

## Accessibility

- Alert creation form is keyboard accessible
- Triggered alert toast has `role="alert"` for screen reader announcement
- Dismissible via Escape key

