# Tara Rose — Design System (TRS Standard v1)

The full brand palette, type, and component rules. Pairs with the **Figma Design System** file (live Variables + swatches + components): https://www.figma.com/design/JxFW72KWcMZI2VQ9J8gPEP → **Design System** page. Token values here match `framer-tokens.css` and the Figma `TRS Brand` variable collection exactly. Last updated 7 July 2026.

---

## Colour

> **LOCKED RULE:** a section/page **background is ALWAYS a base colour** — a warm neutral, an editorial dark, or a grey. **Pastels + turquoise are ACCENT-only, never a ground.** Directions differ by *which base family* they use, not by tinting the ground.

### BASE · Warm neutrals (backgrounds)
| Token | Hex | Role |
|---|---|---|
| Paper | `#FAF8F4` | Page background |
| Cream | `#F1ECE3` | Alt section |
| Stone Soft | `#EFEBE3` | Soft cards / bands |
| Stone | `#E7E2D8` | Cards · media |
| Sand | `#E7DFD2` | Warm ground (Home Care) |

### BASE · Editorial dark (warm charcoal — NEVER blue)
| Token | Hex | Role |
|---|---|---|
| Ink | `#2D2E37` | Body + headings (charcoal) |
| Ink Deep | `#1C1B18` | Dark panels / dark hero |
| Dark grounds | `#12110F` · `#1A1815` · `#211F1C` · `#2B2924` | Dark-mode grounds (warm) |
| Ink Soft | `#74747B` | Secondary text, eyebrows |
| Hair | `#E6E3DD` | Hairline rules (ink 11%) |

Backgrounds are warm (R≥G≥B). A blue-tinted dark (e.g. the retired `#0B0E14`) is **banned**.

### BASE · Greys (warm-neutral — a main background family)
`#ECEAE6` · `#D9D6D1` · `#B7B3AD` · `#8C8883` · `#6A6763` · `#4A4744` · `#302E2B` · `#201F1D`

### Turquoise · Wellness — **the only CTA colour**
| Token | Hex | Role |
|---|---|---|
| Soft | `#DDFBF4` | Tint (tag backgrounds) |
| Base | `#99F6E4` | CTA fill, ticks |
| Deep | `#7DE6D2` | Hover / focus ring |
| Text | `#3AA892` | Accent text on light (AA) |
| Dark | `#256A5B` | Deep shade |

### ACCENTS ONLY — pastels, **never a background**, one pillar per piece
**Lime · Empowerment** — Soft `#F6F9E4` · Base `#EEF3C7` · Deep `#D6E08A` · Text `#7C8A2E`
**Lavender · Business** — Soft `#EDE7FE` · Base `#C4B5FD` · Deep `#A78BFA` · Text `#6D4FD0`
**Coral · Culture** — Soft `#FFE1E1` · Base `#FF9B9B` · Deep `#FF7A7A` · Text `#C25757`

> Turquoise (Wellness) is the 4th pillar and doubles as the universal CTA accent. The other three are for editorial / pillar-specific pieces only — a single pillar per asset.

---

## Type
- **Display:** Playfair Display (400/500, + Medium Italic for the accent voice). Fluid scale ≈ 108 / 74 / 62 / 52 / 44 / 36 / 28 / 24 px.
- **Body:** Inter (300/400/500/600). 18 / 17 / 16 / 15.5 / 14.5 / 13.5 px.
- **Eyebrow:** Inter Medium, UPPERCASE, `.4em` letter-spacing, 11px, in Turquoise/Text or Ink Soft.
- The turquoise **Medium Italic** treatment on one word (e.g. *exceptional*, *guessing*) is the signature accent.

## Radius & motion
- Radius: `--r-lg` 22 · `--r-md` 16 · `--r-sm` 14 · `--r-pill` 100.
- Ease `cubic-bezier(.22,.61,.36,1)`; hover lift −2px; durations .15 / .3 / .7s.

## Core components
Pill button (Turquoise Base fill, Ink Deep text) · Ghost button (Hair outline, Ink text) · Tag (Turquoise Soft bg, Turquoise Text) · Card (Paper on Cream, radius 18, soft shadow) · the shared **Full Loop** ring (only `--lr` changes per family).

## Dark mode
A token override, not a re-theme — swap ~11 variables (see `framer-tokens.css`), turquoise stays the sole accent. Four directions in the Figma `dark-mode/` reference (Editorial Ink · Warm Obsidian · Modern Monochrome · Slate Grey).

## Rules
Turquoise is the only CTA. One pillar accent per piece. Never mix TRS with TRK. British English. No em-dashes / exclamation marks / banned words in client copy (gate via `trs-brand-guardian`).
