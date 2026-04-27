# CoachPage — brand spec

**Version:** 1.0 (concepts shipped 2026-04-27, refined direction A approved)
**Single source of truth for:** logo, colours, typography, OG cards, favicon
**Don't drift from this without updating it first.**

## Palette

| Token | Hex | Usage |
|---|---|---|
| Navy | `#0B1F3A` | Primary brand colour. Backgrounds for dark surfaces (OG card, app icon). Wordmark "coachpa" on light bg. |
| Amber | `#E5A11C` | Accent. Always reserved for the `.ge` in the wordmark, the icon mark, key CTAs, and accent strips on the OG card. Never decorative — every amber pixel must mean something. |
| Cream | `#F5F2EC` | Light surface background. Wordmark "coachpa" on dark bg. |
| Slate | `#1F2937` | Body text on light backgrounds. Never use Navy for body text — too heavy. |
| Mute | `#0B1F3A @ 55-60% opacity` | Secondary text, taglines, mono-tag pills. |

Pair colours: Navy + Amber (primary), Cream + Navy (text-on-bg), Cream + Amber (rare, attention surfaces only).

## Wordmark

- **`coachpa.ge`** — all lowercase. Never CamelCase, never `CoachPage` for the wordmark itself.
- The `.ge` is always amber. The `coachpa` is always navy on light or cream on dark.
- Typography: Inter Bold (700), letter-spacing tight (-4 to -5 at 100px). Never serif. Never italic.
- Minimum size: 64px wide. Below that, use the icon instead.
- Clear space: equal to the height of the wordmark on every side.

The product is referred to in prose as "**CoachPage**" (CamelCase). The URL is "**coachpa.ge**" (lowercase). The logo uses the URL form to make the pun visible.

## Icon

The amber `.ge` in a navy square (or rounded square for app contexts).

- Square: `variants/icon-square.svg` — sharp corners, for OG card embeds, social profile pictures
- Rounded square: `variants/icon-rounded.svg` — 18% corner radius, for iOS / macOS app icons, PWA install
- Favicon: `variants/favicon.svg` — simplified for browser tabs at 16-32px

The icon is the wordmark cropped to its most distinctive 25%. Recognisable on its own once the brand has any awareness; before that, always pair with the wordmark.

## Typography

| Surface | Family | Weight | Notes |
|---|---|---|---|
| Wordmark, headlines | Inter | 700 | Tight tracking. System fallback: Helvetica Neue, Arial. |
| Body | Inter | 400 | Tracking 0. |
| Numerals, monospace, labels | JetBrains Mono | 400 | All-caps + wide tracking for "BLOOMBERG-GRAMMAR" labels on stat strips. System fallback: Menlo, monospace. |
| Coach-page rendered CV | Inter | 400/600 mixed | The actual coach pages stay Inter — consistent with the wordmark. |

Never use Comic Sans, Times, Georgia, Roboto, or any other font outside this list. If a font isn't loaded, fall back through the chain — never silently substitute.

## OG card grammar

Per the share PRD, OG cards follow Bloomberg dashboard grammar:

- Dark navy base, single amber accent
- Top + bottom 6px amber strips (reads as "premium" without being loud)
- Wordmark centred upper-third
- Stat strip lower-third: 4 columns, JetBrains Mono labels above bold numerals
- No gradients, no shadows, no glow

`variants/og-default-1200x630.svg` is the homepage OG. Per-coach OGs (Phase 1e) follow the same grammar with coach name + photo + top 3 licences replacing the stat strip.

## Do / don't

| Do | Don't |
|---|---|
| Use lowercase `coachpa.ge` for the wordmark | Capitalise it |
| Keep amber reserved for `.ge` and accent moments | Use amber for body text or large fills |
| Pair Navy + Amber on dark surfaces | Use light Navy on light Cream (no contrast) |
| Use the icon at favicon scale | Stretch the wordmark to a square |
| Outline text to paths before production deploy | Ship logo with raw `<text>` elements (font dependency risk) |
| Keep the tagline in JetBrains Mono ALL-CAPS spaced | Set the tagline in cursive or italic |

## Production-grade outlining (do before final launch)

The SVGs in `concepts/` and `refined/` use `<text>` elements with Inter / JetBrains Mono font-family declarations. This is fine for browser-rendered surfaces (they load the fonts via Google Fonts or self-hosted webfonts) but NOT for surfaces where the font might be missing.

Before final launch:
1. Open `refined/coachpage-wordmark-*.svg` in Figma or Illustrator
2. Select all text
3. Convert to outlines / vector paths
4. Re-export as `coachpage-wordmark-*-outlined.svg`
5. Use the outlined version in places where fonts can't be guaranteed (PDF exports, print, partner usage)

Until then, ensure `Inter` and `JetBrains Mono` are loaded as webfonts in `app/layout.tsx`.

## Files in this folder

```
coachpage/
├── BRIEF.md                        — original brief + concept rationale
├── BRAND-SPEC.md                   — this file
├── concepts/                       — all 6 concept SVGs (A, B, C × light/dark)
├── refined/                        — Concept A finished
│   ├── coachpage-wordmark-light.svg
│   ├── coachpage-wordmark-dark.svg
│   ├── coachpage-wordmark-with-tagline-light.svg
│   └── coachpage-wordmark-with-tagline-dark.svg
└── variants/                       — derived assets
    ├── icon-square.svg              (any size, sharp corners)
    ├── icon-rounded.svg             (any size, 18% radius — app icon)
    ├── favicon.svg                  (32px optimised, browser tabs)
    └── og-default-1200x630.svg      (homepage OG card template)
```

## How to use in code (coachpage repo)

In `app/layout.tsx`:

```tsx
export const metadata = {
  title: 'CoachPage',
  description: 'The online CV for football coaches.',
  icons: {
    icon: [
      { url: '/favicon.svg', type: 'image/svg+xml' },
      { url: '/icon-32.png', sizes: '32x32', type: 'image/png' },
    ],
    apple: '/apple-touch-icon.png',  // 180x180 PNG
  },
  manifest: '/manifest.json',
  openGraph: {
    images: ['/og-default.png'],     // exported from og-default-1200x630.svg
    type: 'website',
    siteName: 'coachpa.ge',
  },
}
```

PNG exports of the SVG variants happen in the coachpage repo build — drop SVGs into `public/`, run an SVG-to-PNG step to generate the PNG fallbacks for Apple Touch Icon and OG images (modern browsers accept SVG favicons natively, but Apple Touch Icon and og:image must be raster PNG/JPG).

Suggested build script (in `package.json`):

```json
"scripts": {
  "build:assets": "sharp -i public/og-default.svg -o public/og-default.png && sharp -i public/icon-rounded.svg --resize 180 -o public/apple-touch-icon.png && sharp -i public/icon-rounded.svg --resize 192 -o public/icon-192.png && sharp -i public/icon-rounded.svg --resize 512 -o public/icon-512.png"
}
```

Run once in the coachpage Claude Code instance, commit the generated PNGs.
