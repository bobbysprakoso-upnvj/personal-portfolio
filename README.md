# Personal Portfolio Website

A simple, responsive, static portfolio website built with **pure HTML5 and CSS3 — zero JavaScript, zero dependencies, zero build step**.

Content reflects Bobby Suryo Prakoso's verified public profile. No public email address is published — contact is via GitHub and LinkedIn. V1 features two curated GitHub projects; `BRIEF.md`'s "minimal 3 projects" guideline is intentionally deferred until a third project can be featured with verified evidence.

## Features

- Single-page layout: Hero, About, Experience, Projects, Skills, Contact
- Bilingual: English (`index.html`, default) and Indonesian (`id/index.html`), cross-linked via language switchers
- Light theme by default with automatic dark mode (`prefers-color-scheme`)
- Responsive from 320px phones to desktop — navigation stays visible and wraps on small screens (no hamburger menu)
- Smooth scrolling via pure CSS, disabled automatically for users who prefer reduced motion
- Semantic HTML, skip-to-content link, keyboard-visible focus styles

## Project Structure

```text
personal-portfolio/
├── index.html          ← English page (default)
├── id/
│   └── index.html      ← Indonesian page
├── css/
│   └── style.css       ← shared stylesheet (tokens → base → components)
├── assets/
│   └── images/         ← reserved for future images
├── docs/plans/         ← design & implementation plan documents
├── BRIEF.md            ← original project brief
└── README.md
```

Both language pages have identical DOM structure and share one stylesheet; only the text differs. All asset paths are relative, so the site works at a domain root or a subpath without changes.

## Run Locally

No build step required. Either:

1. Open `index.html` directly in a browser, or
2. Serve the folder:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Push this repository to GitHub.
2. Open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select your default branch and the `/ (root)` folder, then **Save**.
5. Your site will be available at `https://<username>.github.io/<repo-name>/`.

The site works identically whether deployed at a user root (`username.github.io`) or project subpath, because all paths are relative.

## Requirements Compliance

See `docs/plans/2026-08-26-personal-portfolio-v1.md` for the full FR/NFR checklist from `BRIEF.md`.
