# PRD: V-Trader — US Stock Options Trading Workstation

Status: APPROVED
Owner: Product
Created: 2026-03-28

## Problem Statement

Existing options trading tools present a dilemma: data-rich tools (IBKR TWS, ThinkorSwim) have terrible UI and are clunky to use; tools with good UX (TastyTrade, OptionStrat) lack analytical depth. As an active US stock options trader, switching between multiple websites and tools daily to manually check options data, calculate Greeks, and evaluate strategy P&L is extremely inefficient.

What's needed is a unified options trading workstation: **IBKR-level data depth + OptionStrat-level visualization + modern UI experience**.

## What Makes This Cool

This is a professional-grade options trading workstation built entirely for personal use. No compromises on any existing tool's limitations — comprehensive data, beautiful visualization, and fast interaction. A single interface covering the entire workflow from screening underlyings, analyzing volatility, building strategies, visualizing P&L, to backtesting. What used to take 30 minutes of pre-market preparation can now be done in 5 minutes.

## Constraints

- **Personal use only** — No user authentication, multi-tenancy, or permission management needed
- **Data sources** — Phase 1 uses free/low-cost APIs (Yahoo Finance, etc.), with IBKR API integration later
- **Local deployment** — Runs locally during development, no rush to deploy
- **Solo developer** — AI-assisted, iterating incrementally in a modular fashion

## Premises

1. Web application (browser-based), accessible from any device
2. Prioritize free APIs for data, with IBKR API integration later
3. Feature priority: ① Option chain + Greeks → ② Strategy builder + P&L chart → ③ IV scanner → ④ Backtesting → ⑤ AI/alerts/flow/earnings
4. Tech stack: Python FastAPI backend + React frontend (decoupled full-stack)
5. Skip user authentication and multi-tenancy, focus on trading analysis experience

## Feature Modules

### Phase 1: Option Chain Data + Greeks Analysis Panel
- Enter a ticker symbol to fetch the complete option chain (all expirations, strikes)
- Real-time display of Delta, Gamma, Theta, Vega, Rho
- Option chain table with sorting, filtering, and ITM/OTM highlighting
- Underlying stock price chart
- Implied volatility vs. historical volatility comparison

### Phase 2: Strategy Builder + P&L Visualization
- Common strategy templates: Covered Call, Protective Put, Bull/Bear Spread, Iron Condor, Straddle, Strangle, Butterfly, Calendar Spread
- Custom multi-leg strategy construction
- Interactive P&L chart (expiration P&L + P&L curves at any date)
- Break-even points, max profit, max loss, win rate calculation
- Composite Greeks panel (aggregate Greeks for the combined strategy)

### Phase 3: IV Scanner + Volatility Analysis
- IV Rank / IV Percentile market-wide scan
- Volatility smile/skew curve visualization
- Historical IV trend chart
- Filter underlyings by IV ranking
- Volatility anomaly detection alerts

### Phase 4: Backtesting Engine
- Select strategy + underlying + time range
- Simulate trades based on historical options data
- Statistical results: win rate, average return, max drawdown, Sharpe ratio
- Backtest result visualization (cumulative return curve, P&L distribution)

### Phase 5: 10x Features (Future)
- AI-assisted decision making: recommend strategies based on current market data
- Earnings calendar: earnings date annotation + historical earnings day volatility analysis
- Options flow monitoring: large order tracking, unusual volume
- Custom alerts: price/IV/Greeks condition-triggered notifications

## Open Questions

1. **IBKR API integration timing** — How far can free data sources support us? Are latency and data completeness sufficient?
2. **Historical options data source** — The backtesting engine requires historical options price data; free sources are limited. Is paid data needed?
3. **Real-time data refresh frequency** — For personal use, what polling interval is appropriate? 5 seconds? 30 seconds?
4. **Data persistence** — Is SQLite sufficient or is PostgreSQL needed?

## Success Criteria

- [ ] Display complete option chain + Greeks within 2 seconds of entering a ticker
- [ ] Build at least 8 common options strategies with P&L curve visualization
- [ ] IV scanner can scan and rank S&P 500 constituents
- [ ] Backtesting engine can process at least 1 year of historical data
- [ ] Overall UI experience is smooth, modern, and comparable to OptionStrat
- [ ] Reduce daily pre-market preparation time from 30 minutes to 5 minutes

## Roadmap

Implement by priority; each phase is usable upon completion:

1. **Phase 1 (Core Foundation)** — Set up project skeleton, implement option chain data fetching + Greeks calculation + basic UI
2. **Phase 2 (Strategy Analysis)** — Strategy builder + P&L visualization
3. **Phase 3 (Market Scanning)** — IV scanner + volatility analysis tools
4. **Phase 4 (Historical Validation)** — Backtesting engine
5. **Phase 5 (Intelligent Enhancement)** — AI recommendations, alerts, large order tracking, earnings calendar

Each phase is independently usable; there's no need to complete all phases before starting to use the tool.
