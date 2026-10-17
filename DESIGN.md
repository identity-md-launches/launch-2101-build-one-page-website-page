# Implemented design

## Overview

This is a single page that says `hello world`. The brief's “0 styling” is the design constraint: there is no authored CSS, reset, inline style, framework UI, or client JavaScript. The browser supplies the presentation. The complete visible source is the `<main>` element at `index.html:19`.

## Colors and tokens

There are no design tokens or declared page colors. In the inspected Chromium rendering, the text was black on the browser's white canvas; the pinned probe measured **21:1** contrast. The body background itself computes to transparent. These are browser defaults, not source-defined palette values, and user preferences can change them.

`public/favicon.svg` uses the named SVG colors `black` and `white`. `public/og-image.png` is a 1200 × 630 screenshot of the plain page. Neither asset is displayed within the page body. There are no accent, border, status, or theme tokens.

## Typography

`index.html:19` contains one normal text run. No font files, font declarations, size scale, weight, line-height, letter-spacing, or capitalization rules are authored. Chromium reported `"Times New Roman"`, 16px, weight 400, and normal line-height and letter-spacing; this describes computed browser defaults, not a bundled or verified font file. The measured line box was 18px high.

The greeting is selectable and wraps using normal HTML flow. It is intentionally body text, without a heading, so it retains the plain text appearance requested. There is no section hierarchy to navigate. `lang="en"` identifies the language.

## Layout and responsive behavior

There are no spacing tokens, fixed dimensions, breakpoints, grids, containers, or positioning rules. `<main>` uses normal block flow. Chromium's default body margin was 8px, so at 390px wide the main block measured 374px wide, beginning at (8, 8). The viewport metadata at `index.html:5` uses the device width and does not restrict zoom.

The greeting was fully visible without horizontal overflow at 320, 390, 768, and 1440 CSS pixels. A temporary 200% text-size override also fit at 390px. That test does not establish native browser zoom behavior. No width-specific source behavior exists.

## Elevation, depth, and shapes

The page has no borders, shadows, cards, rounded corners, clipping, overlays, or layers. The favicon is a separate square white SVG canvas containing a black serif `h`.

## Components

| Pattern | Source | Behavior |
| --- | --- | --- |
| Greeting | `index.html:19` | One native main landmark with the exact text `hello world`; no props, classes, variants, controls, or loading states. Reading and browser-native selection are the primary uses. |
| Document metadata | `index.html:4` | Encoding, scalable viewport, title, description, favicon, and Open Graph fields. All asset references are relative. |
| Static assets | `public/favicon.svg`, `public/og-image.png` | Copied into `dist/` by Vite. No remote resources or runtime generation. |

The page introduces no tab stops, focus handlers, keyboard traps, motion, forms, navigation, or error states. There is no wallet infrastructure.

## Maintenance

Preserve the exact greeting and native browser defaults for this assignment. Keep metadata truthful and asset references relative. Rebuild `dist/` after changing source or public assets. If another plain page is requested later, reuse the document metadata and native main pattern; it needs an explicit build entry because the current export has one page. Adding styles, a hero, buttons, fonts, or app features would change the requested scope.

## Review references

The six-domain review used the pinned Better Interface guidance by Jakub Krehel, commit `267330e1adfc66a718fb65fa6918c1f06d0a689e` (MIT). This document follows the pinned documentation method adapted from Paul Bakaus's Impeccable, commit `9d715cc4f5564a990ca8345abfdd5df6dc9b41c8` (Apache-2.0). The supplied license notices are preserved in [artifacts/design-guidance-license.txt](artifacts/design-guidance-license.txt). See [validation](artifacts/validation.md) for evidence and limitations.
