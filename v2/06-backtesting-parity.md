# Chapter 6 — Backtesting Parity

> Status: 🔲 Not started

## Purpose
Define how v2 maintains faithful parity between the backtest and live execution. A backtest that doesn't match live behavior is not a backtest — it's a fiction.

---

## 6.1 The Parity Contract
*The non-negotiable rules that both live and backtest must follow:*

- Signals fire on bar close, never on tick
- Entry price is the open of the bar following the signal bar
- Exit logic uses the same conditions in both environments
- No look-ahead bias

---

## 6.2 What the Backtester Must Simulate

- Bar-by-bar replay of historical 1-min OHLCV
- Key level derivation at each bar (no future data)
- Heavyweight EMA state at each bar
- Intraday level detection up to the current bar only
- Trade monitoring (TP, SL, BE, time stop) bar-by-bar

---

## 6.3 What the Backtester Cannot Simulate (and How We Handle It)

- Options chain data (no historical Greeks) → MNQ futures only in backtest
- Max pain / OI levels → excluded or approximated
- Slippage and partial fills → configurable slippage model
- Stream disconnects → not simulated (acceptable)

---

## 6.4 Shared Execution Logic
*Which modules are literally shared between live and backtest vs. parallel implementations?*

---

## 6.5 Backtester Architecture in v2
*How does the backtester consume strategy agents? Can strategy logic run unmodified in both contexts?*

---

## 6.6 Validation Approach
*How do we validate that live and backtest produce the same signals on the same data?*

---

## 6.7 Open Questions from This Chapter
