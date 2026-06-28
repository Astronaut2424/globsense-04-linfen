# Linfen 林芬 — Build Brief

**Project:** #04 Linfen 林芬
**Type:** Fictional Chinese skincare brand · AI-dermatology demo
**Built:** 2026-06-28
**Model:** claude-opus-4-7 (delegated under gpt-5.3-codex slot)
**Status:** built · awaiting deploy

## The Concept

Linfen is a fictional rare-botanicals skincare house sourcing from Yunnan,
Wuyi, and Changbai mountains. The AI moment is a phone-camera dermatologist
that reads the user's skin and composes a custom serum with a generated
label and origin story.

## The Build

Single-file `index.html` (~39 KB, no external assets beyond Google Fonts +
shared `_shared/tokens.css`). All artwork is inline SVG (face silhouette,
bottle render, three Yunnan/Wuyi/Changbai landscape panels). All animation
is CSS + ~150 lines of vanilla JS.

### Sections

1. **Hero** — radial moss-stone gradient with SVG noise texture, 林芬 in
   Noto Serif SC at ~240px, italic Latin subtitle, scroll cue with pulsing
   line.
2. **Diagnostic** — SVG face silhouette inside a stage frame. Click
   "Allow camera" (or scroll into view) and:
   - Status flips to `camera · live` with a blinking dot
   - Faint gold grid overlays the stage
   - A gold scan-line sweeps top→bottom three times
   - Five gold corner-bracket labels animate in: hydration 61%, sebum 34%,
     sensitivity high, fine-line 0.18, tone cool · 4.2
   - Accents (small gold circles) light up the face landmarks
   - Result panel slides up from bottom with the verdict in EN + CN
3. **Serum** — Inline SVG bottle (cap, neck, shoulder, glass gradient,
   amber liquid, highlight, reflection). The cream paper label sits over
   the bottle and *types itself out*: CN name 林芬 · 深秋方 47, then EN
   `Linfen Reserve 47 · Changbai Resin & Wuyi Camellia`, then a four-line
   poetic note, then a barcode-style ingredient stack that animates in
   bar-by-bar. Right column: composition metadata (Base / Heart / Top /
   Lead time).
4. **Story** — Three story cards, each with an inline SVG landscape
   (Changbai pine-and-moon, Wuyi terraced rock with a camellia bloom,
   Yunnan rolling terraces with honeysuckle stems), place tag, CN name,
   English narrative.
5. **Order** — ¥780 in giant Noto Serif SC numerals with a gold ¥, meta
   row (30 ml · ships globally · 72 hr atelier), gold pill CTA
   `Reserve your formula →`, italic fine print.

### Aesthetic

- Palette: deep moss (`#0c1110`, `#131a17`, `#1c2520`), cream (`#f0e6d3`),
  warm gold accent (`#c69a4b`).
- Type: Noto Serif SC for Chinese, EB Garamond italic for English display,
  Inter for body, JetBrains Mono for labels/eyebrows.
- Texture: SVG `feTurbulence` noise layers on hero, diagnostic stage, and
  each story panel — gives the "mossy stone close-up" feel called for in
  the brief without any image assets.
- Quiet around the wow moments: hero, story, and order are sparse so the
  diagnostic scan + label typewriter carry the magic.

### Interaction details

- Scroll reveals (IntersectionObserver, threshold 0.15) on copy blocks and
  cards.
- Diagnostic auto-triggers once when the stage scrolls into view (single
  shot), or on button click — whichever first.
- Label generation auto-triggers when the serum section is reached, even
  if the user skipped the diagnostic.
- Cursor blinks during typewriter, removed on completion.
- All durations are under 6s end-to-end so the demo reads as "AI is real
  and fast" rather than "still loading".

### Files

- `index.html` — single file, all CSS + JS inline
- `_status.json` — `needs_deploy: true`
- `assets/` — empty (intentional, all artwork is inline SVG)

### Deploy notes (for the next worker)

Pure static. Drop the folder anywhere. No build step. Honors `back-to-reel`
relative link to `../` and the shared `../_shared/tokens.css`.
