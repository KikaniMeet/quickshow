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

