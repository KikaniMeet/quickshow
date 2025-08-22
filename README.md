#  QuickShow

A modern movie ticket booking platform where users can browse movies (sourced from TMDB), view showtimes created by admins, select seats, and book tickets easily. Powered by a React frontend and an Express + MongoDB backend. Authentication is managed through Clerk (with optional custom JWT), deployments are streamlined via Vercel, and movie metadata is seamlessly integrated using the TMDB API.  
_Status: Active development_

---

##  Features

- **Movie Catalog (TMDB)**: Fetch "Now Playing" and "Popular" movies via TMDB API and store selected titles in MongoDB with `tmdbId` linkage.  
- **Admin Show Management**: Create, schedule, and manage showtimes with custom dates, screen layouts, pricing, and seat configurations.  
- **Showtime Discovery**: Browse and filter shows by movie title or date.  
- **Interactive Seat Selection**: Real-time interactive seat map for choosing available seats.  
- **Booking & Tickets**: Reserve seats and generate confirmation for completed bookings.  
- **Authentication**: Clerk-based authentication with optional custom JWT for inter-service communication.  
- **Admin Dashboard**: Monitor KPIs such as active shows, total bookings, and revenue for better insights.  
- **Scalable Architecture**: Decoupled frontend & backend, environment-based configuration, and well-defined models with Mongoose.  
:contentReference[oaicite:0]{index=0}

---

##  Tech Stack

| Layer      | Technologies |
|------------|--------------|
| **Frontend** | React (with Vite or CRA), React Router, Axios/Fetch, Tailwind CSS or Bootstrap |
| **Backend**  | Node.js, Express, MongoDB (via Mongoose), Clerk (Auth), TMDB API integration, optional Inngest for background jobs/webhooks |
| **Deployment** | Vercel (for frontend and serverless backend), MongoDB Atlas, `.env` + Vercel environment variables |
:contentReference[oaicite:1]{index=1}

---

##  Project Structure (Monorepo)

QuickShow/
├─ README.md
├─ frontend/
│ ├─ src/
│ │ ├─ components/
│ │ ├─ pages/
│ │ ├─ hooks/
│ │ ├─ routes/
│ │ ├─ lib/
│ │ └─ App.jsx / App.tsx
│ ├─ public/
│ ├─ index.html
│ ├─ vite.config.ts or webpack.config.js
│ └─ package.json
└─ backend/
├─ src/
│ ├─ configs/ (e.g., db.ts/js)
│ ├─ controllers/ (e.g., show.controller.ts/js)
│ ├─ models/ (Movie.ts/js, Show.ts/js, User.ts/js)
│ ├─ routes/ (show.routes.ts/js, index.ts/js)
│ ├─ middlewares/ (auth.ts/js, error.ts/js)
│ ├─ services/ (tmdb.service.ts/js)
│ ├─ utils/
│ ├─ inngest/ (optional)
│ ├─ server.ts/js
│ └─ app.ts/js
GitHub

yaml
Copy
Edit

---

##  Setup & Usage

###  Prerequisites

- Node.js (recommended v18+)
- MongoDB (Atlas or local)
- TMDB API key
- Clerk credentials (Client ID, Secret)
- Vercel account (optional but recommended for deployment)

###  Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/KikaniMeet/quickshow.git
Backend Setup

bash
Copy
Edit
cd quickshow/backend
npm install
cp .env.example .env
# Fill in:
# - MONGODB_URI
# - TMDB_API_KEY
# - CLERK_CLIENT_ID
# - CLERK_SECRET_KEY
npm run dev
Frontend Setup

bash
Copy
Edit
cd ../frontend
npm install
cp .env.example .env
# Fill in:
# - VITE_TMBD_API_KEY (if used)
# - VITE_AUTH_DOMAIN, VITE_CLERK_PUBLISHABLE_KEY
npm run dev
Access the App

Frontend: http://localhost:3000 (or Vite's port)

Backend: http://localhost:4000 (or configured port)

Admin Dashboard

Use a Clerk account to log in.

Navigate to admin panel to add shows, create seat layouts, and configure pricing.

Deployment
Using Vercel:

Connect the repository in Vercel.

Set environment variables for both frontend and backend.

Deploy frontend and backend as separate Vercel projects or a combined monorepo.

MongoDB Hosting:

Use MongoDB Atlas.

Secure your connection string via environment variables.

Future Enhancements
Integrated payment gateway (Stripe, Razorpay, etc.)

Email confirmations and PDF ticket generation

Tiered pricing or seat-based pricing models

Caching TMDB data and advanced search filters

Push notifications for seat availability and booking reminders

Contributing
Contributions are welcome! Please follow these steps:

Fork the repository and create a feature branch.

Write clear, descriptive commit messages.

Submit a pull request describing what you’ve added or fixed.

For UI changes, include before/after screenshots or GIFs.

License
This project is open-source and available under the MIT License.

