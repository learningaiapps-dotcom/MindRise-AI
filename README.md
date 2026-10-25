# MindRise AI

A personal, mobile-friendly 30-minute daily personality-development PWA with four activities: reading comprehension (8 min), memory recall (7 min), rapid reasoning (7 min), and speech practice (8 min). English, Hindi, and Gujarati language selection is available; the fallback sample lessons are primarily English.

## Stack
React 19 + Vite frontend, Node.js/Express API, Neon PostgreSQL database, optional OpenAI API for lesson generation, semantic grading, and audio transcription. No Supabase.

## Setup
1. Use Node.js 22 LTS and run `npm install`.
2. Copy `.env.example` to `.env` and set `DATABASE_URL`, `APP_PASSWORD`, and `JWT_SECRET`. Never commit `.env`.
3. Run `npm run db:init` to create the `sessions` and `attempts` tables if they are missing. These tables have already been created in your connected Neon **Self learning** project.
4. For local development, run `npm run dev` and open http://localhost:5173.
5. For deployment, run `npm run build` and `npm start`; the Express server serves the built frontend and API together on `PORT`.

## Render deployment
Create a **Web Service** linked to this GitHub repository. Runtime: Node. Build command: `npm install && npm run build`. Start command: `npm start`. Set Node version to 22 with `NODE_VERSION=22`. In Render's **Environment** tab set:
- `DATABASE_URL`: the Neon pooled PostgreSQL connection URL
- `APP_PASSWORD`: a long private personal sign-in password
- `JWT_SECRET`: a separate random secret, at least 32 bytes
- `NODE_ENV`: `production`
- `OPENAI_API_KEY`: optional, required for AI lessons and transcription
- `OPENAI_MODEL`: optional, defaults to `gpt-4.1-mini`
- `FRONTEND_ORIGIN`: optional, your final Render HTTPS URL

Do not put secret values in GitHub, screenshots, or chat. For this single-user MVP, access is protected by a personal password. It is not a multi-user authentication system.

## Limitations
This is an initial MVP, not a fully validated production release. The 30-minute daily durations are guidance rather than enforced limits. Speech feedback scores transcript content only, not voice quality, pace or intonation. Offline fallback lessons are limited; some translations are partial. The OpenAI API is billed separately. The database schema includes a separate set of `mindrise_*` tables reserved for future development, but the MVP uses `sessions` and `attempts`.

## Security
The GitHub repository is currently public. Make it private before storing personal information. The application must use HTTPS in production. Never expose the Neon connection string or API keys in client-side code.
