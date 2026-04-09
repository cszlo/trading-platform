# Chapter 3 — Strategy Definitions & Signal Contracts

> Status: 🔲 Not started

## Purpose
Get every strategy rule out of code and into plain language. Define a typed "signal contract" — the precise interface between signal detection and trade execution. This becomes the spec both the backtest and live engine implement against.

---

## 3.1 QQQ 0DTE Rejection Strategy

### Entry Conditions
### Signal Direction Logic
### Entry Execution
### Take Profit Logic
### Stop Loss Logic
### Breakeven Logic
### Time Stop
### Edge Cases

---

## 3.2 QQQ 0DTE Breakout Strategy

### Entry Conditions
### Signal Direction Logic
### Entry Execution
### Take Profit Logic
### Stop Loss Logic
### Breakeven Logic
### Time Stop
### Edge Cases

---

## 3.3 MNQ Futures Momentum Strategy

### Entry Conditions
### Signal Direction Logic
### Entry Execution
### Take Profit Logic
### Stop Loss Logic
### Breakeven Logic
### Time Stop
### Edge Cases

---

## 3.4 Signal Contract Definition
*The typed interface each strategy produces. Execution layer consumes this — it does not care which strategy produced it.*

```
SignalContract:
  direction: LONG | SHORT
  instrument: str
  entry_price: float
  tp_price: float | None
  sl_price: float
  time_stop_minutes: int
  strategy_id: str
  confidence: float | None       # if AI-assisted
  metadata: dict                 # strategy-specific context
```

---

## 3.5 Shared Logic Across Strategies
*Logic that is genuinely reusable — extracted here, not duplicated.*

---

## 3.6 Open Questions from This Chapter
