# Forever — Storefront

Next.js 15 (App Router) customer storefront: catalog, product variants, cart, checkout (Razorpay / COD), orders, reviews and profile.

## Setup

```bash
cp .env.example .env   # then edit values
npm install
npm run dev            # http://localhost:5173
```

| Variable | Required | Purpose |
| --- | --- | --- |
| `NEXT_PUBLIC_BACKEND_URL` | yes (build) | Base URL of the Express API |
| `NEXT_PUBLIC_ADMIN_URL` | yes (build) | Admin panel URL for cross-links |
| `NEXT_PUBLIC_RAZORPAY_KEY_ID` | for online payments | Razorpay public key id |

`NEXT_PUBLIC_*` values are inlined at build time; `npm run build` fails fast if they are missing.

## Scripts

- `npm run dev` — dev server on port 5173
- `npm run build` / `npm start` — production build and server
