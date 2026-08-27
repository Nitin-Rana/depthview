# DEPTHVIEW

A live order-flow terminal for Binance — an order book heatmap, DOM ladder, volume profiles and liquidity-wall detection, in a single self-contained HTML file.

**Live:** https://nitin-rana.github.io/depthview/

No backend, no build step, no API keys. The page connects directly from your browser to Binance's public WebSocket and REST endpoints.

## What it shows

**Heatmap** — historical order book depth. Each column is a moment in time, each row a price level, colour = resting size. This is where liquidity was sitting, not just where price traded.

**Candlesticks** — real OHLC, backfilled from klines on load so the chart is populated immediately, then updated live from the trade tape.

**Order book ladder** — 16 levels per side: price, size, cumulative total, with an optional DOM heatmap tinting each row by resting size.

**Liquidity walls** — resting orders ≥5× the median level size, listed with USD notional and marked on the chart with a band, arrow and size label.

**CVP** — cumulative volume delta *by price level*. Green = net buying absorbed at that price, red = net selling. Shows where accumulation or distribution actually happened.

**SVP** — session volume profile with buy/sell split and a POC (point of control) line.

**Also:** cumulative delta chart, book imbalance meter, large-trade alerts with sound and browser notifications, manual price-alert lines (click the chart), time & sales tape, and for futures: funding rate, mark price, open interest and a live liquidation feed.

## Markets

Toggle **SPOT** / **FUTURES** in the top right.

Futures adds the liquidation feed, funding, mark price and open interest, plus symbols that have no spot listing — including **XAG/USDT (silver)**, **XAU/USDT (gold)** and newer perps like BTR, EVAA and RAVE.

## Controls

| Control | What it does |
|---|---|
| **+ ADD SYMBOL** | Search and open a symbol in a new tab |
| **Window** | Visible history: 5m → 4h |
| **Candles** / **Heatmap** | Show or hide each layer |
| **Colours** | Heatmap palette — Rainbow (Bookmap-style), Ice, Fire, or Mono |
| **DOM heat** | Tint ladder rows by resting size |
| Click chart | Drop a price alert line |
| Right-click a line | Remove it |

## Running locally

Open `index.html` directly in a browser, or serve it:

```bash
python -m http.server 8731
```

## Notes

Tick size is detected from the live book rather than hardcoded, so price precision and row aggregation are correct for any symbol — including ones not in the preset list.

Heatmap colour is normalised against a decaying reference maximum, not per-column, so a given colour means a consistent amount of liquidity over time and across markets.

The heatmap builds left-to-right in real time. Binance has no historical order-book API, so only candles can be backfilled — a shorter window fills faster.

This is a read-only market visualisation tool. It places no orders and handles no keys or credentials.
