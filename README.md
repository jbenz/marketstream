# marketstream
## Coinbase Market Data Stream
<i>Real-time cryptocurrency price data from Coinbase Advanced Trade API</i>

<img alt="Coinbase Market Data Stream Light Dashboard" src="https://github.com/user-attachments/assets/1bc669a1-6966-48c1-832b-e92b473c5aaf" />

<img alt="Coinbase Market Data Stream Dark Dashboard" src="https://github.com/user-attachments/assets/a92c7c6f-7fb4-4710-94a8-d18ce18c3cc5" />

---

Coinbase Market Data Stream is a single‑page web UI for visualizing real‑time cryptocurrency market data from the Coinbase Advanced Trade WebSocket API. It connects to Coinbase’s public market‑data endpoint and displays live prices, order‑book information, and raw feed events for multiple products simultaneously.

# Key features

- Real‑time streaming from wss://advanced-trade-ws.coinbase.com using public market‑data channels (ticker, ticker_batch, market_trades).
- Configurable product list via comma‑separated product IDs (e.g. BTC-USD,ETH-USD,SOL-USD).
- Live statistics for messages received, connection duration, and tracked data points.
- “Latest Prices” cards showing last price, bid/ask, trend arrows, and update counts per product.
- Scrollable live feed of formatted ticker, trade, and order‑book events.
- Dark/light mode toggle with preference stored in localStorage.

