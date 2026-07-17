# Alerts Component

## Overview

The Alerts component allows users to set, manage, and receive notifications for price, volume, and technical indicator conditions. Alerts are a critical productivity tool for traders who cannot watch screens continuously.

---

## Alert Types

| Type | Trigger Condition |
|------|------------------|
| **Price Alert** | Asset price crosses above or below a level |
| **Percentage Move** | Asset moves X% from a reference price |
| **Volume Alert** | Volume exceeds threshold within a period |
| **Technical Alert** | Indicator crosses a level (RSI, MA cross, etc.) |
| **Order Alert** | Order fill, rejection, or expiry notification |
| **Margin Alert** | Margin utilization exceeds threshold |
| **Liquidation Alert** | Position approaches liquidation price |
| **AI Signal Alert** | AI-generated signal meets confidence threshold |

---

## Alert Creation Panel

┌────────────────────────────────────┐
│ Create Alert │
├────────────────────────────────────┤
│ Symbol: [AAPL ] │
│ Condition: [Price crosses ▼ ] │
│ Direction: [Above ▼] │
│ Value: [__________155.00] │
├────────────────────────────────────┤
│ Notification: │
│ [✓] In-app toast │
│ [✓] Sound │
│ [ ] Email │
│ [ ] Push notification │
├────────────────────────────────────┤
│ Message: (optional) │
│ [_____________________________] │
├────────────────────────────────────┤
│ Expiry: [No expiry ▼] │
├────────────────────────────────────┤
│ [Cancel] [Create Alert] │
└────────────────────────────────────┘

---

## Alert States

| State | Icon | Color |
|-------|------|-------|
| Active | `alert` | `color-info` |
| Triggered | `alert-active` | `color-warning` |
| Expired | `alert` (dimmed) | `color-neutral` |
| Paused | `alert` (paused) | `color-neutral` |
| Error | `alert` | `color-negative` |

---

## Alert List

| Column | Description |
|--------|-------------|
| Symbol | Instrument |
| Condition | Human-readable condition summary |
| Value | Trigger value |
| Status | Active, Triggered, Expired |
| Created | Creation timestamp |
| Actions | Edit, Pause/Resume, Delete |

---

## Alert Notification (Toast)

When an alert triggers:

┌────────────────────────────────────────┐
│ 🔔 Price Alert: AAPL │
│ Price crossed above $155.00 │
│ Current price: $155.42 │
│ [View Chart] [Dismiss] │
└────────────────────────────────────────┘

- Toast appears in bottom-right corner
- Persists until dismissed (not auto-dismissed for price alerts)
- Sound plays if enabled (user-configurable sound and volume)
- [View Chart] navigates to the relevant chart

---

## AI Alert Attribution

When an alert is AI-suggested:
- `ai-suggestion` icon displayed next to alert condition
- Tooltip: "Suggested by AI based on your trading patterns"
- User must explicitly create the alert — AI cannot create alerts automatically

---

## Accessibility

- Alert creation form uses standard form accessibility patterns
- Triggered alerts use `role="alert"` for immediate screen reader announcement
- Sound alerts must be paired with visual notification
- All notifications must be dismissible via keyboard

---

## Prohibited Patterns

- ❌ Auto-creating alerts based on AI suggestions without user action
- ❌ Auto-dismissing triggered price alerts
- ❌ Playing alert sounds without a volume control mechanism
- ❌ Deleting triggered alerts without user confirmation
