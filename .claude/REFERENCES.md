⚠️ This file contains sensitive infrastructure details. Never commit to a public repo.
# References

## Legacy System (../investment-center/)
Reference freely during planning and implementation. Do not modify.

### What Existed
- Monolithic Python engine, single while loop, multiple strategies
- Next.js frontend + FastAPI backend (investment-center-js/)
- Standalone premarket HTML report generator (premarket-report/)
- Config-driven via strategy.yaml (EMA period, proximity threshold, fees, time window)

### Legacy Architecture
```
Browser
├── REST /api/*  →  Next.js proxy  →  FastAPI at localhost:8000
└── WS ws://localhost:8000  →  FastAPI directly
FastAPI (api/)
└── imports broker/ from ../broker/
Data storage
├── ../data/<TICKER>/<interval>/*.csv   OHLCV candle files
├── trades.db                           Paper trades + Schwab accounts (SQLite)
└── market_data.db                      Candle cache (SQLite)
```

### Legacy Shared Modules
- broker/ — Schwab OAuth, OHLCV fetch, streaming, orders
- trading_core/ — config, data loading, key levels, indicators, heavyweights
- backtest/ — strategy execution against mock data

### Legacy Signal Logic (3 conditions, all required)
- C1 — Level proximity: QQQ within 0.15% of a key level
- C2 — Heavyweight alignment: ≥3/5 above/below 9 EMA
- C3 — Rejection candle: prior candle wicked into level, current body moves away

### Legacy Key Levels Derived
- Overnight high/low
- Prior RTH high/low
- Max pain
- Open interest levels
- Swing pivots

### Legacy Backend Modules
| File/Dir | Role |
|---|---|
| main.py | App entry — CORS, router registration, DB init |
| config.py | StrategyConfig dataclass loaded from strategy.yaml |
| db.py | SQLite helper for trades.db |
| market_data.py | Candle DB operations |
| routers/auth_router.py | Schwab OAuth + user identity |
| routers/live.py | Live trading endpoints + WebSocket stream (500ms loop) |
| routers/data.py | Data manager endpoints |
| strategy/signal.py | 3-condition signal logic (C1, C2, C3) |
| strategy/heavyweights.py | AAPL/MSFT/NVDA/AMZN/META 9-EMA tracking |
| strategy/levels/ | Key level derivation |
| execution/paper_trade.py | 2-contract paper trading (TP1, SL, breakeven, time stop) |
| execution/contracts.py | QQQ option OCC symbol formatting |

### Legacy Deployment (AWS)
- CloudFront → EC2 (FastAPI :8000, premarket-report :5050) + S3 (static frontend)
- Lambda@Edge: JWT auth, admin gating, path rewriting
- EC2: 54.221.246.205, SSH key in terraform/investment-center.pem
- Cognito User Pool: us-east-1_AHegTg5TD

### Legacy Auth & User System
- Cognito JWT cookie: trading_session
- Per-user Schwab OAuth, tokens stored in schwab_accounts table
- Any new OAuth flow revokes previous token — latest always written to schwab_token.json
- Admin users controlled via ADMIN_USERS env var

### Legacy DB Tables (trades.db)
| Table | Purpose |
|---|---|
| paper_trades | Trade history |
| user_settings | Per-user window_start/window_end |
| schwab_accounts | Per-user Schwab token + account hash |
| oauth_state | CSRF nonces for OAuth flow (5-min TTL) |

---

## Data Available
- Tick-level 0DTE options data (within $5 strike range of underlying)
- Greeks collected at tick level
- VIX minute OHLC
- QQQ underlying price (minute)
- Several years historical minute bar data
- PostgreSQL backend (target DB for rebuild)

---

## Strategy Notes

### QQQ 0DTE Rejection
- Active window: 10:00–11:30 AM ET (was overrideable in old system for testing)
- 2-contract paper trading: TP1, SL, breakeven stop, time stop
- OCC symbol formatting handled by execution/contracts.py in legacy

### QQQ 0DTE Breakout
- Distinct strategy from rejection but shared overlapping logic in old codebase
- Clean separation is a primary goal of the rebuild

### MNQ Momentum
- ~59% win rate backtested under strict parameters
- London session high/low as structural reference
- IFVGs as entry trigger
- 9:30 AM sweep detection with midpoint entries

---

## Premarket Report (Legacy Tool)
- Generates daily HTML report with AI-powered scenario commentary
- Uses Claude Sonnet 4.6 via Anthropic API
- Accessible at trading.clayszlosek.com/report (admin only)
- Imports trading_core from ../investment-center-js/ via sys.path
- Worth discussing during planning — potential input source for market context

---

## Schwab API Notes
- Streaming and REST are separate concerns in the legacy system
- Token management is fragile — any re-auth revokes previous token
- schwab_token.json must exist in repo root for streaming to work
- Credentials: SCHWAB_APP_KEY, SCHWAB_APP_SECRET, SCHWAB_CALLBACK_URL