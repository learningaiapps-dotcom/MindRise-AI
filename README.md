# MindRise AI

Personal 30-minute daily development PWA: reading comprehension, memory, rapid thinking, and speech practice. Languages: English, Hindi, Gujarati.

## Status
Initial deployment scaffold. The full MVP project ZIP is available in the ChatGPT conversation; upload its contents into this repository for the complete interface and API.

## Neon
Existing Neon project `Self learning` contains the `sessions` and `attempts` tables required by the MVP source ZIP, plus seven `mindrise_*` future-schema tables.

## Deployment
Use Node.js 22 LTS. Set `DATABASE_URL`, `APP_PASSWORD`, `JWT_SECRET`, `OPENAI_API_KEY`, `FRONTEND_ORIGIN`, and `NODE_ENV` as Render environment variables. Never commit secrets. Run `npm install`, `npm run build`, and `npm start` after uploading the ZIP source. A Render web service can serve the built client and API together.

**Important:** This repo is currently public. Change its visibility to private before adding personal data or configuration.
