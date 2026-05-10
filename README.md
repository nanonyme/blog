# nanonyme's rants

This repository contains the source for a Pelican-powered blog published on GitHub Pages.

## Project Layout

- `content/` holds the blog posts and pages.
- `pelicanconf.py` contains local site settings.
- `publishconf.py` contains production settings for the GitHub Pages build.
- `Makefile` provides the main build and preview targets.
- `.github/workflows/pelican-pr.yml` builds the site for pull requests.
- `.github/workflows/pelican-pages.yml` builds and deploys the site from `main`.
- `.github/workflows/create-post-draft.yml` creates a draft post file and opens a draft pull request.

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

## Create Posts from GitHub Actions

Use the **Create Draft Post** manual workflow to scaffold a new post without cloning the repository locally.

Prerequisites:
- Repository setting **Actions -> General -> Workflow permissions** should allow read and write permissions.
- If your repository or organization blocks PR creation by the default workflow token, also enable **Allow GitHub Actions to create and approve pull requests**.
- Optional fallback: create repository secret `POST_WORKFLOW_TOKEN` with a fine-grained PAT that has `contents: write` and `pull requests: write`. The workflow uses this secret automatically when present.

1. Open the Actions tab and run **Create Draft Post**.
2. Fill in the required inputs:
	- `title` (required)
	- `filename` (required, must end with `.md`, path is always inside `content/`)
	- `tags` (optional, comma-separated)
3. The workflow validates the filename and fails if `content/<filename>` already exists.
4. On success it creates a skeleton post with this header order:
	- `Title`
	- `Date` (auto-generated as current date in `YYYY-MM-DD`)
	- `Tags` (always included, even when empty)
5. The workflow commits the new file on an automation branch and opens a draft pull request targeting `main`.

## Automated Dependency Updates

Dependabot is configured to watch GitHub Actions updates and batch them into grouped pull requests so workflow dependency churn stays manageable.