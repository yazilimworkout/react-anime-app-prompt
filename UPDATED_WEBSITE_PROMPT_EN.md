# YazilimWorkout | Anime: Build From Scratch

Build a working anime discovery site from this brief. Set up the project, implement the pages and interactions, and finish by running a production build.

## Stack and setup

- Create a new Vite application with React and TypeScript. Write components and data files in TSX/TS.
- Install and configure Tailwind CSS. Use Lucide React for icons.
- Use React Router for the `/signin` and `/signup` pages.
- Put the anime catalogue in `src/data/anime.ts`, based on the JSON dataset below.
- Use TanStack Query only for the temporary trailer request and its loading state.

## Design

The brand is **YazilimWorkout | Anime**. Use a black, white, and Netflix red (`#E50914`) palette. Keep spacing tight, typography compact, and corners mostly square. Let the anime artwork provide the color.

Add a slim, sticky navbar with the brand, Discover, Top 6, Films, Hidden Gems, genre filter, search, saved list, and account access. Make navigation easy to use on mobile.

Directly below it, add a full-width **A Silent Voice** hero. The background image must cover the hero from edge to edge and top to bottom. Position the title and details over the image and add a dark gradient for legibility. Use the artwork, rating, and copy from the `heroFeature` record.

## Catalogue

Render all 11 sections from the JSON in the order provided. Under every section heading, render one poster card for each anime listed in `itemIds`. A heading with missing cards is incomplete. The data contains 102 section-card placements.

- In `ranked` sections, overlay large rank numbers near the bottom of each poster.
- In `grid` sections, use six columns on desktop and fewer on tablet and mobile.
- In `strip` sections, use shorter landscape cards.
- Match each section ID to the corresponding catalogue record. Show an image, title, score, and genre on every card.
- If an image fails, show a title-based fallback instead of a broken image or empty card.
- Place the Frieren feature after `ranked-two` and the Spy × Family feature after `action`.

For the long page, append more sections as the visitor scrolls and show a small loader before the current content runs out. Do not leave large black gaps. Cards may fade in gently as they approach the viewport, but they must stay visible if observation is unavailable or a fast scroll skips an event. Respect reduced-motion preferences.

Selecting a card should open a modal with the chosen anime’s artwork and key details. Keep its trailer area temporary: use TanStack Query to request `https://example.com`; show a spinner while waiting, then say that trailer data is not connected yet. Do not add Jikan or YouTube search. We will choose the trailer source later.

## Sign in, sign up, and account menu

Build `/signin` and `/signup` from the attached visual reference: a full-screen anime collage with a dark overlay, a centered black form panel, the YazilimWorkout | Anime logo, white labels, charcoal fields, and a red primary button. Use catalogue images in the collage.

- Sign in needs username or email, password, show/hide control, a password recovery note, and a link to registration.
- Sign up needs username, email, password, confirmation, and a link back to sign in.
- For now, store accounts and sessions in `localStorage`. Store salted PBKDF2 password hashes, never plain-text passwords. Allow sign-in with username or email.
- While signed out, show Sign In in the navbar. After sign-in, show the user’s name immediately to the left of the avatar. Use this avatar image: https://i.pinimg.com/736x/c0/35/c9/c035c9f1ce89541ff98670867ea2534f.jpg.
- Clicking the avatar opens an account menu with Sign Out. Clicking outside or pressing Escape closes the menu. Sign Out clears the `localStorage` session and restores the signed-out navbar.
- Return to Discover after sign-in or sign-up. Direct navigation to `/signin` and `/signup`, including a page refresh, must work.

## README files

Create both `README.md` and `READMEç.md`. Each file must include Turkish and English content. Put a `Türkçe | English` language selector at the very top of both files, with links that jump down to the matching language sections. Explain setup, run and build commands, the stack, main features, routes, and local account behavior in both languages. Check that the language links point to the right sections.

## Data source

The root-level `json-data.json` file is the single source of truth for the catalogue. Read and validate it first: it must contain 48 anime records, 11 sections, and 2 feature banners, and every anime ID referenced by a section must exist in the catalogue. Preserve the titles, scores, images, genres, and ordering.

Convert the JSON into a strongly typed dataset in `src/data/anime.ts` and have the app components consume that TypeScript module. Keep `json-data.json` at the project root and make the conversion reproducible. Do not use a remote API for catalogue data.
## Done means

- All 11 sections appear in order with all 102 section-card placements rendered.
- The hero and both feature banners use the supplied artwork; failed poster images show a fallback.
- Search, genre filtering, navbar, card modal, scroll loading, sign-in, sign-up, account menu, and sign-out work.
- Desktop and mobile layouts have no horizontal overflow or empty black sections.
- Run the production build and fix any build errors.