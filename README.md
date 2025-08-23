# 🎬 QuickShow

A modern movie ticket booking platform where users can browse movies (sourced from TMDB), view showtimes created by admins, select seats, and book tickets easily.  
Powered by a React frontend and an Express + MongoDB backend. Authentication is managed through Clerk (with optional custom JWT), deployments are streamlined via Vercel, and movie metadata is seamlessly integrated using the TMDB API.  

_Status: Active development_

---

## ✨ Features

- 🎥 **Movie Catalog (TMDB)**: Fetch "Now Playing" and "Popular" movies via TMDB API and store selected titles in MongoDB with `tmdbId` linkage.  
- 🛠 **Admin Show Management**: Create, schedule, and manage showtimes with custom dates, screen layouts, pricing, and seat configurations.  
- ⏱ **Showtime Discovery**: Browse and filter shows by movie title or date.  
- 💺 **Interactive Seat Selection**: Real-time interactive seat map for choosing available seats.  
- 🎟 **Booking & Tickets**: Reserve seats and generate confirmation for completed bookings.  
- 🔐 **Authentication**: Clerk-based authentication with optional custom JWT for inter-service communication.  
- 📊 **Admin Dashboard**: Monitor KPIs such as active shows, total bookings, and revenue for better insights.  
- ☁️ **Scalable Architecture**: Decoupled frontend & backend, environment-based configuration, and well-defined models with Mongoose.  

---

## 🛠 Tech Stack

| Layer        | Technologies |
|--------------|--------------|
| **Frontend** | React (Vite), React Router, Axios/Fetch, Tailwind CSS |
| **Backend**  | Node.js, Express, MongoDB (Mongoose), Clerk (Auth), TMDB API |
| **Deployment** | Vercel (Frontend & Backend), MongoDB Atlas, `.env` configs |

---

## 📂 Project Structure

# 🎬 QuickShow

A modern movie ticket booking platform where users can browse movies (sourced from TMDB), view showtimes created by admins, select seats, and book tickets easily.  
Powered by a React frontend and an Express + MongoDB backend. Authentication is managed through Clerk (with optional custom JWT), deployments are streamlined via Vercel, and movie metadata is seamlessly integrated using the TMDB API.  

_Status: Active development_

---

## ✨ Features

- 🎥 **Movie Catalog (TMDB)**: Fetch "Now Playing" and "Popular" movies via TMDB API and store selected titles in MongoDB with `tmdbId` linkage.  
- 🛠 **Admin Show Management**: Create, schedule, and manage showtimes with custom dates, screen layouts, pricing, and seat configurations.  
- ⏱ **Showtime Discovery**: Browse and filter shows by movie title or date.  
- 💺 **Interactive Seat Selection**: Real-time interactive seat map for choosing available seats.  
- 🎟 **Booking & Tickets**: Reserve seats and generate confirmation for completed bookings.  
- 🔐 **Authentication**: Clerk-based authentication with optional custom JWT for inter-service communication.  
- 📊 **Admin Dashboard**: Monitor KPIs such as active shows, total bookings, and revenue for better insights.  
- ☁️ **Scalable Architecture**: Decoupled frontend & backend, environment-based configuration, and well-defined models with Mongoose.  

---

## 🛠 Tech Stack

| Layer        | Technologies |
|--------------|--------------|
| **Frontend** | React (Vite), React Router, Axios/Fetch, Tailwind CSS |
| **Backend**  | Node.js, Express, MongoDB (Mongoose), Clerk (Auth), TMDB API |
| **Deployment** | Vercel (Frontend & Backend), MongoDB Atlas, `.env` configs |

---# 🎬 QuickShow

A modern movie ticket booking platform where users can browse movies (sourced from TMDB), view showtimes created by admins, select seats, and book tickets easily.  
Powered by a React frontend and an Express + MongoDB backend. Authentication is managed through Clerk (with optional custom JWT), deployments are streamlined via Vercel, and movie metadata is seamlessly integrated using the TMDB API.  

_Status: Active development_

---

## ✨ Features

- 🎥 **Movie Catalog (TMDB)**: Fetch "Now Playing" and "Popular" movies via TMDB API and store selected titles in MongoDB with `tmdbId` linkage.  
- 🛠 **Admin Show Management**: Create, schedule, and manage showtimes with custom dates, screen layouts, pricing, and seat configurations.  
- ⏱ **Showtime Discovery**: Browse and filter shows by movie title or date.  
- 💺 **Interactive Seat Selection**: Real-time interactive seat map for choosing available seats.  
- 🎟 **Booking & Tickets**: Reserve seats and generate confirmation for completed bookings.  
- 🔐 **Authentication**: Clerk-based authentication with optional custom JWT for inter-service communication.  
- 📊 **Admin Dashboard**: Monitor KPIs such as active shows, total bookings, and revenue for better insights.  
- ☁️ **Scalable Architecture**: Decoupled frontend & backend, environment-based configuration, and well-defined models with Mongoose.  

---

## 🛠 Tech Stack

| Layer        | Technologies |
|--------------|--------------|
| **Frontend** | React (Vite), React Router, Axios/Fetch, Tailwind CSS |
| **Backend**  | Node.js, Express, MongoDB (Mongoose), Clerk (Auth), TMDB API |
| **Deployment** | Vercel (Frontend & Backend), MongoDB Atlas, `.env` configs |

---

## 📂 Project Structure

**QuickShow/**
```bash
**├─ README.md**
**├─ frontend/**
**│ ├─ src/**
**│ │ ├─ components/**
**│ │ ├─ pages/**
**│ │ ├─ hooks/**
**│ │ ├─ routes/**
**│ │ ├─ lib/**
**│ │ └─ App.jsx**
**│ ├─ public/**
**│ └─ package.json**
**└─ backend/**
├─ src/
│ ├─ configs/ (db.js)
│ ├─ controllers/ (show.controller.js)
│ ├─ models/ (Movie.js, Show.js, User.js)
│ ├─ routes/ (show.routes.js, index.js)
│ ├─ middlewares/ (auth.js, error.js)
│ ├─ services/ (tmdb.service.js)
│ ├─ inngest/ (optional)
│ └─ server.js
└─ package.json
```

---

## 🚀 Setup & Usage

### ✅ Prerequisites
- Node.js (v18+ recommended)  
- MongoDB (Atlas or local)  
- TMDB API key  
- Clerk credentials (Client ID, Secret)  
- Vercel account (optional for deployment)  

### ⚡ Installation

1. **Clone the repo**  
   ```bash
   git clone https://github.com/KikaniMeet/quickshow.git
---
## Backend

- cd quickshow/backend
- npm install
- cp .env.example .env
- Add values for:
- MONGODB_URI, TMDB_API_KEY, CLERK_CLIENT_ID, CLERK_SECRET_KEY
- npm run dev

---
### Frontend 
- cd ../frontend
- npm install
- cp .env.example .env
- Add values for:
- VITE_TMDB_API_KEY, VITE_CLERK_PUBLISHABLE_KEY
- npm run dev

---

### ☁️ Deployment

- Frontend & Backend (Vercel)
- Connect GitHub repo to Vercel.
- Add environment variables for both frontend and backend.
- Deploy as separate projects (frontend/backend) or monorepo.
- Database (MongoDB Atlas)
- Use Atlas for hosting.
- Store connection string in environment variables.

---

### 📌 Roadmap

- 💳 Payment gateway integration (Stripe, Razorpay)
- 📧 Email confirmations + PDF ticket generation
- 🪑 Tiered seat-based pricing models
- ⚡ TMDB caching & advanced search filters
- 🔔 Push notifications for booking reminders

---

### 🤝 Contributing

- Fork the repository
- Create a feature branch (git checkout -b feature-name)
- Commit changes (git commit -m "Added feature XYZ")
- Push to your branch (git push origin feature-name)
- Open a Pull Request

---

### 👨‍💻 Author

Kikani Meet Lalitbhai
- 📧 Email: mitkikani027@gmail.com

