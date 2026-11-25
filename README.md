# EXNYA

A cryptocurrency-exchange interface prototype built with HTML, CSS, JavaScript and Supabase.

> **Project status: prototype / portfolio project.** EXNYA is not a live cryptocurrency exchange, broker, custodian, payment service or investment product. Do not deposit funds, submit identity documents, or use it for real trading.

## Portfolio case study

See the [EXNYA project case study](https://michael-coker-dev.github.io/michael-coker-portfolio/exnya.html) for the project brief, interface scope, technologies and known limitations.

## What the project demonstrates

- Multi-page responsive exchange interface
- Email/password authentication flows
- Account profile and settings screens
- Wallet and asset-balance interface
- Swap and peer-to-peer trading screens
- Admin and KYC review interface concepts
- Supabase database migrations and an Edge Function example
- Dark and light themes

## Technology

- HTML5
- CSS3
- Vanilla JavaScript
- Supabase Auth, PostgreSQL, Storage and Edge Functions
- GitHub Pages-compatible static frontend

## Project structure

- `index.html` — public landing page
- `pl.html` — sign-in page
- `signup.html`, `confirm.html` — account registration and confirmation
- `profile.html`, `settings.html`, `security.html` — account pages
- `markets.html`, `swap.html`, `wallet.html`, `p2p.html` — exchange interface screens
- `admin.html` — administrative interface
- `app-base.js`, `settings.js` — shared frontend helpers
- `supabase/migrations/` — database migration source files
- `supabase/functions/` — Edge Function source

## Running locally

Use a local HTTP server rather than opening the HTML files directly:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000/` in your browser. Authentication and database-backed features require a correctly configured Supabase project.

## Security and deployment status

The repository contains migration and security-hardening work, but source code alone does not prove that the live Supabase project has those migrations, policies, secrets, storage settings or authentication controls applied.

The swap flow currently receives its price data from the browser, so it is not a trusted server-priced exchange. The P2P flow is a prototype state machine, not a verified escrow service. These features must not be used with real funds until independently reviewed and redesigned with trusted server-side pricing, enforced party-specific transitions, and actual escrow custody.

See [SECURITY.md](SECURITY.md) and [DEPLOY.md](DEPLOY.md) before configuring any backend.

## Portfolio note

This project is presented as a demonstration of interface development and application architecture. It does not claim production readiness, real users, processed transactions or financial-service licensing.
