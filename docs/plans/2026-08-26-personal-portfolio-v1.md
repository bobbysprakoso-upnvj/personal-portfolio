# Implementation Plan: Personal Portfolio v1

**Date:** 2026-08-26
**Status:** Approved design, awaiting implementation request
**Input:** `BRIEF.md` + brainstorming decisions (2026-08-26)

## Approved Design Summary

| Decision | Choice |
|---|---|
| Stack | Pure HTML5 + CSS3, **zero JavaScript** |
| Languages | Two files: `index.html` (EN, default) + `id/index.html` (ID), cross-linked |
| Content | Clearly-marked placeholders; real content is a follow-up task after launch |
| Mobile nav | Always-visible wrapped links, no hamburger |
| Theme | Light default + auto dark mode via `prefers-color-scheme` |
| Accent color | Blue — `#2563EB` light / lighter variant dark, as CSS custom properties |
| Typography | System font stack, no webfonts |
| Paths | Relative only → works at Pages root or `/repo-name` subpath |

Structure (revised from BRIEF proposal — `js/` removed):

```text
personal-portfolio/
├── index.html          ← English
├── id/
│   └── index.html      ← Indonesian
├── css/
│   └── style.css       ← shared by both pages
├── assets/
│   └── images/         ← empty for v1 (no images required)
├── docs/plans/         ← this plan
├── README.md           ← updated with run/deploy instructions
└── BRIEF.md
```

---

## Task 1 — Project skeleton and CSS design tokens

Create directories and `css/style.css` containing **only** the token layer:

- `@media (prefers-reduced-motion)` handled later (Task 5).
- `:root` custom properties:
  - Colors: `--bg`, `--surface`, `--text`, `--text-muted`, `--accent` (#2563EB),
    `--accent-strong` (darker hover), `--border`
  - Spacing scale: `--space-1..8` (4px base)
  - Radius: `--radius` (8px)
  - Type scale: `--fs-h1/h2/h3/body/small`
- Dark mode block `@media (prefers-color-scheme: dark)` overriding tokens
  (`--accent` → #60A5FA family, adjusted surfaces/border/text).

**Files:** `css/style.css`, empty dirs `id/`, `assets/images/`

**Verify:** file exists; open a scratch HTML page linking it → no errors, tokens resolve in devtools.

---

## Task 2 — Base styles

Append to `css/style.css`:

1. Minimal reset (box-sizing, margin 0, media max-width 100%)
2. Body defaults: token colors, system font stack, line-height ~1.6
3. `.container`: max-width 1000px, centered, horizontal padding
4. Typography rules h1–h3 using type-scale tokens
5. Links: accent color, underline on body copy, no underline in nav/cards
6. `:focus-visible` visible outline (2px accent, offset) — accessibility
7. `.skip-link` (visually hidden until focused)

**Files:** `css/style.css`

**Verify:** render any heading/link sample → correct fonts, colors, focus ring.

---

## Task 3 — `index.html` (English) full semantic markup

Write complete page with placeholder copy marked by `<!-- TODO(content): ... -->` comments:

- `<html lang="en">`; title + meta description ("Your Name — Software Engineer" placeholders);
  basic Open Graph tags
- Skip link → `#main`
- `header.site-header > nav[aria-label="Main"]`:
  - Brand/name link → `#hero`
  - Anchor links: About, Experience, Projects, Skills, Contact
  - Language switcher: `hreflang="id"` link to `id/index.html`
- `main#main` sections, each with `aria-labelledby` → its `h2`:
  1. `#hero` — `<h1>` name, professional title `<p>`, short description,
     two button-style links: "View Projects" (`#projects`), "Contact Me" (`#contact`)
  2. `#about` — short bio paragraphs, expertise areas list, professional interests list
  3. `#experience` — 2 placeholder entries as `article` (role, org, period, description)
  4. `#projects` — grid of exactly 3 placeholder `article.card`s:
     name, description, tech list, GitHub repo link (`https://github.com/yourusername/repo-name`,
     `rel="noopener"`)
  5. `#skills` — three grouped chip lists: Languages / Tools & Platforms / Expertise Areas
  6. `#contact` — mailto link (`you@example.com`), GitHub profile, LinkedIn profile
     (`rel="noopener"`)
- `footer` — copyright line + repeat language switcher

All hrefs relative. No `<script>` tag anywhere.

**Files:** `index.html`

**Verify:** open via `file://` → all anchors scroll smoothly to correct section;
no console 404s; W3C validator clean.

---

## Task 4 — `id/index.html` (Indonesian)

Mirror of Task 3 structure with translated placeholder copy
("Nama Anda", "Proyek", "Kontak", etc.), same TODO markers. Path adjustments:

- Stylesheet: `../css/style.css`
- Language switcher: `hreflang="en"` → `../index.html`
- Footer switcher likewise
- `<html lang="id">`, translated title/description/OG tags

Identical class names and DOM order as EN page so one stylesheet serves both.

**Files:** `id/index.html`

**Verify:** open via `file://` from `id/` → styling identical to EN page;
switcher round-trips EN ⇄ ID preserving nothing else (acceptable v1).

---

## Task 5 — Component styles + responsive behavior

Append to `css/style.css`:

1. `.site-header`: flex, wrap allowed (mobile = always-visible wrapped links per design),
   subtle border-bottom, sticky top
2. `.btn` / `.btn-secondary`: accent background / outlined variants, radius, hover states
3. Section vertical rhythm via spacing tokens; alternating `--surface` backgrounds optional
4. Experience entries: role/org header layout, muted period text
5. `.projects-grid`: CSS grid, `repeat(auto-fit, minmax(260px, 1fr))` — collapses
   without media queries
6. `.card`: surface bg, border, radius, padding; tech chips small pill spans
7. `.skills-group`: chip lists (pill spans, wrap)
8. Contact links: simple inline list with external-link affordance
9. Footer: muted, small, spaced
10. One breakpoint (~720px) only where auto-fit/flex-wrap insufficient:
    hero buttons stack, nav gap tightening
11. Smooth scroll + reduced motion:
    ```css
    html { scroll-behavior: smooth; }
    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      * { transition: none !important; animation: none !important; }
    }
    ```

**Files:** `css/style.css`

**Verify:** browser widths 320 / 768 / 1200px → no overflow, readable hierarchy,
nav wraps not scrolls horizontally; smooth scroll works; OS dark mode flips theme.

---

## Task 6 — README update

Rewrite/add sections: project overview, local run (open `index.html` or
`python3 -m http.server`), deploy-to-GitHub-Pages steps (Settings → Pages → branch),
structure explanation, note that content is placeholder (link follow-up task),
language-file relationship.

**Files:** `README.md`

**Verify:** instructions accurate against actual structure.

---

## Task 7 — Final verification pass (FR/NFR checklist)

Run through and record results in PR/commit message or README badge-less checklist:

- [ ] FR-01 nav reaches every section (EN + ID)
- [ ] FR-02 smooth scrolling works
- [ ] FR-03 usable at 320px–1440px
- [ ] FR-04 all 3 project cards have working repo links
- [ ] FR-05 contact email/GitHub/LinkedIn clickable
- [ ] FR-06 / NFR-01 static only — opens correctly from `file://`
- [ ] NFR-02 no frameworks (zero dependencies, zero build step)
- [ ] NFR-03 structure matches approved tree; `js/` absent
- [ ] NFR-04 semantic landmarks, single h1/page, validator clean both files
- [ ] NFR-05 CSS organized: tokens → base → components, commented sections
- [ ] NFR-06 zero JavaScript
- [ ] Subpath check: serve under `http://localhost:8000/sub/dir/` → assets/links still resolve
- [ ] Keyboard-only pass: skip link, tab order, focus rings visible
- [ ] Dark-mode contrast spot-check on accent links/buttons

**Files:** none modified (verification only); fix-forward if gaps found.

---

## Out of Scope (follow-up tasks)

- Real content replacement (name, bio, experience, projects, links, photo)
- Favicon / social preview image
- Analytics, forms, search — deliberately excluded (no backend rule)
- Print styles, PWA, i18n beyond EN/ID
