# DashSync (DataSync Dashboard) — Personalized Movies & News Dashboard

A production-oriented **Next.js** dashboard that aggregates **trending movies** and **top headlines**, with **Clerk authentication**, **per-user favorites**, and **preference-driven personalization**. Built with **TypeScript**, **Redux Toolkit + RTK Query**, and a lightweight **Next.js API layer** to proxy external APIs.

---

## Live Demo & Links

| Link | URL |
|------|-----|
| Live Demo | https://datasync-dashboard.vercel.app |
| Repository | https://github.com/RiyaKaushik-tech/datasync-dashboard |

---

## Key Features

- **Authentication & session-aware UI** via **Clerk** (`@clerk/nextjs`)
- **Protected pages** with a reusable guard component (`src/components/ProtectedPage.tsx`)
- **Movies**
  - Trending movies feed (RTK Query)
  - Genre browsing (RTK Query + conditional fetching via `skip`)
  - **Debounced search** on the client (`useDebounce`, 300ms)
- **News**
  - Top headlines via a **Next.js API route** proxying **NewsAPI** (`src/pages/api/news.ts`)
- **Favorites**
  - Add/remove favorites stored **per user**
  - Client-side persistence via **localStorage sync** in the Redux store (`src/store/index.ts`)
  - API route for favorites read/write (`src/pages/api/favorites.ts`)
- **Theme toggle** (light / “soft-dark”) persisted in `localStorage` (`dashsync_theme`)
- **Global error containment** using an `ErrorBoundary` wrapper (`src/components/ErrorBoundary`)

---

## Technical Architecture Overview

**High-level flow**

- **UI Layer (Next.js Pages Router)** renders dashboard pages:
  - `/` (home), `/Movie`, `/News`, `/Favorite`, `/setting`, `/SignIn`, `/SignUp`
- **Auth Layer (Clerk)**
  - `middleware.ts` configures Clerk middleware and declares public routes.
  - Pages and components use `useUser()` to drive gated UX.
- **Data Layer**
  - **RTK Query** drives Movies and News data fetching via feature APIs (`src/features/**`).
  - **Next.js API routes** proxy external calls and encapsulate server-side access to API keys.
- **State Layer (Redux Toolkit)**
  - Central store composed of slices + RTK Query reducers.
  - Store subscribes client-side to persist `favorites` and `userPreferences` to `localStorage`.

---

## Tech Stack

### Frontend
- **Next.js 15** (Pages Router)
- **React 19**
- **TypeScript**

### Backend (if exists)
- **Next.js API Routes**
  - `GET /api/news` → NewsAPI proxy
  - `GET/POST /api/favorites` → per-user favorites persistence helpers

### State Management
- **Redux Toolkit**
- **RTK Query**
- `react-redux`
- (`redux-persist` is installed but local persistence is currently implemented manually via store subscription)

### APIs
- **NewsAPI** (via `https://newsapi.org/v2/top-headlines`)
- **TMDB API** (movies/genres via RTK Query feature API)

### Authentication
- **Clerk** (`@clerk/nextjs`, `@clerk/backend`)

### Styling / UI
- **Tailwind CSS**
- `clsx` / `classnames`
- **Framer Motion** (installed; used for UI animation where applicable)
- **lucide-react** / `react-icons`

### Tooling
- ESLint (Next.js config)
- Jest + Testing Library (installed)
- Cypress (installed)

---

## Folder Structure

```text
datasync-dashboard/
├─ README.md
├─ eslint.config.mjs
├─ middleware.ts
├─ next.config.ts
├─ package.json
├─ postcss.config.js
├─ tailwind.config.js
├─ tsconfig.json
└─ src/
   ├─ app/
   │  └─ layout.tsx
   ├─ components/
   │  ├─ Error.tsx
   │  ├─ ErrorBoundary.tsx
   │  ├─ errorSlice.tsx
   │  ├─ Loadert.jsx
   │  ├─ MovieCard.tsx
   │  ├─ Navbar.tsx
   │  ├─ NewsCard.tsx
   │  ├─ NewsModal.tsx
   │  ├─ ProtectedPage.tsx
   │  ├─ Sidebar.tsx
   │  └─ useDebounce.ts
   ├─ features/
   │  ├─ favorite/
   │  │  └─ favoriteSlice.ts
   │  ├─ movies/
   │  │  └─ movieApi.tsx
   │  ├─ news/
   │  │  ├─ newApi.ts
   │  │  ├─ NewsSlice.ts
   │  │  └─ savedNewsSlice.ts
   │  ├─ ui/
   │  │  ├─ globalErrorSlice.ts
   │  │  └─ uiSlice.ts
   │  ├─ uiError/
   │  │  └─ uiErrorSlice.ts
   │  └─ user/
   │     ├─ preferencesSlice.ts
   │     ├─ UserApi.ts
   │     └─ userSlice.ts
   ├─ layouts/
   │  └─ DashboardLayout.tsx
   ├─ pages/
   │  ├─ _app.tsx
   │  ├─ Favorite.tsx
   │  ├─ index.tsx
   │  ├─ Movie.tsx
   │  ├─ News.tsx
   │  ├─ setting.tsx
   │  ├─ SignUp.tsx
   │  ├─ api/
   │  │  ├─ favorites.ts
   │  │  └─ news.ts
   │  └─ SignIn/
   │     └─ [[...index]].tsx
   ├─ providers/
   │  └─ ThemeProvider.tsx
   ├─ store/
   │  └─ index.ts
   ├─ styles/
   │  └─ globals.css
   ├─ types/
   │  ├─ movieType.ts
   │  └─ NewsArtcle.ts
   └─ utils/
      ├─ clerkFavorites.ts
      └─ userFavorites.ts
```

---

## Installation & Setup

### Prerequisites
- Node.js 18+ (recommended)
- A **Clerk** application (publishable key)
- **NewsAPI** key
- **TMDB** key (required by the movies RTK Query integration)

### Install
```bash
git clone https://github.com/RiyaKaushik-tech/datasync-dashboard.git
cd datasync-dashboard
npm install
```

### Run locally
```bash
npm run dev
# http://localhost:3000
```

### Production build
```bash
npm run build
npm run start
```

---

## Environment Variables

No `.env*` files are committed in the repository. The code references the following environment variables:

| Variable | Where used | Purpose |
|---------|------------|---------|
| `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` | `src/pages/_app.tsx` | Initializes `ClerkProvider` |
| `NEXT_PUBLIC_NEWS_API_KEY` | `src/pages/api/news.ts` | Server-side header to NewsAPI (`X-Api-Key`) |

> TMDB credentials are expected by the movies API layer (`src/features/movies/movieApi.tsx`). Configure the required TMDB key(s) according to that file’s implementation.

Create a local `.env.local`:

```bash
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=...
NEXT_PUBLIC_NEWS_API_KEY=...
# TMDB key(s) as required by src/features/movies/movieApi.tsx
```

---

## Usage Guide

1. **Start the app** and open `http://localhost:3000`.
2. **Sign up / sign in** using Clerk:
   - `/SignUp` for registration
   - `/SignIn` for login
3. Navigate using the top navbar:
   - **Movies** (`/Movie`): trending + filter by genre + debounced search
   - **News** (`/News`): top headlines (via `/api/news`)
   - **Favorites** (`/Favorite`): saved movies for the signed-in user
   - **Settings** (`/setting`): user preferences (stored in Redux + persisted to localStorage)

---

## Engineering Highlights

- **RTK Query for network orchestration**
  - Uses generated hooks (e.g., `useGetTrendingMoviesQuery`, `useGetGenresQuery`)
  - Conditional fetching via `skip` to avoid unnecessary network calls when no genre is selected.
- **Client-side persistence without external storage**
  - Store bootstrap reads from `localStorage` on the client and dispatches `setInitial` actions.
  - Store subscription keeps `favorites` and `userPreferences` consistent across refreshes.
- **API key handling**
  - News requests go through a **server route** (`/api/news`) so the external API call is made server-side.
- **Reusable auth guard**
  - `ProtectedPage` provides a consistent gated UX and uses Clerk’s `SignInButton` modal.

---

## Performance / Optimization Notes

- **Debounced search** for movies reduces render churn and avoids filtering on every keystroke (`useDebounce`, 300ms).
- **Conditional queries** (`skip`) prevent fetching genre-specific movies until a genre is selected.
- **Client-only guards** (e.g., favorites page uses an `isClient` flag) avoid hydration issues when accessing `localStorage`.

---

## Security Considerations

- **Clerk middleware** (`middleware.ts`) enforces authenticated access outside declared public routes.
- **API keys**
  - NewsAPI key is accessed in a server context via `/api/news`, but is currently referenced as `NEXT_PUBLIC_NEWS_API_KEY`. In production, prefer a non-public env var name (e.g., `NEWS_API_KEY`) to reduce accidental exposure patterns.
- **Favorites API**
  - `/api/favorites` accepts a `userId` from the request. For stronger security, validate the caller’s identity server-side (e.g., derive user ID from Clerk session) rather than trusting user-provided IDs.

---

## Future Improvements

- Replace client `alert()` reminders in `DashboardLayout` with a non-blocking toast system.
- Strengthen `/api/favorites` authorization by verifying the authenticated Clerk user on the server.
- Add explicit `.env.example` with required variables and documentation for TMDB configuration.
- Expand automated testing:
  - Unit tests for slices and utilities
  - Cypress coverage for auth-gated flows
- Align theming approach (`next-themes` is installed) to a single source of truth for theme state.

---

## Author

**Riya Kaushik**

---

## License

MIT License (as indicated in the repository README badge). Add a `LICENSE` file to the repository root to make this explicit in-source.
