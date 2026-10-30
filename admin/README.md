# Forever — Admin & Seller Panel

Next.js 15 (App Router) dashboard for super-admins and sellers: catalog and variant management, orders, transactions, reviews moderation, users and 2FA security.

## Setup

```bash
cp .env.example .env   # then edit values
npm install
npm run dev            # http://localhost:5174
```

| Variable | Required | Purpose |
| --- | --- | --- |
| `NEXT_PUBLIC_BACKEND_URL` | yes (build) | Base URL of the Express API |
| `NEXT_PUBLIC_STORE_URL` | yes (build) | Storefront URL for cross-links |

`NEXT_PUBLIC_*` values are inlined at build time; `npm run build` fails fast if they are missing.

## Scripts

- `npm run dev` — dev server on port 5174
- `npm run build` / `npm start` — production build and server
