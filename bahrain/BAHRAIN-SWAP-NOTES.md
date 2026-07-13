# Tara Rose — Bahrain Instance (separate, repurposed)

A full duplicate of the UAE production page set, re-skinned for Bahrain. **Nothing is hard-wired** — every Bahrain-specific value below is a placeholder to swap when the branch details are confirmed. Same design system, same components, its own market.

**Live preview:** https://tararose83.github.io/tara-rose-pages/bahrain/
**Source:** `Landingpages/trs-bahrain/` · **UAE original:** `Landingpages/trs-production/`

## What was already swapped (UAE → Bahrain)
- **Currency:** every `AED __` → `BHD __` (Bahraini Dinar).
- **Locations:** the 4 UAE salons → `Bahrain Location 1–4` with `Address to be confirmed, Bahrain`. Google Maps links point to a generic "Tara Rose Bahrain" search.
- **Phone:** UAE numbers → `+973 __`. Country-code dropdowns now default to **+973**.
- **Schema (JSON-LD):** `addressCountry` `AE` → `BH`; localities → Bahrain.
- **Copy:** "Abu Dhabi / Dubai / UAE" → "Bahrain"; "dirham" → "dinar"; salon-count headings → "Bahrain salons".
- **WhatsApp placeholder** country code → 973.

## Still to fill before go-live (placeholders)
1. **Real Bahrain branch(es)** — names, addresses, phone numbers, Google Maps pins. Delete unused of the 4 location slots.
2. **Real BHD prices** — every `BHD __` (note: BHD is ~10× an AED figure and uses 3 decimals, so re-price, don't just convert).
3. **WhatsApp number** — replace `97300000000`.
4. **Form endpoint** — `__FORM_ENDPOINT__` → the Bahrain GHL webhook (kept separate from the UAE pipeline).
5. **PDPL / consent block** — swap UAE data-consent wording for **Bahrain PDPL (Law No. 30 of 2018)**; local counsel review before publish.
6. **Entity / licence / registered address** — footer + legal placeholders (Bahrain CR).
7. **Founding Glow Pass** — already Bahrain-native; confirm it's the same offer for this instance.

## To duplicate again (any new market)
1. `cp -R trs-production <new-market>`
2. Run the same swap pattern (see `scratchpad/build-bahrain.py` for the mapping) for currency, locations, country code, schema country.
3. Point `build-bahrain.py`'s `DEPLOY` at a new subfolder → its own preview link.

Kept deliberately separate from the UAE set so each market stays clean to repurpose.
