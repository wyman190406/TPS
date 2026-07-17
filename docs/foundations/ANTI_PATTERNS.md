# Anti-Patterns

This document catalogs known design and product anti-patterns in trading interfaces. These are approaches that appear reasonable but cause measurable harm in professional trading environments.

All patterns listed here are **non-compliant** with TPS specifications.

---

## AP-001: Silent Data Staleness

**Description:** Displaying market data without indicating when it was last updated or whether the connection is active.

**Why it's harmful:** Traders acting on stale data make decisions based on incorrect market state, resulting in financial loss.

**TPS Requirement:** All real-time data displays must include a staleness indicator. Data older than a configurable threshold (default: 5 seconds) must be visually flagged.

---

## AP-002: Ambiguous Order Confirmation

**Description:** Using the same visual treatment for "order staged", "order submitted", and "order filled" states.

**Why it's harmful:** Traders may believe an order is filled when it is merely staged, or submitted when it has been rejected.

**TPS Requirement:** Order lifecycle states must be visually distinct. Color, iconography, and label must all change between states. See: Order Status Component specification.

---

## AP-003: Precision Loss in Display

**Description:** Rounding or truncating prices, quantities, or P&L values to fewer decimal places than the instrument requires.

**Why it's harmful:** For instruments traded in sub-cent increments or with high leverage, display rounding creates a material gap between displayed and actual values.

**TPS Requirement:** All numerical displays must respect instrument-level tick size and precision configuration.

---

## AP-004: Confirmation Dialog Overload

**Description:** Requiring multiple confirmation dialogs for routine trading actions.

**Why it's harmful:** In fast-moving markets, extra confirmation steps create dangerous latency between decision and execution. Traders learn to dismiss dialogs reflexively, defeating their purpose.

**TPS Requirement:** Confirmation dialogs are only permitted for destructive or irreversible actions (e.g., cancel all orders, close all positions). Routine order submission must not require confirmation dialogs.

---

## AP-005: Color-Only Status Encoding

**Description:** Using color alone to convey critical status information (e.g., red = loss, green = gain).

**Why it's harmful:** Approximately 8% of men have color vision deficiency. Color-only encoding excludes these users from reading critical financial information.

**TPS Requirement:** All status encoded by color must also be encoded by at least one additional signal: icon, label, position, or pattern.

---

## AP-006: Unstable Layouts During Data Updates

**Description:** UI layouts that shift, reflow, or cause scroll position jumps when new data arrives.

**Why it's harmful:** Traders are often reading or interacting with a UI element at the moment data updates. Layout shifts can cause misclicks on order actions.

**TPS Requirement:** Data updates must not cause layout shifts in components where user interaction is expected. New data must be inserted or updated in-place.

---

## AP-007: Buried Risk Information

**Description:** Placing margin status, liquidation prices, or risk warnings in secondary panels, collapsed sections, or tooltips.

**Why it's harmful:** Traders may not see critical risk information until it is too late to act.

**TPS Requirement:** Critical risk indicators (margin warning, liquidation proximity) must appear in the primary viewport without requiring user action to reveal.

---

## AP-008: Auto-Populating Order Forms from Charts

**Description:** Automatically setting order price or quantity fields based on chart interactions without explicit user intent.

**Why it's harmful:** Accidental chart interactions (zoom, pan) may silently corrupt order parameters the trader has already configured.

**TPS Requirement:** Order form population from chart interactions must require an explicit user action (click-to-set, drag-to-confirm). Passive chart navigation must not modify order fields.

---

## AP-009: Inconsistent Decimal Separators in Internationalization

**Description:** Using locale-dependent decimal separators (comma vs. period) without explicit configuration.

**Why it's harmful:** A price of "1,500" means one thousand five hundred in US locale and one-and-a-half in European locale. This ambiguity is catastrophic in trading contexts.

**TPS Requirement:** Decimal and thousands separators must be explicitly configurable and stored per user account, not inferred from browser locale.

---

## AP-010: Modal Dialogs Blocking Market Data

**Description:** Using modal overlays that block the view of live market data while requiring user input.

**Why it's harmful:** Traders need to see live prices even while configuring orders or settings.

**TPS Requirement:** No modal may obscure the primary market data panel. Use side panels, inline forms, or non-blocking overlays instead.

---

*Anti-patterns are added through the standard community contribution process. Each entry requires a documented real-world incident or research reference.*
