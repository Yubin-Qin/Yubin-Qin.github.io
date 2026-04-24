# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

This is a personal academic website built on **al-folio**, a Jekyll theme for academics. It is deployed to GitHub Pages at `https://yubin-qin.github.io`.

**Owner:** Yubin Qin — Ph.D. Candidate at Tsinghua University, research on energy-efficient AI processors and architecture.

**Tech stack:** Jekyll v4.x, Ruby 3.3.5, Python 3.13 (for nbconvert), Node.js (for Prettier/PurgeCSS). Uses Docker for local development.

## Build & development commands

### Docker (recommended)

```bash
docker compose pull && docker compose up       # Start dev server at http://localhost:8080
docker compose up --build                      # Rebuild after Dockerfile/dependency changes
docker compose down                            # Stop and free port 8080
```

### Code formatting (run before every commit)

```bash
npx prettier . --write
```

### Full pre-commit checklist

1. `npx prettier . --write` — format all files
2. `docker compose up --build` — verify the site builds and renders correctly at http://localhost:8080
3. Check navigation, pages, images, and dark mode all work

## Repository structure

- `_config.yml` — **Primary configuration** (URL, features, plugins, theme settings)
- `_pages/` — Static pages: `about.md`, `cv.md`, `publications.md`, `projects.md`, `teaching.md`
- `_posts/` — Blog posts (filenames MUST be `YYYY-MM-DD-title.md`)
- `_projects/` — Project showcase entries
- `_news/` — News/announcements
- `_bibliography/papers.bib` — BibTeX bibliography for publications
- `_data/` — YAML data: `socials.yml`, `coauthors.yml`, `cv.yml`, `repositories.yml`
- `_includes/` — Reusable Liquid template components
- `_layouts/` — Page layout templates (`about.liquid`, `post.liquid`, `bib.liquid`, `cv.liquid`, etc.)
- `_sass/` — SCSS stylesheets
- `_scripts/` — JavaScript
- `assets/img/` — Images and profile photos

## Critical configuration rules

When modifying `_config.yml`, these must be consistent:
- **This is a personal site:** `url: https://yubin-qin.github.io` + `baseurl:` (empty)
- **YAML quoting:** Quote any string value containing `:`, `&`, or `#` — e.g., `title: "My: Site"`
- **Feature toggles** use `enable_*` keys in `_config.yml` (e.g., `enable_darkmode`, `enable_math`)

## Content authoring quick reference

- **Blog post:** Create `_posts/YYYY-MM-DD-title.md` with frontmatter `layout: post`, `title`, `date`, `categories`
- **Project:** Create `_projects/name.md` with `layout: page`, `title`, `description`, `img`, `importance` (integer, higher = first)
- **News:** Create `_news/title.md` with `layout: post`, `title`, `date`
- **CV:** Edit `_data/cv.yml` and `assets/json/resume.json` (JSONResume format)
- **Publications:** Edit `_bibliography/papers.bib`

## Common pitfalls

- **Port conflict:** Run `docker compose down` before `docker compose up`
- **Site has no CSS after deploy:** `url`/`baseurl` mismatch — personal site must have empty `baseurl`
- **Related posts error ("zero vectors"):** Post has too little meaningful content; add more text or set `related_posts: false` in frontmatter
- **Prettier PR failures:** Run `npx prettier . --write` locally before committing

## More info

Deeper references are available in these files:
- [AGENTS.md](AGENTS.md) — full agent guidelines with links to all instruction files
- [`.github/copilot-instructions.md`](.github/copilot-instructions.md) — tech stack details, CI/CD, pitfalls
- [INSTALL.md](INSTALL.md) — setup and deployment
- [CUSTOMIZE.md](CUSTOMIZE.md) — theming and customization
- [TROUBLESHOOTING.md](TROUBLESHOOTING.md) — detailed troubleshooting
