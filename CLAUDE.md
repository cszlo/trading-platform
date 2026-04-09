# Identity

You are helping Clay rebuild a professional-grade algorithmic trading platform
from scratch. We are currently in the architecture and planning phase.

## On Session Start
- Load ../CLAUDE.md for global workspace context
- Load ../skills/tone.md for communication style

## What This Project Is
A greenfield rebuild of a monolithic Python trading engine. The goals are:
- Clean separation of concerns (the old system's core problem)
- Scalable, maintainable strategy execution
- Some form of intelligent reasoning layer for market regime and risk
- Real-time data handling without the fragility of the old while loop

## Collaboration Style
- Guide, don't just generate. Explain the approach, suggest patterns, provide scaffolding and boilerplate
but allow me to own the code. You're primary goal is to teach and guide as opposed to do.

## Current Phase
**Pre-build planning.** No architectural or implementation decisions are final.
Everything is up for discussion. Challenge assumptions freely.

## Project Rules
- No code until architecture is settled and agreed upon
- Challenge assumptions, especially around execution risk and data integrity
- Explore multiple approaches before recommending one
- Flag edge cases: stale quotes, stream disconnects, partial fills, market
  close/holidays, restart recovery for open trades
- Think in expected value and drawdown, not just win rate
- The old system lives in ../investment-center/ — reference it freely
- Always use a test driven development mindset. Write tests first, write code second when possible

## Known Constraints (non-negotiable)
- Language: Python
- Broker: Charles Schwab API (streaming + REST)
- Database: PostgreSQL
- Instruments: QQQ (0DTE options), MNQ futures, QQQ heavyweights
- Data: Tick-level options + Greeks, VIX minute OHLC, QQQ underlying

## Open Questions (to resolve during planning)
- Agent orchestration approach — LangGraph, custom, or something else?
- Local vs API inference — Ollama, Anthropic API, or hybrid?
- How much of the system actually needs AI vs deterministic logic?
- Monorepo or separate repos for execution vs reasoning layers?
- Deployment target — AWS (like legacy) or different?
- Do we need agents? Where does AI add real value vs. deterministic logic?
- If agents, what roles? Coordinator pattern, pipeline, or something else entirely?
- How should agents communicate — direct calls, message queue, shared state?
- Single agent with context switching vs. multiple specialized agents?