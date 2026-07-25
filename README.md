# LiveWire Frontend

The frontend for LiveWire — a real-time sports broadcast dashboard. It connects to the LiveWire backend over REST and WebSocket to display live matches and commentary as they happen, with no polling or manual refresh required.

**Live site:** https://live-wire-frontend-c1gkesanr-sanjeevcoder.vercel.app
**Backend repo:** https://github.com/Sanj-2/LiveWire

## What it does

- Fetches the current list of matches from the backend on load.
- Lets you select a match to "watch live" — this subscribes to that match over WebSocket.
- Displays incoming commentary instantly as it's broadcast from the server, without needing to refresh the page.
- Shows a live connection status indicator (connected / reconnecting / offline) so you always know if you're receiving real-time updates.

## Tech Stack

- **React** — UI
- **WebSocket API** — real-time subscription to match commentary
- **Vite** — build tool / dev server

## Getting Started

### Prerequisites
- Node.js
- npm
- The [LiveWire backend](https://github.com/Sanj-2/LiveWire) running locally or deployed

### Installation

```bash
git clone https://github.com/Sanj-2/LiveWire-frontend.git
cd LiveWire-frontend
npm install
```

### Environment Variables

Create a `.env` file in the root directory:

```env
VITE_API_BASE_URL="http://localhost:8000"
VITE_WS_BASE_URL="ws://localhost:8000/ws"
```

For a deployed backend, use its HTTPS URL and `wss://` instead:

```env
VITE_API_BASE_URL="https://your-backend-url.onrender.com"
VITE_WS_BASE_URL="wss://your-backend-url.onrender.com/ws"
```

### Running locally

```bash
npm run dev
```

Open the local URL shown in your terminal (usually `http://localhost:5173`).

## How it works

1. On load, the app fetches `/matches` from the backend to show the current match list.
2. Clicking "Watch Live" on a match sends a `subscribe` message over the WebSocket connection for that match's ID.
3. Any new commentary the backend broadcasts for that match arrives instantly over the same WebSocket connection and is rendered live in the commentary feed.
4. The connection status badge reflects the real-time state of the WebSocket connection (connected, reconnecting, or offline).

## Deployment

Deployed on [Vercel](https://vercel.com). Environment variables must be set in the Vercel project settings (Settings → Environment Variables) and a redeploy triggered after any change, since Vite bakes env vars in at build time.
