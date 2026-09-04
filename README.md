# Smart Agriculture Adviser — AgroSense

> A full-stack web application providing AI-assisted crop recommendations, real-time weather data, and interactive farm mapping for Indian farmers. Deployed live on GitHub Pages.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-green?style=for-the-badge&logo=github)](https://vedpatel41.github.io/smart-agriculture-adviser/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow?style=for-the-badge&logo=javascript)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Firebase](https://img.shields.io/badge/Firebase-Auth%20%2B%20Firestore-orange?style=for-the-badge&logo=firebase)](https://firebase.google.com/)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-purple?style=for-the-badge&logo=bootstrap)](https://getbootstrap.com/)

---

## Live Demo

**[https://vedpatel41.github.io/smart-agriculture-adviser/](https://vedpatel41.github.io/smart-agriculture-adviser/)**

---

## Overview

AgroSense is a smart agricultural advisory web portal that helps farmers make data-driven crop decisions. The application integrates real-time weather data from the OpenWeatherMap API, a map interface for location selection, and an intelligent crop recommendation engine based on temperature, humidity, soil type, and season.

User accounts are managed through Firebase Authentication and Firestore, making the system fully client-side with no backend server required.

This was the Full Stack Development (FSD) Project for Semester 3.

---

## Features

- **User Authentication** — Sign up and log in with Firebase Authentication (email/password). Password strength validation enforced (minimum 8 characters, uppercase, lowercase, number, special character).
- **Session Guard** — Protected routes that redirect unauthenticated users. Session state managed via Firebase Auth and `localStorage`.
- **Interactive Map** — Location picker using a mapping interface; users click to select their farm location
- **Real-time Weather Data** — Fetches live temperature and humidity for the selected location via the OpenWeatherMap API using `async/await` Fetch
- **Soil Type Estimation** — Infers soil type (Sandy, Black, Clay, Loamy) from GPS coordinates using a rule-based function
- **Crop Recommendation Engine** — Recommends the top 3 crops ranked by suitability score, calculated from temperature range match, humidity, and current season (Kharif / Rabi / Zaid)
- **Farm Dashboard** — Saves farm analyses (name, location, soil, weather, top crops) to `localStorage` per user
- **Crop Advisory Page** — Dedicated page with crop information
- **Feedback Page** — User feedback form
- **Help Page** — User guidance and documentation
- **Scroll Reveal Animations** — IntersectionObserver-based entrance animations
- **Responsive UI** — Bootstrap 5.3 layout with custom CSS

---

## Tech Stack

| Category | Technology |
|----------|-----------|
| Authentication | Firebase Authentication (v10) |
| Database / Storage | Firebase Firestore |
| Weather Data | OpenWeatherMap API |
| Frontend Framework | Bootstrap 5.3 |
| JavaScript | ES6+ Modules, Async/Await, Fetch API |
| Animations | IntersectionObserver (Scroll Reveal) |
| Deployment | GitHub Pages |

---

## Project Structure

```
smart-agriculture-adviser/
└── fsd_A4-6/
    ├── css/
    │   └── style.css               # Application styles
    ├── images/                     # Hero images (image.jpg, img-2.webp, img-3.webp)
    ├── static/
    │   └── js/
    │       ├── firebase.js         # Firebase initialization (Auth + Firestore)
    │       ├── auth.js             # Sign up, login, logout with Firebase Auth
    │       ├── dashboard.js        # Farm management, weather API, crop recommendation
    │       ├── map.js              # Interactive map and location selection
    │       ├── crops.js            # Crop advisory page logic
    │       ├── help.js             # Help page interactions
    │       ├── scrollReveal.js     # IntersectionObserver scroll animations
    │       └── sessionGaurd.js     # Route protection and session management
    └── templates/
        ├── home.html               # Landing page (guest)
        ├── login.html              # Login page
        ├── signup.html             # Registration page
        ├── index.html              # Main dashboard (authenticated)
        ├── dashboard.html          # Farm list and saved analyses
        ├── map.html                # Interactive map for location selection
        ├── crops.html              # Crop advisory information
        ├── feedback.html           # User feedback form
        ├── help.html               # Help and documentation
        ├── base.html               # Shared layout (authenticated)
        └── base1.html              # Shared navbar (loaded via fetch)
```

---

## How It Works

### Authentication Flow
1. User registers via `signup.html` — Firebase creates a user account and Firestore stores the user profile (name, email)
2. User logs in via `login.html` — Firebase signs in the user
3. Session guard (`sessionGaurd.js`) runs on every page load and redirects unauthenticated users to `home.html` and authenticated users away from the guest home

### Crop Recommendation Engine (`dashboard.js`)
1. User selects a location on the map
2. Weather data is fetched from OpenWeatherMap API using `async/await`:
   ```javascript
   const response = await fetch(
     `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&units=metric&appid=${API_KEY}`
   );
   ```
3. Soil type is inferred from coordinates using a rule-based function
4. Crops are scored based on temperature range, humidity threshold, and current season (Kharif/Rabi/Zaid)
5. Top 3 crops with their ratings are displayed to the user
6. User can save the farm analysis (stored in `localStorage` keyed by user email)

---

## Running Locally

Since this is a static website, simply open it in a browser. Note that Firebase features require network access.

```bash
# Clone the repository
git clone https://github.com/VedPatel41/smart-agriculture-adviser.git

# Open the landing page in your browser
# Navigate to: fsd_A4-6/templates/home.html
```

> A local HTTP server is recommended to avoid CORS issues with ES6 modules:
> ```bash
> python -m http.server 8080
> # Then open: http://localhost:8080/fsd_A4-6/templates/home.html
> ```

---

## Author

**Ved Patel** — B.Tech Computer Engineering Student  
[GitHub](https://github.com/VedPatel41) · [LinkedIn](https://www.linkedin.com/in/ved-patel-0bb446376)
