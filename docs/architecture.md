# Architecture: V-Trader

Status: APPROVED
Owner: Tech Lead / Architect
Created: 2026-03-28

## Approach Selection

### Approach A: Decoupled Full-Stack (FastAPI + React) ✅ Selected

Python FastAPI backend + React frontend, fully decoupled. Backend handles data fetching, Greeks calculation, and backtesting engine. Frontend handles interaction and visualization.

- **Effort:** L (Human team: ~3 weeks / CodeBuddy: ~2-3 hours)
- **Risk:** Low
- **Pros:** Clean architecture, mature Python financial ecosystem, strong React visualization ecosystem, natural extensibility
- **Cons:** Two projects to maintain, two services to run locally

### Approach B: Python Full-Stack (Dash/Streamlit)

Pure Python approach using Dash or Streamlit for the frontend.

- **Effort:** M (Human team: ~1.5 weeks / CodeBuddy: ~1-2 hours)
- **Risk:** Med
- **Pros:** Single language, quick to start
- **Cons:** Low UI ceiling, limited interactivity, cannot achieve modern UX standards

### Approach C: Next.js + Python Microservice

Next.js full-stack + Python computation microservice.

- **Effort:** L (Human team: ~3 weeks / CodeBuddy: ~2-3 hours)
- **Risk:** Low
- **Pros:** Single-entry experience, high UI flexibility
- **Cons:** Dual-language complexity, microservice communication design

## Recommended Approach

**Approach A: Decoupled Full-Stack (FastAPI + React)**

This is the best fit for this project. The Python backend can fully leverage the financial computing ecosystem (numpy/scipy/pandas/mibian), while FastAPI provides high-performance async APIs. The React frontend enables the best interactive experience, paired with Recharts/Lightweight Charts for professional-grade visualization. Clean separation between frontend and backend allows independent debugging and iteration.

## Technology Stack

**Backend (Python FastAPI):**
- FastAPI — High-performance async API framework
- pandas / numpy — Data processing and numerical computation
- scipy — Black-Scholes model, Greeks calculation
- yfinance — Yahoo Finance data fetching
- SQLite — Local data cache (historical data, user configuration)
- APScheduler — Scheduled data refresh tasks

**Frontend (React):**
- React 18 + TypeScript
- Vite — Build tool
- TailwindCSS — Styling system
- Recharts / Lightweight Charts — Financial charts
- TanStack Query — Server state management
- Zustand — Client state management

## System Architecture

```
┌─────────────────────────────────────────────────┐
│                  React Frontend                  │
│  ┌───────────┬───────────┬──────────┬─────────┐ │
│  │ Dashboard │ Option    │ Strategy │ Scanner │ │
│  │           │ Chain     │ Builder  │         │ │
│  ├───────────┼───────────┼──────────┼─────────┤ │
│  │ Greeks    │ P&L       │ Backtest │ Alerts  │ │
│  │ Panel     │ Visualizer│ Engine   │         │ │
│  └───────────┴───────────┴──────────┴─────────┘ │
│                    │ REST API                     │
└────────────────────┼────────────────────────────┘
                     │
┌────────────────────┼────────────────────────────┐
│              FastAPI Backend                      │
│  ┌───────────┬───────────┬──────────┬─────────┐ │
│  │ Market    │ Greeks    │ Strategy │ Backtest│ │
│  │ Data API  │ Calculator│ Analyzer │ Engine  │ │
│  ├───────────┼───────────┼──────────┼─────────┤ │
│  │ IV        │ Option    │ Alert    │ Cache   │ │
│  │ Analyzer  │ Chain     │ System   │ Layer   │ │
│  └───────────┴───────────┴──────────┴─────────┘ │
│                    │                              │
│  ┌─────────────────┼──────────────────────────┐  │
│  │    Data Sources: Yahoo Finance / IBKR API  │  │
│  └────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────┘
```

## API Design

- RESTful endpoints under `/api/v1/`
- Standard response format: `{ data: T, error?: string }`
- Use HTTP status codes correctly (200, 400, 404, 500)
- All financial data endpoints must include data freshness timestamp

## Directory Structure

```
v-trader/
├── backend/          # Python FastAPI backend
│   ├── app/
│   │   ├── api/      # API route handlers
│   │   ├── core/     # Configuration, shared utilities
│   │   ├── models/   # Data models (Pydantic)
│   │   ├── services/ # Business logic (Greeks calc, data fetching, etc.)
│   │   └── main.py   # FastAPI application entry point
│   ├── tests/
│   ├── requirements.txt
│   └── .venv/        # Python virtual environment (git-ignored)
├── frontend/         # React frontend
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── services/  # API client functions
│   │   ├── stores/    # Zustand stores
│   │   ├── types/     # TypeScript type definitions
│   │   └── utils/
│   ├── package.json
│   └── vite.config.ts
├── docs/             # Design docs, API specs
└── README.md
```
