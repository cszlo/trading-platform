# Chapter 5 — Risk Management Layer

> Status: 🔲 Not started

## Purpose
Define the hard limits that govern the system's behavior under all conditions. Risk management is the one layer that cannot be optional, configurable-away, or skippable. It must be enforced at the architecture level, not the strategy level.

---

## 5.1 Position Limits

- Max open positions (per strategy, total)
- Max contracts per trade
- Max concurrent trades across all strategies

---

## 5.2 Loss Limits

- Max loss per trade (enforced at SL)
- Max daily loss (kill switch)
- Max drawdown threshold

---

## 5.3 Risk Enforcement Architecture
*Where does risk live in the system? Options:*
- Enforced by the coordinator before routing to execution
- Enforced by a dedicated risk component that all signals pass through
- Enforced at the execution layer (last line of defense)

*Decision: ___*

---

## 5.4 Kill Switch Behavior
*What happens when a daily loss limit or drawdown threshold is breached?*

- Close open positions immediately vs. let them run to SL
- Block new signals for remainder of session
- Alert mechanism

---

## 5.5 Restart and Recovery
*What happens when the system restarts mid-session with open trades?*

- How are open trades detected and re-adopted?
- Who is responsible for re-subscribing to stream data for open positions?
- What is the max acceptable gap in monitoring coverage?

---

## 5.6 Edge Cases

- Stream disconnect with open trade
- Partial fill handling
- Stale quote detection
- Market close with open trade (time stop)
- Holiday / early close detection

---

## 5.7 Open Questions from This Chapter
