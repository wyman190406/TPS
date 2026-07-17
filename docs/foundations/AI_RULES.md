# AI Integration Rules

## Overview

TPS is an AI-native specification. This means AI capabilities are considered first-class citizens of the trading interface — not bolt-on features. This document defines the rules governing how AI features must be designed, surfaced, and constrained in TPS-compliant products.

---

## Core Principle

> AI in trading interfaces must **augment** human decision-making, never **replace** it.

The consequences of autonomous financial decisions are too significant for AI to operate without explicit human intent and oversight.

---

## Rule 1: Attribution Is Mandatory

Every AI-generated output visible to the user must be clearly attributed as AI-generated.

**Required:**
- Visual indicator (icon, label, or badge) on AI-generated content
- Tooltip or inline explanation of the AI's basis for the output
- Model or signal source disclosure where technically feasible

**Prohibited:**
- Presenting AI-generated prices, forecasts, or signals as market data
- Blending AI output with real-time data without clear delineation

---

## Rule 2: Confidence Must Be Surfaced

AI outputs must communicate uncertainty. Displaying a forecast without confidence bounds is a specification violation.

**Required formats:**
- Confidence percentage or range
- Probability distribution where applicable
- Clear language distinguishing "prediction" from "data"

---

## Rule 3: Human Override Always Available

No AI action may prevent, delay, or complicate human override.

**Required:**
- One-click cancel for any AI-initiated action
- Override must not require confirmation dialogs with more than one step
- Override history must be logged and accessible

---

## Rule 4: AI Cannot Execute Orders Without Explicit Confirmation

AI may **suggest** orders. AI may **stage** orders. AI may **pre-fill** order forms. AI may **not** submit orders without an explicit, unambiguous human action.

The confirmation action must be:
- Distinct from the AI suggestion interaction
- Not pre-selected or auto-focused
- Clearly labeled as "Submit Order" or equivalent

---

## Rule 5: Explain Before Acting

For any AI feature that modifies state (portfolio adjustments, alert creation, order staging), the AI must present a plain-language explanation of what it intends to do before doing it.

---

## Rule 6: Graceful Degradation

AI features must not create dependency for core trading functions. If an AI service is unavailable:

- Core trading functions must remain fully operational
- AI-powered UI elements must display a clear unavailability state
- No core data (prices, positions, orders) may depend on AI service availability

---

## Rule 7: Data Privacy by Default

AI features that process user trading data must:

- Disclose what data is used for model inference
- Not use individual user trading data to train shared models without explicit opt-in
- Provide a mechanism to opt out of AI features entirely

---

## AI Feature Classification

| Feature Type | Autonomy Level | Confirmation Required |
|--------------|----------------|----------------------|
| Price forecast / signal | Informational | No |
| Alert suggestion | Staging | Yes (one-click accept) |
| Order pre-fill | Staging | Yes (explicit submit) |
| Automated rebalancing | Execution | Yes (multi-step confirm) |
| Risk override | Execution | Yes (multi-step confirm) |

---

## Prohibited AI Patterns

- ❌ Auto-submitting orders based on AI signals
- ❌ Hiding AI attribution behind small or low-contrast UI elements
- ❌ Using AI-generated prices as reference for order execution
- ❌ Presenting AI forecasts without uncertainty quantification
- ❌ Blocking access to manual controls when AI is active

---

*These rules will evolve as AI capabilities and regulatory standards develop. Changes follow the standard TPS versioning and deprecation process.*
