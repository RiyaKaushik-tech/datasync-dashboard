# 🚀 DashSync – Personalized Dashboard for Movies & News

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT) [![Next.js](https://img.shields.io/badge/Next.js-13-blue?logo=next.js)](https://nextjs.org/) [![React](https://img.shields.io/badge/React-18-blue?logo=react)](https://reactjs.org/) [![TypeScript](https://img.shields.io/badge/TypeScript-4.9-blue?logo=typescript)](https://www.typescriptlang.org/) [![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.3-blue?logo=tailwind-css)](https://tailwindcss.com/)

DashSync is a **Next.js + TypeScript** web application that aggregates **trending movies** and **top news articles**, personalized to each user’s **preferences** (genre + category) with **authentication**.

---

## 👩‍💻 Author

**Riya Kaushik – Frontend Developer**  
📍 Karnal, Haryana  
📧 [riyakaushik6410@gmail.com](mailto:riyakaushik6410@gmail.com)  
📱 +91 89309 42202  
🔗 [GitHub](https://github.com/riya1807pro) • [LinkedIn](https://www.linkedin.com/in/riyakaushik-webdev)  

---

## 🌟 Live & Code

[![Live Demo](https://img.shields.io/badge/Live-Demo-green)](https://datasync-dashboard.vercel.app) [![GitHub Code](https://img.shields.io/badge/GitHub-Code-blue)](https://github.com/riya1807pro/riya1807pro-datasync-dashboard)

---

## ✅ Features

| Feature | Status |
|--------|--------|
| 🔐 User Authentication (Clerk) | ✅ |
| 😍 Add / Remove Favorites | ✅ Per-user (Local + Clerk) |
| ⚙ User Preference Panel | ✅ Movie & News Preferences |
| 🔥 Trending Movies Feed | ✅ |
| 📰 Top News Feed | ✅ |
| 🧠 Personalized Home | ✅ Based on Preferences |
| 🌓 Light / Soft-Dark Theme | ✅ Toggle in Navbar |
| 🔎 Debounced Movie Search | ✅ |
| 🎞 Hover Trailer (Movies) | ✅ Plays after 2s hover |
| 💬 News Modal | ✅ Opens article without redirect |
| 🛡 Protected Routes | ✅ Favorites, Movies, Settings |

---

## 🛠️ Tech Stack

- **Frontend:** Next.js 15 (Pages Router), React 18, TypeScript  
- **State Management:** Redux Toolkit + RTK Query  
- **Authentication:** Clerk  
- **APIs:** NewsAPI, TMDB API  
- **UI & Animation:** TailwindCSS, Framer Motion  
- **Other:** React hooks, debounce utilities  

---

## 📁 Folder Structure

```text
riya1807pro-datasync-dashboard/
├─ README.md
├─ eslint.config.mjs
├─ middleware.ts
├─ next.config.ts
├─ package.json
├─ postcss.config.js
├─ tailwind.config.js
├─ tsconfig.json
└─ src/
   ├─ app/layout.tsx
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
   │  ├─ favorite/favoriteSlice.ts
   │  ├─ movies/movieApi.tsx
   │  ├─ news/newApi.ts
   │  ├─ news/NewsSlice.ts
   │  ├─ news/savedNewsSlice.ts
   │  ├─ ui/globalErrorSlice.ts
   │  ├─ ui/uiSlice.ts
   │  ├─ uiError/uiErrorSlice.ts
   │  └─ user/
   │       ├─ preferencesSlice.ts
   │       ├─ UserApi.ts
   │       └─ userSlice.ts
   ├─ layouts/DashboardLayout.tsx
   ├─ pages/
   │  ├─ _app.tsx
   │  ├─ Favorite.tsx
   │  ├─ index.tsx
   │  ├─ Movie.tsx
   │  ├─ News.tsx
   │  ├─ setting.tsx
   │  ├─ SignUp.tsx
   │  ├─ api/favorites.ts
   │  ├─ api/news.ts
   │  └─ SignIn/[[...index]].tsx
   ├─ providers/ThemeProvider.tsx
   ├─ store/index.ts
   ├─ styles/globals.css
   ├─ types/
   │    ├─ movieType.ts
   │    └─ NewsArtcle.ts
   └─ utils/
        ├─ clerkFavorites.ts
        └─ userFavorites.ts
```
## ⚙ Setup
```
git clone https://github.com/riya1807pro/riya1807pro-datasync-dashboard.git
cd riya1807pro-datasync-dashboard
bun install              # or npm / yarn
bun dev                  # runs at http://localhost:3000

```

📸 Demo Screenshots

Visit Live: https://datasync-dashboard.vercel.app

---

⭐ If you like this project, please consider giving it a star on GitHub!  
💬 Feedback, suggestions, or collaborations are always welcome.  
🚀 Built with ❤️ by **Riya Kaushik**
