# TRS Production Design System · Asset #0
_The real, current system as built. Supersedes the Batch-1 `trs-design-architect` component list. Last synced 5 July 2026._

Every `trs-production/` page is a **self-contained single HTML file**: locked TRS Standard v1 tokens + base + page CSS inlined into one `<style id="trs">`, with **Playfair + Inter embedded as woff2 data URIs** (offline-safe, Framer-ready). Turquoise CTAs, Playfair + Inter, and the token *values* are locked; everything below is how we compose within them.

---

## Build pipeline (how every page is made)
1. Read the wireframe + `specs/<slug>.md` from the handoff; keep locked copy verbatim.
2. Author the page with a `/*__FONTS__*/` placeholder in `<style id="trs">`.
3. Python step: base64-embed the 3 woff2 (Inter var, Playfair 500, Playfair 500 italic) into the placeholder; emit a body-only `*.artifact.html` for the Artifact tool. (Fonts live in the session scratchpad `fonts/`.)
4. **Brand gate:** grep for em-dashes, client `!`, banned words, BHD/price leaks (exclude the base64 font line + CSS `!important`).
5. Publish the artifact for a live preview; save `index.html` per page.

---

## The elevation layer (universal, on every page)
- **Art-directed image panels** — `.media` is NOT a flat gradient. Layered duotone radial + soft light bloom + fine SVG `feTurbulence` grain + a faint "TARA ROSE" wordmark watermark (all inline SVG data URIs on `::after`). Variants `--sand` / `--warm` / `--cool` shift the hue only. Reads as intentional editorial art until real photography drops in.
- **Type** — `font-optical-sizing:auto`, `text-rendering:optimizeLegibility`, `font-feature-settings:"kern","liga","calt"`.
- **Nav** — `.trs-nav`: centred wordmark, `white-space:nowrap` links, brand `padding` breathing room, `.trs-nav.scrolled` shadow via a scroll listener. Service pages carry the full menu; campaign pages (Founding) use a minimal 3-item nav.
- **Fine details** — button shadows + hover lift (accent-tinted on `--accent`), card soft shadows + hover, menu-row hover wash, visible `:focus-visible` on interactive elements.
- **Motion** — restrained: hero rise-in, ambient loop-ring spin, scarcity pulse. Everything behind `@media (prefers-reduced-motion:no-preference)`.

---

## Per-page skins (each page its own room, within the locked palette)
CTAs stay turquoise everywhere; skins change grounds, card tone, and shadow warmth.
| Page | Skin | Signature move |
|---|---|---|
| Home | Bright Wellness | white cards, airy diffuse shadows |
| Blonde (`blonde-menu-led.html` = canonical) | Cool Luminous | mint-grey grounds + **turquoise Loop ring** |
| Brunette | Deep Dimensional | warm grounds + **dark charcoal `.bcard--hero`** + **bronze Loop ring** |
| Cut | Architectural Grey | grey grounds + **slate Loop ring** |
| Treatments | Soft Lavender | clinical calm + **lavender Loop ring** |
| Home Care | Calm Sand | warm neutral + **sand Loop ring** |
| Founding Glow Pass | Warm Campaign | Hero-C + live countdown |
| Recruitment (`recruitment/`) | Careers Warm | Hero-A centred + Safety-Net chips + Three Paths + TRK founder split |

---

## Component catalogue
**Shared shell:** `TRS/Nav` (+ mobile overlay on service pages) · `TRS/Footer` (+ `.foot__legal`, permit line) · `TRS/Belief` (dark pull-quote) · `TRS/FAQ` (dark accordion + FAQPage schema) · `TRS/TrustStrip` · `TRS/ChipRow`.

**Service-page blocks:** `Hero-A` (centred) / `Hero-Ed` (split editorial, Blonde) · **`Menu`** — two variants. (a) Dotted-leader priced list: `.menu-list .mrow .mname .mdots .mprice .mdesc .mmeta .mtag` (Cut / Blow-dry). (b) **Two-families model (Blonde/Brunette/Cut, current):** opens with a **range showcase** (`.shades` grid of art-directed tone/shape tiles + `.shades-cap` — Blonde: Cool·Creamy·Honey·Golden · Brunette: Chestnut·Mocha·Chocolate·Espresso · Cut: Bob·Long Layers·Fringe·Restyle) → `.menu-intro` (Refresh vs Transformation) → `.menu-fam` sub-menus with `.mcols` (two `.mcol` columns Refresh/Transformation) → **per-service prices** (`.mitem` = `.mi-tag?` + `.mi-top`[`.mi-name` + `.mi-price` right-aligned "AED __"] + `.mi-desc`; correction/add-ons use `.mi-price.poa` "Price on application" / "from AED __") → a `.look-band` feature image mid-menu → `.menu-block` for Colour Correction + Colour Add-Ons (`.menu-grid2`). **`.feature-band`** = captionless art-directed image placeholders dropped throughout the page (faint wordmark; `width:100%` + `aspect-ratio`, NEVER `min-height` — that combo overflows on mobile) · **`The Full Loop`** (the signature ring, `--lr` colour per page; ring centre "The Full Loop", nodes Create→Protect→Keep-on-Track/Reshape). **Framing (locked):** the loop is the UNIVERSAL system covering Colour·Cut·Treatments·Home Care·Maintenance — belief "Good hair isn't one visit. It's the Full Loop." + a `.fullloop`/`.fl-part` covers-it-all strip (current family `.on`). Per-service **rhythm** sits under it: `.loop-belief` h3 + `.loop-why` + ring + `.visits`/`.visit-card` (Visit 1/2/3) + `.tiers` Low/Mid/High Maintenance + `.rhythm-compare` (Off-loop vs On-loop `.rcmp`) + `.loop-out` + `.loop-cta` · `PlanTierLadder` (`.bcard`; Blonde Soft/Signature/Transformation, Brunette Polished/Dimensional/Luxury + `.menu-line` correction, Cut Shape/Frame/Finish = architecture not price) · `TreatmentSubset` / `TreatmentGrid` (`.tcard-x`) · `MaintenanceLoop` cards (`.lcard`) / `FlowStrip` · `Education` (`.rhythm-list` 5-Block Rhythm) + **`ScienList`** (science-made-simple glossary) + **`MythsTable`** (`.myth`, The Shift) · `HomeCareLadder` · `Split` · `Testimonials` (`.tcard`, real quotes only) · `Locations` · `ConfidencePromise` · `FinalCTA`.

**Funnel blocks (from Founding):** `Hero-C` (dark campaign hero, grain + champagne wash) · **`Countdown`** (live JS timer, tabular-nums, closed-state) · `Scarcity` pill (pulse) · `AvatarSelector` (`.acard`, click-to-preselect the form) · `BeliefsStrip` (4 shifts) · `Includes` cards · `Timeline` (buyer journey) · Founder (TRK) + Owner (Daisy) splits · **`ReserveForm`** (contact-first: name · WhatsApp+country · email · avatar radio) · **`PDPLBlock`** (required + optional consent, data-controller notice, GHL/US disclosure, rights).

**Conversion pattern (locked 5 Jul):** every service-page CTA opens **WhatsApp** — `https://wa.me/971500000000?text=…` (placeholder number, page-specific prefilled message, `target="_blank" rel="noopener"`). No dead `#` anchors. Funnel CTAs point to `#reserve` (the form). Testimonials show real cleared quotes only (Marelize + Sannah) — placeholder sections are removed, not shown.

---

## Reuse & white-label
To rebrand, re-theme, or spin these into a white-label: follow **`WHITE-LABEL-SWAP-SHEET.md`** (Asset #0b) — it lists every per-brand variable (name, WhatsApp, prices, palette, fonts, locations, legal, photography), where it lives, and the rebrand + brand-gate checklist. Keep pages self-contained; never split tokens into shared CSS.

## Framer handoff
See **`FRAMER-HANDOFF.md`** (the full, current handover) + **`framer-tokens.css`** (the Framer Variable source). In short: each block → one Framer component; bind all colour/radius/font to Framer variables from `framer-tokens.css`; move repeated content (menu, locations, testimonials, FAQs, treatments) into **CMS collections** so pages — and new markets — are data, not rebuilds; point every form at the GHL webhook (`__FORM_ENDPOINT__`). The Full Loop is one shared component (only `--lr` changes per page). Emails/PPTX (Batches 2/4/5) stay out of Framer.
