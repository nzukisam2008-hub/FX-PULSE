# FX Pulse — Live Trading Intelligence

A professional-grade trading assistant dashboard built with Next.js 16, TypeScript, Tailwind CSS 4, and shadcn/ui. Combines live charts from TradingView, market sentiment from MyFXBook, currency strength from FXBlue, an economic calendar, a 110+ indicator library, AI-powered screenshot analysis, and a full trading calculator suite.

![FX Pulse](https://img.shields.io/badge/Next.js-16.1.3-black) ![TypeScript](https://img.shields.io/badge/TypeScript-5-blue) ![Tailwind](https://img.shields.io/badge/Tailwind-4-38bdf8) ![License](https://img.shields.io/badge/License-MIT-green)

---

## Features

### 5 Tabs, 1 Dashboard

| Tab | Description |
|---|---|
| **Dashboard** | Live TradingView chart (12 pairs × 6 intervals), FXBlue currency strength heat map, MyFXBook community sentiment, 4 mini sparkline cards, multi-asset market overview watchlist |
| **Indicators** | 6 live trade signal cards at the top, Day Trading / Scalping mode toggle (5-min / 15-min refresh), Pair Trend Scanner (12 pairs), 112-indicator library with BUY/SELL/NEUTRAL signals, win rates, and confidence scores |
| **News** | Live TradingView economic calendar timeline + Forex Factory feed with day-grouped events, Before/After News trend panels, validation flags (TRUE/FALSE/PENDING), and impact labels |
| **D-Analysis** | Upload screenshots from Barchart, Fastbull, Options Tables, or any trading tool — AI vision model analyzes each screenshot and combines them into a single trading recommendation (direction, confidence, entry, SL, TP). Includes a preset strategy reference library. |
| **Calculator** | 9 trading calculators: Position Size, Pip Value, Profit/Loss, Margin, Risk/Reward, Pivot Points (Standard/Fibonacci/Camarilla), Fibonacci Retracement, Compound Interest, Options Greeks (Black-Scholes) |

---

## Tech Stack

- **Framework:** Next.js 16 (App Router, Turbopack)
- **Language:** TypeScript 5
- **Styling:** Tailwind CSS 4 + shadcn/ui (New York style)
- **Icons:** Lucide React
- **AI Vision:** Z-AI Web Dev SDK (for D-Analysis screenshot analysis)
- **Data Sources:** TradingView widgets, Forex Factory JSON feed, MyFXBook widget, FXBlue
- **Package Manager:** Bun

---

## Project Structure

```
src/
├── app/
│   ├── layout.tsx                      # Root layout (dark theme, fonts)
│   ├── page.tsx                        # Main page with 5-tab switcher
│   ├── globals.css                     # Global styles + dark theme tokens
│   └── api/
│       ├── ff-news/route.ts            # Forex Factory calendar proxy (JSON + XML merge)
│       └── analyze-screenshots/route.ts # AI vision screenshot analysis
│
├── components/
│   ├── dashboard/
│   │   ├── TabNav.tsx                  # 5-tab navigation (Dashboard/Indicators/News/D-Analysis/Calculator)
│   │   ├── DashboardHeader.tsx         # Header with logo, live clock, symbol/interval pills
│   │   ├── DashboardFooter.tsx         # Footer with disclaimer + last-refreshed time
│   │   ├── FxPulseLogo.tsx             # SVG logo
│   │   ├── LiveClock.tsx               # Africa/Nairobi live clock
│   │   ├── SymbolSelector.tsx          # 12-pair dropdown
│   │   └── IntervalSelector.tsx        # 6-interval toggle (1m/5m/15m/1H/4H/1D)
│   │
│   ├── trading/
│   │   ├── symbols.ts                  # Pair definitions, intervals, timezone
│   │   ├── use-tradingview-widget.ts   # Hook for injecting TradingView widgets
│   │   ├── TradingViewTickerTape.tsx   # Full-width scrolling ticker
│   │   ├── TradingViewAdvancedChart.tsx# Main candlestick chart
│   │   ├── TradingViewTechnicalAnalysis.tsx # Symbol snapshot widget
│   │   ├── TradingViewMiniSymbol.tsx   # Mini sparkline cards
│   │   ├── TradingViewMarketOverview.tsx # Multi-tab watchlist
│   │   ├── FXBlueCurrencyStrength.tsx  # Forex heat map (FXBlue proxy)
│   │   ├── MyFXBookSentiment.tsx       # Community outlook (official JS widget)
│   │   └── resilient-iframe.tsx        # Fallback-aware iframe component
│   │
│   ├── indicators/
│   │   ├── indicators-data.ts          # 112 indicators, time-bucket signal rotation
│   │   ├── TradeSignals.tsx            # 6 live trade signal cards
│   │   └── IndicatorsTab.tsx           # Full indicators tab + Pair Trend Scanner
│   │
│   ├── news/
│   │   ├── trend-logic.ts              # Trend rules, validation logic, impact labels
│   │   └── NewsTab.tsx                 # TradingView timeline + FF calendar (day-grouped)
│   │
│   ├── danalysis/
│   │   └── DAnalysisTab.tsx            # Screenshot upload + AI analysis + strategy reference
│   │
│   ├── calculator/
│   │   └── CalculatorTab.tsx           # 9 trading calculators
│   │
│   └── ui/                             # shadcn/ui components (40+ files)
│
├── hooks/
│   ├── use-mobile.ts
│   └── use-toast.ts
│
└── lib/
    ├── utils.ts                        # cn() helper
    └── db.ts                           # Prisma client

public/
└── strategies/
    └── barchart-options-reversal.png   # Preset strategy reference photo
```

---

## Installation

### Prerequisites

- Node.js 18+ or Bun
- npm/bun package manager

### Setup

```bash
# Clone the repository
git clone https://github.com/yourusername/fx-pulse.git
cd fx-pulse

# Install dependencies
bun install
# or
npm install

# Create .env file
echo "DATABASE_URL=file:./db/custom.db" > .env

# Run the development server
bun run dev
# or
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Build for Production

```bash
bun run build
bun run start
```

---

## Usage Guide

### 1. Dashboard Tab

- **Chart:** Select from 12 pairs (EUR/USD, GBP/USD, USD/JPY, USD/CHF, AUD/USD, USD/CAD, NZD/USD, EUR/JPY, GBP/JPY, XAU/USD, BTC/USD, ETH/USD) and 6 intervals (1m, 5m, 15m, 1H, 4H, 1D). Full drawing toolbar, OHLC readout, EMA overlay.
- **Currency Strength:** Live forex heat map showing relative strength of 8 major currencies.
- **Sentiment:** MyFXBook community outlook showing retail long/short positioning for 45+ pairs.
- **Market Overview:** Multi-tab watchlist (Overview / Forex / Crypto / Indices) with live prices.

### 2. Indicators Tab

- **Trading Style Toggle:** Switch between **Day Trading** (112 indicators, 5-min refresh) and **Scalping** (60 fast indicators, 15-min refresh).
- **Live Trade Signals:** 6 auto-generated trade cards with entry, SL, TP1/TP2/TP3, R:R, confidence, and indicator confluence.
- **Pair Trend Scanner:** Pick any of 12 pairs to see the overall trend (BULLISH/BEARISH/NEUTRAL) derived from all indicators, with confidence %, signal breakdown, and top confluence indicators.
- **Indicator Library:** 112 indicators across 6 categories (Trend, Momentum, Volatility, Volume, Support/Resistance, Pattern). Each card shows win rate (60–80%), confidence, signal direction, and category. Search, filter, and sort.

### 3. News Tab

- **Live Economic Calendar:** TradingView timeline widget showing real-time forex events.
- **Economic Events:** Forex Factory feed grouped by day (like FF's calendar). Each event card shows:
  - Previous / Forecast / Actual values
  - Before News direction panel (forecast vs previous)
  - After News direction panel (actual vs forecast, or PENDING)
  - Validation flag (TRUE if both directions agree, FALSE if they disagree)
  - Market impact label (High / Medium / Low / Watch Only / No Impact)
  - "View on FF" link for actual values

### 4. D-Analysis Tab

- **Strategy Reference:** Preset strategy photos (Barchart Options Reversal) with key conditions.
- **Upload Screenshots:** Drag & drop or browse PNG/JPG/WEBP from any trading tool (Barchart, Fastbull, Options Tables, TradingView, etc.).
- **AI Analysis:** Click "Analyze & Combine" — the AI vision model reads each screenshot, extracts key data, and combines them into a single recommendation:
  - Direction (BULLISH / BEARISH / NEUTRAL)
  - Confidence %
  - Rationale
  - Entry / Stop Loss / Take Profit
- **Individual Analyses:** Each screenshot's analysis is shown below the combined recommendation.

### 5. Calculator Tab

9 calculators in a tabbed interface:

| Calculator | Inputs | Outputs |
|---|---|---|
| Position Size | Account balance, risk %, pair, entry, stop | Risk amount, stop distance, pip value, lot size, units |
| Pip Value | Pair, lot size, price | Pip value, per-pip value, position size |
| Profit / Loss | Pair, lot size, entry, exit, direction | Pips, P/L in $ |
| Margin | Pair, lot size, leverage, price | Notional value, required margin |
| Risk / Reward | Entry, stop, take profit | Risk, reward, R:R ratio |
| Pivot Points | High, low, close, type | PP, R1-R3, S1-S3 (Standard/Fibonacci/Camarilla) |
| Fibonacci | Swing high, swing low, direction | 0/23.6/38.2/50/61.8/78.6/100% levels |
| Compound | Principal, rate, periods, compoundings | Final amount, total interest |
| Options Greeks | Spot, strike, days, IV, rate, type | Price, Delta, Gamma, Theta, Vega, Rho (Black-Scholes) |

---

## API Routes

### `GET /api/ff-news`

Proxies the Forex Factory economic calendar. Fetches both the JSON feed (for event data) and the XML feed (for event-page URLs), merges them, and marks each event with `isReleased` based on the current time. Cached for 90 seconds.

**Response:**
```json
{
  "source": "Forex Factory",
  "fetchedAt": 1698000000000,
  "cached": true,
  "count": 75,
  "events": [
    {
      "title": "CPI m/m",
      "country": "AUD",
      "date": "2026-11-24T19:30:00-05:00",
      "impact": "High",
      "forecast": "0.4%",
      "previous": "0.8%",
      "actual": "",
      "url": "https://www.forexfactory.com/calendar/...",
      "isReleased": false
    }
  ]
}
```

### `POST /api/analyze-screenshots`

Analyzes uploaded screenshots using the Z-AI vision language model and combines them into a trading recommendation.

**Request:**
```json
{
  "images": [
    { "id": "img-1", "source": "Barchart", "dataUrl": "data:image/png;base64,..." }
  ]
}
```

**Response:**
```json
{
  "analyses": [
    { "id": "img-1", "source": "Barchart", "summary": "...", "keyData": ["..."] }
  ],
  "combinedMove": {
    "direction": "BEARISH",
    "confidence": 80,
    "rationale": "...",
    "entry": "1.0965",
    "stopLoss": "1.0990",
    "takeProfit": "1.0920"
  }
}
```

---

## Data Sources & Limitations

| Source | What it provides | Limitation |
|---|---|---|
| **TradingView** | Live charts, ticker tape, heat map, market overview, timeline | Widgets load via external scripts (5–15s initial load) |
| **Forex Factory** | Economic calendar (forecast, previous) | Public JSON feed does **not** include actual values — click "View on FF" for actuals |
| **MyFXBook** | Community outlook (retail long/short sentiment) | Main site blocks iframes; uses official JS widget from `widgets.mfbcdn.net` |
| **FXBlue** | Currency strength meter | Main site blocks iframes; uses TradingView forex heat map as live in-page alternative |
| **Z-AI VLM** | Screenshot analysis for D-Analysis | Server-side only; takes ~11 seconds per analysis |

---

## Key Technical Decisions

### Time-Bucket Signal Rotation

Indicator signals are salted by a time bucket so they rotate on a schedule:
- **Day Trading mode:** 5-minute bucket (signals change every 5 min)
- **Scalping mode:** 15-minute bucket (signals change every 15 min)

Win rates stay stable per indicator (they're claimed historical figures), but the live signal direction shifts to simulate "fresh market reads."

### MyFXBook Widget Integration

MyFXBook blocks third-party iframes (`X-Frame-Options: SAMEORIGIN`). The dashboard uses MyFXBook's **official JavaScript widget** from `widgets.mfbcdn.net/scripts/fxOutlook.js`, which renders the Community Outlook table directly into the page. The widget's validation script requires a specific DOM structure (`.powered` script tag + `.myfxbookLink` credit link with `href="https://www.myfxbook.com"`), which is reproduced exactly. The `document.write()` error path is neutralized so a validation failure can't wipe the dashboard.

### Forex Factory Actual Values

The FF public JSON/XML feeds do not include actual values — even for past events. The FF website is behind Cloudflare's managed challenge and cannot be scraped server-side. The dashboard marks events as `RELEASED_PENDING_ACTUAL` when the event time has passed, and provides "View on FF" / "View Actual" links to Trading Economics and the specific FF event page.

### AI Screenshot Analysis

The D-Analysis tab uses a two-step process:
1. **Per-screenshot analysis:** The VLM reads each image, extracts key data (indicator readings, sentiment, option flow, signals), and returns a structured summary.
2. **Combined recommendation:** All individual analyses are fed into a text-only LLM call that synthesizes them into a single trading move (direction, confidence, entry, SL, TP).

---

## Disclaimer

**This dashboard is for informational and educational purposes only and is not financial advice.**

- Trading involves substantial risk of loss. Never risk more than you can afford to lose.
- Indicator signals are mechanically derived from deterministic hashes — they are **not** real-time market analysis.
- Trade signals on the Indicators tab are deterministic demo data for layout demonstration.
- Win rates shown are claimed historical figures, not guaranteed future performance.
- AI-generated analyses (D-Analysis) may misread screenshots or miss context. Always verify data yourself.
- Economic calendar data may lag up to 2 minutes behind the live Forex Factory site.
- Always combine these tools with your own technical analysis and proper risk management.

---

## License

MIT License — feel free to use, modify, and distribute.

---

## Author

Built with [FX Pulse](https://github.com/yourusername/fx-pulse) — Live Trading Intelligence.
