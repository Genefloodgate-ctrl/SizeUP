# SizeUP

Static landing page for SizeUP, hosted on GitHub Pages.

## Layout

- `site/` — everything published to the web. `site/index.html` is the landing page.
- `.github/workflows/deploy.yml` — publishes `site/` to GitHub Pages on every push to `main`.

## Local preview

```bash
python3 -m http.server 8000 --directory site
# http://localhost:8000
```

## Deploying

1. In the repo: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
2. Push to `main` (or run the workflow manually from the Actions tab).
3. The site goes live at `https://genefloodgate-ctrl.github.io/SizeUP/`.

### Custom domain

Add a `site/CNAME` file containing the bare domain (e.g. `sizeup.app`), point the
domain's DNS at GitHub Pages, then set the domain under Settings → Pages.
