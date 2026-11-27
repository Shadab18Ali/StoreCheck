# StoreCheck — Project Status

Last updated: 2026-11-27

This file is the source-of-truth checklist for what has been implemented, verified, and remains to be done. Update it whenever a meaningful project milestone changes.

## Product goal

Build a free-first website and Shopify store checker. Users can enter a public website URL; StoreCheck scans a small set of same-origin pages and reports practical SEO, accessibility/content, indexability, and technical checks. Shopify storefronts are supported alongside ordinary websites.

## Completed in the repository

- [x] Created the `Shadab18Ali/StoreCheck` GitHub repository and established `main` as the working branch.
- [x] Added the Cloudflare Worker application in `worker/index.ts`.
- [x] Added a browser-based interface for entering a website URL and viewing scan findings.
- [x] Added the `/api/health` and `/api/scan` endpoints.
- [x] Implemented a bounded scan of the homepage and up to four additional same-origin pages discovered from sitemap/homepage links.
- [x] Added checks covering page title, meta description, H1, canonical URL, image alt text, document language, mobile viewport, noindex, HTTPS, robots.txt, and sitemap availability.
- [x] Added Shopify storefront signal detection without excluding ordinary websites.
- [x] Added findings, score, evidence, recommendations, and browser print / Save as PDF support.
- [x] Added `wrangler.toml`, `package.json`, and `tsconfig.json`.
- [x] Added GitHub Actions workflow `.github/workflows/ci-deploy.yml` for validation and deployment.
- [x] Updated `README.md` with product scope, features, limitations, and deployment setup.
- [x] GitHub Actions TypeScript validation passed in run [45971021489](https://github.com/Shadab18Ali/StoreCheck/actions/runs/45971021489).

## Cloudflare setup — current status

- [x] Cloudflare account dashboard opened.
- [x] GitHub repository `Shadab18Ali/StoreCheck` selected in the Cloudflare Workers & Pages creation flow.
- [ ] Finish Cloudflare project creation / first deployment.
- [ ] Confirm the Worker is deployed and record its actual `workers.dev` URL.
- [ ] Configure GitHub repository secrets `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` for the GitHub Actions deployment workflow, if using that workflow.
- [ ] Verify a successful GitHub Actions deployment after credentials are configured.
- [ ] Run live smoke tests against the deployed `/api/health` and `/api/scan` endpoints.

**Important:** The previously inspected Actions run passed validation, but its deployment step was skipped because the Cloudflare GitHub secrets were blank. That run does not prove that StoreCheck has been deployed. The Cloudflare dashboard's GitHub connection wizard is currently in progress; repository selection alone is not a completed deployment.

## Remaining product and launch work

- [ ] Review and improve URL validation and SSRF protections, including DNS resolution / private-address checks and redirect handling.
- [ ] Add abuse protection such as rate limiting and sensible scan quotas before exposing the scanner publicly.
- [ ] Add robust handling for timeouts, oversized pages, malformed HTML, and unreachable sitemap/robots files.
- [ ] Test against representative Shopify stores and ordinary websites.
- [ ] Review accessibility, mobile layout, and scan-result clarity.
- [ ] Add automated tests for scanner parsing and security-sensitive URL handling.
- [ ] Document supported checks and known limitations for users.
- [ ] Decide whether to add scan history, exports, or additional checks after the MVP is stable.

## Operating rules

- Keep the product free-first unless a cost is explicitly approved.
- Make changes directly in GitHub / online services; do not require the project owner to use a local terminal or install tools locally.
- Never ask the project owner to paste API tokens or secrets into chat.
- Never describe a deployment or live test as successful until the platform confirms it.
- Update this checklist whenever a task is completed, verified, blocked, or descoped.
