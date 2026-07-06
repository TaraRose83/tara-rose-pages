# White-Label & Template Swap Sheet · Asset #0b
_The one checklist that turns a rebuild into a guided find-and-replace. Follow top to bottom, then run the brand gate. Last synced 5 July 2026._

**Two jobs this sheet covers**
1. **Template reuse** (same brand, new page or rewritten copy) — swap the copy, keep tokens/brand/legal.
2. **White-label** (new brand or new location group) — swap everything below, in order.

**Golden rule:** every page in `trs-production/` is a **self-contained single HTML file** — do NOT split tokens into shared CSS. A white-label = editing the same well-defined zones inside each file. Keep it self-contained (Framer-ready, offline-safe).

**Pages in scope (7):** `home/` · `blonde/blonde-menu-led.html` (canonical) · `brunette/` · `cut/` · `treatments/` · `home-care/` · `founding-glow-pass/`

---

## The swap variables (in replace order)

| # | Variable | Where it lives | Current placeholder | Notes |
|---|---|---|---|---|
| 1 | **Brand name** | Nav wordmark, headings, footer, `<title>`, belief bands | `Tara Rose` (11–20× per file) | Case-sensitive find-and-replace per file. Watch the wordmark letter-spacing markup. |
| 2 | **WhatsApp number** | Every CTA deep-link | `wa.me/971500000000` (44× total) | Replace with real number, digits only, no `+`. Keep the `?text=` prefill. |
| 3 | **Prices** | `Menu` blocks (dotted-leader rows) | `AED __` (18× total) | Swap currency **and** amount. If white-labelling to another market, change `AED` too. |
| 4 | **Palette** | `:root` token block in `<style id="trs">` | 16 hex vars (below) | Change values only — **never rename the vars**, every component reads them. |
| 5 | **Fonts** | `@font-face` base64 blobs + `font-family` | Playfair Display + Inter (3 woff2 embedded) | Re-embed as base64 data URIs. Keep the display/body/util role split. Update `font-family` names to match. |
| 6 | **Loop-ring colours** | `--lr` var per page | turquoise / bronze / slate / lavender / sand | One colour per service family. Same diagram everywhere — only `--lr` + node copy change. |
| 7 | **Locations** | Footer + `Locations` block | Mamsha al Saadiyat · Khalifa City A · Al Qouz · Motor City | Names, addresses, hours, "Take me there" map links. |
| 8 | **Legal / entity** | Footer `.foot__legal` | `[Entity name · placeholder]` · `[Licence number · placeholder]` · `[Registered address · placeholder]` | 4 bracketed placeholders. Also the Privacy/Terms links. |
| 9 | **Photography** | `.media` panels | Art-directed duotone placeholders | Drop in real shots. The placeholder is intentional editorial art until then. |
| 10 | **PDPL / consent** (Founding only) | `PDPLBlock` in the form | data-controller notice, GHL/US disclosure | Update controller entity + jurisdiction per brand. Counsel-review before launch. |
| 11 | **Countdown deadline** (Founding only) | `Countdown` JS | `2026-08-15` | Set the real close date; closed-state copy already handled. |
| 12 | **Form API endpoint** (Confidence Mapping · Recruitment · Founding) | `var FORM_ENDPOINT` in each form's `<script>` | `__FORM_ENDPOINT__` | **Nothing is hardwired.** Swap this one placeholder for the brand's CRM/GHL inbound webhook URL and every form POSTs its captured lead there as JSON. While it holds `__FORM_ENDPOINT__` the form stays inert (validates + shows the result/thank-you, sends nothing). |
| 13 | **Internal page links** | `href="/colour"`, `/cut-finish`, `/treatments`, `/home-care`, `/confidence-mapping`, `/careers`, `/contact`, `/privacy`… | production clean-URL paths | Source templates use production paths (for tararosesalon.com). The **deployed/zipped copy** rewrites them to relative `../folder/file.html` so the preview is clickable (see `scratchpad/build-navigable.py`). `/contact` + `/legal/*` currently map to `#` (no pages built yet). |

### Palette tokens (edit values, keep names)
```
--paper:#FAF8F4   --cream:#F1ECE3   --stone:#E7E2D8   --stone-soft:#EFEBE3   --sand:#E7DFD2
--ink:#2D2E37     --ink-deep:#1C1B18  --ink-soft:#74747B
--accent:#99F6E4  --accent-deep:#7DE6D2  --accent-soft:#EEF3C7  --accent-text:#3aa892
--coral:#FF9B9B   --lavender:#C4B5FD   --lime:#EEF3C7   --err:#C9685F
```
CTAs are `--accent` (turquoise) everywhere. Per-page **skins** re-tone grounds/cards within these tokens — see `COMPONENTS.md`.

---

## Rebrand checklist (run per page)

- [ ] 1. Replace **brand name** (all cases) + `<title>`.
- [ ] 2. Replace **WhatsApp** number in every `wa.me/…` link.
- [ ] 3. Fill every **`AED __`** with real currency + price.
- [ ] 4. Swap the **`:root` palette** values (names unchanged).
- [ ] 5. Re-embed **fonts** as base64; update `font-family` names.
- [ ] 6. Set **`--lr`** loop colour for the page's family.
- [ ] 7. Replace **locations** (names, addresses, hours, map links).
- [ ] 8. Fill the 4 **legal** placeholders + Privacy/Terms links.
- [ ] 9. Swap **`.media`** placeholders for real photography.
- [ ] 10. (Founding) Update **PDPL** controller + **countdown** date.
- [ ] 11. **Re-embed fonts** via the Python step if you edited the placeholder → emit fresh `*.artifact.html`.

## Final gate (never skip)
- [ ] Run the **brand gate**: grep for em-dashes, client `!` (excl. `!important`), banned words, and any **leftover placeholder** (`971500000000`, `AED __`, `[… · placeholder]`, old brand name).
- [ ] Confirm no old-brand hex leaked into the `:root` block.
- [ ] **No external font CDN.** Fonts are embedded as base64 — the head must NOT also carry `fonts.googleapis.com` / `fonts.gstatic.com` `<link>` or `preconnect` tags. They break the offline/CSP-safe promise. (Auto-check with `scratchpad/wl-audit.py`.)
- [ ] No off-brand fonts in markup (Poppins, Arial, Cormorant, DM Sans, Montserrat…).
- [ ] For a *different* brand: the banned-word list is TRS-specific — replace it with the new brand's own banned list before gating.

## White-label test log
- **5 Jul 2026 — all 8 pages PASS.** Audited tokens · embedded-fonts/no-CDN · brand-name replaceable · WhatsApp placeholder/none · price placeholder/none · legal placeholders · no off-brand fonts · no retired hexes. Fix applied: stripped leftover Google Fonts `<link>`+preconnect (3 lines each) from 7 pages that were already embedding fonts. Re-run anytime: `python3 scratchpad/wl-audit.py`.

---

## What to build later (not now)
A **brand-config → auto-stamp generator** (one JSON of the values above → all pages emitted) is the real white-label engine. Worth building once a **second brand actually exists**. Premature before that — this sheet + find-and-replace is faster for 1–2 brands.
