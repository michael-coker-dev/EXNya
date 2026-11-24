# EXNYA — Security status

This document describes the security posture visible in this repository. It is not a penetration-test report, and it does not establish that the live Supabase project is configured safely.

> **Important: prototype only.** Do not use EXNYA to hold funds, execute real trades, collect real identity documents or provide financial services.

## What is present in the source

- A browser Supabase client configured with the project URL and public anon key. A Supabase anon/publishable key is designed to be public; security depends on correctly configured Row Level Security and backend permissions.
- SQL migration files that enable RLS and define user/admin policies.
- Security-definer database functions for swap and P2P state transitions.
- A password-reset Edge Function source file that expects service credentials and email-provider secrets to be stored in the Edge Function environment, not in browser code.
- A Content Security Policy meta tag on several pages. The current policy permits inline scripts and styles, so it is not a strict nonce/hash-based CSP.

These are source-code observations only. The actual deployed database, storage bucket, Auth settings, Edge Functions and secrets have not been verified.

## Important limitations found during repository review

1. **Swap pricing is client supplied.** The browser sends the price object to `swap_execute`. The SQL function validates the submitted quote against that same supplied object; it does not independently obtain a trusted market price. This is not safe for real-value exchange.
2. **P2P is not real escrow.** The SQL describes escrow as conceptual and does not demonstrate funds being held by a trusted custodian or on-chain contract. The transition function also needs stricter role-specific authorization for each action before any real-value use.
3. **Deployment state is unknown.** A migration file in GitHub does not mean it has been applied to Supabase. Confirm the live schema, grants, RLS policies, Storage policies and Edge Function configuration separately.
4. **Security headers need deployment configuration.** A meta CSP does not replace HTTP response headers such as HSTS, `X-Content-Type-Options` and an appropriate `Permissions-Policy`.
5. **KYC handling needs a production review.** Keep the KYC bucket private, enforce file size and MIME restrictions, verify object ownership server-side, and use short-lived signed URLs only where necessary.

## Before any production use

- Replace browser-supplied swap prices with a trusted server-side quote source and enforce freshness, slippage, asset allow-lists and transaction limits.
- Redesign P2P transitions so only the correct party can perform each action; implement actual escrow custody and dispute resolution before describing funds as reserved.
- Review every RLS policy, SQL function grant and Storage policy against the deployed project.
- Confirm service-role and email-provider secrets exist only in server-side secret storage. Rotate any privileged secret if it was ever exposed.
- Enable email confirmation, leaked-password protection, sensible rate limits/CAPTCHA and MFA policy.
- Add server-side validation, monitoring, audit review, backups and incident-response procedures.
- Obtain an independent security review before handling money or identity documents.

## Reporting a security issue

Do not publish credentials, personal data or exploitable details in a public issue. Contact the repository owner privately with a concise description and reproduction steps.
