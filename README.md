# SizeUP

Static landing page for SizeUP. Target domain: **sizeup.fun**.

## Layout

- `docs/` — everything published. `docs/index.html` is the whole site: inline
  CSS/JS, base64 images, no build step, no dependencies.
- `wrangler.jsonc` — Cloudflare Workers static-assets config (primary host).
- `.github/workflows/deploy.yml` — GitHub Pages fallback, if Actions is ever needed.

## Local preview

```bash
python3 -m http.server 8000 --directory docs
# http://localhost:8000
```

## Deploying to Cloudflare (primary)

```bash
npx wrangler login     # one-time, opens a browser
npx wrangler deploy
```

That publishes to `sizeup.<your-subdomain>.workers.dev`.

### Attaching sizeup.fun

1. Register **sizeup.fun** and add the zone to Cloudflare (either register it
   through Cloudflare Registrar, or register elsewhere and point the registrar's
   nameservers at the two Cloudflare gives you).
2. Add the routes to `wrangler.jsonc`:

   ```jsonc
   "routes": [
     { "pattern": "sizeup.fun", "custom_domain": true },
     { "pattern": "www.sizeup.fun", "custom_domain": true }
   ]
   ```

3. `npx wrangler deploy`. Cloudflare creates the DNS records and issues the TLS
   certificate itself — there are no records to copy by hand.

Deploying from CI instead of a laptop needs a `CLOUDFLARE_API_TOKEN` with the
*Edit Cloudflare Workers* template, set as a secret rather than committed.

## GitHub Pages (fallback)

Settings → Pages → Source: **Deploy from a branch** → `main`, folder `/docs`.
Serves at `https://genefloodgate-ctrl.github.io/SizeUP/` with no Actions run
required. `docs/.nojekyll` keeps Jekyll from touching the files.

## www

Workers' `_redirects` only accepts relative URLs, so the www-to-apex redirect
cannot live in this repo. Add it as a zone-level Redirect Rule instead:
Cloudflare dashboard, Rules -> Redirect Rules -> hostname equals
`www.sizeup.fun` -> dynamic redirect to `concat("https://sizeup.fun", http.request.uri.path)`, 301.

## Images

The logo is white artwork whose shape lives entirely in the alpha channel, so
both images are encoded as palette PNGs where the palette index *is* the alpha
level and every palette entry is white. Lossless, and about half the bytes of a
plain RGBA PNG. If you re-export the logo, re-run that encoding rather than
pasting a raw RGBA export back in.

## Email signups

The form posts to Formspree (`https://formspree.io/f/xgaewwnd`). Submissions land
in the inbox attached to that form — there is no backend in this repo.
