# Style: art-deco-luxury (9:16 Vietnamese news edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build: heritage and luxury stories with one hero object and few numbers: a perfume, watch or jewellery house relaunching or marking an anniversary of a classic, a heritage boutique opening, a gala or a season lookbook, a centenary of a brand or building. It carries 1-3 numbers well (a year, an anniversary, a short price ladder) and names, quotes and materials better than numbers. Not for dense data (more than ~4 numbers), code, charts with axes, urgent or sad news, enforcement, or anything that needs bright colour. Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the design as built and measured in the first real build (2026-11-11, 57.0 s video `guerlain-shalimar-100-nam`, 6 scenes). Section 12 lists the traps seen in that build with numbers. Where a later section disagrees with an earlier one, the later section wins.

**Clips and screenshots are optional.** This build used none (only agy illustrations, each labelled "MINH HOẠ"). If a later build inserts a clip or page screenshot, the media-first rule of the other owner documents applies (media at least 900 px wide and the largest element).

**Example videos show the visual recipe, not the niche.**

**Status.** Written 2026-11-12 from the first build; not yet reviewed by the owner. Marks: **ASSUMED** = the profile gives no value and this build chose one; **SUBST** = a profile font is not installed and a local one replaces it; **DEVIATION** = knowingly differs from the profile.

A 1920s luxury advertisement on a phone: charcoal ground, champagne-gold foil lines, one stepped-arch "display case" holding the hero object, notched plaques for the facts, a thin double gold border around the whole frame, a sunray field turning slowly behind everything. Energy 2: poised, no bounce, no shake, no flash. Motion is expensive-looking: outlines draw outward from the centre axis, a fan of wedges opens to change scenes, a slow light glint crosses gold type and frames.

## 1. Tokens

```css
:root{
  --bg:#1c1b19;        /* profile bg, main ground */
  --ink:#f3ead6;       /* profile ink: headlines, names     14.38:1 on bg, 12.28:1 on charcoal */
  --accent:#c9a45c;    /* profile accent: gold type, lines   7.33:1 on bg,  6.26:1 on charcoal -> allowed for text of any size */
  --gold-deep:#9c7a3c; /* profile gold-deep: LINES ONLY      4.31:1 on bg, 3.19:1 on cream -> never text */
  --cream:#efe5cf;     /* profile cream: caption text, cream ground; 13.75:1 under --bg text, 11.74:1 under --charcoal text */
  --charcoal:#2a2825;  /* profile charcoal: price columns, fan wedges, text on cream (11.74:1) */
  --gold-ink:#6e5426;  /* ASSUMED: gold-brown TEXT on cream, 5.67:1 */
  --ray:#3a3327;       /* ASSUMED: sunray field lines (decor only, about 1.3:1, below the frame-check ink threshold on purpose) */
}
```
Contrast computed with the WCAG relative-luminance formula by hand for every pair above (the build machine blocked ad-hoc scripts; see 12.8). Rules: text only in `--ink`, `--accent`, `--cream` on dark grounds; `--charcoal` or `--gold-ink` on cream. `--gold-deep` is a line colour. No other hue anywhere, including the generated images (prompts name the hexes and "no other colours"). All tokens at opacity 1; depth comes from nested frames, never from transparency.

## 2. Fonts (glyph test: a HyperFrames snapshot of every Vietnamese capital and lower-case vowel with a Courier fallback; a missing glyph shows in Courier)

| File | Result | Role |
|---|---|---|
| `SegUIVar.ttf` | all present (weights 300 and 600 tested) | SUBST for Bodoni Moda / Poiret One / Josefin Sans. Headlines: weight 300, ALL CAPS, `letter-spacing:.12em` (reads as a thin deco display face). Kicker 600 caps +.22em. Body/plaque labels 500-600. Captions 500. Prices 600. |
| `cambriai.ttf` | all present | SUBST for the didone serif voice: product names (`L'Essence`, `Jicky`), people's names, years in the medallion (230 px), the quote card, the closing line. Italic only. |
| `CascadiaMono.ttf` | all present | not used (a mono face breaks the 1920s look) |
| `segoepr.ttf` | **only đ and € render; every other test letter fell back** | never use |

No didone (Bodoni-class) face is installed, so the profile's "high-contrast didone headlines 140-220 px" are not reachable; the thin tracked caps plus Cambria Italic were the closest look and read as luxury on the phone. Line-height 1.2 for caps with stacked marks (Ể, Ẩ, Ố sit above the cap height of SegUI 300).

### Type scale (1080 x 1920, as built)

| Token | Font | Size | Notes |
|---|---|---|---|
| `.kick` | Seg 600 caps +.22em (+.12em when long) | 30 | `--accent` (cream scene `--gold-ink`), 12 px rotated-square diamonds left and right |
| `.hl` cover | Seg 300 caps +.12em | 116 | one word ("SHALIMAR"), y 208 |
| `.hl` scene | Seg 300 caps +.12em | 72 (84 on the cream scene and samples) | 2 lines, explicit `<br>`, y 206 |
| `.it` subline | Cambria Italic | 80 (cover), 64 (samples), 52 (cream) | `--accent` |
| medallion year | Cambria Italic | 230 | `--accent` |
| names | Cambria Italic | 46-80 | `--ink` or `--accent` |
| plaque label `.t1` | Seg 600 caps +.14em | 30 | `--accent` |
| plaque value `.t2` | Cambria Italic | 48-50 | `--ink` |
| price | Seg 600 | 72 | `--cream` on charcoal column |
| size label | Seg 600 | 44 | `--charcoal` on cream |
| source line `.foot` | Seg 500 | 30 | `--accent`, y 1304 |
| tag "MINH HOẠ" | Seg 600 caps +.12em | 30 | cream on `--bg` chip |
| caption | Seg 500 +.02em | 46 / 1.3 | see section 8 |

No text below 30 px anywhere.

## 3. Safe areas and grid (1080 x 1920, as built)

```
y 28/40      double gold border (2 px --gold-deep outer, 1.5 px --accent inner), stepped corner marks
y 166-205    kicker
y 206-400    headline (2 lines of 72 px) or 116 px cover word + 80 px italic at y 352
y 410-1290   BODY: hero frame + plaques; lowest content edge 1290 in every scene (1306 on the cream scene's size labels)
y 1304-1340  source line (one line, 30 px)
y 1360       footer rule: 3 px --accent + 1 px --gold-deep, centred 28 px diamond
y 1360-1920  footer band, solid --bg (captions at top 1396, 1-2 lines -> ends <= 1515); nothing else
x            centre axis 540; side margin 70 (plaques) to 250 (arches); everything symmetric about x 540
```
Every layout is bilaterally symmetric. Two-plaque rows: 455 x 144-182 at x 70 and x 555 (gap 30) or 420 x 146 at x 70 / x 590 with a 56 px gold diamond "+" between.

## 4. Layers, back to front

`#bg` flat `--bg` -> `#rays` (64 solid lines from (540, 860), every 4th 3 px, others 1.5 px, plus two rings r 420 / 640, colour `--ray`; rotates 0 -> 9 deg and scales 1 -> 1.04 linearly over the whole video) -> scene sections (each with a `.cam` wrapper, origin 540 860) -> `#fan` (transition wedges) -> `#footer` band -> `#frame` (double border, foreground, static) -> `#caps`. No flash layer, no shake, no fade-to-black: the first and last frames are full compositions.

## 5. Components

- **Stepped-arch display case** (signature): a clip-path polygon of 16 points on the unit box `[0,1] [0,.2] [.08,.2] [.08,.11] [.2,.11] [.2,.045] [.34,.045] [.34,0] [.66,0] ... [1,.2] [1,1]`, holding a generated image (`object-fit: cover`). Outline = two SVG paths per ring (left half and mirrored right half, both starting at the top centre and ending at the bottom centre) so the frame can draw outward symmetrically; outer ring 3 px `--accent` inset 1.5, inner ring 1.5 px `--gold-deep` inset 14. Sizes used: 640 x 800 (cover), 540 x 660, 580 x 690, 600 x 610 (samples). The same polygon with `--bg` fill and text inside is the **arch medallion** (the "Jicky 1889" card, 580 x 520).
- **Notched plaque**: `--bg` fill, clip-path with 22 px square notches at the corners, outer path 2.5 px `--accent`, inner path 1.5 px `--gold-deep` inset 10. Holds one label (`.t1`) and one value (`.t2`), or a quote. A `.ring` (3 px `--accent` rectangle 8 px outside) marks the plaque being spoken.
- **Medallion**: a notched plaque 740 x 560 with the year 230 px Cambria, a 300 x 2 px `--gold-deep` rule, the name 66 px.
- **Stepped price column** (cream scene): `--charcoal` column 240 px wide with a two-step stepped top (steps 24 / 60 px wide, 30 px high), 3 px `--accent` outline and a 1.5 px `--gold-deep` inner line; height on ONE common scale (4.2 px per euro: 86 -> 361 px, 120 -> 504 px, 158 -> 664 px) from a 3 px `--gold-deep` base line at y 1240; price inside the top, size label under the base.
- **Drop + connector**: an SVG teardrop 80 x 112 in `--accent`, a 2 px vertical `--accent` line drawing down into the medallion.
- **Glint**: a baked PNG (`sheen.png`, 260 x 2400, ffmpeg `geq` gaussian alpha, peak alpha 150, warm white #f6e6be) rotated 18 deg, inside an `overflow:hidden` layer with `mix-blend-mode: screen`, swept left to right.
- **Tag "MINH HOẠ"** on every generated image, inside the arch near its top-right step.
- **Source line** `Nguồn: <publisher>, <date>` per scene, or the publisher and date in the kicker when the body needs y 1304.

## 6. Motion language

Energy 2 (profile). Eases: `expo.inOut` (outline draws, fan, iris), `expo.out` (rules, settles), `power3.out` (plaque rises 18-24 px), `power2.inOut` (glints), `sine.inOut` (drop float), `none` (camera drift, rays). No `back`, no `elastic`, no bounce, no shake, no flash, no counters (numbers are final text; see 12.4).

| Verb | Recipe as built |
|---|---|
| symmetric-draw (profile) | `strokeDashoffset 1 -> 0` on both halves at once, 0.8-1.1 s `expo.inOut`, starting 0.1-0.3 s before or after the scene start; the content inside is already visible, the line is the accent |
| fan-unfold (profile) | 24 wedges (alternating `--charcoal` / `--bg`, 3 px `--accent` edges) from (540, 860), R 1500: in `scale 0 -> 1.12, rotation -40 -> 0` 0.32 s `expo.in` ending on the cut; scenes swap on the cut; out `scale 1.12 -> 0, rotation 0 -> 40` 0.34 s `expo.out`; the incoming `.cam` settles 1.04 -> 1 over 0.7 s `expo.out` |
| iris-step (profile) | the incoming section, OPAQUE `--bg` during the wipe, is clipped by the stepped-arch polygon scaled around (540, 860) from 0 to 1.25 x (1400 x 2600 px) in 0.45 s `expo.inOut`, ending on the cut; outgoing hidden on the cut; clip removed 0.01 s later |
| draw cut | outgoing `autoAlpha 1 -> 0` 0.15 s ending on the cut, incoming 0 -> 1 0.2 s from cut - 0.08, a gold rule under the headline grows `scaleX 0 -> 1` 0.7 s `expo.out` from the axis |
| internal cut-in (scene > 8 s) | part A out `autoAlpha` + scale 1 -> 0.97 over 0.18 s; part B in scale 1.03 -> 1 over 0.3 s from tB - 0.06 (overlap 0.12 s) |
| glint (profile "slow glint") | 0.9-1.3 s sweep, on the headline about 0.5 s after a scene opens and on the plaque or frame whose word is spoken; one every 2-4 s |
| ring walk | `.ring` opacity 0 -> 1 with scale 1.04 -> 1 in 0.25 s at W(word) - 0.1; previous ring out 0.2 s |
| camera | one family per scene, never the same in neighbours: push-in 1 -> 1.035 (s1), static (s2), image pan yPercent 2 -> -3 (s3), push-in 1 -> 1.03 with image 1.08 -> 1 (s4), locked (s5), pull-out 1.05 -> 1 (s6) |
| price emphasis | the size label under the spoken column turns `--gold-ink` and scales 1.12 (0.3 s) until the next size is spoken |

Pacing: scenes 6.4-14.7 s; every framing changes within 8 s (the 14.7 s scene has a cut-in at its 9 s mark); something visibly moves every 2-4 s (glint, ring, drop float, rays).

## 7. Scene recipes (S = scene start; W() = estimated word onset; all starts clamped >= 0)

**R1 Cover / hook (s1, 6.4 s).** Kicker, one-word product name 116 px, italic subline 80 px, stepped arch 640 x 800 at (220, 486) with the hero illustration, a plaque 500 x 90 at (290, 1196) overlapping the arch base ("1925 · 100 NĂM"). Frame 0 is the finished composition; motion: push-in, image 1 -> 1.06, glints on the name (0.5 s), the arch (1.6 s), the plaque (on the product word) and the name again before the cut. Exit: fan.

**R2 Origin medallion + quote plaque (s2 part A).** Headline 2 lines, medallion 740 x 560 at y 432 (year, rule, creator), quote plaque 860 x 268 at y 1022 (Cambria 52 px in quotes, attribution 32 px). Both rise 18 px and their outlines draw in the first 0.9 s; ring on the medallion at the year, then on the quote at its first word.

**R3 Cause -> object diagram (s2 part B, cut-in).** Drop (y 440) falls 60 px into place, label "vài giọt ethylvanillin" (y 580), a connector line draws down into an arch medallion 580 x 520 at y 770 (name 120 px, year 96 px, result line 46 px that rises on its spoken word). Drop floats 10 px until the cut.

**R4 Display case + two plaques (s3).** Arch 540 x 660 at (270, 420) with the detail image (pan), two plaques 455 x 182 at y 1108; ring walks from left to right on the two spoken names. Exit: draw cut.

**R5 Person + formula (s4).** Gold rule under the headline, name plate (Cambria 80 px gold, role 34 px ink), a notched image frame 480 x 470 at y 646, formula row at y 1144: plaque, gold diamond "+", plaque. Ring walk on the spoken ingredients. Exit: fan.

**R6 Price ladder on cream (s5).** The only cream scene (mixed palette): paper texture, its own inner double border in `--gold-deep`, kicker with publisher and date, headline 84 px charcoal, italic product name in `--gold-ink`, three stepped columns growing `scaleY 0 -> 1` from the base (0.55 s `power3.out`, 0.1 s stagger, all done by S + 0.75; they grow under the opening fan), prices final from the first frame, size labels emphasised on their spoken words. Exit: iris-step.

**R7 Closing bookend (s6 + 1.0 s tail).** The cover layout again (bookend), a smaller arch 580 x 690, a wide plaque 860 x 94 with the closing line in Cambria 50 px, kicker with the launch channel and date. Slow pull-out, symmetric redraw of the arch, glints; the last 1.5 s hold the full composition (no fade).

## 8. Captions

- Profile: "No pill; cream text over a charcoal fade, current word gold; bottom band." As built: the band is the solid footer (`--bg`, from y 1360) under a gold double rule, which is the charcoal fade made opaque.
- Seg 500 46 px / 1.3, `letter-spacing:.02em`, `--cream` (13.75:1), current word `--accent` (7.33:1), centred, width 900, top 1396, 1-2 lines.
- Chunks: spoken words split after punctuation once a chunk has >= 3 words, hard cap 7 words, a trailing chunk under 3 words merges into the previous one; never across a scene end. Visibility and highlight only with `tl.set` (no fades: no half states).
- Text = the spoken text (numbers in words); digits live in the graphics.
- Word times are ESTIMATED (character share of each scene's speech, same formula as `motion_tools.py`); computed inside the page from `{start, speech}` per scene plus the scene text, so no build script is needed.

## 9. Sound

Voice only (VieNeu "Hải Đăng", 6 scenes joined with 0.35 s gaps), no music, no SFX. The profile's jazz-age swing / string quartet 84-104 BPM and glass-chime SFX were not available. Mux: -15.6 LUFS integrated, peak -4.2 dBFS.

## 10. Images (agy)

- Recipe that worked first time for all five images (57-101 s each, 768 x 1376): "A 1920s Art Deco advertisement illustration: <one object> ... standing on a stepped plinth, centred, strict bilateral symmetry, champagne gold sunray lines radiating behind it, flat charcoal background #1c1b19, gold foil linework #c9a45c, cream highlights #efe5cf, no other colours, generous empty space, no text, no logo."
- Objects that worked: a faceted perfume bottle; a fan-shaped crystal stopper ("no blue" kept it gold); a bundle of vanilla pods tied with a gold ribbon inside a stepped frame; a rectangular wristwatch with baton marks ("no numbers, no letters, no brand" kept the dial clean); a faceless flapper-gown silhouette under a stepped arch ("faceless and featureless head shape, not a real person").
- The images arrive with their own deco border; crop it away with ffmpeg so only the subject and rays sit in the arch (bottle `crop=600:760:84:250`, stopper `crop=720:960:24:100`, vanilla `crop=600:640:84:320`, watch `crop=640:650:64:300`, gown `crop=680:690:44:250`), re-encode `-q:v 3` (72-156 KB each).
- The image ground (about #22211d) is close enough to `--bg` that no keying is needed inside the arch.
- Every generated image is decoration, never evidence of the real product: label "MINH HOẠ" on screen.

## 11. Must not

- No hue outside gold / charcoal / cream (also in images); no neon, no glass, no glow, no gradients on text.
- No bounce, elastic, back, shake, flash, whip or smear; no hard cut without a fan, iris or draw.
- No asymmetric layout; no rounded UI cards (corners are notched or stepped).
- No transparency as a style (every held element at opacity 1); no text under 30 px.
- No counters; no bar that does not start at the base line; columns on one scale.
- No name, number or claim that the opened page does not state word for word in substance (12.5).
- No `segoepr.ttf`; no Cascadia Mono in this style.
- No call to like/share/subscribe, no prediction, no advice, no hype.

## 12. Traps seen in real builds (first build, 2026-11-11, measured)

1. **Iris-step showed both scenes at once.** The incoming section was transparent, so during the 0.45 s wipe the outgoing headline showed through the incoming one ("TỪ MỘT CHAI" over "CẢM HỨNG"). Fix: `backgroundColor:#1c1b19` on the incoming section for the wipe, back to transparent 0.01 s after the cut.
2. **...and then hid the captions.** The first fix also set `zIndex:2` on the incoming section, which lifted it over the footer, border and captions for 0.45 s (frames at 19.9-20.1 s showed no caption and no frame). Fix: no z-index; the DOM order (later scenes later) already stacks it correctly.
3. **Emphasis that breaks the chart.** Lifting the spoken price column 14 px (`y:-14`) opened a gap above the base line, so the bar no longer started at zero. Fix: emphasise the size label under the column instead (colour `--gold-ink`, scale 1.12).
4. **No counters needed.** With 3 prices and 2 years, numbers as final text from the first visible frame avoided every mid-count frame; columns grow (0.55 s) instead of numbers counting.
5. **Facts gate caught three over-reaches after re-opening the pages.** (a) "Raymond Guerlain": the page says only "his nephew Raymond" -> on screen and in voice "người cháu Raymond". (b) "Jicky ra đời năm 1889": the page says "a bottle of Jicky 1889, giving birth to Shalimar" -> "một chai Jicky 1889, và Shalimar ra đời". (c) Prices: the page gives no market; the launches were "unveiled in global travel retail this September" -> the closing says "ra mắt ở kênh bán lẻ du lịch từ tháng 9.2025". All three needed a re-voice (55.99 s instead of 54.70 s). Re-open the pages before locking the script, not after.
6. **Voice length.** First draft (about 230 words, including a spoken publisher name and one extra sentence) = 58.59 s; final 221 words, 6 scenes, gap 0.35 = 55.99 s (3.95 words/s including gaps); video = voice + 1.0 s tail = 57.0 s. Aim at 200-220 words.
7. **Caption orphan.** A 6-word cap split "Một trăm năm sau ngày ra / đời, Shalimar ...". Fix: cap 7 words and split at punctuation first.
8. **Locked-down machine.** Only `motion_tools.py`, `frame_check.py`, `npx hyperframes`, ffmpeg and simple file commands ran without approval; `python3 <own script>` and `node <own script>` needed approval. Glyph coverage was checked with a HyperFrames test page (each font with a Courier fallback) and `snapshot`; contrast by hand with the WCAG formula; caption timing computed inside the page.
9. **`snapshot -o` with a relative path resolved outside the project** (`../../work/...` from `samples/t103` wrote to `~/work/`). Always pass absolute paths to `-o`.
10. **Tool facts (hyperframes 0.7.26).** lint 0 errors / 4 warnings (overlap warnings for `#fan` and `#drop` are tweens at different times; file size); validate 0 errors, 3 contrast warnings for the "+" glyph (1.98:1 reported; real pair `--bg` on `--accent` = 7.33:1: false positive, the glyph sits on a sibling diamond); inspect 0 errors, 588 `container_overflow` warnings from the 64 sunray lines and footer diamond even with `data-layout-allow-overflow` on the SVG (accepted, decorative). Render about 33 s for 57 s; silent 20.8 MB at standard quality (fine gold lines compress poorly), final 15.0 MB.
11. **Frame check.** `frame_check.py` on silent and final: 114 frames, 0 BLANK, 0 TOPHEAVY. Transition strips (10 fps, 0.6 s around each cut) showed no ghost after fixes 1-2: the fan covers the swap, the draw cut overlaps 0.08 s.
12. **Arch outlines draw after the content appears.** In s2 part B the medallion text is visible 0.2-0.3 s before its outline finishes; this reads as intended (content first, ornament second) and is not a "headline only" frame.
13. **Freshness.** 16 searches found no relaunch of a 1920s fragrance in the last 48 h; the newest fitting story (Shalimar L'Essence for Shalimar's centenary; pages dated 24.09.2025 and 13.10.2025) is about 13-14 months old and flagged in the manifest.
14. **Not ear-checked.** VieNeu default readings (no respelling) of Shalimar, Guerlain, Jacques, L'Essence, Jicky, ethylvanillin, Raymond, Art Deco, Baccarat, Delphine Jelk, Madagascar: listed in `ear-check.txt` for a native listener's ear.
