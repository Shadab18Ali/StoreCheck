# StoreCheck

A free-first Shopify storefront health checker built as a Cloudflare Worker. No Shopify Admin access, paid API, database, or build step is required for the starter MVP.

## Run locally

Install Node.js 20+ and run:

```bash
npm install
npm run dev
```

Open the local URL printed by Wrangler. Health endpoint: `/api/health`.

## Deploy for free

1. Create/sign in to Cloudflare.
2. Run `npx wrangler login`.
3. Run `npm run deploy`.

The first deployment uses the free `workers.dev` subdomain. No custom domain is required.

## Current MVP checks

- Public URL validation and basic private/local hostname rejection.
- Redirect handling with redirect target validation.
- Page title and meta description.
- H1 count and canonical signal.
- Image alt attributes.
- HTML language attribute.
- Shopify storefront signals.
- Robots noindex signal.
- Public robots.txt and sitemap.xml availability.

## Limitations

This is an early MVP and scans the homepage only. Performance metrics, deep crawling, PDF export, authentication, saved scan history, and robust global rate limiting are not yet implemented. Add platform-level rate limits and further SSRF hardening before opening the scanner to unrestricted public traffic. The score is an advisory checklist score, not a Google ranking prediction.
