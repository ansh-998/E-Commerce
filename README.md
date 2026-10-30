# 🛍️ Forever --- Full Stack eCommerce Website

Forever is a modern Full-Stack eCommerce Web Application built using
Next.js, Node.js, Express, and MongoDB with secure authentication and
multiple payment integrations including Stripe, Razorpay, and Cash on
Delivery.

------------------------------------------------------------------------

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white)
![Razorpay](https://img.shields.io/badge/Razorpay-0C2451?style=for-the-badge&logo=razorpay&logoColor=white)

Production-ready MERN eCommerce platform featuring JWT authentication, role-based admin dashboard, product management system, and Stripe + Razorpay payment gateway integration deployed on Vercel serverless infrastructure.

------------------------------------------------------------------------

## 🌐 Live Project Links

🚀 Frontend (User Panel)  
https://forever-frontend-two-azure.vercel.app

🛠 Admin Dashboard  
https://forever-admin-tau-mauve.vercel.app

⚙️ Backend REST API  
https://forever-backend-psi-nine.vercel.app

------------------------------------------------------------------------

## 📌 Project Overview

Forever allows users to:

-   Register and login securely
-   Browse products
-   View product details
-   Add items to cart
-   Place orders
-   Choose payment method
-   View order history

Admin & Sellers can:

-   Register and login securely as Seller / Admin
-   Add products with Cloudinary image uploads
-   Remove products
-   View all customer orders and dashboard statistics
-   Update order status

------------------------------------------------------------------------

## 🚀 Features

### 👤 User Features

-   JWT Authentication
-   Product Listing Page
-   Product Detail Page
-   Cart System
-   Order Placement System
-   Order History
-   Stripe Payment Integration
-   Razorpay Payment Integration
-   Cash on Delivery (COD)

### 🛠️ Admin & Seller Features

-   Seller Registration with store name, email, password, and phone
-   Dual Login: Environment Super Admin & Registered Database Sellers
-   Interactive Dashboard with total revenue, orders, and sales charts
-   Add Products with multi-image Cloudinary upload
-   Remove Products
-   View All Orders with real-time status update dropdowns

### 🔐 Security Features

- JWT authentication
- Role-based admin authorization
- Protected API routes
- Secure image upload validation
- Payment verification middleware

------------------------------------------------------------------------

## 🧑‍💻 Tech Stack

Frontend & Admin:

-   Next.js (App Router)
-   React 19
-   Tailwind CSS v4 & PostCSS
-   Axios
-   React Toastify

Backend:

-   Node.js
-   Express.js
-   MongoDB
-   JWT Authentication
-   Multer (Image Upload Middleware)

Payments:

-   Stripe
-   Razorpay
-   Cash on Delivery

Deployment:

-   Vercel (Frontend)
-   Vercel (Admin Panel)
-   Vercel Serverless Backend

------------------------------------------------------------------------

## 📁 Folder Structure

```
Forever-Ecommerce/
│
├── frontend/
├── admin/
└── backend/
```

## 🧱 Application Architecture

Client (Frontend / Admin)\
        ↓\
REST API (Express Serverless Backend)\
        ↓\
Authentication Middleware (JWT)\
        ↓\
Controllers\
        ↓\
MongoDB Database\
        ↓\
Cloudinary (Image Storage)\
        ↓\
Stripe / Razorpay (Payments)

------------------------------------------------------------------------

## 🔗 Backend API Routes

Base URL: `/api/v1` · Health check: `GET /` → `"Forever eCommerce API is running..."`

| Area | Routes |
| --- | --- |
| User / auth | `POST /user/register` · `POST /user/login` · `POST /user/admin` · `POST /user/register-seller` · `POST /user/logout` |
| 2FA | `POST /user/2fa/setup` · `/2fa/verify-setup` · `/2fa/verify-login` · `/2fa/disable` · `GET /user/2fa/status` |
| Profile | `GET/PUT /user/profile` · admin: `GET /user/all` · `POST /user/create` · `POST /user/update-user` · `POST /user/delete` |
| Products | `GET /product/list` · `POST /product/single` · seller/admin: `POST /product/add` · `/update` · `/discount` · `/remove` · `GET /product/insights/:productId` |
| Categories | `GET /category` · `GET /category/:id` · admin: `POST /category` · `PUT/DELETE /category/:id` |
| Cart | `POST /cart/get` · `/cart/add` · `/cart/update` |
| Orders | `POST /order/checkout` · `/order/place` · `/order/razorpay` · `/order/verifyRazorpay` · `/order/validate-coupon` · `GET /order/userorders` · seller/admin: `GET /order/list` · `POST /order/status` · `GET /order/dashboard` |
| Payments | `POST /payment/verify` · `POST /payment/webhook` · seller/admin: `GET /payment/list` · `POST /payment/refund` |
| Reviews | `GET /review/product/:productId` · `POST /review/add` · `DELETE /review/:id` · seller/admin: `GET /review/admin/list` · `POST /review/admin/update-status` |
| Newsletter | `POST /newsletter/subscribe` |

------------------------------------------------------------------------

## 🔐 Authentication & Security

-   JWT authentication with server-side token revocation (logout blacklist)
-   Role-based access control (buyer / seller / admin) with ownership checks
-   Optional TOTP two-factor authentication with backup codes
-   CORS restricted to the configured storefront and admin origins
-   Rate limiting on all API routes, stricter on credential endpoints
-   NoSQL-injection input sanitisation
-   Server-side pricing (client-sent prices are never trusted)
-   Razorpay signature verification (timing-safe HMAC) and signed webhooks
-   Image uploads restricted to image MIME types, 5 MB each

------------------------------------------------------------------------

## 🔐 Environment Variables

Each app ships an `.env.example`. Copy it to `.env` and fill it in; `.env` files are git-ignored.

| App | Template | Must set |
| --- | --- | --- |
| backend | `backend/.env.example` | `MONGODB_URI`, `JWT_TOKEN_SECRET`, `ADMIN_JWT_SECRET` (server refuses to start without them), plus `FRONTEND_URL` / `ADMIN_URL` for CORS |
| frontend | `frontend/.env.example` | `NEXT_PUBLIC_BACKEND_URL`, `NEXT_PUBLIC_ADMIN_URL` (build fails without them) |
| admin | `admin/.env.example` | `NEXT_PUBLIC_BACKEND_URL`, `NEXT_PUBLIC_STORE_URL` (build fails without them) |

The env super-admin login is only enabled when `ADMIN_PASSWORD` is set. Leave `ALLOW_MOCK_PAYMENTS` and `ALLOW_UNSIGNED_WEBHOOKS` unset in production.

------------------------------------------------------------------------
## ▶️ Run Project Locally

Requires Node.js 20+ and a MongoDB instance.

```bash
git clone <your-repo-url>
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

## 🚢 Production Checklist

- `NODE_ENV=production` on the backend (hides internal error details, disables localhost CORS)
- Strong, distinct `JWT_TOKEN_SECRET` and `ADMIN_JWT_SECRET`
- `FRONTEND_URL` / `ADMIN_URL` set to the real deployed origins
- `RAZORPAY_WEBHOOK_SECRET` configured if webhooks are used
- `NEXT_PUBLIC_*` vars set in the frontend/admin build environment

## 💳 Payment Methods Supported

Stripe\
Razorpay\
Cash on Delivery (COD)

------------------------------------------------------------------------

## 📈 Project Highlights

✔ Full-stack MERN eCommerce platform  
✔ Role-based Admin Dashboard  
✔ Stripe + Razorpay payment gateway integration  
✔ JWT-based authentication & authorization  
✔ Secure image upload using Cloudinary + Multer  
✔ Serverless backend deployment on Vercel

## 🏗 Architecture Highlights

- RESTful API architecture with versioning (/api/v1)
- MVC-based backend structure
- Middleware-based authentication & authorization
- MongoDB schema-based data modeling using Mongoose
- Cloudinary integration for image storage
- Payment verification workflow for Stripe & Razorpay
- Separate frontend and admin panel applications

------------------------------------------------------------------------

## 🌍 Deployment

Project deployed on **Vercel Serverless Infrastructure**

Frontend: https://forever-frontend-two-azure.vercel.app

Admin Panel: https://forever-admin-tau-mauve.vercel.app

Backend API: https://forever-backend-psi-nine.vercel.app

------------------------------------------------------------------------

## 📊 Future Improvements

-   Wishlist Feature
-   httpOnly-cookie sessions instead of localStorage tokens
-   Automated test suite and CI
-   Order tracking notifications

------------------------------------------------------------------------

## 👨‍💻 Author

**Rohansinh Vihol**

Full-Stack Developer  
BCA Student | Future Software Engineer 🚀

🔗 GitHub: https://github.com/RohansinhVihol  
🔗 LinkedIn: www.linkedin.com/in/rohansinhvihol
