# TPS Terminology Glossary

This glossary defines the canonical terms used throughout TPS specifications. Using consistent terminology across design, engineering, and product reduces ambiguity and prevents costly miscommunication.

---

## A

**Ask Price**
The lowest price at which a seller is willing to sell an asset. Also called the "offer price". Displayed in TPS interfaces in a designated ask color (default: red in most markets).

**Asset**
Any financial instrument that can be traded, including equities, derivatives, cryptocurrencies, and fixed income instruments.

---

## B

**Bid Price**
The highest price at which a buyer is willing to purchase an asset. Displayed in TPS interfaces in a designated bid color (default: green in most markets).

**Book** *(Order Book)*
A real-time list of buy and sell orders for a specific asset, organized by price level. See: Market Depth.

---

## C

**Candle / Candlestick**
A chart element representing price movement over a time period, showing open, high, low, and close (OHLC) values.

**Component**
In TPS, a component is a specified UI element with defined appearance, behavior, states, and accessibility requirements.

---

## D

**Depth** *(Market Depth)*
The quantity of orders available at each price level in the order book. Displayed via depth charts or ladder views.

**DOM** *(Depth of Market)*
A UI pattern showing aggregated order book depth, commonly used by active traders. Synonym for ladder view.

---

## F

**Fill**
The execution of an order. A partial fill means only part of the order quantity was executed.

**Flatness** *(Flat Position)*
A position with zero net exposure to an asset. A trader who has closed all positions is "flat".

---

## G

**Greeks**
A set of risk measures for options positions: Delta, Gamma, Theta, Vega, and Rho.

---

## L

**Ladder View**
A vertically-oriented UI component showing price levels with associated bid/ask quantities and the ability to place orders by clicking price levels.

**Latency**
The delay between a market event occurring and it being reflected in the UI. TPS specifications distinguish between data latency and render latency.

**Leverage**
The use of borrowed capital to increase potential return. Expressed as a ratio (e.g., 10:1).

**Limit Order**
An order to buy or sell at a specific price or better.

**Liquidation**
The forced closure of a position when margin falls below the maintenance requirement.

---

## M

**Margin**
Collateral deposited to open and maintain leveraged positions.

**Market Order**
An order to buy or sell immediately at the best available current price.

**Mark Price**
A calculated reference price used for margin and settlement, typically different from the last traded price.

---

## O

**OHLC**
Open, High, Low, Close — the four price points used to describe price action over a period.

**Order**
An instruction to buy or sell an asset under specified conditions.

**Order Book**
See: Book.

---

## P

**P&L** *(Profit and Loss)*
The financial gain or loss on a position. Unrealized P&L exists while the position is open; Realized P&L is locked in after closing.

**Position**
The amount of an asset held by a trader, and the direction (long or short).

---

## S

**Slippage**
The difference between the expected execution price and the actual execution price.

**Spread**
The difference between the bid and ask price.

**Stop Order**
An order that becomes a market order when a specified price level is reached.

---

## T

**Tick**
The minimum price increment by which an asset's price can move.

**Time-in-Force (TIF)**
A parameter specifying how long an order remains active. See: DAY, GTC, IOC, FOK.

---

## U

**Underlying**
The asset upon which a derivative contract is based.

---

## V

**Volatility**
A measure of price variation over time. Implied volatility (IV) is derived from options prices.

**Volume**
The number of units of an asset traded over a given period.

---

*Terms are added as new specifications are introduced. Community-proposed terms are reviewed in the standard contribution process.*
