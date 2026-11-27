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
- [x] Created the Cloudflare Worker project `storecheck` from the connected GitHub repository.
- [x] First Cloudflare deployment completed successfully: green Build #9be11e5b, with initialization, cloning, installation, and deployment stages all successful (17 seconds).
- [x] Confirmed deployment settings in Cloudflare: project `storecheck`, repository `Shadab18Ali/StoreCheck`, branch `main`, root directory `/`, no build command, deploy command `npx wrangler deploy`, and build token named `StoreCheck GitHub Deployment`.
- [ ] Enable the `workers.dev` subdomain and verify the public URL `storecheck.shadab18ali.workers.dev` (Cloudflare currently shows workers.dev Disabled and No URLs enabled).
- [ ] Configure GitHub repository secrets `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` for the GitHub Actions deployment workflow, if using that workflow.
- [x] Verified automatic Cloudflare deployment from GitHub: Cloudflare Overview shows a GitHub-linked `main` build (`27fec49d`) marked Ready after the project-status commit.
- [ ] Separately verify the GitHub Actions deployment workflow; the earlier Actions run skipped its deploy step because the GitHub repository secrets were blank.
- [ ] Run live smoke tests against the deployed `/api/health` and `/api/scan` endpoints after enabling workers.dev.

**Deployment note:** Cloudflare now shows a successful first deployment (Build #9be11e5b) from the connected `main` branch. The screenshot labels this deployment “Manually deployed”; automatic deployment on subsequent GitHub commits still needs to be verified. The separate GitHub Actions workflow's deploy step was previously skipped because `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` were blank. Do not treat that workflow as deployed until its own run succeeds.

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
