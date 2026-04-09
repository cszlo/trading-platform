# Trading Platform v2

A ground-up rebuild of a live multi-strategy algorithmic trading platform for QQQ 0DTE options and MNQ futures.

## Status: Architecture & Planning Phase

No code yet — by design. The planning phase is conducted collaboratively with Claude (Anthropic) before a single line of implementation is written. The goal is to make deliberate architectural decisions, challenge assumptions, and produce a phased roadmap before committing to any implementation.

## Planning Documents

| Chapter | Topic | Status |
|---|---|---|
| [01](v2/01-current-system-audit.md) | Current System Audit | 🔲 Not started |
| [02](v2/02-goals-and-success-criteria.md) | Goals & Success Criteria | 🔲 Not started |
| [03](v2/03-strategy-definitions-and-signal-contracts.md) | Strategy Definitions & Signal Contracts | 🔲 Not started |
| [04](v2/04-data-architecture.md) | Data Architecture | 🔲 Not started |
| [05](v2/05-risk-management.md) | Risk Management Layer | 🔲 Not started |
| [06](v2/06-backtesting-parity.md) | Backtesting Parity | 🔲 Not started |
| [07](v2/07-observability-and-auditability.md) | Observability & Auditability | 🔲 Not started |
| [08](v2/08-where-does-ai-belong.md) | Where Does AI Actually Belong? | 🔲 Not started |
| [09](v2/09-agent-architecture.md) | Agent Architecture & Boundaries | 🔲 Not started |
| [10](v2/10-phased-roadmap.md) | Phased Roadmap | 🔲 Not started |

## What We're Building

A multi-strategy paper trading system that streams real-time market data from Charles Schwab's API, executes three distinct strategies against live market conditions, and provides a full backtesting framework against historical minute bar data.

**Strategies:**
- QQQ 0DTE Rejection — key level proximity, heavyweight EMA alignment, rejection candle confirmation
- QQQ 0DTE Breakout — momentum-based breakout through key levels
- MNQ Futures Momentum — London session levels, IFVGs, 9:30 AM sweep entries

**v1 Reference:** [investment-center](https://github.com/cszlo/investment-center) — the working v1 system this rebuilds.
