# Interaction Design: V-Trader

Status: APPROVED
Owner: UX / Interaction Designer
Created: 2026-03-29
Design review: All 7 dimensions reviewed via /plan-design-review

## Information Architecture

**Layout Model:** Tab-based switching within the main workspace.

**Page Structure:**
- `/` — Workspace (core analysis interface, tab-based)
- `/scanner` — IV Scanner (standalone fullscreen)
- `/backtest` — Backtest Engine (standalone fullscreen)
- `/alerts` — Alert Management (standalone fullscreen)

**Navigation:**
- 1st level: Left sidebar (4 top-level entries, always visible)
  - 🏠 Workspace (default)
  - 📊 Scanner
  - 🔬 Backtest
  - ⚠ Alerts
- 2nd level: Top bar ticker search (global, available on any page)
- 3rd level: Workspace tab bar (switch between analysis views)

## Workspace Tabs (5 tabs)

1. **📈 Overview Tab (default)**
   - 1st: Stock price chart (top half, primary visual focus)
   - 2nd: Key metric cards row (price, change%, IV, IV Rank, next earnings date)
   - 3rd: Quick action area (view option chain, build strategy, add to watchlist)

2. **📋 Option Chain Tab**
   - 1st: Expiration date selector (horizontal tabs, nearest expiry highlighted)
   - 2nd: Option chain table (Call left | Strike center | Put right, ITM background color)
   - 3rd: Bottom Greeks summary bar

3. **🔧 Strategy Tab**
   - 1st: Strategy template selector / current strategy legs list
   - 2nd: Interactive P&L payoff diagram (primary visual focus)
   - 3rd: Strategy Greeks + key metrics (breakeven, max profit/loss, win rate)

4. **📊 Greeks Tab**
   - 1st: Delta/Gamma/Theta/Vega 2×2 dashboard
   - 2nd: Greeks vs. underlying price curves
   - 3rd: Greeks vs. time decay curves

5. **📉 Volatility Tab**
   - 1st: IV vs HV comparison chart
   - 2nd: Volatility smile/skew curve
   - 3rd: IV historical trend chart

## Page Layout

```
┌─────────────────────────────────────────────────────────────┐
│  TOP BAR: Ticker Search [____AAPL____] | Watchlist | ⚙     │
├──────────┬──────────────────────────────────────────────────┤
│          │  [Overview] [Chain] [Strategy] [Greeks] [Vol]    │
│  SIDEBAR │  ┌──────────────────────────────────────────┐   │
│          │  │                                          │   │
│  🏠 Work  │  │         Active Tab Content               │   │
│  📊 Scan  │  │                                          │   │
│  🔬 Back  │  │                                          │   │
│  ⚠ Alert │  │                                          │   │
│          │  │                                          │   │
│          │  └──────────────────────────────────────────┘   │
├──────────┴──────────────────────────────────────────────────┤
│  BOTTOM BAR: Position summary | Composite Greeks | Updated  │
└─────────────────────────────────────────────────────────────┘
```

## Interaction State Matrix

**First-open experience:** Default loads SPY data so the user sees a complete workspace immediately.

| Feature | Loading | Empty | Error | Success | Partial |
|---------|---------|-------|-------|---------|---------|
| Ticker Search | Skeleton below search box | "Enter a ticker to start" | "XXXX not found" + suggestions | Auto-switch to Overview | — |
| Overview Price Chart | Pulsing chart placeholder | "Search a ticker to start" | "Data load failed" + retry | Smooth chart render | Show available data + note |
| Overview Metric Cards | Each card skeleton shimmer | Cards show "—" | Card shows "!" + tooltip | Numbers fade in | Partial metrics, missing show — |
| Option Chain Table | 10-row skeleton table | "No options data for this ticker" | "Option data load failed" + retry | Rows stagger fade-in | Show loaded expirations only |
| Greeks Dashboard | Dashboard digits pulse | "Select an option contract" | "Calculation failed" + reason | Smooth value transition | — |
| Strategy P&L Chart | Chart placeholder + progress | "Add strategy legs to begin" | "Calculation error" + details | Curve draw animation | <2 legs: show incomplete note |
| IV Scanner Results | Table skeleton + progress % | "No tickers match criteria" | "Scan interrupted" + partial results | Results table fade-in | Real-time show during scan |
| Backtest Results | Progress bar + stage indicator | "Configure params to start" | "Backtest failed" + reason | Dashboard fade-in | — |

## Component Behavior Specifications

### Option Chain Table
- Layout: Call data | Strike column | Put data (symmetrical 3-column)
- Call columns: Bid | Ask | Last | Volume | OI | Delta | IV
- Strike column: centered, ATM row highlighted (yellow left border 3px)
- Put columns: Delta | IV | OI | Volume | Last | Ask | Bid
- ITM rows: subtle background tint
- Hover row: full row highlight, [B][S] buttons appear at row edges
- Click [B]/[S]: adds leg to strategy, row shows selected state (green left bar)
- Expiration tabs: horizontal scroll, format "Apr 18 (21d)" with days remaining
- Sort: click column header, default ascending by strike
- Row height: 32px, monospace font for numbers

### Price Chart
- Type: Candlestick (default) / Line (toggle)
- Toolbar: time range button group [1D] [1W] [1M] [3M] [1Y] [All]
- Crosshair follows mouse with price + time display
- Mouse wheel zoom, drag to pan
- Volume bars overlaid at bottom (20% chart height)

### Greeks Dashboard
- Layout: 2×2 grid (Delta | Gamma / Theta | Vega)
- Each cell: main value large mono font (20px), label small gray (12px), change arrow green/red
- Hover: tooltip with one-line Greek explanation
- Value transitions: 300ms ease

### P&L Chart
- Type: Area + line overlay
- Profit area: semi-transparent green fill. Loss area: semi-transparent red fill
- Breakeven: vertical dashed line + label. Max profit/loss: horizontal dashed line + label
- Current price: highlighted vertical solid line
- Hover: shows P&L amount at any price point
- Multiple lines: expiration P&L + current P&L + custom date P&L
