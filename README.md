# Ravi AI Trading Pro
React + Vite client (`/client`) and Express API (`/server`). Educational tool — not financial advice.

## Structure
server/index.js (market data proxy, optional AI, rate limit, validation) · client/src/{indicators,strategy,backtest}.js, App.jsx

## Run locally (Node 18+)
1. `cd server && cp .env.example .env && npm install && npm run dev`
2. `cd client && npm install && npm run dev` → open http://localhost:5173

## Market data
Default provider: Yahoo Finance chart endpoint (no key, unofficial, **delayed ~15 min**; intraday history is limited: 1m≈5d, 5m/15m≈1mo). Pick "Demo" in Settings to test offline — demo prices are generated and labelled DEMO. For licensed/real-time Indian data, add a provider (e.g. Zerodha Kite, Upstox, Twelve Data) in `server/index.js` `/api/candles`, keeping keys in `.env`. Verify symbols (e.g. TATAMOTORS.NS) with your provider.

## AI (optional)
Set `AI_API_KEY`, `AI_MODEL` (and `AI_API_URL` if not Anthropic) in `server/.env`. Without them the app uses the rule-based engine and says so.

## Deploy
Backend: Render/Railway/Fly — root `server`, start `npm start`, set env vars, `CORS_ORIGIN=<frontend URL>`.
Frontend: Vercel/Netlify/Cloudflare Pages — root `client`, build `npm run build`, output `dist`, env `VITE_API_URL=<backend URL>`.

## Troubleshooting
"Market data unavailable": provider blocked/rate-limited or market closed with no recent intraday data — try 1d or Demo. CORS error: fix `CORS_ORIGIN`. AI 501: key not set. Empty backtest: not enough candles in range.

## Not included (be aware)
No user login (none implemented rather than a fake one); settings and paper trades are stored in the browser; backtest exits at Target 2 only; no real-time streaming.
