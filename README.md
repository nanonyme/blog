# nanonyme's rants

This repository contains the source for a Pelican-powered blog published on GitHub Pages.

## Project Layout

- `content/` holds the blog posts and pages.
- `pelicanconf.py` contains local site settings.
- `publishconf.py` contains production settings for the GitHub Pages build.
- `Makefile` provides the main build and preview targets.
- `.github/workflows/pelican-pr.yml` builds the site for pull requests.
- `.github/workflows/pelican-pages.yml` builds and deploys the site from `main`.

## Local Development

Install the site generator dependencies and build the site locally:

```bash
python -m pip install --upgrade pip
pip install pelican markdown
make html
```

Useful targets from the `Makefile`:

- `make html` builds the site into `output/`.
- `make clean` removes generated files.
- `make regenerate` rebuilds automatically when content changes.
- `make publish` builds the production version.
- `make serve` serves the generated site locally.
- `make devserver` builds and serves with live regeneration.

## Publishing

Changes merged to `main` are built by GitHub Actions and deployed to GitHub Pages. Pull requests run the same build without deploying.
The canonical production URL is `https://nanonyme.github.io/`.

## Automated Dependency Updates

Dependabot is configured to watch GitHub Actions updates and batch them into grouped pull requests so workflow dependency churn stays manageable.