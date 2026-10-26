# YazilimWorkout | Anime

Build an anime discovery site with Vite, React, and TypeScript. Set up the project, implement the pages and interactions, then run a production build.

## Stack and components

- Start with the shadcn/ui CLI: `npx shadcn@latest init -t vite`. Use React, TypeScript, and Tailwind CSS.
- Choose shadcn/ui Luma, the `mist` base color, and Tabler icons. Set `components.json` to `style: "base-luma"`, `baseColor: "mist"`, `iconLibrary: "tabler"`, `tsx: true`, with aliases `@/components`, `@/components/ui`, and `@/lib/utils`.
- Add required components: `npx shadcn@latest add button card badge aspect-ratio input label select dropdown-menu navigation-menu sheet dialog alert alert-dialog skeleton separator scroll-area tooltip avatar spinner`. If needed, install Tabler with `npm install @tabler/icons-react`.
- Build the interface from shadcn/ui components. Anime and film cards use `Card`; artwork uses `AspectRatio`; genre and score labels use `Badge`; actions use `Button`. Use `NavigationMenu` for navigation, `Sheet` for mobile navigation, `Select` for genre filtering, `Input` for search, `DropdownMenu` for account access, and `Dialog` for title details.
- App-specific components may compose shadcn components. Do not create custom button, card, field, select, menu, or modal primitives. Use semantic HTML only for page structure, text, and images. Use only `@tabler/icons-react` for icons.
- Use React Router for `/signin` and `/signup`. Serve data from `src/data/anime.ts`. Use TanStack Query only for the trailer placeholder loading state.

## Visual design

The brand is **YazilimWorkout | Anime**. Use a cinematic dark anime look with raspberry pink `#EB1F5B` for primary actions, rose pink `#F14B78` for secondary accents, petal pink `#F7A3AB` and pale sakura `#F8DCDD` for soft surfaces, and cool blue `#D5E2F1` for focus and secondary accents. Keep text readable and let anime artwork lead the visual presentation.

Add a sticky navbar with the brand, Discover, Top 6, Films, Hidden Gems, genre filter, search, saved list, and account menu. Use `Sheet` on mobile. Below it, add a full-width **A Silent Voice** hero. Its image must cover the whole area. Place its title and details over a dark gradient in a shadcn `Card` composition. Use the `heroFeature` data.

## Catalogue and data

The root `json-data.json` file is the single source of catalogue data. Validate it first: it must contain 48 anime, 11 sections, and 2 feature banners; every section ID must match a catalogue item. Preserve titles, scores, artwork, genres, and ordering. Convert the data into strongly typed definitions in `src/data/anime.ts`, use that module in the app, and keep the conversion repeatable.

Render all 11 sections in the supplied order, with 102 card placements total. Each anime/film card must show artwork, title, score, and genre. Show a title-based fallback if artwork fails. Build poster cards with shadcn `Card`, `AspectRatio`, `Badge`, and `Button`.

- `ranked`: large rank numbers. `grid`: six columns on desktop and fewer on narrow screens. `strip`: landscape cards.
- Place the Frieren feature after `ranked-two` and the Spy × Family feature after `action`.
- Load sections as the visitor scrolls, without large blank gaps. Show shadcn `Spinner` while loading. Use subtle card entrance motion, respect reduced-motion preferences, and keep cards visible during fast scrolling.
- Open title details in a shadcn `Dialog`. For the temporary trailer state, use TanStack Query to request `https://example.com`; show a spinner while waiting, then say trailer data is not connected. Do not use a remote anime catalogue API.

## Sign in and account

Build `/signin` and `/signup` from the attached reference: full-screen anime collage, dark overlay, centered dark form card, brand logo, clear field labels, and a raspberry-pink primary action. Use shadcn/ui Luma components for form controls and menus.

- Sign in: username or email, password, show/hide control, password recovery note, and registration link.
- Sign up: username, email, password, confirmation, and sign-in link.
- Store accounts and sessions in `localStorage`; store salted PBKDF2 password hashes. Allow sign-in with username or email.
- While signed out, show Sign In. When signed in, place the user’s name to the left of the avatar. Avatar: https://i.pinimg.com/736x/c0/35/c9/c035c9f1ce89541ff98670867ea2534f.jpg.
- Include Sign Out in the avatar menu. Close the menu on outside click or Escape. Sign Out clears the local session and updates the navbar. Return to Discover after sign-in/sign-up; direct access and refresh must work on `/signin` and `/signup`.

## README and delivery

Create `README.md`. Both must contain Turkish and English sections, with `Türkçe | English` links at the top that jump to the matching sections. Explain setup, run and build commands, stack, features, routes, and local account behavior.

Run the production build and fix errors. Search, genre filtering, catalogue cards and dialog, scroll loading, sign-in, sign-up, account menu, and sign-out must work. Desktop and mobile layouts must have no horizontal overflow or empty catalogue sections.
