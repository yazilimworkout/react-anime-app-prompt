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
  <img src="docs/assets/homepage-preview.jpg" alt="YazilimWorkout Anime homepage showing the featured A Silent Voice film and anime discovery cards" width="100%">
</p>

## About

YazilimWorkout | Anime is a dark, cinematic catalog for browsing anime series and films. The homepage puts a featured title up front, then guides visitors through community rankings, new episodes, recommendations, hidden gems, and themed collections. Search and genre filters make it easy to narrow down the catalog, while each title can be opened for more details.

The project is built as a responsive single-page experience with React and Vite. Sign-in and registration currently use browser local storage, so accounts are for demonstration and remain on the current device.

## Features

- Featured anime and film presentations with title details and genre information
- Searchable catalog with genre filtering
- Ranked anime cards and curated discovery sections
- Title details modal with related trailer area
- Sign-in and registration screens with a profile menu and sign-out
- Responsive layout for desktop and smaller screens
- Loading states for catalog content

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

- React for the user interface
- Vite for development and production builds
- Tailwind CSS for utility styling
- TanStack Query for asynchronous data state
- Lucide React for interface icons

## Authentication note

Authentication is a front-end demo. User details are stored in the browser's local storage; there is no server-side account system yet. Avoid using real passwords or sensitive information.
