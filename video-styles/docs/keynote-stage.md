# Style: keynote-stage (9:16 edition, first build, demo only)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY, observed in this build).** One headline number that falls or rises, followed by 2-3 plain consequences and one small comparison of 3 values (rate drops, price changes, a milestone crossed, a launch claim). It fits a story that is a sequence of big confident claims, one idea per slide. It does not fit stories with more than 4 numbers, dense tables, quotes, bad-news or enforcement stories (the black stage and the gradient read as celebration). Tier 2 never widens tier 1.

**Reading order.** One pass, sections 1 to 12. Section 13 holds the traps from this build.

**Status.** Written 2026-11-14 from ONE 12.0 s silent sample (`sample-t001.mp4`, topic shape t001, Jev fit 0.73). **Voice-over, captions, word timing, sound and music were NOT exercised** (demo build): sections 8 and 9 are the profile's values, marked ASSUMED, and untested. Illustrative content only, labelled "Minh hoạ" on screen. Not merged into the skill folder.

Profile: `skill/references/styles/profiles/keynote-stage.yaml` (energy 2, dark, brand-inspired). Black stage, one giant gradient number, a magic-move into the next slide's slot, bullets that build one by one, a three-bar chart. Format 1080 x 1920, 30 fps.
Marks: **ASSUMED** = the profile gives no value and this build invented one. **SUBST** = a named font is not installed. **DEVIATION** = knowingly differs from the profile.
SUBST: Inter and Be Vietnam Pro are not installed; `SegUIVar.ttf` replaces both.
DEVIATION 1: profile margin 160 px; 9:16 uses 120 px (840 px content width) because the giant number and bullets need the width.
DEVIATION 2: no `push-left`, no `dissolve` beyond a 0.3 s fade: a 12 s demo has only 3 slides.

## 1. Tokens

```css
:root{
  --bg:#000000;     /* profile bg */
  --ink:#ffffff;    /* 21.0:1 on bg */
  --mute:#a3a3a3;   /* ASSUMED solid grey instead of the profile's rgba(255,255,255,.5): 8.3:1 on bg */
  --bar:#3a3a3a;    /* ASSUMED, fill only (non-text) */
  --g1:#ff6b3d; --g2:#b44cff; --g3:#3d8bff; /* profile gradient, 100deg, hero only */
  --accent:#f5821f; /* profile accent; NOT used in this build */
}
```
Measured with the WCAG formula by hand (the scripted measurement was blocked in this session; values are within about 0.1): ink 21.0, mute #a3a3a3 8.3, g1 7.4, g2 5.4, g3 6.3, accent 7.7, profile rgba(255,255,255,.5) = #808080 equivalent 5.3. `hyperframes validate` reported "5 text elements pass WCAG AA". Rules: text uses only `--ink` and `--mute`; the gradient is for exactly one element per slide; `--bar` is a fill, never text. Never use opacity below 0.9 on held text: take the softer look from `--mute` (a solid colour), not from `opacity`.

## 2. Fonts

| File | Role |
|---|---|
| `SegUIVar.ttf` | everything read: numbers 700, titles 600, bullets and labels 500. SUBST for Inter. |
| `CascadiaMono.ttf` | the footer "Minh hoạ" line (26 px) and the axis note (30 px) |
| `cambriai.ttf` | copied into the project, unused (no quote in this style) |
| `segoepr.ttf` | never used: lacks Vietnamese letters |

Vietnamese diacritics check: the fontTools glyph test was NOT run (the tool call was blocked in this session). Instead every on-screen string was checked by eye on the 1080 x 1920 snapshots and the rendered video: all of `ã ấ ầ ề ạ ế ộ ớ ơ ư đ ă â ê ô ữ ặ` that appear rendered as real letters, with no fallback boxes. Run the glyph test before reusing the font for new words. Gradient text (`background-clip:text`) renders correctly with these glyphs, including the `,` and `%`.

### Type scale (1080 x 1920, px)

| Role | Size / line / weight | Note |
|---|---|---|
| Hero number | 330 / 330 / 700, tracking -0.045em | slide 1; later scaled to 0.42 (139 px) and 0.30 (99 px) |
| Slide title | 68 / 80 / 600 (slide 1), 64 / 76 / 600 (chart) | profile says 72; 64-68 fits 2 lines in 840 px |
| Sub line | 48 / 60 / 500 | |
| Bullet | 46 / 58 / 500, 56 px indent, 16 px white dot | profile body is 36; 46 is readable on a phone |
| Bar label | 40 / 48 / 500, `--mute` | |
| Bar value | 64 / 72 / 700 | |
| Axis note | 30 / 38 mono | smallest text except footer |
| Footer | 26 / 34 mono, `--mute` | the only text under 30 px |

## 3. Safe areas and grid (1080 x 1920)

- Side margin 120 px, content width 840 px. Top: nothing above y 110. Bottom: footer at y 1790; nothing else below y 1560.
- Slide 1: title y 250-410, hero box y 640-970 (centred), sub line y 1170.
- Slide 2: hero at x 120, y 110 (scaled 0.42, ends about y 250), bullets at y 720 / 900 / 1080 (step 180).
- Slide 3: title y 300, rows at label y 760 / 1020 / 1280, bar 72 px high 56 px under its label, axis note y 1560.
- Bar scale: 437 px per percentage point from a 5 % baseline (6.6 = 700 px, 6.2 = 525, 5.9 = 394), always with the written note "Trục bắt đầu từ 5%".

## 4. Layers, back to front

1. `#root` black stage.
2. `#spot`: baked spotlight PNG (1080 x 1920, centre y 820, peak luminance 70/255 = 27 %, power 1.6 falloff), made once with ffmpeg `geq`, drifting up 40 px over 12 s (`ease:"none"`): the only motion on a held frame in the first slide.
3. Content: titles, hero, bullets, bars, values.
4. Footer "Minh hoạ" line, always visible, never animated.

## 5. Components

- **Hero number**: one element, `background-clip:text` gradient, `transform-origin:0 0`, positioned only with `x`, `y`, `xPercent` and `scale` (never `left`/`font-size` tweens). It is the slide 1 centre, the slide 2 corner label and the slide 3 value of the winning bar: the same DOM node.
- **Bullet**: white 16 px dot plus 46 px text, built one at a time.
- **Bar row**: mute label, 72 px bar (radius 10) that grows from the left (`scaleX`), value to its right. Winner bar white `#fff`, other bars `--bar`. The gradient lives only on the hero value.
- **Axis note** (mono 30 px) whenever a bar scale does not start at zero.
- **Footer**: "Minh hoạ · số liệu giả định, không phải tin thật".

## 6. Motion language

Energy 2: nothing bounces, no shake, no flash, no beat reaction. All eases from `power2` / `power3`.

| Move | Values as built |
|---|---|
| Title / sub rise | `y` 30 to 0, opacity 0 to 1, 0.5 s `power3.out` |
| Counter | 6,4 to 5,9, 1.7 s `power3.out`, `snap 0.1`, text set in `onUpdate`; starts 0.6 s, final value 2.3 s, then 1.6 s hold |
| Fade out | 0.3 s `power1.in`, opacity only |
| Magic-move (hero, slide 1 to 2) | `x` 540 to 120, `xPercent` -50 to 0, `y` 640 to 110, `scale` 1 to 0.42, 0.8 s `power2.inOut`; title and sub fade out over the first 0.3 s |
| Bullet build | `y` 24 to 0, opacity, 0.4 s `power2.out`, 0.9 s apart |
| Bars | `scaleX` 0 to 1, 0.8 s `power2.out`, rows 0.3 s apart; value and label 0.4 s |
| Magic-move (hero, slide 2 to 3) | to the end of bar 3: `x` 534, `y` 1322, `scale` 0.30, 0.9 s `power2.inOut` |
| Final settle | scale 0.30 to 0.32 to 0.30 over 0.65 s (micro-motion; no mid-count) |

## 7. Scene recipes (as built, 12.0 s)

- **R1 Single number slide (0 - 3.9 s).** Title (2 lines) rises at 0.1 s, hero fades in at 0.1 s and counts from 6,4 to 5,9 between 0.6 and 2.3 s, sub line "Lần đầu dưới 6% trong năm nay" rises at 2.5 s. Hold to 3.9 s with the spotlight drifting.
- **R2 Build slide (3.9 - 8.3 s).** Title and sub fade out (0.3 s) while the hero magic-moves to the top-left; bullets build at 4.5, 5.4, 6.3 s; hold to 8.3 s.
- **R3 Chart slide (8.3 - 12.0 s).** Bullets fade out 8.3-8.6 s; title rises 8.7 s; three bars grow 8.9 / 9.2 / 9.5 s; the hero travels 9.9-10.8 s and lands as the winning bar's value; the last 1.5 s are a full, still composition.

Rhythm: slide 1 holds 1.6 s after the count, slides 2 and 3 hold 2 s and 1.2 s. Do not add a fourth slide in under 15 s.

## 8. Captions

NOT exercised (demo build, silent). The profile says: no pill, 42 px, centred bottom band, unread words in mute. If captions are used, the bottom band starts at y 1500 for this layout: the axis note (y 1560) and footer (y 1790) would have to move; resolve that in the first voiced build.

## 9. Sound

NOT exercised. Profile values only (warm pad or light electronic bed 80-100 BPM, a soft click on builds at volume 0.2). Silent here.

## 10. Images (agy)

No image was generated: the style needs none. The only asset is the baked spotlight PNG. If an image is ever added (a product or a screenshot), prompt: "Dark studio, single soft spotlight, matte product on black, no text, no logo, no people", and put it in a 1 px hair frame.

## 11. Must not

- No second gradient element on a slide; no gradient on bars (the build keeps the winner bar white).
- No flash, shake, beat pulse, bounce or elastic. No mascot.
- No more than 3 bullets, no dense UI collage, no fast cutting.
- No opacity below 0.9 on a held frame; softness comes from `--mute`.
- No text under 30 px except the single footer line.
- No real brand, price or rate presented as news: this demo uses illustrative numbers only.
- A bar chart with a non-zero baseline always carries a written note of the baseline.

## 12. Acceptance results of this build (12.0 s, 1080 x 1920, 30 fps, 1.0 MB)

`hyperframes lint`: 0 errors, 0 warnings. `validate`: no console errors, 5 text elements pass WCAG AA. `inspect`: 0 layout issues across 9 samples. Probe: h264 1080x1920, 12.0 s, 1.1 MB. The last 1.5 s show the full chart composition; the counter ends at 2.3 s; no held frame uses opacity under 0.9.

## 13. Traps seen in real builds (this build)

1. **Hero parked in the title slot.** In the first version the hero shrank to the top-left at y 240 and the slide 3 title entered at y 300: at 9.0 s the 139 px tall number (y 240-380) overlapped the title (y 300-376) in the snapshot. Fix: park the hero at y 110 (ends about y 250) so the title slot stays free. Check every magic-move's parking slot against the next slide's title slot.
2. **Bar value off the frame.** With 5 % baseline at 520 px per point, the 6,6 bar reached x 900 and its 64 px value ("6,6%", about 150 px wide) would end at 1074 px, 6 px from the edge. Fix: 437 px per point; the value ends near x 990 (margin 90).
3. **Empty second slide.** After the hero moved (3.9-4.7 s) the first bullet only came at 4.9 s: the frame held only a 139 px number for 1.0 s. Fix: bullets at 4.5, 5.4, 6.3 s so the longest sparse stretch is about 0.6 s.
4. **Top-heavy slide 2.** Hero at the top plus bullets at y 720-1140 leaves 600 px of empty black below on the 1920 px frame. Not fixed in this demo; a fuller recipe would add a product or screenshot centre (profile `ui_choreography`) or let the bullets start at y 800.
5. **Tools blocked or missing.** In this session Python helper calls (fontTools glyph test), a node contrast script and `frame_check.py` (numpy missing) could not run. Contrast was hand-calculated, diacritics were checked by eye, and the frame check was replaced by an ffmpeg 2 fps contact sheet read by eye. Install numpy and Pillow for the real `frame_check.py` before a full build.
6. **Gradient needs a `padding-right`.** Gradient text clips the last glyph's edge if the box is tight with negative tracking; the hero carries `padding:0 12px 0 0`.
7. **Scaling a gradient text node.** Scaling with `scale` keeps the gradient aligned (it scales with the box); tweening `font-size` would re-wrap and jitter. Always scale, never resize.
8. **Counter text via `onUpdate` with `snap`.** Works deterministically under seeking; the first frame shows the start value 6,4, so the counter must be at full opacity only after it is set (it is set statically in HTML).
