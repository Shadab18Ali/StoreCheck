# StoreCheck

StoreCheck is a free website and Shopify storefront audit tool. It is designed for ordinary websites, ecommerce stores, and Shopify stores. The app is a Cloudflare Worker with a lightweight browser interface; it does not require a Shopify login, private API token, paid API, database, or frontend build pipeline.

## Current features
- Accepts public HTTP and HTTPS website URLs.
- Follows a limited number of redirects and validates redirect destinations.
- Inspects the homepage plus up to four additional same-origin pages discovered from the sitemap or homepage links.
- Checks page titles, meta descriptions, H1 headings, canonical links, image alt attributes, document language, indexability, and mobile viewport signals.
- Checks HTTPS, robots.txt, and sitemap.xml availability.
- Detects common public Shopify storefront signals while continuing to audit non-Shopify websites.
- Reports pass/warning/fail findings with evidence and recommended actions.
- Displays a simple advisory health score and supports browser print / Save as PDF.

## Architecture
- Cloudflare Workers (free tier suitable for an early, low-volume MVP).
- TypeScript; no database or paid third-party API.
- worker/index.ts serves the app and the /api/scan endpoint.
- /api/health returns a basic service health response.

## Deploy
The project is configured for a free workers.dev subdomain. Deployment requires an authorized Cloudflare account. A repository-connected deployment workflow can be added after the Cloudflare account is connected and its deployment credentials are configured securely in GitHub Actions. Do not commit API tokens or account secrets to this repository.

## Developer commands
These commands are for maintainers who choose to work locally; they are not required for a user of the hosted application.

```bash
npm install
npm run typecheck
npm run dev
npm run deploy
```

## Current limitations and safety
- The scanner samples a maximum of five pages; it is not a complete site crawler.
- The score is a simple checklist score, not a Google ranking prediction, Core Web Vitals measurement, accessibility certification, or conversion analysis.
- Performance lab metrics, authenticated scans, saved scan history, scheduled scans, PDF generation beyond browser print, and competitor comparisons are not implemented yet.
- Only public storefront HTML and a small number of same-origin resources are inspected. Pages blocked by bot protection or requiring login may not be accessible.
- URL and redirect validation blocks common local/private address patterns, but a public URL scanner needs additional platform-level abuse controls and stronger network-level SSRF protections before unrestricted public launch. Keep the early deployment low-volume and add rate limiting / abuse monitoring before promoting it widely.
- Never submit private URLs, internal hostnames, credentials, or sensitive customer data.

## Cost
The intended MVP uses Cloudflare Workers' free tier and does not depend on paid APIs or a database. Cloudflare's current plan limits and pricing always apply; monitor usage before public promotion.
