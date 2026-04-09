# Current Project

## What We Are Building
A greenfield rebuild of a monolithic Python trading engine. The goal is a clean,
scalable trading system that handles three strategies well. The architecture
is TBD — that is what this planning phase is for.

## Current Phase
Pre-build architecture and planning. No code until the following are resolved:
- Overall system architecture
- Where and how AI adds value (if at all)
- Agent design (if agents are the right call)
- Data flow between components
- Implementation roadmap with clear phases

## Strategies to Implement
1. QQQ 0DTE Rejection Strategy
   - Key level proximity (within 0.15% of level)
   - Heavyweight alignment (≥3/5 MSFT/NVDA/GOOGL/AAPL/AMZN above/below 9 EMA)
   - Rejection candle confirmation
   - Active window: 10:00–11:30 AM ET

2. QQQ 0DTE Breakout Strategy
   - Shares some logic with rejection in old system — separation approach TBD

3. MNQ Futures Momentum Strategy
   - London session highs/lows
   - Inverse Fair Value Gaps (IFVGs)
   - 9:30 AM sweep detection, midpoint entries
   - Backtested ~59% win rate under strict parameters

## What Good Looks Like
- Architecture decisions made deliberately, not assumed
- Each strategy's entry/exit/stop/target logic documented independently
- No redundancy or overlap between strategies
- A phased implementation roadmap before any code is written

## What to Avoid
- Writing code before architecture is settled
- Repeating the monolith problem from the old system
- Carrying over assumptions from the old system without questioning them
- Letting familiarity with LangGraph or any other tool bias the architecture decision