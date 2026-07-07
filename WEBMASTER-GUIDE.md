# MEMC Website — Webmaster Guide

This guide is for whoever maintains the MEMC website. **You do not need to know
HTML.** All editing is done by asking Claude Code in plain English; this guide
tells you what to ask for and how the pieces fit together.

## How the site works (2-minute version)

- The website is a set of plain HTML files in the `docs/` folder of this
  project. `docs/index.html` is the About Us page; the other pages are
  `committee.html`, `conference.html`, `seminars.html`, and `signup.html`.
- The site is hosted **free on GitHub Pages**. GitHub watches the repository,
  and whenever a change is pushed, the live site updates automatically within
  a minute or two. Publishing = pushing to GitHub. Nothing else to do.
- The member sign-up form on the Sign Up page is a **Google Form** embedded in
  the page. Submissions land automatically in a **Google Sheet** (the member
  database). The website never touches the data — Google handles all of it.
- Every change is saved in git history, so any mistake can be undone.

## Everyday tasks — what to say to Claude

Open Claude Code in this project folder and ask in plain English. Examples:

| You want to… | Say something like… |
|---|---|
| Add a seminar | "Add a seminar to the current season: Jane Doe (MIT Sloan), March 3 2027, 11am ET, paper title X, her website is …" |
| Start a new seminar season | "Archive the current seminar season and start the 2027–28 season" |
| Update the conference | "Update the Annual Conference page for the 3rd MEM conference: [dates, venue, committee]. Here's the program PDF: [file path]" |
| Change committee members | "Remove X from the organizing committee and add Y, position Z, at University W. Photo is at [file path]" |
| Edit any text | "On the About page, change the sentence '…' to '…'" |
| Publish changes | "Commit and push my changes so the live site updates" |
| Undo a mistake | "The last change broke something — revert it" |

To **preview before publishing**, ask Claude to open the page locally, or just
double-click any `.html` file in `docs/` to view it in your browser.

After Claude makes a change, it is only on your computer until you ask Claude
to **commit and push** — that's the publish step.

## One-time setup (current status and remaining steps)

### 1. GitHub account and repository — IN PROGRESS
(Steps 1–2 done: the `mem-consortium` organization exists, contact email
`mem.consortium@gmail.com`. Remaining: steps 3–6.)

You only need **one** GitHub account (your own; if you already have one, use
it — no need for a separate account). Recommended structure so the site
survives webmaster handovers:

1. Sign up / sign in at github.com (your **personal** account — GitHub access
   works through personal accounts added to the organization, never a shared
   login).
2. Create a **free organization** (github.com → + → New organization → Free)
   named `mem-consortium`. The organization owns the website, not any
   one person's account. Set the organization's contact email to
   `mem.consortium@gmail.com`.
3. Create a repository in that organization named `website` (public —
   required for free GitHub Pages).
4. Ask Claude: "Push this project to the GitHub repository
   mem-consortium/website" (Claude will give you the one-time login
   steps if needed).
5. On github.com: repository → Settings → Pages → Source: "Deploy from a
   branch" → Branch: `main`, folder: `/docs` → Save.
6. The site goes live at `https://mem-consortium.github.io/website/`.

**Handover:** the outgoing webmaster adds the incoming one as an organization
owner (github.com → organization → People → Invite). Never share passwords.

### 2. Google Form + member database — TO DO

The consortium's shared Google account is **`mem.consortium@gmail.com`**.
It owns the sign-up form and the member spreadsheet (and is the GitHub
organization's contact address). At webmaster handover, pass on the
password securely and update the account's recovery email/phone
(Google Account → Security) to the new webmaster.

1. Signed in as `mem.consortium@gmail.com`, go to forms.google.com →
   new form titled "MEMC Membership Sign-Up" with questions: First name,
   Last name, Affiliation, Email, Brief description of research interests.
2. In the form: Responses tab → "Link to Sheets" → create the spreadsheet.
   That spreadsheet **is** the member database; share it with committee
   members who need it.
3. In the form: Send → embed icon `< >` → copy the URL inside `src="…"`.
4. Ask Claude: "Here's the Google Form embed URL: … — connect it to the
   sign-up page." Then publish.

**Handover:** nothing to transfer — the form and sheet stay owned by
`mem.consortium@gmail.com`; just hand over that account (see above).

### 3. Custom domain — TO DO (optional)

Buy a domain (~$10–20/year, e.g. Namecheap or Cloudflare Registrar) — the only
cost in this whole setup. Then either:

- **Proper setup (recommended):** repository Settings → Pages → Custom domain →
  enter the domain, and at your domain registrar add the DNS records GitHub
  shows you. HTTPS is automatic. Ask Claude for step-by-step help.
- **Simple forwarding:** at the registrar, forward the domain to the GitHub
  Pages URL. Works, but visitors see the github.io address after landing.

## Where things live

| What | Where |
|---|---|
| Website pages | `docs/*.html` |
| Design (colors, fonts, layout) | `docs/css/style.css` |
| Photos used on the site | `docs/images/` |
| PDFs (conference programs) | `docs/files/` |
| Committee photos | `docs/images/committee/` (square crops look best) |
| Full photo archive from old Wix site | `site_media/` (not published) |
| Old Wix site content (reference only) | `wix_html/` (not published) |
| This guide | `WEBMASTER-GUIDE.md` |
| Instructions for Claude itself | `CLAUDE.md` |

## Rules that keep this maintainable

1. **All changes go through this repository.** Don't edit files on github.com
   directly unless it's an emergency — local edits via Claude keep everything
   consistent.
2. **Keep this guide current.** When a process changes (new domain, new form,
   new page), ask Claude: "Update WEBMASTER-GUIDE.md to reflect this."
3. **The navigation menu appears in every HTML file.** If a page is added or
   renamed, the menu must be updated in all of them — Claude knows this
   (it's noted in the files), but check all pages after such a change.
4. **Don't rename or move the Google Form questions** once created — the
   linked spreadsheet columns depend on them.
