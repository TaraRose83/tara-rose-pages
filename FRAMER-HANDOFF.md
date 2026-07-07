# Framer Handoff — Tara Rose pages

_How to bring the production pages into Framer as a **reusable, repurposable** system — not eleven one-off pages. Last refreshed 7 July 2026._

**Pipeline position:** HTML (built, this folder) → **Framer (you are here: polish + CMS + domain)** → GHL (forms/nurture/booking). The HTML pages are the locked reference; Framer is where copy becomes editable-without-code and content becomes data.

**The one principle:** build the system **once** (tokens + components + CMS), then every page — and every new market — is data, not a rebuild. The Bahrain instance (`../trs-bahrain/`, live at `/bahrain/`) already proves the pages repurpose cleanly; Framer makes that a 10-minute CMS swap instead of a find-and-replace.

---

## Pages in scope (11 + 1 instance)

| # | Page | Folder | Type |
|---|---|---|---|
| 1 | Home | `home/` | Flagship |
| 2 | Blonde (canonical) | `blonde/blonde-menu-led.html` | Service + menu |
| 3 | Brunette | `brunette/` | Service + menu |
| 4 | Haircut & Finish | `cut/` | Service + menu |
| 5 | Treatments | `treatments/` | Service |
| 6 | Home Care | `home-care/` | Service |
| 7 | Confidence Mapping | `confidence-mapping/` | Funnel (quiz) |
| 8 | Founding Glow Pass | `founding-glow-pass/` | Funnel (countdown) |
| 9 | Recruitment / Careers | `recruitment/` | Funnel |
| 10 | Contact & Locations | `contact/` | Utility |
| 11 | Dark Mode directions | `dark-mode/` | Showcase (reference, not a public page) |
| — | **Bahrain instance** | `../trs-bahrain/` | Separate market (BHD, +973) — its own Framer project |

---

## Two ways in — pick per goal

**Path A · Fast bridge (embed the HTML as-is).**
Each page is a **single self-contained HTML file** (fonts embedded, no CDN, no internet). Drop it into a Framer **Embed/Code** component or host the file and iframe it. Live in minutes, pixel-perfect — but **not** natively editable and **no** Framer CMS. Use for a stakeholder preview or a stopgap launch, not the long-term site.

**Path B · Native rebuild (recommended).**
Rebuild in Framer using the four setup steps below. More work once; then copy edits, CMS, A/B, domains and per-market duplication are all native. This is the real destination.

---

## Step 1 — Design system as Framer Variables

Open `framer-tokens.css` (this folder). Create Framer **Variables** from it, once:
- **Colour variables** for every token (grounds, ink, accent, pillar accents, `--lr`).
- **Number variables** for the radii (`--r-lg/md/sm/pill`).
- **Text styles** for the type scale (Playfair display sizes; Inter body sizes; the `.4em`-tracked uppercase eyebrow).

Rules that keep it on-brand and reusable:
- **Never rename a variable** — every component reads them by name (same contract as the HTML).
- **Turquoise `--accent` is the only CTA colour**, on every page and both themes.
- Bind **all** colour/radius/font on every component to variables — no hard-coded hex, ever. That is what makes a re-skin (or a white-label) a variable swap.

## Step 2 — Component (section) library

Rebuild each locked block from `COMPONENTS.md` as **one Framer component with props**, then compose pages from them. The set:
Nav · Hero (A centred / B split / C campaign) · Trust strip · Belief pull-quote (dark) · Education 5-Block · Environment 4-card · Pain list · Route selector · Split image+copy · **The Full Loop** (ring + covers-it-all strip + belief + visit nodes) · Home-Care ladder · Menu (dotted-leader priced rows) · Science glossary · Myths table · Testimonials · Locations · FAQ (dark) · Final CTA · Footer. Funnel-only: Countdown · Avatar selector · Quiz · PDPL block.

**The Full Loop is now identical on every service page** (same belief, why, strip, ring centre, and Create → Protect → Keep on Track nodes) — build it **once** as a component; the only per-page prop is the ring colour `--lr`. Do not fork it per service.

## Step 3 — Make it data-driven (this is the reuse engine)

Move every repeated content block into a **CMS Collection** so pages render from data. Duplicating for a new campaign or a new market then = new rows, not new pages.

| Collection | Key fields |
|---|---|
| **Services / Menu items** | name · family (`Refresh` / `Transformation`) · service group (Blonde Highlighting / Blonde Balayage / Brunette Colour / Haircut / …) · price (`AED __` / `Price on application`) · description · tag (e.g. "New placement") |
| **Locations** | name · city/country · address · hours · map link · phone |
| **Testimonials** | quote · name · service · cleared? (only cleared quotes publish) |
| **FAQs** | question · answer · page/topic |
| **Treatments** | one of the canonical 8 · problem · science · result · home-care pairing |

Bind the Menu, Locations, Testimonials, FAQ and Treatment components to these. Now Bahrain (or any market) = its own CMS entries against the same components.

## Step 4 — Wire the forms to GHL

Every form (Confidence Mapping, Recruitment, Founding, Contact) carries the placeholder **`__FORM_ENDPOINT__`** and posts the captured lead as JSON. In Framer, point each form's submit at the market's **GHL inbound webhook URL**. Nothing else is hardwired — until the endpoint is set the form validates and shows its result but sends nothing. Keep the PDPL/consent block per market (UAE PDPL vs Bahrain PDPL Law 30/2018).

## Step 5 — Dark mode

Dark mode is a **token override**, not a re-theme: a Framer "dark" variant that swaps ~11 variables (see the `[data-theme="dark"]` block in `framer-tokens.css`) plus a toggle that follows the OS by default. Four approved directions live in `dark-mode/` (Editorial Ink · Warm Obsidian · Modern Monochrome · Slate Grey) — pick one; the turquoise CTA stays across all.

---

## Repurpose for a new brand or market (white-label)

Because content is CMS and design is variables, a new market is:
1. **Duplicate the Framer project.**
2. Swap the **Variable values** (palette, fonts, `--lr`) — names stay.
3. Replace the **CMS rows** (services, locations, testimonials, FAQs).
4. Point forms at the new **GHL endpoint**; swap the **PDPL** block + legal entity.
5. Set brand name, WhatsApp number, prices/currency, photography.
6. Run the **brand gate** (below).

Every variable and its location is catalogued in **`WHITE-LABEL-SWAP-SHEET.md`**. The **Bahrain** instance is the worked example of exactly this.

## Import checklist (per page, Path B)

- [ ] Page composed only from Step-2 components (no bespoke one-offs).
- [ ] All colour/radius/font bound to Variables — zero hard-coded hex.
- [ ] Repeated content pulled from CMS, not typed inline.
- [ ] Form submit → GHL webhook; PDPL block correct for the market.
- [ ] Fonts loaded as Framer assets (Playfair Display + Inter) — **no** Google Fonts CDN link.
- [ ] `--lr` set to the page's family colour; Full Loop component unchanged otherwise.
- [ ] Canonical URL → the real domain (not the github.io preview).

## Gotchas

- **Self-contained is deliberate.** The HTML embeds fonts as base64 and carries no CDN link (CSP/offline-safe). In Framer, load Playfair + Inter as project assets — don't add a `fonts.googleapis.com` link.
- **Brand gate before publish:** no em-dashes, no client `!`, no banned words (premium · luxury · upsell · guarantee · discount · pamper · incredible · stunning), no leftover placeholders (`971500000000`, `AED __`, `[… placeholder]`). Gate via `trs-brand-guardian` / `marketing-brand-review`.
- **Two brand voices, never mixed:** TRS (salon "we") vs TRK (founder "I"). These pages are all TRS.
- **Emails / PPTX / PDFs** (Batches 2/4/5) stay **out** of Framer — Framer is web pages only.

---

_Companion docs: `COMPONENTS.md` (component catalogue + per-page skins) · `WHITE-LABEL-SWAP-SHEET.md` (every swap variable) · `HOSTING-GUIDE.md` (where to host) · `framer-tokens.css` (the variable source)._
