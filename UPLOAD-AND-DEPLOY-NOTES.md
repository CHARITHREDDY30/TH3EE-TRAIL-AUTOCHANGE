# TH3EE — GitHub Upload Package

This package contains the project source and configuration needed to install and build the TH3EE storefront.

## Important

- `.env` and `.insforge/` were deliberately excluded because they can contain credentials or project-specific secrets.
- `dist/` and source maps were excluded because they are generated build artifacts.
- `node_modules/` is not included; install dependencies using `npm ci`.

## Setup

1. Upload these files to the intended GitHub repository.
2. In the hosting provider's environment-variable settings, configure the required values from `.env.example`:
   - `VITE_INSFORGE_URL`
   - `VITE_INSFORGE_ANON_KEY`
   - `VITE_R2_PUBLIC_BASE_URL`
   - `VITE_RAZORPAY_KEY_ID` only if the frontend uses Razorpay checkout.
3. Use only a public/anonymous InsForge key in browser-facing `VITE_` variables. Never expose InsForge full-access keys, R2 secret keys, or payment secret keys.
4. Run `npm ci`, `npm run typecheck`, and `npm run build`.

## Hosting limitation

GitHub Pages hosts static frontend files only. It does not run the `functions/r2-upload/index.ts` server/edge function or any backend process. Deploy that function separately to the supported InsForge Edge Functions environment and configure its secrets there. InsForge database/auth and Cloudflare R2 remain external services.

For Vite SPA routing, configure the appropriate base path for the GitHub repository, or use Vercel for the existing domain/root-path setup. Verify all routes and environment variables in a Preview deployment before using production.
