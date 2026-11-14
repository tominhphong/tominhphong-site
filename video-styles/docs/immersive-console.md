# Style: Immersive console (9:16 console-reveal edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in the one demo build (topic shape t121, Jev fit 0.75):** a hardware or product reveal where a hero object comes first and then 2 to 4 plain facts (a price, a capacity, a launch list): consoles, headsets, a game or entertainment-hub launch, a streaming-box launch. Works for 2 to 4 numbers and one short list of 3 to 5 named items. Not for dense data (more than 4 numbers), long explainers, serious or sad news, anything that needs a warm colour, or spec tables (the profile lists `spec`, `terminal`, `code` as avoid).

**Reading order.** Sections 1 to 11 are the design, written from one 12 s silent build. Section 12 holds the traps measured in that build. Where this file and `styles/profiles/immersive-console.yaml` differ, this file wins (it has real numbers).

**Status. Written 2026-11-14 from a DEMO-ONLY build:** one 12.0 s silent sample, no voice-over, no captions, no music, no word timing, no full video. **Voice rules, caption timing, sound and beat-sync were NOT exercised**; sections 8 and 9 repeat the profile and are marked ASSUMED. Everything else is measured on the sample unless marked ASSUMED. Content in the sample is generic and labelled "Minh hoạ" (449 USD, 1 TB and four game genres are invented illustration, not real facts).

One sentence: a deep navy void with drifting light particles; a glossy hero object appears by a bright rim tracing its silhouette; the hero then shrinks to the top while UI tiles glide in perspective (rotateY -12 deg), and a white focus ring with blue glow travels tile to tile. Energy 4 in the profile, played controlled: weight and glow, not jitter.

## 1. Tokens

```css
--bg: #00091a;     /* void; ink on it 19.9:1 */
--navy: #001f4d;   /* gradient centre, chip fill; ink 16.1:1 */
--ink: #ffffff;    /* all headline, numeral and label text */
--glow: #4fb3ff;   /* rims, focus glow, labels, the key word; 8.75:1 on bg, 7.08 on navy, 6.29 on light tile, 8.14 on dark tile (text-safe) */
--accent: #2a62e0; /* art fills and marks ONLY: 3.72:1 on bg (fails as text); white on accent 5.36 */
--mute: #8c9098;   /* footer and sub line; 6.22:1 on bg, 5.03 on navy */
tile fill: linear-gradient(160deg, #06285c, #00132f)   /* ink 14.3 / 18.5, glow 6.29 / 8.14 */
```

Contrast was computed by hand with the WCAG formula (node and python were not allowed to run in this session); `hyperframes validate` independently reported "10 text elements pass WCAG AA". Blue-only world: no warm hue anywhere, white for type. The profile's `mute` is `rgba(255,255,255,0.55)`: on `--bg` it blends to `#8c9098`, so the build uses that solid colour (a translucent colour makes the 0.9-opacity acceptance rule ambiguous). Never put `--accent` text on the void.

Material: tiles radius 14, 1 px border `rgba(79,179,255,0.45)`; focus ring 3 px solid white, radius 19, `box-shadow: 0 0 28px 6px rgba(79,179,255,0.7)`; hero rim 3 px `--glow` stroke with `drop-shadow(0 0 14px rgba(79,179,255,0.8))`.

## 2. Fonts (3 local files; the profile's Outfit and Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline (light), tile titles, labels, numerals, chip, strip, footer | Outfit 300 / 600, Be Vietnam Pro 500 | `SegUIVar.ttf`, weight axis 300-700 (`font-weight: 300 700` in @font-face): headline 300, tile titles and labels 600, strip 500 | all tone marks rendered correctly in snapshots (ắ, ề, ổ, ạ, ữ, ư, đ seen on screen) |
| Index tags "01".."04" | none | `CascadiaMono.ttf` 500 | digits only |
| Never | | `segoepr.ttf` | lacks nearly all Vietnamese letters |
| Not used | | `cambriai.ttf` | no serif line in this style |

Light weight 300 at 78 px stays legible on the navy gradient (ink 16-20:1). Do not use 300 below 60 px.

### Type scale (1080 x 1920, px, as built)

| Token | Font / size / line | Notes |
|---|---|---|
| `.hd` headline | Seg 300, 78 / 1.16, +0.02em | max 2 lines, centred; key word `<b>` weight 600 in `--glow` |
| chip "MINH HOẠ" | Seg 600, 32, +0.14em | pill, 2 px glow border, fill `rgba(0,31,77,0.85)` |
| tile label `.lb` | Seg 600, 32, +0.10em, `--glow` | uppercase |
| tile numeral `.nm i` | Seg 300, 150 / 1.1, tabular | "449" is about 252 px wide; fits a 440 px tile with 34 px padding |
| numeral unit `.nm u` | Seg 600, 50 | "USD", "TB" on the numeral baseline |
| game tile title `.tt` | Seg 600, 32 | longest title "Hành động" fits 210 px tile |
| game tile index `.ix` | Casc 500, 30 | `--glow` |
| strip | Seg 500, 38 | one line, 900 x 92 pill |
| sub line | Seg 400, 40, +0.04em, `--mute` | beat 1 only |
| footer | Seg 400, 28, `--mute` | the ONE line under 30 px |

Nothing else is under 30 px (smallest in-tile text is 30).

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  platform UI: empty
y 176  -240  chip "MINH HOẠ"
y 236  -410  headline (beat 1: 2 lines, beats 2-3: 1 line, y 236-330)
y 395  -745  hero console at scale 0.5 (beats 2-3), centre (540, 570)
y 520  -1220 hero console at scale 1 (beat 1), centre (540, 870)
y 840  -1140 beat 2 row: two tiles 440 x 300, x 80 and 560 (gap 40)
y 840  -1240 beat 3 row: four tiles 210 x 400, x 93 + i*228 (gap 18)
y 1296 -1388 summary strip (beat 3), x 90-990
y 1310       sub line (beat 1)
y 1436 -1464 footer
y 1480 -1920 empty (platform UI)
```

Hero position is one element tweened between slots (match-move), never rebuilt: `#heroPos` x 360, y 520 -> 220, scale 1 -> 0.5. Rows are children of absolute boxes; their rotateY (-12 deg, perspective 1600) turns the whole box, so the near edge grows about 6% and the far edge shrinks about 6%: the 894 px row stays inside 996 px.

## 4. Layers, back to front

`#bg` (one radial gradient navy to void, 900 x 1100 ellipse at 50% 40%) -> `#rays` (2 skewed 260 x 2300 gradient bars, rotate 14 deg, opacity peak 0.16, drift x +40 over 12 s) -> `#pts` (60 seeded particles, 3 depths) -> `#heroPos > #heroCam > #heroFloat` (bloom, base glow, SVG console) -> chip -> headlines -> rows (tiles, ring, ripples) -> strip -> footer. No flash layer and no fade layer (frame 0 already shows chip, footer, particles and rays; the last frame is the full composition).

Three wrappers on the hero, one job each, so tweens never fight: `#heroPos` position and scale, `#heroCam` crane (y 80 -> 0, rotateX 8 -> 0, 3 s `power2.inOut`) and the shake, `#heroFloat` the bob (y 0 -> -8, `sine.inOut`, yoyo).

## 5. Components

- **Hero console (CSS/SVG, no image).** viewBox 360 x 700: two mirrored shell paths (`M164 8 C86 8 32 60 28 150 L28 560 C32 650 86 692 164 692 Z` and its mirror at x 196) with a white-to-pale-blue horizontal gradient, a 32 px black core between them, a 6 x 440 glow LED line. A generic slab: no logo, no port art.
- **Rim**: the two shell outlines with `pathLength=1`, `stroke-dasharray 1`, offset 1 -> 0.
- **Bloom**: ONE 1020 x 1000 radial-gradient div behind the hero (no `filter: blur`), opacity 1 -> 0.55.
- **Particle**: 3 to 13 px dot `#bfe4ff` with `box-shadow: 0 0 10px 3px rgba(79,179,255,0.55)`.
- **Stat tile** (beat 2): 440 x 300; label top-left at (34, 30), numeral at (34, 92). Never dim a tile (see trap 6).
- **Game tile** (beat 3): 210 x 400; art 208 x 250 on top (an inline SVG of 3 to 4 flat blue/white shapes: stripes, mountains, rings, ball), title at y 276, index at y 330.
- **Focus ring**: a 222 x 412 (or 452 x 312) box at tile -6 px, scale 1.08; the focused tile scales to 1.08 with `power3.out` 0.3 s, the old one back to 1.
- **Ripple**: 140 px circle, 3 px `--glow` border, scale 0.2 -> 2.4, opacity 0.9 -> 0 in 0.6 s, centred on the tile art or numeral.
- **Strip**: pill with `--navy` fill at 0.95 alpha (kept above 0.9), 2 px glow border; text with `--glow` dots between facts.
- **Chip and footer**: "MINH HOẠ" from frame 0 to the end, plus the footer line "Minh hoạ · nội dung giả định, không phải sản phẩm thật".

## 6. Motion language

Easing as built: entrances `expo.out` (headline 0.8-0.9 s) and `power3.out` (tiles 0.7 s); camera and hero moves `power3.inOut` 0.9 s or `power2.inOut` 3 s; exits `power2.in` 0.25-0.3 s (about 40% of the entrance, shorter than the 60% rule on purpose: ghosts under 0.15 s). Hero and particle drifts use `ease: "none"`; the bob `sine.inOut`.

Depth: particles move at three speeds (far 25-45 px/s, mid 60-90, near 130-170), rays at 40 px per 12 s, hero bob 8 px: parallax about 0.3 : 1 : 1.6.

Something visibly changes every 1 to 3.4 s. Nothing is ever frozen: particles drift all 12 s, the hero bobs until 11.0 s, the row drifts y -10 and rotateY -12 -> -9, the ring breathes 1.08 <-> 1.1 in the last 1.4 s.

Transitions in this build: (1) perspective glide: the old row exits `x -260` with opacity 0 in 0.28 s while the new row enters `x 320 -> 0` with 0.07 s stagger; (2) match-move of the hero between slots; (3) particle layer swell (scale 1 -> 1.05 -> 1, 0.7 s) on each cut. The profile's particle dissolve and light-edge reveal between scenes were NOT built; the light-edge reveal is used once, for the hero in beat 1.

## 7. Scene recipes (S = beat start; sample is 12.0 s, 3 beats)

### R1 Reveal (0 - 3.5 s)
0.05-1.35 rim traces the silhouette (`power2.inOut`) while the crane rises; headline lines rise `y 50 -> 0` with 0.14 s stagger from 0.5. 1.15 shells fill (0.7 s), bloom to 1, base glow, a skewed white sweep crosses the shell (0.9 s, clipped to the silhouette), a 6-frame 3 px shake at 1.2 (0.035 s steps), LED at 1.7. Sub line "Giá · Dung lượng · Game ra mắt" at 1.9. Hold 2.7-3.3 with bob and drift. Exit: sub 3.3, headline 3.4 (0.3 s).

### R2 Price and capacity (3.5 - 7.2 s)
3.5 hero shrinks to the top slot (0.9 s). Headline at 3.85. Two tiles glide in at 4.1 (stagger 0.07). Price counter 0 -> 449 from 4.35, `power3.out` 0.75 s, final at 5.10. Ring and ripple on the price tile at 5.3; ring moves to storage at 6.3, storage numeral pops 1.12 -> 1 at 6.5 with a ripple. Exit at 7.2: row `x -260` and headline up, 0.25-0.28 s.

### R3 Lineup (7.2 - 12.0 s)
Headline 7.45, four tiles glide in from 7.45 (finished 8.36). Ring appears at 8.35 and steps to tile 1 (8.5), 2 (9.1), 3 (9.7), 4 (10.3): ring and tile scale start 0.15 s before each step, with a ripple. Strip rises at 9.7 (0.55 s). From 10.3 to 12.0 the frame holds the full composition: headline, hero, 4 tiles with the ring on tile 4, strip, footer. No fade-out.

## 8. Captions
NOT exercised in this build (silent). ASSUMED from the profile: navy pill `rgba(0,31,77,0.85)` or darker, radius 20, 42 px Seg 500, current word `--glow` (8.75:1 on bg). Captions would use the band y 1370-1480 (nothing from this build lives there except the strip at 1296-1388: move the strip up 100 px when captions are added).

## 9. Sound
NOT exercised (no voice, no music, no SFX). ASSUMED from the profile: 90-120 BPM hybrid orchestral/electronic, sub boom on the reveal at 1.15 s, ticks on ring steps, whoosh on row glides. The 6-frame shake and the bloom are timed to 1.15-1.2 s so a boom can land there.

## 10. Images (agy)
Not used. `motion_tools.py image` was attempted for a hero photo and was blocked by the permission layer in this session, so the hero is vector. The vector slab reads clearly as a console at 0.5 scale; a generated photo would add realism but risks logos and fake ports. If used later: ask for "deep navy void, glossy white and black slab, blue rim light, no text, no logos", expect a navy ground (not black), blend with a radial mask, and never place it near numbers.

## 11. Must not

- No warm colour, no emoji, no gradient on text, no flat bright illustration, no paper or clay texture, no fast jittery cuts.
- Max 80 particles (60 used), seeded `rng`, never `Math.random`.
- No real game art, console shape, logo, price or spec; invented content carries "Minh hoạ" for the whole video.
- No `--accent` as text; no text under 30 px except one footer line; nothing below y 1480.
- No dimmed tiles (opacity under 0.9) on a held frame; no counter caught mid-count.
- `segoepr.ttf` never; no `filter: blur` layers (the bloom is a gradient).

## 12. Traps seen in real builds (this build, 2026-11-14)

1. **Missing `position: absolute` on a shared class.** The three headlines were stacked in normal flow instead of overlaid: snapshot showed "Máy chơi game / thế hệ mới" at y 75-225 colliding with the chip at y 176, and `inspect` reported `canvas_overflow #h1 ... overflowed top 47px`. Fix: `.hd { position: absolute }` (one CSS line). Always read the first inspect run for "overflowed top" before trusting the layout.
2. **inspect false alarms.** 13 warnings and 5 infos remained after the fix, all expected: `content_overlap #row2 inside #row3` (both rows share y 840 and exist in the DOM while one is invisible), `canvas_overflow #row2/#row3` (rows start at `x +300`), `container_overflow #fills inside #heroSvg 40-80 px` (the sweep rectangle starts left of the SVG). 0 errors; `validate` passed with no console errors. Mark `#fills` with `data-layout-allow-overflow`; the row warnings are accepted.
3. **Lint `overlapping_gsap_tweens` on `.gt` scale 0.00-0.30 s.** Reported once, false: the selector `.gt` is matched against the stagger tween; each tile's scale tweens never overlap. Left as is (0 errors, 1 warning).
4. **Counter caught mid-count.** In the 2.5 fps contact sheet the frame at 4.4 s showed the price as "334" while the tile was still gliding. No held frame shows it (count ends 5.10 s, 0.75 s long), but the tile enters at 4.1 with the counter starting at 4.35, so for 0.7 s the tile is visible with a partial number. Rule held to: count 0.75 s, finish before the first ring at 5.3.
5. **Ripple inside a rotated row** looks like a faint ellipse, not a circle (the row's rotateY 12 deg squashes it about 2%): invisible at 0.6 s, acceptable; do not rely on a ripple being round.
6. **Dimming the unfocused tiles fails the 90% rule.** The profile says a focused tile scales up, and common console UI dims the others; here the others stay at 100% opacity and only the ring plus scale 1.08 mark focus, so every held frame passes.
7. **Hero at scale 0.5 is small.** At 540 x 350 px of a 1080 frame it is readable but weak after beat 1; the recipe compensates with the persistent glow, the bob and the 0.5 -> 0.53 push over beat 3. If a lead object needs more weight in beats 2-3 use scale 0.6 and push the rows down 60 px (they end at y 1388, strip bottom; room remains to 1480).
8. **Bottom 22% of the frame is empty by rule.** Content spans y 176-1464, so the composition reads top-heavy on a desktop preview; on a phone the platform UI covers y 1480+. Do not "fill" it.
9. **Tooling in this session:** `frame_check.py` needs numpy, which was not installed and could not be installed; the check was done with ffmpeg (`blackdetect`, `freezedetect`) and a 2.5 fps contact sheet. freezedetect found one 0.2 s still segment at 3.23-3.43 s (beat 1 hold; only the particles move, below the detector's threshold). No black frames.
10. **Render:** 11.4 s for 12.0 s of video, 3.8 MB, h264 1080x1920 at 30 fps, silent (no audio stream).
