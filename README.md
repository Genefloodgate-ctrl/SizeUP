# SizeUP

Static landing page for SizeUP, served from `docs/`.

## Layout

- `docs/` — everything published to the web. `docs/index.html` is the landing
  page: fully self-contained, with inline CSS/JS and base64 images. No build step.
- `docs/.nojekyll` — tells Pages to serve the files as-is, without Jekyll.
- `.github/workflows/deploy.yml` — optional. Publishes `docs/` to Pages on every
  push to `main`, for when Actions is available.

## Local preview

```bash
python3 -m http.server 8000 --directory docs
# http://localhost:8000
```

## Deploying

Two routes, both landing at `https://genefloodgate-ctrl.github.io/SizeUP/`.
Pick one — the repo is laid out so either works unchanged.

### Branch source (no Actions required)

**Settings → Pages → Build and deployment → Source: Deploy from a branch →
Branch: `main`, folder: `/docs` → Save.**

Pages builds it directly. Nothing to run, no Actions minutes consumed. Every
later push to `main` republishes automatically.

### GitHub Actions source

**Settings → Pages → Build and deployment → Source: GitHub Actions.**

Uses `.github/workflows/deploy.yml`. Requires Actions to be enabled and able to
schedule runs on this account.

## Custom domain

Add `docs/CNAME` containing the bare domain (e.g. `sizeup.xyz`), point the
domain's DNS at GitHub Pages, then set the domain under Settings → Pages. Also
update the `og:url` meta tag in `docs/index.html` to match.

## Email signups

The form posts to Formspree (`https://formspree.io/f/xgaewwnd`). Submissions land
in the inbox attached to that Formspree form — no backend in this repo.
