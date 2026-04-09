# Chapter 7 — Observability & Auditability

> Status: 🔲 Not started

## Purpose
Define what gets logged, at what granularity, and how decisions can be replayed and understood after the fact. In a trading system — especially one with AI components — you must be able to answer "why did that trade happen?" for every trade.

---

## 7.1 What Must Be Logged

### Per Signal
- Timestamp (bar close that triggered evaluation)
- All condition states at evaluation time (C1, C2, C3 etc.)
- Signal outcome (fired / suppressed / cooldown)
- Strategy ID and config snapshot used

### Per Trade
- Entry: timestamp, price, direction, strategy, signal reference
- All TP/SL/BE events with timestamps and prices
- Exit: reason, price, timestamp, P&L
- Any mid-trade state changes

### Per Agent Decision (v2 AI components)
- Input context provided to the agent
- Reasoning output (structured)
- Decision made and confidence if applicable
- Timestamp

---

## 7.2 Log Storage
*Where do logs live? Structured DB tables vs. append-only log files vs. both?*

---

## 7.3 Session Replay
*Can we reconstruct exactly what happened in a session from the logs?*

- What is the minimum data needed for full replay?
- What tooling enables this?

---

## 7.4 Alerting
*What conditions should trigger an alert? What is the alert mechanism?*

- Daily loss limit approached / breached
- Stream disconnect
- No signal evaluation for unexpected duration
- Trade open past expected time stop window

---

## 7.5 Performance Monitoring
*What metrics track system health over time?*

- Signal frequency per strategy
- Win rate, average P&L per strategy
- Drawdown tracking
- Stream uptime / reconnect frequency

---

## 7.6 Open Questions from This Chapter
