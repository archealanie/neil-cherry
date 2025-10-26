<!-- .github/copilot-instructions.md: Guidance for AI coding agents working on the neil-cherry repo -->
# Repository snapshot

This is a small static website (single-page) for a wedding invite built with plain HTML, Tailwind CSS (via CDN) and a few local assets. The codebase is intentionally minimal — no build system, no Node tooling present in the repository root.

# What you should know up front

- Primary entry: `index.html` (single page, contains layout, animations and light JS).
- Local styles: `src/css/app.css` and `src/css/font.css` (custom classes and font-face declarations).
- Images and static assets live under `src/img/*`, `src/font/*`.
- A local copy of Tailwind appears under `js/tailwind.3.4.7.js` but the page also loads Tailwind from CDN. Changes to design usually happen via `app.css` or inline Tailwind classes in `index.html`.
- There are no unit tests, package.json, or CI workflows in this repository (searches found no `.github` rules or README-derived agent docs before this file was added).

# Goals for edits and PRs

- Keep the site static and dependency-free where reasonable — the simplest change that works is preferred.
- Preserve image paths and filenames (they are referenced directly in `index.html` with relative paths like `src/img/temp/hill.jpg`).
- Avoid introducing heavy build tooling without explicit user instruction. If adding tooling, include a minimal README and a single-purpose `package.json` and explain why.

# Common code patterns and examples (use these when changing code)

- Inline Tailwind utility classes are used extensively in `index.html`. Prefer editing `src/css/app.css` for project-wide changes, and use Tailwind classes for quick, localized styling.
  - Example: a hero heading uses classes: `<h1 class="text-8xl font-gellatio">Neil</h1>` — to change typography prefer editing `font.css` or `app.css` rather than mutating every inline class.

- Background images are set with inline style attributes and relative paths. Preserve exact file names and directories when editing.
  - Example: `<div class="..." style="background-image: url('src/img/temp/hill.jpg');"></div>`

- Small, vanilla JS is embedded in `index.html` for UI features (countdown timer, accordion, AOS init). Keep changes lightweight and inline unless you add a clear reason to extract to `src/js/`.
  - Example: the countdown uses a plain Date object and updates elements with IDs `days`, `hours`, `minutes`, `seconds`.

# Debugging and developer workflows

- To preview the site locally, open `index.html` in a browser. On Windows PowerShell you can run a quick static server if needed (not provided in repo):
  - Python 3: `python -m http.server 8000` (run from repo root) and open `http://localhost:8000`.
  - If you add a Node-based dev server, add a `package.json` and document how to run it in README.

- There are no automated tests or linters configured. If you add automated checks, keep them opt-in and document changes in the README and this instructions file.

# Conventions and repository-specific rules

- Minimal changes: prefer editing `src/css/app.css` and `index.html` only. Avoid moving image files unless you update all references.
- Keep fonts and custom classes in `src/css/font.css` / `src/css/app.css`. If introducing new fonts add them under `src/font/` and update `font.css`.
- Don't change CDN-hosted libraries (AOS, Tailwind CDN, Font Awesome) to local files unless asked.

# Integration points and external resources

- External CDNs used (do not remove unless replacing intentionally):
  - Tailwind CSS via `https://cdn.tailwindcss.com`
  - AOS (animate on scroll) via jsdelivr
  - Font Awesome and Google Fonts via their respective CDNs

- Google Maps and Google Forms are embedded via iframes — do not attempt to rewrite these as server-side components.

# Examples of safe edits

- Fixing the countdown target date: update the `weddingDate` in the inline script near the bottom of `index.html`.
- Adding a new image: put the file under `src/img/<folder>` and reference it using the same relative path in `index.html` or `app.css`.
- Small accessibility fixes: add alt text to any `<img>` elements missing `alt` (there are several `img` tags without alt text).

# When to ask the repo owner before making changes

- Adding build tooling (npm, webpack, PostCSS) — confirm first. The author prefers a simple static site.
- Moving or renaming asset directories (anything under `src/img`, `src/font`) — confirm since paths are referenced directly.

# Where to look for follow-ups

- Primary file to read for overall behavior: `index.html`.
- Styling and font definitions: `src/css/app.css`, `src/css/font.css`.
- Local JS: currently inline; if you need to split it out place files under `src/js/` and update `index.html`.

If anything above is unclear or you want me to add examples for a specific change (for example: extract inline JS, add a dev server, or add a minimal README and package.json), tell me which direction and I'll update this file accordingly.
