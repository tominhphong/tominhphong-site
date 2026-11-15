# Style: Vaporwave Memphis (9:16 Vietnamese aesthetic / music-promo edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build (topic shape t136, Jev 0.62).** A mood-first promo with ONE hero idea and a short list: a music or album release, a creative or brand teaser, a playful "coming soon", a retro-tech or nostalgia story, a festival or event card. Good for 8-15 s social cuts and for the opening or closing beat of a longer piece. Not for numbers (no tile fits a retro window), enforcement, bad news, specs, code or terminals, dense text. Jev 0.62 for "Synthwave album release with a neon visual concept" is a middling fit: the mood is perfect, but the style carries almost no information, so a story with facts to prove needs another style.

**Reading order.** One section after another; section 12 holds the traps from this build and wins on any conflict.

**Status.** Written 2026-11-15 from ONE real demo build (`samples/sample-t136.mp4`, 12.0 s, 1080x1920, 30 fps, silent, 2.8 MB, three beats). DEMO-ONLY: voice-over, word timing, captions and music were NOT exercised. The caption look in section 8 and the sound in section 9 are copied from the profile and marked ASSUMED; they have never been tested. All content on screen is invented and labelled "MINH HOẠ".

The look: a pink-to-violet dusk sky, a big sliced sun sitting on a teal horizon line, a perspective neon grid scrolling toward the viewer, flat Memphis shapes (hard dark outlines) drifting in the side margins, and a bevelled grey retro OS window that pops open, grows into the next scene and holds the content. Energy 3: dreamy, slow, never sharp; no shake, no flash.

Source of values: `styles/profiles/vaporwave-memphis.yaml`. Anything the profile does not give is marked **ASSUMED**.

## 1. Tokens

```css
--bg:#2b1055;      /* sky top                                              ink on it 14.97:1 */
--ink:#fff4fb;     /* all light text                                        */
--pink:#ff71ce;    /* sun base, bars, shadows. NEVER text under ink: ink on pink 2.30:1 */
--teal:#01cdfe;    /* horizon line, grid lines, offset shadow, CTA border   9.6:1 on floor #1d0a3d */
--mint:#05ffa1; --lilac:#b967ff; --sun:#fffb96;  /* shapes, slice bars; sun yellow as text 16.8:1 on floor */
--win:#c0c0c0; --navy:#000080; --out:#1a1a2e;     /* window body, title bar, outlines */
/* ASSUMED, from this build */
--floor:#1d0a3d;   /* grid floor / lowest band of the frame */
--sky-mid:#4a1a78 (30%), #b0359e (48%)  /* gradient stops between #2b1055 and #ff71ce at the horizon */
```

Measured contrast (WCAG formula, computed by hand from relative luminance; the HyperFrames `validate` also reported "10 text elements pass WCAG AA"):

| Pair | Ratio |
|---|---|
| `#fff4fb` on sky top `#2b1055` | 14.97 |
| `#fff4fb` on sky at y 200 (about `#3d1668`) | 12.95 |
| `#fff4fb` on sky at y 470 (about `#a0309a`, the lightest part under the display word) | 5.78 (text is 250 px, so the 3:1 large-text bar applies) |
| `#1a1a2e` on window `#c0c0c0` | 9.38 |
| `#ffffff` on title bar / selected row `#000080` | 16.0 |
| `#fff4fb` on CTA plate `#1a1a2e` | 15.9 |
| `#fffb96` on floor `#1d0a3d` | 16.8 |
| `#1a1a2e` on pink `#ff71ce` | 6.9 |
| `#fff4fb` on pink `#ff71ce` | 2.30 (FAIL: never put light text on pink) |

Colour rules: pink, teal, mint, lilac and sun are for shapes, shadows, bars and the glow only. Text is `--ink`, `--sun` (on the dark floor only), or `--out` on the grey window. Material (profile): flat pastel shapes with 4 px `#1a1a2e` outlines; window bevel is 3 px white top-left, 3 px `#404040` bottom-right, 4 px `#1a1a2e` border, hard offset shadow `14px 14px 0 rgba(26,26,46,.85)` (no blur).

## 2. Fonts (3 local files; the profile's Monoton / Rubik / Space Mono are NOT installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Display word, headlines, CTA, kicker | Monoton 160 / Rubik 800 italic 80 | `SegUIVar.ttf`, weight 700, uppercase for the display word, `letter-spacing` 0.06em on it, -0.02em on headlines. Neon is faked with `text-shadow` glow (pink) plus a hard 6 px teal offset | Rendered frames show Ớ, Ạ, À, Ô, ằ, ầ, ế, ê, ố, Ă correctly. The full 36-letter fontTools cmap test was done in the sibling owner docs for this same file (all present); it was NOT re-run in this build (sandbox blocked the script), so treat it as inherited, plus the visual check |
| Window title, file names, track numbers, sub line | Space Mono | `CascadiaMono.ttf`, weight 600-700 | present (same inherited note) |
| Never | | `segoepr.ttf` | lacks Vietnamese letters |
| Not used | | `cambriai.ttf` | no serif line was needed |

Substitution to report to anyone reading the style: Monoton (the multi-line outline neon face) is replaced by a glowing heavy Segoe. The look reads as "neon sign" at 250 px; it loses the striped letter outline. If Monoton is ever installed, keep Segoe for any text with Vietnamese tone marks, because Monoton has no Vietnamese coverage (EM ĐOÁN: it is a Latin-only display face).

Declare faces with `font-display: block`; variable ones with `font-weight: 300 700` / `200 700`.

### Type scale (1080 x 1920, px; all measured from this build)

| Token | Font | Size | Notes |
|---|---|---|---|
| `#neon` display word (one per beat) | Segoe 700 | 250 / 1.1 | letter-spacing 0.06em, glow `0 0 18px pink, 0 0 46px pink`, breathes to 30 px / 80 px |
| `#t3a` closing title line 1 | Segoe 700 | 150 | pink/teal stacked offset `7px 7px 0 pink, -4px -4px 0 teal` |
| `#t3b` closing title line 2 | Segoe 700 | 170 | same glow as the display word |
| `.h1` beat headline | Segoe 700 | 84 / 1.1, -0.02em | 2 lines, offset `5px 5px 0 pink, -3px -3px 0 teal` |
| kicker | Segoe 700 | 38, +0.16em | one line, uppercase |
| window main line | Segoe 700 | 68 | on grey, `--out` |
| window sub line | Segoe 600 | 40 | |
| track row | Segoe 600 | 50, number Cascadia 700 44 | row pitch 124, row height 104 |
| CTA plate | Segoe 700 | 54 | |
| sub line on floor | Cascadia 600 | 38, +0.04em | `--sun` |
| window title | Cascadia 600 | 30 | white on navy |
| footer "MINH HOẠ" | Segoe 700 | 30, +0.14em | the one footer line; nothing else is below 38 px |

Vietnamese runs 15-25% longer than English: the longest line "Ngày Cuối Băng Từ" at 50 px is 411 px wide in a 888 px row. `.mask` boxes carry `padding: 10px 0 22px` and `line-height >= 1.05` so Ạ, Ớ and Ộ marks are not cut by `overflow: hidden`.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -150  top platform UI: empty
y 150  -190  kicker (beat 1)                 | y 175-370  .h1 (beat 2) | y 150-480 closing title (beat 3)
y 215  -470  display word NEON (beat 1)
y 540  -1120 sun, 580 px circle, x 250-830 (sliced bands)
y 1112 -1118 teal horizon line (58% of the height, profile)
y 1114 -1920 grid floor (perspective), haze gradient y 1114-1414
y 1250 -1630 window, beat 1 (x 90-990, 900 x 380)
y 470  -1660 window, beat 2 (x 60-1020, 960 x 1190)
y 1290 -1440 CTA plate, beat 3 (x 120-960, 840 x 150)
y 1480 -1520 sub line, beat 3
y 1800 -1830 footer "MINH HOẠ" (the only footer)
y 1830 -1920 bottom platform UI: empty
x 0-130 and x 930-1080  Memphis margin lanes (shapes live here; titles stay inside x 140-940 except the 150/170 px closing title, 85-1000)
```

No captions band was used (silent demo). A real voiced edition must keep the profile's bottom caption band and move the window/CTA up by one caption pill; that was not tried (ASSUMED).

## 4. Layers, back to front

`#sky` (CSS gradient `#2b1055 -> #4a1a78 30% -> #b0359e 48% -> #ff71ce 100%`, y 0-1114) -> `#sun` (CSS circle with a `mask-image` of 4 transparent bands that get thicker toward the bottom: 3%, 4.5%, 5.5%, 6.5% of the height) -> `#floor` (perspective grid) -> `#haze` (pink-to-transparent, hides the horizon seam) -> `#horizon` (6 px teal) -> `#shapes` (13 SVG shapes) -> beat text (kicker, NEON, h1, closing title, CTA, sub line) -> `#win` -> `#foot` -> `#bars` (slice-bar transition, topmost). Depth ratio: sky 0, sun (scale 1.00 -> 1.04 over the video), grid 120 px per second, shapes drift 18-40 px.

## 5. Components

- **Sliced sun:** `580 x 580` circle, gradient `#fffb96 -> #ffb8a0 45% -> #ff71ce`, so its base melts into the horizon colour. The slice mask is static CSS; one element, so it is cheap.
- **Grid floor:** baked asset `assets/grid.svg` (120 px tile, 3 px `#01cdfe` lines on `#1d0a3d`) scrolled with `backgroundPositionY 0 -> 1440` over the full 12 s (linear, 120 px/s: this is the "dolly"). Plane: `#floorin` 3480 x 520 px, `rotateX(70deg)`, `transform-origin: 50% 0`, parent `perspective: 600px; perspective-origin: 50% 0`.
- **Retro window:** grey body, bevel as in section 1, title bar 58 px `#000080` with the mono file name left and two fake 34 px buttons right. Content is in two absolute groups (`.g1` intro, `.g2` tracklist) so the window can grow without re-laying out text.
- **Chunky progress bar:** 10 segments, each `scaleY 0 -> 1` in 0.05 s, staggered 0.17 s, pink on white, 4 px outline.
- **Track row:** 104 px high; the selected row is `#000080` fill, white text, 4 px `--out` border; selection steps down with `tl.set` (no tween), like an old list box.
- **Memphis shape:** 110 px SVG, flat fill from the palette, 4 px `#1a1a2e` outline (or a thick stroke without fill for rings, zigzags, waves, plus, dots). 13 in the sample (profile limit about 16).
- **CTA plate:** `#1a1a2e` box, 4 px teal border, hard pink offset shadow `10px 10px 0`.
- **Slice bars:** 8 bars of 240 px, 5 palette colours cycling pink, teal, lilac, mint, sun, pink, teal, lilac.

## 6. Motion language (energy 3)

- Easing: entrances `expo.out` (0.6-0.7 s), shape pop `back.out(1.6)`, window growth `power3.inOut` 0.7 s, bars `power2.inOut`. Window pop-open is `steps(4)` over 0.24 s (the retro stutter), scale 0 -> 1 (profile says 0.2; 0 is cleaner under `steps`).
- Letters of the display word rise from 60% below with a 0.1 s stagger, opacity 0 -> 1, then the glow breathes 18/46 px -> 30/80 px on a 1.4 s sine yoyo.
- Constant micro-motion on every frame: grid scroll, sun scale 1.00 -> 1.04, shapes rotating 25-45 deg and bobbing 18-40 px, window sway `y -8` over 3 s in beat 2. Nothing is frozen.
- No shake, no flash, no impact frame (profile: "No shake").
- Beat response (profile) was not tested: no music in this build.

### Transitions used (two, different)

1. **Window pop -> grow-into-scene** (1.50 s pop, 4.0-4.7 s growth): the beat-1 window grows from 900 x 380 to 960 x 1190 while the beat-1 text exits upward in 0.35 s and the beat-2 headline rises at 4.5 s. This is the profile's "window-pop; next scene inside it goes full-frame".
2. **Sun-slice bars** (7.9-8.88 s): 8 colour bars slide in from alternating sides 0.34 s each (0.03 s stagger), the content is swapped at 8.47 s when the frame is fully covered, bars leave 8.5-8.88 s. Both profile moves; grid-dive and confetti wipe were not used.

## 7. Scene recipes (S = beat start; times are absolute in the 12 s sample)

### R1 Cover (0-4.0 s): the neon title
Sky fades in 0-0.6, sun rises 150 px in 1.2 s (`expo.out`), kicker rises from its mask at 0.4, NEON letters at 0.6-1.7, shapes pop at 0.5-1.5 (seeded stagger), window pops at 1.5-1.74, `.g1` content in at 1.8, progress segments fill 1.9-3.6 (done well before the cut). Hold 3.6-4.0: full composition.

### R2 Feature list (4.0-7.9 s): the tracklist
Beat-1 text leaves (3.9-4.25, then `visibility: hidden` at 4.3), window grows 4.0-4.7, headline rises 4.5-5.1, 8 rows slide in from x +60 with 0.1 s stagger at 4.6-5.6, the selection moves row 1 -> 2 at 6.0 and row 2 -> 3 at 6.9. Hold on the full list from 5.6.

### R3 Outro (8.5-12.0 s): the closing title
Bars clear 8.5-8.88; line 1 rises at 8.6, line 2 at 8.78, CTA plate rises 60 px at 9.0 (0.5 s), the sun scales 1.04 -> 1.10 on 8.5, glow breathes from 9.3. The last 1.5 s (10.5-12.0) is the full composition with the grid still scrolling.

## 8. Captions (ASSUMED, NOT EXERCISED: demo build, silent)
Profile: retro window strip, `#c0c0c0` bevel box, 42 px Be Vietnam Pro 700 `#1a1a2e`, current word `#ff71ce`. Danger measured in this build: `#ff71ce` on `#c0c0c0` is only about 1.8:1 (EM ĐOÁN from luminance .375 vs .527), so a current-word highlight must be a navy fill with white text (16.0:1, as the track-row selection here), not pink text. Karaoke timing and Vietnamese line breaks were not tested.

## 9. Sound (ASSUMED, NOT EXERCISED: no music, no SFX in the demo)
Profile: vaporwave / future funk / chillwave 80-100 BPM, OS dings on window pops, tape wobble on transitions. Not tested. The timing in this build (window pop at 1.5 s, growth at 4.0 s, bars at 7.9 s) is not on any beat grid; when music is added, move the three transitions to bar lines.

## 10. Images
No generated image was used. The sample is 100% CSS plus one baked SVG tile (`grid.svg`, 200 bytes) and 13 inline SVG shapes; render time 11.3 s, file 2.8 MB. An optional agy image (a pastel marble bust with pink/teal rim light on `#2b1055`, no text, no real people) was planned for beat 2's empty left margin and dropped to keep the demo lean. Never use photoreal product renders (profile).

## 11. Must not
- Corporate blues and greys; the only grey is the window `#c0c0c0`.
- Light text on pink (2.30:1). Use `--out` on pink, or put the text on a dark plate.
- More than one display (glow) word per beat; more than about 16 shapes; shapes in the title zone or over a held text line.
- Fast aggressive cuts, shake, flash, impact frames.
- `segoepr.ttf`; any real band, album, label or logo; any real date, price or spec (all invented content carries "MINH HOẠ").
- Numbers, charts, code, terminals (profile `avoid`).
- A grid built as a tall rotated plane without checking the perspective maths (trap 1).

## 12. Traps seen in real builds (THIS build, 2026-11-15, with measured numbers)

1. **The perspective grid vanished.** First try: `#floorin` 2600 px tall, `rotateX(74deg)`, parent `perspective: 520px`. A point at the bottom ends up at z = h sin(theta) = 2600 x 0.96 = about 2500 px, far past the 520 px camera, so the plane is behind the viewer and the floor rendered as flat dark. Fix: keep h x sin(theta) below the perspective distance for the visible part: h 520, theta 70 deg, perspective 600, `perspective-origin: 50% 0` (the vanishing point on the horizon). Result: lines converge to the horizon, 120 px cells near the horizon and about 300 px at the bottom.
2. **`inspect` reported 8 errors, all `text_occluded` / 4 `content_overlap`, all false.** Text waiting in an `overflow:hidden` mask at `yPercent: 110` still counts as visible text, and text under the slice bars at 8.67 is genuinely covered. Fix: parents of not-yet-shown text start at `opacity: 0` (set to 1 at reveal); exited text gets `visibility: hidden` (`#neon`, `#kick` at 4.3 s); text intentionally covered by the wipe bars carries `data-layout-allow-occlusion` on the element the tool names (the inner `#t3ai`, `#t3bi`). After that: 0 layout issues in 9 samples.
3. **Half-empty window.** First tracklist: 5 rows in a 1090 px window left 40% of the grey body empty (rows ended at y 1140 of 1560). Fix: 8 rows (matches "8 bài"), pitch 124 px, window 1190 px high; rows end at 1064 of 1190 and the bar sits at 1100.
4. **A Memphis shape sat on the display word.** The cyan zigzag at (920, 380) touched the right N of NEON (x 740-900, y 270-460). Shapes are placed by hand in the margin lanes (x < 130 or > 930) AND outside the y range of the current title; moved to y 730.
5. **Swap under the bars too early.** Content swap was at 8.35 s but the last bar (index 7, entering 7.9 + 7 x 0.03 = 8.11) only covers the frame at 8.45 s, so the bottom 240 px could show the new beat for 0.1 s. Swap moved to 8.47 s, after the last bar is in and before the first bar (leaving at 8.5 s) reveals anything.
6. **Lint `overlapping_gsap_tweens`** on `#sun` (scale 1.00 -> 1.04 long tween vs the 8.5 s pop to 1.10) and on `.row` colours (tweens of 0.01 s overlapping at 0 s). Fix: `overwrite: "auto"` on the short pop; row selection with `tl.set`, not `tl.to`.
7. **Empty grey panel while the window grows.** From 4.0 to 4.6 s the grown window shows no content (`.g1` fades at 4.0-4.18, first row enters 4.6): 0.42 s, inside the 0.5 s limit but close. Start rows at 4.45 to leave margin in a longer build.
8. **Ink text on the pink band looks fine in a thumbnail and fails the number** (2.30:1). The headline and title stay in the dark top of the sky; every on-pink label uses `--out` (6.9:1) or sits on a plate.
9. **Fonts the profile asks for are missing.** Monoton / Rubik / Space Mono are not on the machine; see section 2. This is a visible downgrade for the display word, not a bug.
10. **The pre-delivery `frame_check.py` could not run** (no `numpy` in the default `python3`). Frame check was done on an ffmpeg 2 fps sheet read by eye instead (see `selfcheck.md`). Install numpy and Pillow before the next build so the BLANK / TOPHEAVY flags exist.
11. **Hand-timed beats are not on any grid** (no audio): see section 9.
