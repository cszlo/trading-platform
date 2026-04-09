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
- MNQ moves ≥ 0.40% over 5 consecutive RTH 1-min bars (CHART_FUTURES stream)
- Signal fires on bar close only — no intra-bar firing
- Full RTH session: 9:30 AM – 4:00 PM ET
- Both directions (LONG and SHORT)
- One active signal at a time; 15-min cooldown after any trade exit

### Signal Direction Logic
- Move is positive → LONG signal
- Move is negative → SHORT signal

### Entry Execution
- Wait for MNQ to retrace 25 points from the signal bar close
- Entry triggers on live Level 1 tick hitting the pullback level (checked every ~0.5s)
- Entry recorded at pullback trigger price
- Abandon if pullback not reached within 15 minutes of signal

### Take Profit Logic
- Single target: entry ± (stop_points × risk_reward) = entry ± 45 points
- Full position close at target (1 contract) — no partials
- Recorded as "TP1" in trade log

### Stop Loss Logic
- Hard stop: 15 points below/above entry
- No breakeven stop mechanic (unlike QQQ option strategies)

### Breakeven Logic
- None — hard stop only

### Time Stop
- 15 minutes from entry (falls back to `OptionsConfig.time_stop_minutes` default in v1 — fragile, see Chapter 1.4)
- v2 must define `time_stop_minutes` explicitly in a futures-specific config section

### Edge Cases
- Signal fires near session end — pullback timeout may expire at 4:00 PM before entry triggers
- Clustered signals (multiple 0.40%+ moves in quick succession) — cooldown prevents overlapping trades
- Stream disconnect with open trade — no recovery mechanism in v1

### v1 Parity Status
✅ Signal detection matches backtest (bar close, candle low/high for pullback check)
✅ Entry price matches backtest (pullback trigger level)
✅ Stop, target, time stop all match backtested winner config
⚠️ time_stop_minutes sourced from wrong config section — correct by accident

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
