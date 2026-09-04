# BVI Support — website

Static website for BVI Support: accounting, financial statements and Annual Financial Returns for BVI companies, serving registered agents and corporate service providers.

## Files

- `Home.dc.html`, `Services.dc.html`, `Pricing.dc.html`, `About.dc.html`, `Contact.dc.html`, `Legal.dc.html` — site pages
- `404.html` — not-found page (plain HTML, no runtime)
- `.htaccess` — clean URLs + redirects + 404 handling (see below)
- `support.js` — page runtime (required, do not remove)
- `robots.txt`, `sitemap.xml`
- `favicon.png`, `ashwani.jpg`, `nripesh.jpg`

## URLs

Pages are served at clean paths — `/`, `/services`, `/pricing`, `/about`, `/contact`, `/legal` — via `.htaccess` rewrites to the `*.dc.html` files. The old `*.dc.html` URLs 301 to the clean paths. Internal links use absolute paths (`/services`, `/support.js`, …).

## Deploy

Auto-deploys to bvisupport.com on push to `main`.

> **Do not remove the `build` script from `package.json`.** Hostinger's pipeline
> runs `npm run build` on every deploy (Framework: Other, Node 22.x). The script's
> `dist/` output is unused — the site is published from the repo root — but if the
> script is missing, `npm run build` errors and the whole deploy fails with
> "Build failed". It exists purely to give that command something to succeed at.

- **Hostinger:** LiteSpeed honours `.htaccess`. Publish directory = repo root.
- **Netlify / Vercel:** would need the clean-URL rules ported to `_redirects` / `vercel.json` (currently Apache/LiteSpeed `.htaccess` only).

## Editing

Contact email: contact@bvisupport.com · Phone: (+1) 778 636 0270 — both appear in every page footer and the Contact page.
Contact-form leads are delivered by Web3Forms (access key in `Contact.dc.html`).
