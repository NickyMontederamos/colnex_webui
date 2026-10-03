# Colnex Design Style — Master Prompt

Copy everything below the line into any AI tool (Claude, ChatGPT, v0, Lovable, etc.). Replace the `[BRACKETS]`.

---

You are a senior front-end designer. Build **[WHAT: page / component / app]** for **[WHO + PURPOSE]** using the "Colnex" design system described below. Output one self-contained HTML file (inline CSS and JS, no image files, no frameworks unless I ask). Mobile-first, accessible (visible focus, 4.5:1 text contrast, respects `prefers-reduced-motion`).

## 1. Mood
Dark neoclassical, gothic, dark academia. Regal and melancholy, lit by a single warm source in a black void (a gold glow, an amber moon). Think carved gold, aged rosewood, drifting embers, cracked stone. Calm and confident, never loud. Inspired by the Kingdom of Dark Strings aesthetic and two reference images (a laurel-crowned figure in cracked stone with glowing eyes, and a horned silhouette against a huge amber moon). Do **not** use those images; recreate the feel with CSS only.

A second family of skins comes from the SlickLab.Digital studio style: paper and ink, square corners, hard offset shadows, dot grid, mono uppercase labels, numbered section eyebrows ("01 / What we do").

## 2. Theme system (required)
Every colour, font, radius and shadow must come from CSS custom properties, so the whole page can be re-skinned by changing `<html data-skin="...">`. Define skins as `html[data-skin="id"] { ... }`. Never hard-code a colour outside the skin blocks.

Tokens: `--bg --bg2 --card --line --line-s --accent --accent2 --on-accent --text --muted --dim --warm --ok --bad --ember (r,g,b triplet) --halo` and structure tokens `--f-head --f-body --f-mono --f-eyebrow --f-btn --ls-head --r-panel --r-btn --r-sm --r-pill --bw --shadow-panel --shadow-node --btn-bg --halo-size`.

Scale tokens (shared by all skins): spacing `--sp-1..6 = 4, 8, 12, 16, 20, 32px` (no other padding/gap/margin values); type `--fs-2xs 10px · --fs-xs 11px · --fs-sm 12.5px · --fs-md 14px · --fs-lg 18px`; motion `--dur-1 180ms · --dur-2 300ms · --dur-3 500ms`, `--ease-out cubic-bezier(0,0,.3,1)`, `--ease-in-out cubic-bezier(.5,0,.5,1)` (Open Props). No ad-hoc font sizes or transition timings.

Every skin must pass WCAG AA: text, muted and accent on card ≥ 4.5:1; big numbers ≥ 3:1; button text on button ≥ 4.5:1. Use `--dim` only for borders and decoration, never for text.

Ship these skins (hex values are the source of truth):

| id | bg / card | accent / accent2 | text |
|---|---|---|---|
| dark-strings (default) | #0B0B0E / #1C1A22 | #C2A662 / #E5C158 | #D9CBB0 |
| eclipse | #060507 / #17110D | #E8A33D / #FFC766 | #EBD3B0 (+ CSS moon) |
| cracked-marble | #0E0D0C / #221F1C | #B89A62 / #E0C48A | #D8D0C2 (+ crack overlay) |
| moonlit-slate | #070A10 / #131B2A | #8FB3D9 / #C5DDF5 | #D3DEEC |
| parchment (light) | #EBE2CE / #F5EEDD | #8A5A1F / #B07A2E | #2D2013 |
| crimson-requiem | #0A0507 / #1E0E13 | #C23049 / #E8647C | #EAD3D6 |
| cathedral-violet | #08060E / #181024 | #9B7BD4 / #C9B0F5 | #E0D6F0 |
| verdigris-crypt | #050B0B / #101F1D | #4FB3A0 / #8FE0CC | #CFE3DC |
| ashen-monochrome | #0A0A0A / #1B1B1B | #BDBDBD / #F0F0F0 | #DADADA |
| rosewood-cello | #0D0806 / #24160F | #C0703A / #E9A06A | #E8D2BC |
| mocha-nocturne | #181825 / #313244 | #CBA6F7 / #F5C2E7 | #CDD6F4 |
| kanagawa-ink | #16161D / #2A2A37 | #E6C384 / #FFA066 | #DCD7BA |
| latte-linen (light) | #EFF1F5 / #F7F8FB | #8839EF / #FE640B | #4C4F69 |
| slick-paper (light) | #EFECE4 / #F8F6F0 | #0B8F89 / #8A6F38 | #121311, ink buttons (#121311), 2px ink borders, 6px 6px 0 #121311 shadows, square |
| slick-ink | #121311 / #1B1C1A | #B8975A / #E3C98C | #EFECE4, gold hard shadows, square |
| gothic-slick | #0B0B0E / #1C1A22 | #C2A662 / #E5C158 | #D9CBB0 + SlickLab structure (square, 2px border, hard gold shadow, dot grid) |

Include a skin switcher (chips) that saves the choice in `localStorage` (wrapped in try/catch).

## 3. Typography
- Gothic skins: headings **Cinzel** (700, letter-spacing .06em), subtitles **Cormorant Garamond** italic, body **Montserrat**, mono labels `ui-monospace`.
- SlickLab skins: headings **Bricolage Grotesque** (700/800, letter-spacing -.01em), body **Geist**, labels **Geist Mono** uppercase.
- Eyebrows: 11px, uppercase, wide tracking (.3em gothic / .14em mono), accent colour. Numbered like "03 / Service menu".
- Hero heading may use a text gradient `accent → text → accent`.

## 4. Components
- **Panel/card:** `--card` background, `var(--bw) solid var(--line)`, radius from `--r-panel` (12px gothic, 0 SlickLab), `--shadow-panel`. Hover: border to `--line-s`.
- **Button:** uppercase, bold, tracked. Primary uses `--btn-bg` or a gold gradient with a slow shimmer on hover. Secondary is outline with `--line-s`.
- **Inputs:** `--bg2` background, 1px `--line`, focus ring `--accent2`.
- **Nodes / tiles:** small cards with a monogram circle, hard offset shadow `--shadow-node`.
- **Chips:** pill (or square on SlickLab skins), `aria-pressed` state in accent.
- **Log/code boxes:** mono, `--bg` background, accent2 text.
- **Toast:** bottom-right, accent2 border, soft glow.
- **Diagrams:** inline SVG recoloured through CSS attribute selectors or tokens, never separate images.

## 5. Optional effects (toggle with `html.fx-*` classes)
`grain` (SVG feTurbulence noise at 9% overlay), `vignette` (inset shadow), `foil` (gold gradient text on headings), `corners` (8-gradient corner ticks on panels), `glow` (panel glow with a strength slider `--glow-k`), `dots` (24px dot grid from `--ember`), `mono` (mono labels), `square` (all radii 0, 2px borders), `hard` (6px hard shadows). Ambient layer: ~45 slow rising ember particles on a fixed canvas, coloured from `--ember`, with an on/off toggle.

## 6. Motion
Slow and heavy: 300–600 ms ease transitions, breathing glow on the hero element, embers, shimmer on primary buttons. Packets or pulses travel along connection lines for "live" diagrams. Disable all of it under `prefers-reduced-motion`.

## 7. Copywriting
Plain, practical English. Short paragraphs. No buzzwords. Say what the thing does and what to click next.

## 8. Deliverable checklist
1. One `.html` file, opens by double-click.
2. All colours from tokens; switching `data-skin` fully re-skins the page.
3. A "Skin CSS" panel that shows the active skin's CSS (scoped and `:root` versions) with copy buttons, plus the CSS of any active effects.
4. Works at 360px wide with no horizontal scroll (long chip rows become one swipeable row).
5. Exports the active skin as W3C Design Tokens JSON (`$type`/`$value`; colours as `{colorSpace:"srgb",components,alpha,hex}`).
6. After the code, list: the skins included, any assumptions, and one thing you would improve next.

**Task details:** [DESCRIBE FEATURES, SECTIONS, DATA, AND ANY BRAND COPY HERE]
