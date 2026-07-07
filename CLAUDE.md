# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Website for MEMC (Management in Emerging Markets Consortium), an academic
research community. Plain static HTML/CSS — **no build step, no framework, no
dependencies**. Hosted free on GitHub Pages, served from the `docs/` folder.
Publishing = commit + push; GitHub Pages redeploys automatically.

The site owner and future maintainers are **not web developers** — they edit
the site by asking Claude in plain English. `WEBMASTER-GUIDE.md` is their
manual. Two consequences for you:

1. Keep everything simple and boring: plain HTML, one page per file, shared
   `docs/css/style.css`. Do not introduce build tools, frameworks, or JS
   unless truly necessary.
2. When a process or structure changes, update `WEBMASTER-GUIDE.md` (and this
   file) in the same commit.

## Structure

- `docs/` — the published website (GitHub Pages serves this folder, nothing else).
  - `index.html` (About Us / landing), `committee.html`, `conference.html`,
    `seminars.html`, `signup.html`
  - `css/style.css` — all styling; colors/fonts defined in `:root` variables
  - `images/`, `files/` — only assets actually used by the site
- `site_media/` — unpublished photo archive from the old Wix site (April 2024
  photos are from the 1st MEM Conference at Wharton). Copy into `docs/images/`
  with a descriptive kebab-case name when a photo is needed.
- `wix_html/` — saved HTML of the old Wix site; content reference only. Large
  machine-generated files — Grep them, don't read whole files.
- `instructions.md` — original project requirements.

## Editing conventions

- The nav menu and footer are duplicated in every HTML file. Any nav change
  must be applied to all five pages; keep the `class="current"` marker on each
  page's own link.
- HTML comments starting with "HOW TO UPDATE" inside the pages document the
  recurring edit patterns (new seminar season, new conference, committee
  changes). Follow and preserve them.
- Seminar/conference updates follow an archive pattern: current items move
  down into the "Past" section, new items take their place.
- The Sign Up page embeds a Google Form (responses → Google Sheet = member
  database). The embed URL is the only integration point; placeholder is
  `REPLACE_WITH_GOOGLE_FORM_EMBED_URL` until the form exists.
- Preview: open `docs/*.html` directly in a browser (or `python -m http.server`
  from `docs/`). No build or test commands exist.

## Status / pending setup

Remaining one-time steps (details in `WEBMASTER-GUIDE.md`): create GitHub
org + repo and enable Pages from `main:/docs`; create the Google Form and
replace the embed placeholder in `signup.html`; optional custom domain.
Committee page currently lists the 2025 program committee with initials
placeholders — real positions and photos still needed from the owner.
