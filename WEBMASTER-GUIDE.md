# MEMC Website — Webmaster Guide

This guide is for whoever maintains the MEMC website. **You do not need to know
HTML.** All editing is done by asking Claude Code in plain English; this guide
tells you what to ask for and how the pieces fit together.

## How the site works (2-minute version)

- The website is a set of plain HTML files in the `docs/` folder of this
  project. `docs/index.html` is the About Us page; the other pages are
  `committee.html`, `conference.html`, `seminars.html`, `pdws-symposia.html`,
  and `signup.html`.
- The site is hosted **free on GitHub Pages** and lives at
  **https://mem-consortium.org**. GitHub watches the repository, and whenever
  a change is pushed, the live site updates automatically within a minute or
  two. Publishing = pushing to GitHub. Nothing else to do.
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
| Add a PDW or symposium | "Add our AOM 2027 PDW to the PDWs & Symposia page. The session page is saved as a PDF in `pdws_symposia/`" |
| Change committee members | "Remove X from the organizing committee and add Y, position Z, at University W. Photo is at [file path]" |
| Edit any text | "On the About page, change the sentence '…' to '…'" |
| Publish changes | "Commit and push my changes so the live site updates" |
| Undo a mistake | "The last change broke something — revert it" |

To **preview before publishing**, ask Claude to open the page locally, or just
double-click any `.html` file in `docs/` to view it in your browser.

After Claude makes a change, it is only on your computer until you ask Claude
to **commit and push** — that's the publish step.

## One-time setup (current status and remaining steps)

### 1. GitHub account and repository — DONE
(The site lives in the `mem-consortium.github.io` repository of the
`mem-consortium` organization, contact email `mem.consortium@gmail.com`,
and is published at https://mem-consortium.org — see section 3 for the
domain. The steps below are kept as a record of how it was set up.)

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
3. Create a repository in that organization named `mem-consortium.github.io` (public —
   required for free GitHub Pages).
4. Ask Claude: "Push this project to the GitHub repository
   mem-consortium/mem-consortium.github.io" (Claude will give you the
   one-time login steps if needed).
5. On github.com: repository → Settings → Pages → Source: "Deploy from a
   branch" → Branch: `main`, folder: `/docs` → Save.
6. The site goes live at `https://mem-consortium.github.io/`.

**Handover:** the outgoing webmaster adds the incoming one as an organization
owner (github.com → organization → People → Invite). Never share passwords.

### 2. Google Form + member database — DONE
(The "MEMC Sign Up" form is embedded in the Sign Up page and owned by
`mem.consortium@gmail.com`; its linked response spreadsheet is the member
database. Members from the pre-2026 mailing list were imported into it.
The steps below are kept as a record of how it was set up.)

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

### 3. Custom domain — DONE

The site's public address is **https://mem-consortium.org**.
`www.mem-consortium.org` and the old `mem-consortium.github.io` address both
redirect to it automatically.

- **Registrar: Domain.com**, under the consortium's account. The domain must be
  **renewed every year** — this is the only recurring cost of the whole site
  (~$10–20). Keep auto-renew switched on and the card on file current; if the
  domain lapses, the site goes dark. Record the renewal date here once you've
  checked it in Domain.com → My Domains.
- **Where DNS is managed:** Domain.com → My Domains → `mem-consortium.org` →
  DNS & Nameservers → DNS Records. The domain uses Domain.com's *default*
  nameservers — don't switch it to custom/third-party nameservers, or that
  editor stops working. (Ignore the "Custom Nameservers" page entirely; it is
  a different, advanced feature.)
- **The records that make the site work.** Don't delete or edit these:

| Type | Name / Host | Value |
|---|---|---|
| A | blank (`@`) | `185.199.108.153` |
| A | blank (`@`) | `185.199.109.153` |
| A | blank (`@`) | `185.199.110.153` |
| A | blank (`@`) | `185.199.111.153` |
| CNAME | `www` | `mem-consortium.github.io` |
| TXT | `_github-pages-challenge-mem-consortium` | GitHub domain-verification code |

  The four A records are GitHub's servers. If a registrar ever adds its own
  "parking" A record alongside them (Domain.com used `208.91.197.27`), delete
  it — otherwise a fraction of visitors land on a placeholder page instead of
  the site, seemingly at random.

- **`docs/CNAME`** in this project contains `mem-consortium.org`. That file is
  what tells GitHub Pages to serve the site at the custom domain. **Do not
  delete or rename it** — if it disappears, the site reverts to the github.io
  address.
- **HTTPS** is automatic: GitHub issues the certificate. "Enforce HTTPS" should
  be ticked in repository Settings → Pages. It is greyed out for up to an hour
  after a domain change while the certificate is issued — that's normal.

**Email:** there is no email on this domain (no MX records); consortium mail
uses `mem.consortium@gmail.com`. If you ever set up `@mem-consortium.org`
addresses, tell Claude first so the new DNS records don't collide with the
ones above.

**Handover:** pass on the Domain.com login along with the other accounts.

## Where things live

| What | Where |
|---|---|
| Website pages | `docs/*.html` |
| Custom domain setting | `docs/CNAME` (don't delete — see section 3) |
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
