# Chapter 4 — Data Architecture

> Status: 🔲 Not started

## Purpose
Define what data flows through the system, at what latency, and how it is stored and accessed. Every architectural decision downstream depends on getting this right.

---

## 4.1 Data Sources

| Source | Type | Latency | Consumer |
|---|---|---|---|
| Schwab Level 1 stream | Tick (quotes) | Real-time | Trade monitoring |
| Schwab CHART_EQUITY | 1-min bars | Per bar close | Signal evaluation |
| Schwab CHART_FUTURES | 1-min bars | Per bar close | MNQ signals |
| Schwab REST (candles) | OHLCV | On-demand | Warmup, backtest |
| Schwab 0DTE options | Tick + Greeks | Real-time | Options data collection |
| VIX | 1-min OHLC | Per bar | Context |
| PostgreSQL | Historical OHLCV | Query-time | Backtesting |

---

## 4.2 Data Consumers and Their Requirements
*What each component needs, at what frequency, and with what staleness tolerance.*

---

## 4.3 PostgreSQL Schema (v2)
*What changes from v1? What new tables are needed?*

### Tables to Carry Forward
### Tables to Redesign
### New Tables

---

## 4.4 Stream Architecture
*How does the Schwab WebSocket stream get consumed in v2?*

- Bar buffer management
- Warmup strategy (REST → stream handoff)
- Reconnection and recovery
- Who owns the stream — one consumer or multiple?

---

## 4.5 Historical Data Access
*How does the backtester access historical data? Same DB, same schema.*

---

## 4.6 Data Contracts Between Components
*What data shapes are passed between layers? Define them here.*

---

## 4.7 Open Questions from This Chapter
