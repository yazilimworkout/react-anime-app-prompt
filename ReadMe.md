<p align="center">
  <a href="READMEç.md">Türkçe</a> | English
</p>

<div align="center">
  <h1>YazilimWorkout | Anime</h1>
  <p>A curated anime discovery experience for finding your next favorite series or film.</p>
  <p>
    <img alt="React" src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
    <img alt="Vite" src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white">
    <img alt="Tailwind CSS" src="https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white">
    <img alt="TanStack Query" src="https://img.shields.io/badge/TanStack_Query-FF4154?style=for-the-badge&logo=reactquery&logoColor=white">
    <img alt="Lucide" src="https://img.shields.io/badge/Lucide-Icons-F56565?style=for-the-badge">
  </p>
</div>

<p align="center">
<img width="1915" height="931" alt="image" src="https://github.com/user-attachments/assets/7fe4af79-59b5-49bf-b6f3-72bd5adf7c04" />

  <img src="https://github.com/user-attachments/assets/4d1feba2-74dc-4476-9392-d7514d785329" alt="YazilimWorkout Anime homepage showing the featured A Silent Voice film and anime discovery cards" width="100%">
  <img width="1897" height="941" alt="image" src="https://github.com/user-attachments/assets/319f204d-e901-4ea1-b64c-f86b679bfa05" />

</p>

## About

YazilimWorkout | Anime is a dark, cinematic catalog for browsing 48 anime series and films across 11 curated sections. The homepage opens with a featured title and then flows through horizontal rails of landscape artwork, so visitors can scroll each section independently. Hovering over a card (or tapping it on touch devices) reveals a compact preview, and a larger details dialog shows episodes, season selection, recommendations, and credits.

The app is a responsive single-page experience built with React, TypeScript, and Vite. It supports light and dark themes that follow the system preference on first visit. Profiles let several people share one account, and each profile keeps its own name and avatar.

## Features

- Netflix-style homepage with a featured title and 11 horizontal catalogue rails
- Top 6 ranking with oversized numerals on the artwork
- Hover previews on desktop and a details dialog opened by hover, tap, or keyboard
- Season selector, episode list, "More Like This" recommendations, and an About section in the details dialog
- Profile picker with add, edit, and switch actions
- Light and dark themes with persisted preference
- Animated logo transition between pages
- Local sign-in and sign-up with salted PBKDF2 password hashing
- Responsive layout for desktop and mobile, with touch swipe support on every rail

## Routes

- `/signin`: sign-in screen with username or email login
- `/signup`: registration screen
- `/`: profile selection followed by the catalogue, available only after sign-in

Signed-out visitors are redirected to `/signin`. Direct access and page refresh work on the authentication routes.

## Getting started

Use Node.js and npm, then run:

```bash
npm install
npm run dev
```

Vite prints the local address when the development server is ready.

## Production build

```bash
npm run build
npm run preview
```

## Tech stack

- React and TypeScript for the user interface
- Vite for development and production builds
- Tailwind CSS with shadcn/ui components
- Redux Toolkit for application state, with redux-persist for storage
- React Router for navigation
- TanStack Query for asynchronous data state
- Swiper for horizontal catalogue rails
- Motion for hover preview and transition animations
- Tabler Icons for interface icons

## Local accounts

Accounts and sessions are stored in the browser's `localStorage`. Passwords are never stored in plain text. They are hashed with salted PBKDF2, and the Redux store holds only the authentication state, never passwords. Profile and watch data are partitioned by account, so one account cannot see another account's profiles or saved titles.

## Authentication note

Authentication is a front-end demo. There is no server-side account system yet, and accounts remain on the current device. Avoid using real passwords or sensitive information.
