# Chapter 1 — Current System Audit

> Status: 🔲 Not started

## Purpose
Establish an honest, precise picture of v1 before designing v2. We cannot make good architectural decisions without fully understanding what we're replacing and why.

---

## 1.1 Strategy Inventory
*Map each strategy exactly as it runs today — inputs, conditions, execution, exits.*

- [ ] QQQ 0DTE Rejection Strategy
- [ ] QQQ 0DTE Breakout Strategy
- [ ] MNQ Futures Momentum Strategy

---

## 1.2 Shared vs. Unique Logic
*Identify what is genuinely shared across strategies vs. accidentally coupled.*

---

## 1.3 What Works Well
*Things in v1 that should be preserved or ported directly.*

---

## 1.4 What Is Broken or Fragile
*Known bugs, races, fragile assumptions, or things held together with duct tape.*

### Strat E — time_stop_minutes sourced from wrong config section
`check_mnq_paper_trade()` reads `config.options.time_stop_minutes` for the
time stop, not a futures-specific field. `strategy_e.yaml` has no `options:`
section, so this falls back to the `OptionsConfig` dataclass default (15 min),
which happens to match the backtested 15-bar hold. This is correct by accident.
If a `time_stop_minutes` is ever added under `futures:` in `strategy_e.yaml`
it would be silently ignored. v2 must give futures strategies their own
time stop parameter.

---

## 1.5 What Is Redundant
*Overlapping logic, duplicate code paths, unnecessary coupling.*

---

## 1.6 Key Decisions Made in v1 (and Whether They Still Hold)
*Decisions that were made under constraints that may no longer apply.*

### Strat E — research validated simple momentum continuation; live impl adds pullback entry
The original research (`research/runs/02_mnq_momentum`) validated a bare
momentum signal (≥0.40% move over 5 bars → enter immediately). The execution
research (`execution_report.md`) then added the 25pt pullback entry to fix the
problem of entering at the top/bottom of the initiating move. The pullback
entry was backtested and validated across train/validate/test periods.

The live implementation correctly mirrors the backtested pullback entry — entry
triggers on a tick hitting the pullback level (equivalent to the backtest
checking candle low/high). Parity is confirmed.

### Strat E — 13 live trades is not enough data to evaluate the strategy
The backtest required 400+ trades in the test period to show the edge. 13 trades
across 9 sessions is noise. The recent run of SL hits (8 of last 9 trades) is
consistent with a tariff/geopolitically-driven low-follow-through regime where
intraday momentum does not persist. The strategy should be allowed to run.

### Strat E — the research finding that EMA filters add no value was honored
The live implementation uses no EMA alignment filters, consistent with the
research conclusion that confluence filters halve sample size without improving
win rate. This was the right call.

---

## 1.7 Open Questions from This Chapter
*Questions surfaced during the audit that need to be resolved before proceeding.*

- Should v2 include a regime filter for Strat E that reduces or halts trading when
  intraday momentum follow-through characteristics break down? (→ Chapter 8 candidate)
- Does the current cooldown logic (15 min post-trade) match the backtested cooldown_bars=15?
