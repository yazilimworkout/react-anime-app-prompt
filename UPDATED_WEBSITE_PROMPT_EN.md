# YazilimWorkout | Anime

Build an anime discovery site with Vite, React, and TypeScript. Do not return only a design or plan: set up the project, implement every page and interaction, then run a production build.

## Setup order and completion gate

1. From an empty project root, run `npx shadcn@latest init -t vite` to create a Vite app using React, TypeScript, and Tailwind CSS. When the CLI asks, choose the Vite template, Luma style, `mist` base color, and Tabler icons.
2. From the project root, run `npm install react-router-dom @tanstack/react-query @tabler/icons-react motion`. Then add the required shadcn/ui components with `npx shadcn@latest add button card badge aspect-ratio input label select dropdown-menu navigation-menu sheet dialog skeleton scroll-area tooltip avatar spinner --yes`. If a command fails, resolve the error and add any missing components before building the app.
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

## Visual design

The brand is **YazilimWorkout | Anime**. Use a cinematic dark anime look with raspberry pink `#EB1F5B` for primary actions, rose pink `#F14B78` for secondary accents, petal pink `#F7A3AB` and pale sakura `#F8DCDD` for soft surfaces, and cool blue `#D5E2F1` for focus and secondary accents. Make the interface feel editorial and specific to the brand and catalogue artwork. Avoid generic SaaS layouts, unnecessary badges, decorative labels, and ornament that does not serve the content. Keep text readable and let anime artwork lead the visual presentation. Never use glow, neon, bloom, luminous edges, colored halos, or text shadows on any component, including buttons, cards, fields, and focus states. If elevation is needed, use only a very subtle neutral shadow. Show keyboard focus with a crisp, high-contrast border or outline, never a blurred ring.

Add a sticky navbar with the brand, Discover, Top 6, Films, Hidden Gems, genre filter, search, saved list, an appearance toggle, and account menu. Build the appearance toggle as an icon-only shadcn `Button` using Tabler sun/moon icons; clicking it must switch between light and dark immediately. Follow the operating system `prefers-color-scheme` on first visit. When the user changes the theme, save the explicit light/dark preference in `localStorage` and use it on later visits instead of the system value. Use `Sheet` on mobile. Define shadcn Luma tokens for both light and dark themes, maintain readable text/surface/focus contrast, and keep the brand pinks as accents. Below it, create a wide, cinematic hero `Card` inspired by the reference composition and adapted to the anime catalogue: a broad landscape image area with subtly rounded corners, artwork covering the full area, and the main character or focal point kept on the right. In the lower-left, place a large, confident title, followed by score, genres, format, and duration/release details, then Play and More Info actions using shadcn `Button`. Use a restrained gradient that darkens from the left toward the bottom for legibility; do not crowd the title with extra copy. Use the **A Silent Voice** content and artwork from `heroFeature` without inventing details. On mobile, stack the title and actions without overflow.

## Page transitions and profile selection

Use a brief **Page transition** between routes: reveal the words `YazilimWorkout | Anime` over a dark background, then open the destination page with a short **Crossfade**. Time these steps as one **Orchestration**. Keep the animation brief and limited to `opacity` and `transform`; add no glow, neon, bloom, or unnecessary delay. Show the branded transition after successful sign-in/sign-up and whenever an authenticated user opens or reloads the app, then send them to profile selection. Remove the transition or complete it immediately when reduced motion is preferred.

Require authentication for every app route except sign-in and sign-up. Redirect signed-out visitors to `/signin`. After sign-in or sign-up, and on every app launch with an existing session, require profile selection before opening the catalogue. No catalogue route may be accessed until a profile has been selected. Once selected, open the intended destination.

Keep the profile picker simple and full-screen, following the reference: a centered “Who’s watching?” heading, shadcn `Card` choices showing each profile name and avatar, and a `Button`/`Dialog` flow for adding a profile. Give each profile card a separate Edit Profile action. Open a shadcn `Dialog` that lets the user update the profile name and avatar without triggering profile selection. Require an avatar choice from the anime dataset when creating a profile, and save that image URL on the profile. Profile editing must allow choosing a replacement image from the same dataset, persist edits in the account localStorage data, and update the navbar name/avatar immediately when the active profile changes. Store profiles in `localStorage` under their account. Selecting a profile makes it active and updates the navbar avatar to that profile’s saved image and the adjacent label to that profile’s name; do not show the account owner’s name in place of the profile name. If the account has no profiles, do not offer a skip or exit from the picker. Require profile creation, then select the new profile before continuing. Keep the active profile for the session. Add a Switch Profile action to the account menu that returns to the picker. Clear the active profile when signing out.

## Catalogue and data

The root `json-data.json` file is the single source of catalogue data. Validate it first: it must contain 48 anime, 11 sections, and 2 feature banners; every section ID must match a catalogue item. Preserve titles, scores, artwork, genres, and ordering. Convert the data into strongly typed definitions in `src/data/anime.ts`, use that module in the app, and keep the conversion repeatable.

Render all 11 sections in the supplied order, with 102 card placements total. Every card must show artwork, title, score, and genre, with a title-based fallback if artwork fails. Follow the card layout and interaction rules below.

- `ranked`: keep the reference-style large, thin pink-outline rank numbers 1–6 behind the Top 6 posters at all times. Hover must not remove, change, or duplicate them. `grid`: six columns on desktop and fewer on narrow screens. `strip`: horizontal card shelves.
- Apply the same hover/focus behavior to every anime/film card in all 11 sections, not only `strip`. Use one reusable shadcn `Card`-based `AnimeCard` trigger; its behavior must not depend on whether it appears in `ranked`, `grid`, or `strip`. Keep a single page-wide `activeCardId` and show only one preview at a time. While the active card or its preview is hovered/focused, suppress hover styling and preview triggers on every other card; keep background cards static and never open a second preview. Keep it open while the pointer moves from the active card into its preview. Once both the active card and preview are fully left, close it; if the pointer enters another card, close the current preview first, then open only the new card if the pointer remains over it; the two previews must never overlap or coexist.
- The preview must be a substantially wider and taller landscape card like the Netflix Suits reference: 16:9 artwork at the top, large title over a dark lower-left overlay, then a details panel with Play, Saved, Like, and More Info/expand icon actions. Do not use a small tooltip, short caption, or merely enlarged copy of the poster. Show episode name/number, duration, score, and genre only when present in the dataset. Show a progress line and time counter only when real watch progress exists; never fabricate them.
- Prevent clipping by keeping the preview outside the shelf/card DOM. Read the source card ref with `getBoundingClientRect()` and render the preview through a `document.body` portal as `position: fixed`, aligned to the exact center of the source card (`left/top` at its center and `translate(-50%, -50%)`). Target roughly 360–420 px wide and 320–380 px tall, clamped to the viewport on smaller screens. Give it a `z-index` above all shelves; source row `overflow: hidden/clip`, transforms, and stacking contexts must not clip it. Reposition on scroll/resize or close it when its source card leaves the viewport.
- Implement the preview with `motion/react` from the `motion` package. Use one `AnimatePresence` and one `motion.div` controlled by the shared `activeCardId`; animate from the measured source card size to the wider/taller preview with a Motion layout/size transition while keeping the measured center fixed. Prevent content from jumping as the panel grows. Use a brief ease-out, add no glow/neon, and respect reduced motion.
- Keep Top 6 rank numbers in their normal card positions. Do not imitate hover on touch devices; tapping any card opens its details in a shadcn `Dialog`, accessible to keyboard and screen-reader users.- Place the Frieren feature after `ranked-two` and the Spy × Family feature after `action`.
- Load sections as the visitor scrolls, without large blank gaps. Show shadcn `Spinner` while loading. As cards first enter the scroll area, use a brief, subtle opacity/position transition to signal new content; avoid cascading stagger sequences and parallax. Keep interaction motion purposeful and short, animate only the properties needed, and do not use `transition: all`. Respect reduced-motion preferences and keep cards visible during fast scrolling.
- Make the shadcn `Dialog` accessible to keyboard and screen-reader users. For the temporary trailer state, use TanStack Query to request `https://example.com`; show a spinner while waiting, then say trailer data is not connected. Do not use a remote anime catalogue API.

## Sign in and account

Build the `/signin` and `/signup` backgrounds from image URLs in the anime dataset. Arrange the posters in staggered, slightly angled rows that extend beyond the viewport, with clear black gutters between them, creating a Netflix-style anime poster wall. Use only catalogue artwork from `src/data/anime.ts`; do not add external or random images. Place a static dark overlay over the artwork so the form remains readable; do not add auto-scrolling or parallax. Center a dark form card with the brand logo, clear field labels, and a raspberry-pink primary action. Use shadcn/ui Luma components for form controls and menus.

- Sign in: username or email, password, show/hide control, password recovery note, and registration link.
- Sign up: username, email, password, confirmation, and sign-in link.
- Store accounts and sessions in `localStorage`; store salted PBKDF2 password hashes. Allow sign-in with username or email.
- While signed out, show Sign In. After profile selection, show the active profile’s saved image as the navbar avatar and its name to the left. Do not use a fixed or external avatar image; if a profile image is missing, show the profile name’s initials.
- Include Edit Profile, Switch Profile, and Sign Out in the avatar menu. Edit Profile opens a shadcn `Dialog` to change the active profile name and choose a replacement avatar from the anime dataset. Close the menu on outside click or Escape. Sign Out clears the local session and active profile, then updates the navbar. Direct access and refresh must work on `/signin` and `/signup`.

## README and delivery

Create `README.md` and `READMEç.md`. Both must contain Turkish and English sections, with `Türkçe | English` links at the top that jump to the matching sections. Explain setup, run and build commands, stack, features, routes, and local account behavior.

Run the production build and fix errors. Search, genre filtering, catalogue cards and dialog, scroll loading, sign-in, sign-up, account menu, and sign-out must work. Desktop and mobile layouts must have no horizontal overflow or empty catalogue sections.


