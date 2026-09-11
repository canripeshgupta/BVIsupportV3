# BVI Support — website

Static website for BVI Support: accounting, financial statements and Annual Financial Returns for BVI companies, serving registered agents and corporate service providers.

## Files

- `index.html`, `services/`, `pricing/`, `about/`, `contact/`, `legal/` — site pages, one `index.html` per directory
- `404.html` — not-found page (plain HTML, no runtime)
- `.htaccess` — 404 handling + 301s from the old URL layout
- `support.js` — page runtime (required, do not remove)
- `robots.txt`, `sitemap.xml`
- `favicon.png`, `ashwani.jpg`, `nripesh.jpg`

## URLs

Pages are served at `/`, `/services/`, `/pricing/`, `/about/`, `/contact/`, `/legal/` — real
directories, so any static host resolves them without rewrite rules. Internal links use
absolute paths (`/services/`, `/support.js`, …).

`.htaccess` 301s the two older URL shapes to these: the `*.dc.html` filenames and the
extensionless paths (`/services` → `/services/`).

## Deploy

Auto-deploys to bvisupport.com on push to `main`.

> **Do not remove the `build` script from `package.json`.** Hostinger's pipeline
> runs `npm run build` on every deploy (Framework: Other, Node 22.x). There is
> nothing to build — the site is published from the repo root — but if the script
> is missing, `npm run build` errors and the whole deploy fails with "Build
> failed". It exists purely to give that command something to succeed at.

- **Hostinger:** LiteSpeed honours `.htaccess`. Publish directory = repo root.
- **Netlify / Vercel / GitHub Pages:** the directory layout gives clean URLs on its
  own; only the 404 page and the legacy 301s would need porting.

## Editing

Pages come from the client's design-canvas export, which ships as this directory
layout. When a new export arrives, drop the pages in and re-check the items under
"Kept outside the export" below — the export does not carry them.

### Kept outside the export

These are maintained here and are **dropped by every fresh canvas export**, so
re-apply them after each one:

- `<link rel="canonical">` + `og:url` on all six pages
- Web3Forms lead delivery in `contact/index.html` (access key in that file), and the
  matching data-processor disclosure in the Legal page's `privacy` list
- `robots.txt`, `sitemap.xml`, `.htaccess`, `404.html`, `package.json`
- The real leadership portraits on About (the export replaces them with empty
  `<image-slot>` placeholders)

The export also **reverts content fixes** back to whatever the canvas still holds.
These three came back as stale values in the 2026-09-09 export and will keep
returning until the client corrects them in the canvas itself:

| Value | Correct | Canvas still has |
|---|---|---|
| `priceRange` in the Home page structured data | `$150 - $850` | `$100 - $750+` |
| Pricing, hourly tier `tag:` | `Time & materials` | `Time &amp; materials` |
| Pricing, hourly tier `price:` | `Starting from $15` | trailing non-breaking space |
| Contact form WhatsApp fallback | `17786360270` | `919855142280` |

`priceRange` must match the fixed-fee tier on the Pricing page; `Time &amp;`
renders verbatim because bound values go through text interpolation, which
escapes them.

Contact email: contact@bvisupport.com · Phone: (+1) 778 636 0270 — both appear in every page footer and the Contact page.
Contact-form leads are delivered by Web3Forms (access key in `contact/index.html`).
