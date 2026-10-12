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
    `seminars.html`, `pdws-symposia.html`, `signup.html`, `brand.html`
    (Logo & Brand page — linked from the footer only, not the nav)
  - `css/style.css` — all styling; colors/fonts defined in `:root` variables
  - `images/`, `files/` — only assets actually used by the site.
    `images/memc-logo.png` is the full-size logo (brand page + download);
    `images/memc-logo-small.png` (480px wide) is the header logo on every page.
    `images/memc-logo-white.png` is the same logo with the lettering recolored
    white (globe, rings, underline untouched) for dark backgrounds: the home
    page hero and the brand page's second download.
  - `favicon.ico` (+ `images/favicon-32.png`, `images/apple-touch-icon.png`)
    — the globe cropped from the logo.
  - `sitemap.xml`, `robots.txt` — for search engines. Add/rename a page →
    update `sitemap.xml`.
  - `CNAME` — the custom domain (`mem-consortium.org`). Required for Pages to
    serve the site there; deleting it reverts to the github.io address.
- `site_media/` — unpublished photo archive from the old Wix site (April 2024
  photos are from the 1st MEM Conference at Wharton). Copy into `docs/images/`
  with a descriptive kebab-case name when a photo is needed.
- `wix_html/` — saved HTML of the old Wix site; content reference only. Large
  machine-generated files — Grep them, don't read whole files.
- `annual_conferences/`, `pdws_symposia/` — local-only source material (agenda
  PDFs, saved AOM session pages, notes). Git-ignored on purpose: pull content
  out of them into `docs/`, never commit them.
- `brand/` — local-only: original logo file and the draft brand page the
  live `brand.html` was based on. Git-ignored.
- `instructions.md` — original project requirements.

## Editing conventions

- The header (logo + nav menu) and footer are duplicated in every HTML file.
  Any change must be applied to all seven pages; keep the `class="current"`
  marker on each page's own nav link (`brand.html` has none — it is not in
  the nav).
  The header logo `<img>` carries `width="180" height="60"` so it renders at
  the right size even when a browser is still holding an older cached
  `style.css` (GitHub Pages caches it 10 minutes); keep those attributes in
  step with `.wordmark img` in the CSS.
- Every page's `<head>` carries the same SEO block: title
  "<Page> — Management in Emerging Markets Consortium (MEMC)", a meta
  description naming the consortium, canonical URL, favicon links and Open
  Graph tags. Copy it for a new page. The home page also has a JSON-LD
  Organization block (name, "MEMC" alternate name, logo).
- HTML comments starting with "HOW TO UPDATE" inside the pages document the
  recurring edit patterns (new seminar season, new conference, committee
  changes). Follow and preserve them.
- Seminar/conference updates follow an archive pattern: current items move
  down into the "Past" section, new items take their place. A past conference
  can carry its full agenda in a collapsed `<details class="program">` block
  (`.agenda` / `.slot` markup) inside its `.event` entry; the 2026 conference
  is the working example.
- The Sign Up page embeds a Google Form (responses → Google Sheet = member
  database), owned by `mem.consortium@gmail.com`. The embed URL is the only
  integration point.
- Preview: open `docs/*.html` directly in a browser (or `python -m http.server`
  from `docs/`). No build or test commands exist.

## Status / pending setup

One-time setup is complete (details in `WEBMASTER-GUIDE.md`): the site is
published from `main:/docs` of `mem-consortium/mem-consortium.github.io`, the
Google Form is embedded in `signup.html`, and the custom domain
**mem-consortium.org** is live (registrar Domain.com, DNS on Domain.com's
default nameservers, four GitHub A records + `www` CNAME).
Google Search Console: Domain property created and its verification TXT record
added at Domain.com on 2026-10-12 (guide, section 4); sitemap submission and
indexing request still to do. The site was not appearing on Google as of that
date. Check DNS with a trailing dot (`nslookup -type=TXT mem-consortium.org.
ns89.worldnic.com`) — without it, Windows appends the local search suffix.
Committee page currently lists the 2025 program committee with initials
placeholders — real positions and photos still needed from the owner.
