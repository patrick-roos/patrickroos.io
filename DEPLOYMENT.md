# Deploy and SEO Checklist

## Cloudflare Pages setup

1. Create a new Cloudflare Pages project connected to this GitHub repo.
2. Use these build settings:
   - Build command: `npm run build`
   - Build output directory: `dist`
   - Node version: `20` (or newer LTS)
3. Add custom domain `patrickroos.io` to the Pages project.
4. Set primary domain to `https://patrickroos.io` and enable automatic HTTPS.

## Ongoing content updates

- Add new posts in `src/content/posts/*.md` with this frontmatter:

```md
---
title: Your Title
description: One-sentence summary for SEO and post cards.
pubDate: 2026-02-18T12:00:00Z
tags:
  - ai
  - ml
---
```

- Run locally:
  - `npm run dev`
  - `npm run build`

## SEO actions after first deploy

1. Submit sitemap: `https://patrickroos.io/sitemap-index.xml` in Google Search Console.
2. Verify domain property in Google Search Console and Bing Webmaster Tools.
3. Keep post titles/descriptions specific and human-readable.
4. Keep redirects in `public/_redirects` when changing URLs.
5. Add internal links between related posts when possible.

