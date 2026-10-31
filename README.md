# 🛍️ Forever — Multi-Vendor E-Commerce Platform

Forever is a full-stack, multi-vendor e-commerce platform made of three apps: a **Next.js storefront** for buyers, a **Next.js admin panel** for sellers and admins, and an **Express 5 + MongoDB REST API**. It covers secure authentication with optional 2FA, role-based access control, Cloudinary media uploads, product reviews, coupons, and payments through Razorpay, Stripe and Cash on Delivery.

![Next.js](https://img.shields.io/badge/Next.js_15-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React_19-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS_4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js_20+-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express_5-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Razorpay](https://img.shields.io/badge/Razorpay-0C2451?style=for-the-badge&logo=razorpay&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white)

---

## 🌐 Live Demo

| App | URL |
| --- | --- |
| 🛒 Storefront | https://forever-frontend-two-azure.vercel.app |
| 🛠 Admin Panel | https://forever-admin-tau-mauve.vercel.app |
| ⚙️ REST API | https://forever-backend-psi-nine.vercel.app |

---

## 🚀 Features

### 🛒 Storefront (buyers)

- Register / login with JWT and optional TOTP two-factor authentication
- Home, collection (search and filters), product detail, about and contact pages
- Product variants with per-variant pricing and images
- Cart, checkout and coupon codes (e.g. `FIRST` — free delivery on the first order)
- Razorpay online payments and Cash on Delivery
- Order history and profile management
- Product reviews and ratings
- Newsletter subscription

### 🛠 Admin Panel (sellers & admins)

- Seller registration and login; env-configured super-admin login
- Analytics dashboard: KPI cards, sales charts, recent orders, low-stock alerts and restock actions
- Product management: add, edit, discount and remove, with multi-image Cloudinary uploads and variant pricing
- Per-product insights dashboard
- Category management
- Order management with status updates
- Transactions view with refunds
- Review moderation (approve / reject, including email action links)
- User management and role assignment (admin only)
- Security settings with 2FA setup and backup codes
- Light / dark theme and command palette

---

## 🧑‍💻 Tech Stack

| Layer | Technologies |
| --- | --- |
| Storefront & Admin | Next.js 15 (App Router), React 19, Tailwind CSS v4, Axios, React Toastify, Lucide icons (admin) |
| Backend | Node.js 20+, Express 5, MongoDB + Mongoose 9, JWT, bcrypt, Multer, express-rate-limit, Nodemailer, otplib + qrcode (2FA) |
| Media | Cloudinary |
| Payments | Razorpay, Stripe (optional), Cash on Delivery |
| Shared UI | `design-tokens` package (JSON / JS / CSS tokens used by both Next.js apps) |
| Deployment | Vercel (both Next.js apps and the serverless Express API) |

---

## 📁 Project Structure

```
E-Commerce/
├── package.json        # root scripts that drive all three apps
├── backend/            # Express 5 REST API
│   ├── src/
│   │   ├── config/        # Cloudinary setup
│   │   ├── controllers/   # cart, category, order, payment, product, review, user
│   │   ├── db/            # MongoDB connection
│   │   ├── middlewares/   # auth, admin auth, RBAC/ACL, rate limiting, validation, payment verification, uploads
│   │   ├── models/        # Mongoose schemas
│   │   ├── routes/        # /api/v1 routers
│   │   ├── scripts/       # migrations, seeding and verification scripts
│   │   ├── utils/         # ApiError/ApiResponse, mail, TOTP, pricing helpers
│   │   ├── app.js
│   │   └── server.js
│   └── vercel.json
├── frontend/           # Next.js storefront (port 5173)
├── admin/              # Next.js admin panel (port 5174)
└── design-tokens/      # shared design tokens
```

---

## 🧱 Architecture

```
Storefront (Next.js)      Admin Panel (Next.js)
          \                     /
           ▼                   ▼
     Express 5 REST API  (/api/v1)
   CORS → rate limit → sanitise → JWT auth → RBAC
                    │
         Controllers / Mongoose models
           │            │             │
        MongoDB     Cloudinary   Razorpay / Stripe
```

---

## 🔗 API Reference

Base URL: `/api/v1` · Health check: `GET /` → `"Forever eCommerce API is running..."`

| Area | Routes |
| --- | --- |
| Auth | `POST /user/register` · `/user/login` · `/user/admin` · `/user/register-seller` · `/user/logout` |
| 2FA | `POST /user/2fa/setup` · `/2fa/verify-setup` · `/2fa/verify-login` · `/2fa/disable` · `/2fa/regenerate-backup-codes` · `GET /user/2fa/status` |
| Profile | `GET/PUT /user/profile` · `POST /user/update-profile` |
| Users (admin) | `GET /user/all` · `POST /user/create` · `/user/update-user` · `/user/role` · `/user/delete` · `DELETE /user/:id` |
| Products | `GET /product/list` · `POST /product/single` · seller/admin: `POST /product/add` · `/update` · `/discount` · `/remove` · `GET /product/insights/:productId` |
| Categories | `GET /category` · `/category/list` · `/category/:id` · admin: `POST /category` · `PUT/DELETE /category/:id` |
| Cart | `POST /cart/get` · `/cart/add` · `/cart/update` |
| Orders | `POST /order/checkout` · `/order/place` · `/order/razorpay` · `/order/verifyRazorpay` · `/order/validate-coupon` · `GET /order/userorders` · seller/admin: `GET /order/list` · `/order/dashboard` · `POST /order/status` · `/order/delete` |
| Payments | `POST /payment/checkout` · `/payment/verify` · `/payment/webhook` · `GET /payment/order/:orderId` · seller/admin: `GET /payment/list` · `POST /payment/refund` |
| Reviews | `GET /review/product/:productId` · `/review/my-review/:productId` · `POST /review/add` · `DELETE /review/:id` · seller/admin: `GET /review/admin/list` · `POST /review/admin/update-status` |
| Newsletter | `POST /newsletter/subscribe` |

---

## 🔐 Security

- JWT authentication with server-side token revocation (logout blacklist)
- Role-based access control (buyer / seller / admin) with ownership checks
- Optional TOTP two-factor authentication with backup codes
- CORS restricted to the configured storefront and admin origins (plus `CORS_ORIGINS`)
- Rate limiting on all API routes, stricter on credential endpoints
- NoSQL-injection input sanitisation and 16 KB request body limit
- Server-side pricing — client-sent prices are never trusted
- Razorpay signature verification (timing-safe HMAC) and signed webhooks
- Image uploads restricted to image MIME types, 5 MB each

---

## ⚙️ Environment Variables

Each app ships an `.env.example`. Copy it to `.env` and fill it in — `.env` files are git-ignored.

| App | Template | Required |
| --- | --- | --- |
| backend | `backend/.env.example` | `MONGODB_URI`, `JWT_TOKEN_SECRET`, `ADMIN_JWT_SECRET` (the server refuses to start without them), plus `FRONTEND_URL` / `ADMIN_URL` for CORS |
| frontend | `frontend/.env.example` | `NEXT_PUBLIC_BACKEND_URL`, `NEXT_PUBLIC_ADMIN_URL` (build fails without them), `NEXT_PUBLIC_RAZORPAY_KEY_ID` |
| admin | `admin/.env.example` | `NEXT_PUBLIC_BACKEND_URL`, `NEXT_PUBLIC_STORE_URL` (build fails without them) |

Optional backend settings:

- **Cloudinary** — `CLOUDINARY_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_SECRET_KEY`
- **Razorpay** — `RAZORPAY_KEY_ID`, `RAZORPAY_KEY_SECRET`, `RAZORPAY_WEBHOOK_SECRET`
- **Stripe** — `STRIPE_SECRET_KEY`, `STRIPE_PUBLISHABLE_KEY`, `STRIPE_WEBHOOK_SECRET`
- **Email** — `SMTP_*` or `GMAIL_USER` / `GMAIL_APP_PASSWORD` (emails are logged to the console if neither is set)
- **Super admin** — `ADMIN_EMAIL` / `ADMIN_PASSWORD` (the env super-admin login is disabled while `ADMIN_PASSWORD` is empty)

`ALLOW_MOCK_PAYMENTS` and `ALLOW_UNSIGNED_WEBHOOKS` are test-only switches — leave them unset in production.

---

## ▶️ Run Locally

Requires **Node.js 20+** and a MongoDB instance (local or Atlas).

```bash
git clone https://github.com/anshgangwar786/E-Commerce.git
cd E-Commerce
npm run install:all

cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
cp admin/.env.example admin/.env
# edit the three .env files

npm run dev:backend    # http://localhost:4000
npm run dev:frontend   # http://localhost:5173
npm run dev:admin      # http://localhost:5174
```

### Root scripts

| Script | Description |
| --- | --- |
| `npm run install:all` | Install dependencies for backend, frontend and admin |
| `npm run dev:backend` / `dev:frontend` / `dev:admin` | Start an app in development mode |
| `npm run build:frontend` / `build:admin` / `build:all` | Production builds of the Next.js apps |
| `npm run start:backend` / `start:frontend` / `start:admin` | Start an app in production mode |

### Backend maintenance scripts

Run from `backend/`:

```bash
npm run migrate:orders              # migrate legacy order documents
npm run backfill:category-emojis    # add emojis to existing categories
```

---

## 🚢 Deployment

All three apps are deployed on **Vercel**. The backend runs as a serverless function via [backend/vercel.json](backend/vercel.json).

Production checklist:

- `NODE_ENV=production` on the backend (hides internal error details, disables localhost CORS)
- Strong, distinct `JWT_TOKEN_SECRET` and `ADMIN_JWT_SECRET`
- `FRONTEND_URL` / `ADMIN_URL` set to the real deployed origins
- `RAZORPAY_WEBHOOK_SECRET` configured if webhooks are used
- `NEXT_PUBLIC_*` variables set in the frontend and admin build environments

---

## 📊 Roadmap

- Wishlist
- httpOnly-cookie sessions instead of localStorage tokens
- Automated test suite and CI
- Order tracking notifications

---

## 👨‍💻 Author

**Ansh Gangwar**

Full-Stack Developer<br>
Software Engineer 🚀

🔗 GitHub: https://github.com/anshgangwar786<br>
🔗 LinkedIn: https://www.linkedin.com/in/ansh-gangwar/
