# Campus Cue Frontend (`client`)

React 19 + Vite + Tailwind CSS v3 frontend for **Campus Cue (`clg.inbox`)**.

## Setup & Scripts

```bash
# Install dependencies (or run `npm run install:all` from the repo root)
npm install

# Start Vite dev server at http://localhost:5173 (proxies /api -> http://localhost:5001)
npm run dev

# Build production bundle into client/dist/
npm run build

# Run UserContext & greeting state verification tests
npm run test:user
```

## Key Implementation Notes

- **API Client & User Isolation (`src/utils/api.js`):** All API requests go through `apiFetch()`, which attaches the `x-user-email` header (`getActiveUserEmail()`) so backend endpoints return `401` on unauthenticated calls and isolate data per user.
- **Deployment (`VITE_API_URL`):** Leave `VITE_API_URL` unset during local development to use the Vite `/api` proxy in `vite.config.js`. Set `VITE_API_URL` in `client/.env` (or your hosting provider) when deploying the frontend separately from the backend.
- **AI Transparency UI:** `InboxView`, `EmailDetailView`, `DigestView`, `HomeView`, and `SettingsModal` surface live `/api/health` AI probe status (`aiMode`, `model`, `aiError`) and distinguish `AI-generated` analysis from `Basic analysis (AI offline)` and `AI Failed` states with one-click reprocess controls.
