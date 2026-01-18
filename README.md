# marketstream
## Coinbase Market Data Stream
<i>Real-time cryptocurrency price data from Coinbase Advanced Trade API</i>

Coinbase Market Data Stream is a single‑page web UI for visualizing real‑time cryptocurrency market data from the Coinbase Advanced Trade WebSocket API. It connects to Coinbase’s public market‑data endpoint and displays live prices, order‑book information, and raw feed events for multiple products simultaneously.

# Key features

- Real‑time streaming from wss://advanced-trade-ws.coinbase.com using public market‑data channels (ticker, ticker_batch, market_trades).
- Configurable product list via comma‑separated product IDs (e.g. BTC-USD,ETH-USD,SOL-USD).
- Live statistics for messages received, connection duration, and tracked data points.
- “Latest Prices” cards showing last price, bid/ask, trend arrows, and update counts per product.
- Scrollable live feed of formatted ticker, trade, and order‑book events.
- Dark/light mode toggle with preference stored in localStorage.

# Light Dashboard

<img alt="Coinbase Market Data Stream Light Dashboard" src="https://github.com/user-attachments/assets/1bc669a1-6966-48c1-832b-e92b473c5aaf" />

# Dark Dashboard

<img alt="Coinbase Market Data Stream Dark Dashboard" src="https://github.com/user-attachments/assets/a92c7c6f-7fb4-4710-94a8-d18ce18c3cc5" />

---



# Coinbase Market Data Stream

A lightweight web UI for streaming real‑time cryptocurrency market data from the **Coinbase Advanced Trade WebSocket API**. It connects to Coinbase’s public market data endpoint and visualizes live prices, order book snapshots, and raw feed events for selected products.

## Features

- Connects to Coinbase Advanced Trade **market data WebSocket** at `wss://advanced-trade-ws.coinbase.com`.
- Supports multiple products via comma‑separated **product IDs** (e.g. `BTC-USD,ETH-USD,SOL-USD`).
- Channel selector for:
    - `ticker` – real‑time price updates on trades.
    - `ticker_batch` – batched ticker updates.
    - `market_trades` – trade snapshots/updates.
- Live stats:
    - Messages received.
    - Connection duration.
    - Distinct data points (tracked products).
- “Latest Prices” cards showing:
    - Last price, best bid/ask, trend arrow, and update count.
- Scrollable **live feed** of human‑readable events.
- **Dark mode** toggle with persisted preference (localStorage).


## Getting started

### Prerequisites

- Any modern browser (Firefox, Chrome, Safari, Edge).
- Optional but recommended: Python 3 for a quick local HTTP server.

Coinbase **API keys are not required** for public market‑data channels such as `ticker`, `ticker_batch`, `market_trades`.

### Run locally

1. Clone or download this repository.
2. From the project directory, start a simple web server (example with Python 3):

```bash
python3 -m http.server 8000
```

3. Open the app in your browser:

```text
http://localhost:8000/Coinbase%20Market%20Data%20Stream.html
```

4. In the UI:
    - Enter one or more product IDs.
    - Choose a channel (e.g. **Level 2 Orderbook**).
    - Click **Connect** to begin streaming.

### Controls

- **Product IDs**: Comma‑separated list of Advanced Trade product IDs (e.g. `BTC-USD`).
- **Channel**: WebSocket channel to subscribe to:
    - `ticker`, `ticker_batch`, `market_trades`.
- **Max Feed Entries**: Maximum number of log entries kept in the live feed.
- **Connect**: Open WebSocket and subscribe to the selected channel/products.
- **Disconnect**: Unsubscribe and close the WebSocket.
- **Clear Feed**: Clear the live feed area without disconnecting.
- **Dark Mode**: Toggle between light and dark themes; choice is saved per browser.


## Architecture

All logic lives in a single HTML file:

- `CoinbaseMarketStream` class encapsulates:
    - WebSocket lifecycle (`connect`, `disconnect`, `subscribe`, `unsubscribe`).
    - Message routing based on `message.channel` (`ticker`, `ticker_batch`, `market_trades`).
    - Per‑product state tracking in a `Map` (`dataPoints`).
    - DOM rendering for stats, price cards, and the live feed.

Per‑channel handlers:

- **Ticker / ticker_batch**: Parses `events[].tickers[]` entries and updates last price, best bid/ask, and 24h volume per product.
- **Market trades**: Parses `events[].trades[]` and stores last trade price, side, and size.
- **Level 2**: Interprets order book updates to derive best bid/ask and a mid‑price per product, then logs a compact summary entry for the feed.


## Customization

- Add or remove default products by editing the `value` of the `#productIds` input.
- Adjust price formatting rules in `formatPrice` and `addCommas`.
- Change card layout or styling via the CSS at the top of the HTML file.
- Extend channel support (e.g. `candles`, `status`, `user`) by adding new handlers wired from `handleMessage` in line with Coinbase’s documented channel schemas.

