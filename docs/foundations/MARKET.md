# Market Structure Reference

## Purpose

This document provides the foundational market structure knowledge that informs TPS specifications. Product and design decisions cannot be made correctly without understanding the domain they serve.

---

## Asset Classes

TPS specifications cover the following asset classes:

| Asset Class | Examples | Notes |
|-------------|----------|-------|
| **Equities** | Stocks, ETFs | Primary coverage in v1 |
| **Derivatives** | Options, Futures | v1 partial coverage |
| **Cryptocurrency** | BTC, ETH, altcoins | v1 partial coverage |
| **Fixed Income** | Bonds, Treasuries | Planned for v2 |
| **Forex** | Currency pairs | Planned for v2 |
| **Commodities** | Gold, Oil | Planned for v2 |

---

## Order Types

TPS-compliant order entry interfaces must support and clearly distinguish:

### Core Order Types
- **Market Order** — Execute immediately at best available price
- **Limit Order** — Execute only at specified price or better
- **Stop Order** — Trigger a market order when price reaches stop level
- **Stop-Limit Order** — Trigger a limit order when price reaches stop level

### Time-in-Force
- **Day** — Valid for current trading session only
- **GTC** (Good Till Cancelled) — Valid until explicitly cancelled
- **IOC** (Immediate or Cancel) — Fill immediately, cancel remainder
- **FOK** (Fill or Kill) — Fill entirely immediately or cancel entirely
- **GTD** (Good Till Date) — Valid until specified date

---

## Market Participants

Understanding participant types informs UI persona design:

| Participant | Characteristics | UI Implications |
|-------------|-----------------|-----------------|
| **Retail Trader** | Lower volume, longer timeframes | Simplified order entry acceptable |
| **Active Trader** | High frequency, intraday | Full keyboard shortcut support required |
| **Institutional** | Large size, complex orders | Algorithmic order types, iceberg support |
| **Market Maker** | Two-sided quotes | Spread management UI, auto-quote tools |
| **Algorithmic** | Programmatic execution | API-first, monitoring dashboards |

---

## Price Discovery

TPS interfaces must correctly represent:

- **Bid Price** — Highest price a buyer will pay
- **Ask Price** — Lowest price a seller will accept
- **Spread** — Difference between bid and ask
- **Last Price** — Most recent executed trade price
- **Mid Price** — Mathematical midpoint between bid and ask
- **Mark Price** — Reference price for margin/settlement (derivatives)

---

## Market Sessions

Trading interfaces must account for session-based behavior:

| Session | Description |
|---------|-------------|
| **Pre-Market** | Before regular trading hours |
| **Regular Hours** | Primary trading session |
| **After-Hours** | Post-close extended trading |
| **Closed** | No trading activity |
| **Halted** | Trading suspended (circuit breaker, news) |

Session state must always be visibly indicated in TPS-compliant interfaces.

---

## Risk Concepts

The following risk concepts must be surfaced in relevant UI contexts:

- **Margin** — Collateral required to hold leveraged positions
- **Leverage** — Ratio of position size to margin
- **Liquidation Price** — Price at which position is force-closed
- **P&L (Profit & Loss)** — Realized and unrealized gains/losses
- **Greeks** — Options risk measures (Delta, Gamma, Theta, Vega)
- **VaR (Value at Risk)** — Statistical risk measure

---

*This document is a living reference. Asset class coverage expands with each TPS milestone.*
