# Chapter 10 — Phased Roadmap

> Status: 🔲 Not started

## Purpose
Sequence the implementation so each phase ships something real and testable. No phase should be purely scaffolding — every phase should produce a system that can be validated against the prior one.

---

## Guiding Principles

- Each phase has a clear exit criteria before the next begins
- Backtesting parity is validated at the end of every phase that touches strategy logic
- No phase introduces AI components before the deterministic foundation is solid
- Phases are sized to be completable — not infinite sprints

---

## Phase 1 — Foundation
*Goal: Data layer, shared contracts, project structure.*

**Deliverables:**
- [ ] PostgreSQL schema finalized and migrated
- [ ] Stream handler (Schwab WebSocket) isolated as a standalone module
- [ ] Signal contract types defined
- [ ] Bar buffer management (warmup → live handoff)
- [ ] Project structure established

**Exit criteria:** Stream connects, bars flow, schema is live, contracts are typed.

---

## Phase 2 — Strategy Execution (Deterministic)
*Goal: All three strategies implemented as independent, testable execution modules.*

**Deliverables:**
- [ ] QQQ 0DTE Rejection strategy module
- [ ] QQQ 0DTE Breakout strategy module
- [ ] MNQ Momentum strategy module
- [ ] Backtester running all three strategies
- [ ] Backtest results match v1 within acceptable tolerance

**Exit criteria:** All strategies backtested and validated. Live paper trading on at least one strategy.

---

## Phase 3 — Risk Management & Trade Lifecycle
*Goal: Risk enforcement layer and complete trade lifecycle.*

**Deliverables:**
- [ ] Risk manager module (position limits, loss limits, kill switch)
- [ ] Trade lifecycle manager (entry → TP1 → BE → exit)
- [ ] Restart recovery (open trade re-adoption on startup)
- [ ] Full observability / audit logging

**Exit criteria:** System handles all trade lifecycle events correctly including edge cases. Kill switch tested.

---

## Phase 4 — Reasoning Agents
*Goal: Add AI reasoning components that survived the Chapter 8 filter.*

**Deliverables:**
- [ ] TBD (populated after Chapters 8 & 9)
- [ ] Coordinator routing logic
- [ ] Agent communication layer
- [ ] Fallback behavior when agents are unavailable

**Exit criteria:** AI components add measurable value over the deterministic baseline. Failure modes tested.

---

## Phase 5 — Production Hardening
*Goal: The system is live-tradeable.*

**Deliverables:**
- [ ] Deployment infrastructure (AWS or equivalent)
- [ ] Monitoring and alerting
- [ ] Frontend (or replace with minimal dashboard)
- [ ] Real account integration (Schwab live orders)
- [ ] Runbook: startup, shutdown, incident response

**Exit criteria:** System runs unattended through a full trading session without intervention.

---

## Open Questions from This Chapter
