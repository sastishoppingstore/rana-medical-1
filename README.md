# Rana Medical — Clinic 1

Full-stack clinic website: static frontend (multi-page, single index.html) + Vercel serverless demo API.

## Layout
- `web/` — static frontend (deployed to Firebase Hosting at `https://wafasmart.tech/clinic1`)
- `api/` — Vercel serverless backend (deployed as its own Vercel project)
  - `api/index.js` — single dispatcher for all `/api/*` routes
  - `lib/policies.js` — role permissions & helpers
  - `vercel.json` — rewrites + CORS
  - `local-server.js` — local dev server (node local-server.js)

## Backend (Vercel project `rana-medical-clinic1`)
- Auth: stateless HMAC bearer token. The frontend stores `rmh_demo_token` in
  localStorage and injects `Authorization: Bearer <token>` on every `/api` fetch.
- Data: one Supabase Postgres database, table `demo_state` (single-row JSONB).
- Env var on Vercel: `DATABASE_URL` (Supabase transaction pooler, port 6543):
  `postgresql://<user>:<pass>@aws-1-ap-south-1.pooler.supabase.com:6543/clinic1`

## Local dev
```bash
cd api && npm install && DATABASE_URL=postgresql://...:6543/clinic1 node local-server.js
```
Frontend: serve `web/` over HTTP and open it; the built-in fetch patch targets the Vercel URL.
