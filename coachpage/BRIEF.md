# CoachPage — logo brief

**Date:** 2026-04-27
**Status:** Concepts ready for selection
**Source PRD:** `360tft-hub/docs/prd/CoachPage_P0_2026-04-27-brand-identity-and-social-sharing.md`

## Five qualifying answers (per `feedback_logo_design_sequence.md`)

| Question | Answer |
|---|---|
| **Palette** | Navy `#0B1F3A` primary + Amber `#E5A11C` accent. Same family as 360TFT, distinguishable by typography weight + structure. White / off-white `#F5F2EC` for backgrounds. |
| **Audience** | Football coaches: grassroots, academy, semi-pro. UK-first. Pasting their CoachPage URL into LinkedIn next to Premier League academy coaches. They want to look polished, not amateur. |
| **Emotional target** | Credible, professional, polished. Bloomberg-grammar serious — NOT consumer-warm, NOT mascot-cute. The card should make a parent reading it think "this coach is the real thing." |
| **Do** | Geometric sans, mono-feel where possible, deliberate use of the `pa.ge` pun, single accent colour, works at favicon scale, works on dark navy AND light cream. |
| **Don't** | No mascots, no footballs as the icon (cliché), no swooshes, no AI-generated photographic logos, no gradients, no drop-shadows, no emoji, no the-letter-G-as-a-football. |

## References (mood)

- **indiepa.ge** — direct sibling product, stripped wordmark with chunky underline. Use as anti-reference for the underline approach (don't be a clone).
- **Bloomberg Terminal** — dark base, single accent, monospace pricing tables. Aesthetic north-star for the OG card; logo plays nice with that.
- **Premier League club crests** — for the badge/monogram direction (Concept B). Roundel + monogram = footballing institutional credibility.
- **Stripe wordmark** — for the wordmark+accent direction (Concept A). Geometric sans, single accent on one character, no decoration.
- **Linear / Vercel** — for the precision wordmark direction.

## Concept directions

Three distinct directions, each with light + dark variants in `concepts/`. Pick one (or a hybrid).

### Concept A — Geometric wordmark with amber `.ge`

The pun made visible. "Coachpa" in navy, ".ge" in amber, all one word. Monoline geometric sans (Inter / DM Sans), even letter spacing. Reads as both the brand and the URL simultaneously.

**Pros:** Strong link between the brand and the domain. Visual hierarchy carries the joke. Works at every size.
**Cons:** Loses meaning when stripped of colour (e.g., black-and-white print).

Files:
- `concepts/A-wordmark-amber-ge-light.svg`
- `concepts/A-wordmark-amber-ge-dark.svg`

### Concept B — "CP" monogram in navy roundel

Premier League badge gravitas. Capital C with a hidden P inside the negative space, set in a navy circle with a thin amber outer ring. Letter mark stands alone as an icon for favicons / app icons. Wordmark sits beside or below.

**Pros:** Strongest icon-only credentials. Footballing institutional feel. Coaches paste a "real badge" not just text.
**Cons:** Monograms are common (every academy has a CP / FC / SC); risk of looking generic. Needs strong execution to escape that trap.

Files:
- `concepts/B-cp-monogram-roundel-light.svg`
- `concepts/B-cp-monogram-roundel-dark.svg`

### Concept C — Wordmark with amber underline

The CV-line / signature treatment. "CoachPage" in clean geometric sans, amber underline beneath stretching the full width — like a pen-stroke under your name on a CV. Direct visual metaphor for the product (it IS your CV).

**Pros:** Reinforces the product story (CV → underline = signature). Works mono. Subtle enough to age well.
**Cons:** Very close to indiepa.ge's stripped aesthetic — risk of looking derivative unless we differentiate the underline weight / shape.

Files:
- `concepts/C-wordmark-underline-light.svg`
- `concepts/C-wordmark-underline-dark.svg`

## Recommendation

**Concept A (geometric wordmark with amber `.ge`)** is the strongest opening bet. It carries the brand-story (the URL pun) at every viewing size and works as both wordmark and standalone (the amber `.ge` becomes the icon). Concept B is the safe institutional play but risks looking like every other academy. Concept C is closest to indiepa.ge's existing aesthetic — borrowing too heavily.

Final call is yours. Reply with **A**, **B**, **C**, or "let me see hybrids."

## Next steps after selection

1. Refine the chosen direction — `refined/<concept>-final.svg` (light + dark)
2. Generate variants — `variants/`:
   - Icon-only (square, 1:1)
   - Favicons: `favicon-16.png`, `favicon-32.png`, `apple-touch-icon-180.png`, `icon-192.png`, `icon-512.png`
   - Wordmark light + dark backgrounds
3. Push to `360tft/360TFT_BRAND_ASSETS/coachpage/` per existing convention
4. Write `coachpage/docs/brand/coachpage.md` mini-spec (palette, typography, do/don't)

## Notes on SVG portability

Concept SVGs use `font-family: Inter, ...` with system fallbacks for preview. Before production deploy, the chosen direction will have its text **outlined to vector paths** so the final logo never depends on a font being installed on the rendering machine.
