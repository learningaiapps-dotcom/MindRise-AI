# Cloudflare Worker setup

This Worker replaces the Express API when the React PWA is hosted on Render Static Sites.

## Deploy
1. Create a Cloudflare account and open Workers & Pages.
2. In the GitHub repository, use the `worker` directory as the Worker project root.
3. Install dependencies and deploy from that directory with `npm install` and `npm run deploy` (Wrangler login is required).
4. Set Worker environment variables and secrets in Cloudflare dashboard under Settings > Variables and Secrets:
   - Secret: `DATABASE_URL` (Neon pooled connection string)
   - Secret: `JWT_SECRET` (long random secret)
   - Secret: `OPENAI_API_KEY` (optional)
   - Variable: `GOOGLE_CLIENT_ID`
   - Variable: `GOOGLE_ALLOWED_EMAIL`
   - Variable: `FRONTEND_ORIGIN` (exact Render static HTTPS origin, no trailing slash)
   - Variable: `OPENAI_MODEL` (optional)
5. Deploy and test `https://<worker-address>/api/health`.

## Render Static Site
Repository: MindRise-AI. Build command: `npm install && npm run build`. Publish directory: `client/dist`.
Add **build-time** variable `VITE_API_URL=https://<worker-address>`. Redeploy after setting it.

## Google Cloud
Add your exact Render HTTPS origin to Authorized JavaScript origins of the Google Web OAuth client. No Google client secret is needed for the ID-token button flow.

## Known limitation
Because the static site and API use different top-level domains (`onrender.com` and `workers.dev`), the current authentication cookie uses `SameSite=None; Secure`. Browsers that block third-party cookies can reject it, breaking login persistence. A same-site custom domain with an API subdomain, or a carefully designed alternative session transport, is required for reliable cross-browser production use. Do not consider this deployment production-ready until login, session persistence and all exercise flows are tested on your target devices.

## Security
Do not commit real credentials or put them in the frontend `VITE_*` variables. Cloudflare secrets must stay server-side.
