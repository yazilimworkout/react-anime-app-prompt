# YazilimWorkout | Anime

Build an anime discovery site with Vite, React, and TypeScript. Do not return only a design or plan: set up the project, implement every page and interaction, then run a production build.

## Setup order and completion gate

1. From an empty project root, run `npx shadcn@latest init -t vite` to create a Vite app using React, TypeScript, and Tailwind CSS. When the CLI asks, choose the Vite template, Luma style, `mist` base color, and Tabler icons.
2. From the project root, run `npm install react-router-dom @tanstack/react-query @tabler/icons-react motion @reduxjs/toolkit react-redux redux-persist tailwind-scrollbar-hide`. Then add the required shadcn/ui components with `npx shadcn@latest add button card badge aspect-ratio input label select dropdown-menu navigation-menu sheet dialog skeleton scroll-area tooltip avatar spinner --yes`. If a command fails, resolve the error and add any missing components before building the app.
3. Inspect `package.json`, `components.json`, and `src/components/ui/`. Merely listing packages in this prompt or README is not enough: dependencies must be installed, shadcn component files must exist, and the app must import and use them.
4. After implementation, run `npm run build` and fix any errors. Never claim a command ran if it did not; report the main installed packages and actual build result briefly at the end.

## Stack and components

- Create `components.json` with this valid structure and verify it before adding CLI components. Point the Vite and TypeScript `@/*` aliases to `src`:

```json
{
  "$schema": "https://ui.shadcn.com/schema.json",
  "style": "base-luma",
  "rsc": false,
  "tsx": true,
  "tailwind": {
    "config": "",
    "css": "src/index.css",
    "baseColor": "mist",
    "cssVariables": true,
    "prefix": ""
  },
  "iconLibrary": "tabler",
  "aliases": {
    "components": "@/components",
    "utils": "@/lib/utils",
    "ui": "@/components/ui",
    "lib": "@/lib",
    "hooks": "@/hooks"
  }
}
```
- Add only the shadcn components used by the interface through the CLI; verify the component list against `package.json` and actual code imports.
- Build the interface from shadcn/ui components. Use the shadcn `Card` base for anime and film cards; use `AspectRatio` for artwork, `Badge` for genre and score labels, and `Button` for actions. Do not let the default `Card` padding, radius, border, or surface styles dictate the reference design: apply project-specific Tailwind/CSS directly to `Card` or adjust the local `components/ui/card.tsx` styles while preserving shadcn `data-slot` attributes and accessible semantics. Do not create a parallel non-shadcn card primitive. Use `NavigationMenu` for navigation, `Sheet` for mobile navigation, `Select` for genre filtering, `Input` for search, `DropdownMenu` for account access, and `Dialog` for title details.
- App-specific components may compose shadcn components. Do not create custom button, card, field, select, menu, or modal primitives. Use semantic HTML only for page structure, text, and images. Use only `@tabler/icons-react` for icons.
- Use React Router for `/signin` and `/signup`. Serve data from `src/data/anime.ts`. Use TanStack Query only for the trailer placeholder loading state.
- Manage application state with Redux Toolkit: use `createSlice`, `configureStore`, typed `useAppDispatch`/`useAppSelector` hooks, and the React Redux `Provider`; do not scatter global state across components. Persist appearance preference, account profiles, saved/liked title IDs, and watch progress to `localStorage` with `redux-persist`. Partition account data by `accountId` so one account never sees another account’s profiles or saved titles. Never put passwords or password hashes in Redux or its persistence layer; keep existing local authentication records separate. Use `PersistGate` to show a loading state until persisted state is rehydrated before protected routes render or redirect. Ignore only the redux-persist action types required by Redux Toolkit’s serializability check. Keep `react` and `react-dom` on compatible matching versions and verify there is a single React installation with `npm ls react react-dom`. Render Redux `Provider` as JSX inside `createRoot(...).render(<Provider store={store}>...</Provider>)`; never invoke it as a plain function. Call hooks only at the top level of React function components or custom hooks, never during ordinary function calls or inside conditions/loops. If an `Invalid hook call` appears during development, do not proceed until the stack trace and `npm ls react react-dom react-redux` output identify and resolve a version mismatch or duplicate React copy; clear the Vite cache, restart the app, and confirm the error is gone.
- Install `tailwind-scrollbar-hide` and activate it for the installed Tailwind version: for Tailwind v4, add `@import 'tailwind-scrollbar-hide/v4';` to `src/index.css`; for v2/v3, add it to the Tailwind config `plugins` array. Verify the setup and apply `scrollbar-hide` to the dialog body.

## Visual design

The brand is **YazilimWorkout | Anime**. Use a cinematic dark anime look with raspberry pink `#EB1F5B` for primary actions, rose pink `#F14B78` for secondary accents, petal pink `#F7A3AB` and pale sakura `#F8DCDD` for soft surfaces, and cool blue `#D5E2F1` for focus and secondary accents. Make the interface feel editorial and specific to the brand and catalogue artwork. Avoid generic SaaS layouts, unnecessary badges, decorative labels, and ornament that does not serve the content. Keep text readable and let anime artwork lead the visual presentation. Never use glow, neon, bloom, luminous edges, colored halos, or text shadows on any component, including buttons, cards, fields, and focus states. If elevation is needed, use only a very subtle neutral shadow. Show keyboard focus with a crisp, high-contrast border or outline, never a blurred ring.

Add a sticky navbar with the brand, Discover, Top 6, Films, Hidden Gems, genre filter, search, saved list, appearance toggle, and account menu. Use an icon-only shadcn `Button` with Tabler sun/moon icons. Follow `prefers-color-scheme` on first visit, then persist explicit user choices through Redux Persist and update the theme immediately. Use `Sheet` for mobile navigation. Define shadcn Luma tokens for light and dark themes with readable text, surface, and focus contrast.

Below the navbar, create a full-bleed, edge-to-edge `w-screen` hero `Card` with at least one viewport of height minus the navbar (use `min-height: calc(100svh - var(--navbar-height))` and define `--navbar-height` from the actual navbar height), without causing horizontal page overflow. Let the background artwork fill the hero and position its content absolutely over the image at the lower-left. Adapt the reference composition to the anime catalogue. Use **A Silent Voice** content from `heroFeature`. Only a genuinely landscape `backgroundImage` may fill the wide image area; never stretch or crop portrait artwork to fake a landscape image. Place the title, score, genre, format, runtime/release information, and Play/More Info shadcn `Button` actions at the lower-left. Use a restrained dark gradient for legibility. Stack text and actions on mobile without overflow.

## Page transitions and profile selection

Use a brief **Page transition** between routes: reveal the words `YazilimWorkout | Anime` over a dark background, then open the destination page with a short **Crossfade**. Time these steps as one **Orchestration**. Keep the animation brief and limited to `opacity` and `transform`; add no glow, neon, bloom, or unnecessary delay. Show the branded transition after successful sign-in/sign-up and whenever an authenticated user opens or reloads the app, then send them to profile selection. Remove the transition or complete it immediately when reduced motion is preferred.

Require authentication for every app route except sign-in and sign-up. Redirect signed-out visitors to `/signin`. After sign-in or sign-up, and on every app launch with an existing session, require profile selection before opening the catalogue. No catalogue route may be accessed until a profile has been selected. Once selected, open the intended destination.

Keep the profile picker simple and full-screen, following the reference: a centered “Who’s watching?” heading, shadcn `Card` choices showing each profile name and avatar, and a `Button`/`Dialog` flow for adding a profile. Give each profile card a separate Edit Profile action. Open a shadcn `Dialog` that lets the user update the profile name and avatar without triggering profile selection. Require an avatar choice from the anime dataset when creating a profile, and save that image URL on the profile. Profile editing must allow choosing a replacement image from the same dataset, update the Redux slice and persist profiles through `redux-persist` under the matching `accountId`; do not create a second localStorage source for profile data. Update the navbar name/avatar immediately when the active profile changes. Selecting a profile makes it active and updates the navbar avatar to that profile’s saved image and the adjacent label to that profile’s name; do not show the account owner’s name in place of the profile name. If the account has no profiles, do not offer a skip or exit from the picker. Require profile creation, then select the new profile before continuing. Keep the active profile for the session. Add a Switch Profile action to the account menu that returns to the picker. Clear the active profile when signing out.

## Catalogue and data

The root `json-data.json` file is the single source of catalogue data. Validate it first: it must contain 48 anime, 11 sections, and 2 feature banners; every section ID must match a catalogue item. Preserve titles, scores, artwork, genres, and ordering. Validate that every `recommendationIds` value points to a different existing catalogue item. Use the `details` object on each catalogue record as the detail-dialog source: `backdropImage`, `format`, `releaseYear`, `synopsis`, `runtimeMinutes`, `maturityRating`, `contentDescriptors`, `audio`, `cast`, `director`, `writers`, `studio`, `recommendationIds`, `seasons`, and `sources`, an array of source URLs. Keep sources in JSON for provenance; do not display them in the About interface. Build series episode rows from `seasons[].episodes[]`; `episodeCount` is the season total, while the JSON `episodes` array contains the entries to render. Omit null values and empty arrays from the interface, and preserve the existing base catalogue fields. Convert the data into strongly typed definitions in `src/data/anime.ts`, use that module in the app, and keep the conversion repeatable.

Render all 11 sections in the supplied order, with 102 card placements total. Every card must show artwork, title, score, and genre, with a title-based fallback if artwork fails. Follow the card layout and interaction rules below.

- Card layouts: `ranked` keeps its rank numbers visible behind the posters; hover never removes or duplicates them. `grid` uses six desktop columns and adapts to smaller screens. `strip` is a horizontal shelf. Use the same shadcn `Card`-based `AnimeCard` in every layout.
- On desktop, hover previews must work for every card across all 11 sections. Use one page-wide `activeCardInstanceId` so only one preview can be open. Since a title may appear in multiple sections, derive a unique card-instance key from `sectionId + itemId + index`; use the catalogue item ID only to select the title data. While its source card or preview is hovered, suppress hover highlights and triggers on all other cards. Keep the preview open while the pointer moves between that card and its preview; close it after both are left. When moving to another card, close the current preview first, then open the new one only if the pointer remains there. Never show two previews at once.
- Do not imitate hover on touch devices; tapping a card opens the detail `Dialog` directly. Make cards keyboard-focusable with a visible focus style. Enter/Space opens the detail dialog directly; do not run the hover expansion animation for keyboard actions.
- Make the hover preview a clearly wider landscape card like the Netflix Suits reference: artwork with a large lower-left title above a details panel containing Play, Saved, Like, and More Info actions. Do not use a tiny tooltip or a simple enlarged poster. Show runtime, score, episode details, and progress only when the data provides them.
- Render the preview outside the shelf in a `document.body` portal. Measure the source card with `getBoundingClientRect()`, use `position: fixed`, align the preview center to the source-card center, and clamp it to the viewport. Aim for about 360–420 px wide and 320–380 px tall on desktop. Shelf overflow, transforms, and stacking contexts must not clip it. Reposition on scroll/resize and close it when its source card leaves view.
- Use `motion/react`. Use a FLIP/shared-layout transition between the source card and preview; animate the size change with `transform` and `opacity`, never by animating CSS `width` or `height`. Confirm hover intent with a short delay. Keep entry near 180 ms and exit shorter and interruptible. Do not use `ease-in`, `transition: all`, glow, or neon. With reduced motion, remove position/scale movement and retain only a brief opacity transition if helpful.
- More Info closes the hover preview and opens a separate, wide shadcn `Dialog`. On desktop, set width to `min(1100px, calc(100vw - 32px))` and height to at most 92% of the viewport; scroll inside the dialog body. Make it nearly full-screen on mobile. Include a close button, title, and 16:9 hero artwork only when the source asset is truly landscape. Put metadata and synopsis below the hero; show episode lists for series and film information for movies. Omit missing data and never fabricate details.
- Preserve each image’s source aspect ratio. Do not assume `image` is a poster and `backdropImage` is landscape based on field names alone; check the actual `naturalWidth/naturalHeight`. Use shadcn `AspectRatio` at the poster’s source ratio and render it with `object-fit: contain`. Use a true landscape `backdropImage` in the detail hero when available. If only portrait art exists, do not crop it with `cover` to fake a 16:9 image; show it with `contain` at its original ratio. Use episode thumbnails only when landscape episode artwork is provided. For the main hero, use only a landscape `backgroundImage`; otherwise preserve the artwork without cropping.
- Detail-dialog order: available metadata and synopsis; for series, a season selector and episode rows from `seasons[].episodes[]`; then **More Like This**; finish with **About [Title]**. Resolve recommendations from `recommendationIds`; if empty, deterministically choose up to three catalogue entries with the same format and similar genre/score. Selecting a recommendation replaces the content in the same open dialog. In About, show available director, writer(s), cast, studio, genres, format, year, maturity rating, and content descriptors in readable rows. Films have no episode list. Omit unavailable rows and do not display `sources` in the interface.
- Apply `scrollbar-hide` to the scrollable dialog body. Keep scrolling available with mouse, trackpad, touch, and keyboard; make the scroll area focusable and retain a visible focus style. Support Escape and the close button, accessible title/description, and correct focus handling.
- Render local JSON catalogue data immediately; do not leave blank sections or add artificial delays while scrolling. Lazy-load large images and, if needed, prepare section components as they approach the viewport. Show a spinner only during real asynchronous work, while preserving the section’s space.
- For the trailer placeholder only, use TanStack Query to request `https://example.com`; show a shadcn `Spinner` while waiting, then a short message that trailer data is not connected. Do not use a remote anime catalogue API.

## Sign in and account

Build the `/signin` and `/signup` backgrounds from image URLs in the anime dataset. Arrange the posters in staggered, slightly angled rows that extend beyond the viewport, with clear black gutters between them, creating a Netflix-style anime poster wall. Use only catalogue artwork from `src/data/anime.ts`; do not add external or random images. Place a static dark overlay over the artwork so the form remains readable; do not add auto-scrolling or parallax. Center a dark form card with the brand logo, clear field labels, and a raspberry-pink primary action. Use shadcn/ui Luma components for form controls and menus.

- Sign in: username or email, password, show/hide control, password recovery note, and registration link.
- Sign up: username, email, password, confirmation, and sign-in link.
- Store accounts and sessions in `localStorage`; store salted PBKDF2 password hashes. Allow sign-in with username or email. Represent authentication in the RTK store without passwords; keep persisted profile/catalogue data partitioned by the signed-in `accountId`.
- While signed out, show Sign In. After profile selection, show the active profile’s saved image as the navbar avatar and its name to the left. Do not use a fixed or external avatar image; if a profile image is missing, show the profile name’s initials.
- Include Edit Profile, Switch Profile, and Sign Out in the avatar menu. Edit Profile opens a shadcn `Dialog` to change the active profile name and choose a replacement avatar from the anime dataset. Close the menu on outside click or Escape. Sign Out clears the local session and active profile, then updates the navbar. Direct access and refresh must work on `/signin` and `/signup`.

## README and delivery

Create `README.md` as the primary English README and `READMEç.md` as its Turkish counterpart. Put `Türkçe | English` language links at the top of each file, linking to the other language. Include a real full-page screenshot of the entire app in both (`docs/screenshots/full-page.png`); do not use only the hero or first viewport. Add a concise product introduction, relevant technology badges, features, screenshot, setup/run/build commands, routes, and local account behavior.

Run the production build and fix errors. Search, genre filtering, catalogue cards and detail dialog, section scrolling, sign-in, sign-up, profile menu, and sign-out must work. Local catalogue sections must not be blank or show artificial loading delays. Desktop and mobile layouts must have no horizontal overflow or empty catalogue sections.
