# Hosting & Sharing Guide

_Where to put the Tara Rose pages so you can share them, run campaigns, and edit copy without a developer. Last updated 5 July 2026._

Every page in `trs-production/` is a **single self-contained HTML file** (fonts embedded, no internet needed). That makes them portable — but "portable" and "easy to edit for campaigns" are two different jobs, so here's the split.

---

## The shareable index
`index.html` (root of `trs-production/`) is a **page library** — one on-brand page linking all 8.
- Preview link (yours): https://claude.ai/code/artifact/3f39b123-9bbe-4c0e-bfb4-6cb72a07d433

## Sharing with the team — read this
There are two versions of the library on purpose, because a *link* and a *folder* need different link types:

| Give the team | What it is | Do the links work? |
|---|---|---|
| **`Tara-Rose-Pages-Share.zip`** ⭐ | The whole folder — gallery + all 8 pages + docs. They unzip and open `index.html`. | ✅ Yes, **offline**. The gallery's buttons open the real pages in the zip. No login, no internet. |
| **Host the folder** (Vercel/Framer) | One permanent team URL (e.g. `pages.tararosesalon.com`) | ✅ Yes, forever, for anyone with the URL. Best long-term. |
| The **claude.ai preview link** | The published gallery on your account | ⚠️ Its buttons open claude.ai artifacts that are **private until you share each one**. Fine for a quick solo look, not the team. |

**So for the team: send the ZIP, or host the folder.** Don't rely on the claude.ai link — those artifacts are private to your account until you toggle sharing on each.

---

## Where to host — pick by job

| Job | Host | Why |
|---|---|---|
| **The real marketing site + easy copy edits + campaigns** | **Framer** ⭐ | Visual editor (edit copy with no code), CMS for services/testimonials, custom domains, duplicate-a-page per campaign, built-in A/B. This is already Step 3 of your pipeline. |
| **Get the exact HTML live fast, under your domain** | **Vercel** | Drag-drop or Git deploy, free tier, instant custom domain. You already use it (dashboard). Copy edits mean editing the HTML though — dev-ish. |
| **The funnel pages (Founding, Careers)** | **GHL** | GHL owns the form backend, deposits, and nurture. Point the page's form/CTA at GHL; host the page in Framer/Vercel and let GHL catch the submit. |
| **Quick client/stakeholder preview** | **claude.ai artifact links** | Already live (see the library). Private until you choose to share. Not for production traffic. |

### Recommendation
**Framer is your home for anything you'll edit or run as a campaign.** The self-contained HTML is the *bridge* asset — perfect for sharing, previewing, and handing to Framer — not the long-term editable copy. Flow: **HTML (here) → Framer (edit + campaign + domain) → GHL (funnel backend).**

---

## Running a campaign variant (the repeatable move)
1. In Framer: duplicate the page → new campaign URL (e.g. `/blonde-summer`).
2. Edit copy in the visual editor (headline, offer, CTA text).
3. Swap the `wa.me` number / booking link if the campaign routes elsewhere — see `WHITE-LABEL-SWAP-SHEET.md`.
4. Gate the new copy through `trs-brand-guardian` before publish.
5. Point the ad/email/social at the campaign URL. One page = one campaign.

**Before Framer, if editing the raw HTML:** the copy lives in the `<body>`; tokens/fonts/CSS live once in `<style id="trs">` — never touch those for a copy change. Re-run the brand gate after editing.

---

## Custom domains
- Marketing site → `tararosesalon.com` (+ `/colour/blonde`, `/careers`, etc.) via Framer or Vercel.
- Campaigns → subpaths or a `go.tararosesalon.com` subdomain.
- Keep the funnel forms pointing at GHL regardless of where the page is hosted.
