# QuickShow

A modern movie ticket booking platform where users can browse movies (from TMDB), view showtimes added by admins, select seats, and book tickets. Built with a **React** frontend and an **Express + MongoDB** backend. Authentication is handled by **Clerk** (with optional custom JWT), deployment is optimized for **Vercel**, and media metadata is sourced from **TMDB**.

> **Status:** Active development. This README is comprehensive and designed to help you run, develop, and deploy QuickShow end‑to‑end.

---

## ✨ Features

* **Movie catalog (TMDB)**: Fetch now‑playing / popular movies via TMDB API and store selected titles in MongoDB with `tmdbId` linkage.
* **Admin shows management**: Create shows per movie with date/time, screen, pricing, and seat layout.
* **Showtime discovery**: List all shows; filter by movie and date.
* **Seat selection**: Interactive seat map with live availability.
* **Bookings & tickets**: Reserve seats, generate booking confirmation.
* **Authentication**: Clerk-based auth; optional custom JWT for service-to-service calls.
* **Dashboard**: KPIs for active shows, total bookings, and revenue.
* **Scalable architecture**: Separate frontend and backend; environment-based configuration; MongoDB via Mongoose models.

---

## 🧱 Tech Stack

**Frontend**

* React + Vite (or CRA) (TypeScript optional)
* React Router, Axios/Fetch
* Tailwind CSS / Bootstrap (choose one)

**Backend**

* Node.js + Express
* Mongoose (MongoDB)
* Clerk (Auth) + optional custom JWT
* TMDB API integration
* Inngest (optional) for background jobs / webhooks

**DevOps / Hosting**

* Vercel (Frontend + possibly serverless API)
* MongoDB Atlas
* Environment variables via Vercel / .env files

---

## 📁 Monorepo / Folder Structure

```
QuickShow/
├─ README.md
├─ package.json                # (optional root if using workspaces)
├─ frontend/
│  ├─ src/
│  │  ├─ components/
│  │  ├─ pages/
│  │  ├─ hooks/
│  │  ├─ routes/
│  │  ├─ lib/
│  │  └─ App.jsx/tsx
│  ├─ public/
│  ├─ index.html
│  ├─ vite.config.ts | webpack.config.js
│  └─ package.json
└─ backend/
   ├─ src/
   │  ├─ configs/
   │  │  └─ db.ts/js
   │  ├─ controllers/
   │  │  └─ show.controller.ts/js
   │  ├─ models/
   │  │  ├─ Movie.ts/js
   │  │  ├─ Show.ts/js
   │  │  └─ User.ts/js
   │  ├─ routes/
   │  │  ├─ show.routes.ts/js
   │  │  └─ index.ts/js
   │  ├─ middlewares/
   │  │  ├─ auth.ts/js (Clerk/JWT)
   │  │  └─ error.ts/js
   │  ├─ services/
   │  │  └─ tmdb.service.ts/js
   │  ├─ utils/
   │  ├─ inngest/
   │  ├─ server.ts/js
   │  └─ app.ts/js
   ├─ vercel.json (if using Vercel functions)
   └─ package.json
```

*Your actual structure may differ—update the tree if needed.*

---

## 🔐 Environment Variables

Create `.env` files in **frontend/** and **backend/**. Never commit these.

### Backend `.env`

```
# Mongo
MONGODB_URI=mongodb+srv://<user>:<pass>@cluster0.xxxxx.mongodb.net
MONGODB_DB=quickshow

# Server
PORT=5000
NODE_ENV=development

# Clerk
CLERK_PUBLISHABLE_KEY=<your_clerk_publishable_key>
CLERK_SECRET_KEY=<your_clerk_secret_key>
CLERK_JWT_ISSUER=<issuer_url_if_applicable>

# Custom JWT (optional)
JWT_SECRET=<strong_random_secret>
JWT_EXPIRES_IN=1d

# TMDB
TMDB_API_KEY=<your_tmdb_api_key>
TMDB_BASE_URL=https://api.themoviedb.org/3

# Inngest (optional)
INNGEST_EVENT_KEY=<inngest_event_key>
INNGEST_SIGNING_KEY=<inngest_signing_key>
```

### Frontend `.env`

```
VITE_API_URL=http://localhost:5000
VITE_CLERK_PUBLISHABLE_KEY=<your_clerk_publishable_key>
VITE_TMDB_IMAGE_BASE=https://image.tmdb.org/t/p
```

> **Note:** The backend should consistently use **TMDB `tmdbId`** for lookups and foreign keys in `Show` documents. Avoid using Mongo `_id` for movie routing.

---

## 🗄️ Data Models (Mongoose)

### Movie

```ts
{
  _id: ObjectId,
  tmdbId: Number,            // unique
  title: String,
  overview: String,
  posterPath: String,
  backdropPath: String,
  genres: [String],
  runtime: Number,
  releaseDate: String,
  language: String,
  createdAt: Date,
  updatedAt: Date
}
```

**Index**: `tmdbId` unique. Ensure you never insert `null` here (see Troubleshooting).

### Show

```ts
{
  _id: ObjectId,
  movie: ObjectId,           // ref: Movie._id
  tmdbId: Number,            // mirror for convenience (optional)
  screen: String,
  date: String,              // YYYY-MM-DD
  startTime: String,         // HH:mm
  price: Number,
  seatLayout: {
    rows: Number,
    cols: Number,
    unavailable: ["A1", "B5", ...]
  },
  createdAt: Date,
  updatedAt: Date
}
```

### User

```ts
{
  _id: ObjectId,
  name: String,
  email: String,
  image: String,
  clerkId: String,           // from Clerk
  createdAt: Date,
  updatedAt: Date
}
```

### Booking (if applicable)

```ts
{
  _id: ObjectId,
  show: ObjectId,            // ref: Show
  user: ObjectId,            // ref: User
  seats: [String],           // ["A1","A2"]
  amount: Number,
  status: "CONFIRMED" | "CANCELLED",
  paymentId: String,
  createdAt: Date
}
```

---

## 🔌 API Overview

Base URL: `http://localhost:5000/api`

### Movies

* `GET /movies/now-playing` — fetch now‑playing from TMDB (pass through or cached)
* `POST /movies` — create a movie from TMDB `tmdbId` (admin)
* `GET /movies` — list movies in DB
* `GET /movies/:tmdbId` — details by TMDB id

### Shows

* `POST /shows` — create a show (admin)
* `GET /shows` — list all shows
* `GET /shows/by-movie/:tmdbId` — list shows for a specific movie (use TMDB id)

### Bookings

* `POST /bookings` — create booking
* `GET /bookings/me` — my bookings

> Protect admin routes with Clerk roles or a custom middleware.

---

## ▶️ Local Development

### 1) Clone

```bash
git clone https://github.com/KikaniMeet/quickshow
cd QuickShow
```

### 2) Install dependencies

```bash
# Backend
cd backend
npm install

# Frontend (new terminal)
cd ../frontend
npm install
```

### 3) Configure env

Create `.env` in both `backend/` and `frontend/` as described above.

### 4) Run

```bash
# Backend
cd backend
npm run dev  # e.g., nodemon server.js

# Frontend
cd ../frontend
npm run dev   # Vite dev server
```

Open [http://localhost:5173](http://localhost:5173) (Vite default) and ensure `VITE_API_URL` points to your backend.

---

## 🧪 Seed & Test Data

Optionally add a seed script to create sample movies/shows:

```bash
# Example
node scripts/seed.js          # inserts movies by tmdbId and a few shows
```

**Seed ideas**

* Insert a few TMDB titles by id
* Generate shows for today+7 days
* Block a few seats to simulate partial occupancy

---

## 🚀 Deployment (Vercel + MongoDB Atlas)

### Frontend

1. Push `frontend/` to GitHub.
2. Import the project to Vercel.
3. Set `VITE_API_URL`, `VITE_CLERK_PUBLISHABLE_KEY`, and other envs in Vercel.

### Backend

**Option A: Vercel Serverless Functions**

* Place API in `api/` or configure `vercel.json`.
* Use Edge/runtime where appropriate.
* Add `MONGODB_URI`, `CLERK_*`, `TMDB_*` envs in Vercel.

**Option B: Dedicated Node Server**

* Deploy to services like Render, Railway, Fly.io, or a VPS.
* Whitelist IPs if using MongoDB Atlas.

> Ensure CORS is configured for your frontend domain.

---

## 🧰 Troubleshooting

### `E11000 duplicate key error ... index: tmdbId_1 dup key: { tmdbId: null }`

* Cause: Attempted to insert a Movie without `tmdbId` (or `null`).
* Fix: Validate `tmdbId` in controllers before `Movie.create`. Ensure unique index exists and `tmdbId` is required.

### `.env not loaded / MONGODB_URI is not defined`

* Fix: Ensure `dotenv` is imported early (e.g., `import "dotenv/config"`) **before** using `process.env`. Verify `.env` file path and Vercel env settings.

### Shows not appearing in UI

* Check that `Show.movie` references an existing `Movie._id` and **also** ensure queries use TMDB `tmdbId` consistently on both frontend and backend routes.
* Confirm your dashboard uses the correct identifiers and your aggregation joins on `movie` or `tmdbId` as intended.

### Date validation error (Django note if relevant)

* API expects `YYYY-MM-DD`. Validate and sanitize inputs on the frontend before POST.

---

## 🔒 Security Notes

* Never expose secrets in the frontend or in the repo.
* Validate user auth on backend for bookings and admin routes.
* Sanitize inputs to avoid injection.
* Rate-limit sensitive endpoints as needed.

---

Support
For support, email elyseniyibizi502@gmail.com or create an issue in the GitHub repository.
---
## 🗺️ Roadmap

* Payments integration (Razorpay/Stripe)
* Email confirmations & PDFs
* Show seat‑by‑seat pricing tiers
* Caching TMDB responses
* Advanced filters and search

---

## 🤝 Contributing

1. Fork the repo and create a feature branch.
2. Commit with conventional messages.
3. Open a PR with screenshots and a clear description.

---

## 📸 Screenshots

*Add screenshots or GIFs here*

* Home / Movies Grid
* Movie Detail + Showtimes
* Seat Selection
* Booking Confirmation
* Admin Dashboard

---

## 📜 License

MIT (or add your chosen license here)

---

## 🙏 Acknowledgements

* [TMDB](https://www.themoviedb.org/) for movie data and images
* [Clerk](https://clerk.com/) for authentication
* [Vercel](https://vercel.com/) for hosting

---

## 📝 Notes for Maintainers

* Prefer `tmdbId` for routing; keep a unique index on `Movie.tmdbId`.
* Ensure Mongoose connection logs on `connected` and exits on fatal errors.
* Keep controller logic slim—delegate to services for TMDB and business rules.
* Add integration tests for booking flows and seat locking.


