# PDFPro Editor

Full-featured browser-based PDF editor with freemium model (10 free edits) and Google AdSense ads.

## Quick Start

```bash
# Install all dependencies
cd frontend && npm install
cd ../backend && npm install

# Start frontend (http://localhost:3000)
cd frontend && npm run dev

# Start backend (http://localhost:5000) — optional, needed for Stripe payments
cd backend && npm run dev
```

## Features

| Feature | Free | Premium |
|---------|------|---------|
| Upload PDF | ✅ | ✅ |
| Add text annotations | ✅ (10 edits) | ✅ Unlimited |
| Highlight & draw | ✅ (10 edits) | ✅ Unlimited |
| Rotate pages | ✅ (10 edits) | ✅ Unlimited |
| Digital signatures | ✅ (10 edits) | ✅ Unlimited |
| Redact text | ✅ (10 edits) | ✅ Unlimited |
| Merge PDFs | ✅ (10 edits) | ✅ Unlimited |
| Add/delete pages | ✅ (10 edits) | ✅ Unlimited |
| Download edited PDF | ✅ | ✅ |
| Ads | Yes | No |

## Revenue Streams

### 1. Google AdSense
Replace `ca-pub-XXXXXXXXXXXXXXXX` in `frontend/index.html` with your real AdSense publisher ID.

Ad placements:
- **Leaderboard** (728×90) — top and bottom of upload page
- **Sidebar** (160×600) — left and right of upload page  
- **Rectangle** (300×250) — center of upload page, editor right panel
- **Banner** (728×90) — editor header (free users only)
- **Interstitial** — shown every 3 edits to free users

### 2. Stripe Payments (freemium)
Copy `.env.example` to `.env` and fill in your Stripe keys:

```
STRIPE_SECRET_KEY=sk_live_...
STRIPE_PRICE_MONTHLY=price_...   # $4.99/month
STRIPE_PRICE_ANNUAL=price_...    # $29.99/year  
STRIPE_PRICE_LIFETIME=price_...  # $79.99 once
```

Create products in [Stripe Dashboard](https://dashboard.stripe.com/products).

## Tech Stack

- **Frontend**: React 18, TypeScript, Vite, Tailwind CSS
- **PDF Rendering**: PDF.js (Mozilla)
- **PDF Editing**: pdf-lib (client-side, no server needed)
- **Payments**: Stripe Checkout
- **Ads**: Google AdSense
- **Backend**: Express.js + Stripe webhooks

## Architecture

All PDF editing happens **client-side** using `pdf-lib`. No PDFs are sent to the server.
The backend only handles Stripe payment sessions and webhooks.

Edit count is tracked in `localStorage` with a unique session ID.
