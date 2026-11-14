# Style: Mid-century retro (9:16 Vietnamese 1950s-ad edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in the t125 build (a toy company releases a build-it-yourself robot kit for kids): cheerful product launches and promos for physical, tangible things (toys, gadgets, kits, appliances, food, events), "how it goes together" in 2 to 4 numbered steps, anything that wants nostalgia and optimism. Not for enforcement, bad news, deaths, dense data or finance dashboards, dark or serious stories, code or terminal scenes (profile `avoid`). Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a 12.0 s silent 1080x1920 sample (`samples/sample-t125.mp4`, 3.6 MB). Voice-over, word timing, captions, music and SFX were NOT exercised (demo-only build); sections 7 and 8 are therefore the profile's rules marked **ASSUMED**, not tested. There was no owner document before this one. Source of values: `styles/profiles/mid-century-retro.yaml`; everything the profile does not give is marked **ASSUMED**.

**One-line look.** A 1950s magazine ad on aged cream stock: slab headlines with a hard ink offset shadow, a hero in a ringed circle, a red starburst sticker, teal and mustard diagonal bands, springy `back.out` / `bounce.out` landings. Energy 4 (profile), but the build used no shake and no flash: the juice is overshoot, bounce and the starburst wipe.

## 1. Tokens

```css
--bg:#f4ead2;      /* aged cream page (profile) */
--ink:#1f1b16;    /* type, outlines, offset shadows        14.4:1 on bg, 15.6:1 on cream, 8.5:1 on mustard */
--cream:#fbf3df;  /* panels, pills, circle rim */
--red:#d93a2b;    /* starburst, key word, number block     3.8:1 on bg, 4.1:1 on cream: LARGE text only (>= 48 px bold) */
--mustard:#f2a71b;/* pills, bands, circle fill             ink on it 8.5:1 */
--teal:#1d8a8a;   /* robot head, bands, circle fill        ink on it 4.2:1, cream on it 3.8:1 */
--orange:#ef6c2f; /* robot body, number block              ink on it 5.6:1, cream on it 2.8:1 (fails as plain text) */
```

Ratios were computed by hand with the WCAG luminance formula (the `motion_tools.py`/`frame_check.py` scripts could not be run in this session, see selfcheck); `hyperframes validate` independently reported "15 text elements pass WCAG AA".

Rules from the build:
- Body text and every small text is `--ink` on cream, mustard or bg. Red text only at >= 130 px (the script tagline, the red headline word); never red at 34-60 px on bg.
- Cream numerals on a coloured block (orange 2.8:1, teal 3.8:1, red 4.1:1) read only because they carry a 4 px ink outline (`-webkit-text-stroke` + `paint-order: stroke fill`). Without the outline they fail. Keep the outline.
- Two or three of red / mustard / teal / orange per scene on cream (profile). Starburst is always red (profile). No gradients; shapes are flat ink with a hard offset shadow `Xpx Ypx 0 ink` (8-12 px).
- Light mode only. Transition layers are flat accent colours (mustard, then red), never black.

## 2. Fonts (3 local files; the profile's Alfa Slab One, Yellowtail and Bebas Neue are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Slab headline | Alfa Slab One 150-240 px | `SegUIVar.ttf` weight 700, uppercase, 130-200 px, `-webkit-text-stroke: 3px ink` + `text-shadow: 5px 6px 0 ink` to fake the wood-type weight | all 36 test letters present (ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ), measured earlier by the same fontTools check as the owner docs; rendered "BỘ", "TỰ LẮP", "BƯỚC", "KHỚP", "TẮC", "CÔNG" correctly in the snapshots |
| Script tagline | Yellowtail 72 px | `cambriai.ttf` (Cambria Italic, 400 only) at 130 px, red | all present; rendered "tự hào khoe!" correctly |
| Labels, pills, panel text | Bebas Neue 44 px | `SegUIVar.ttf` 600-700 at 34-60 px | all present |
| Never | | `segoepr.ttf` | lacks most Vietnamese tone letters |

Honest note: the substitute slab is a sans, so the look is "poster sans with ink outline", not real wood-type. The outline plus offset shadow carries the retro read. If a real slab (Alfa Slab One, OFL) can be installed, swap it in and re-check diacritics: slab fonts with tall caps often clip stacked marks like Ặ and Ắ.

### Type scale (1080 x 1920, px; measured in this build)

| Token | Font | Size | Notes |
|---|---|---|---|
| `.slab` H1 line 1 | Seg 700 caps | 150 (nowrap, 900 px box) | "BỘ ROBOT" is 8 characters: at 186 px it wrapped (see Traps) |
| `.slab` H1 line 2 / hero word | Seg 700 caps, red | 200 | "TỰ LẮP" |
| `.slab` H2 | Seg 700 caps | 130-160 | "3 BƯỚC LẮP" 130, "TỰ TAY LẮP" 160 |
| `.script` | Cambria italic red | 130 | one line only |
| `.pt` panel title | Seg 700 caps | 60 | |
| `.ps` panel sub | Seg 600 | 40 | smallest text in a panel |
| `.num` step numeral | Seg 700 | 160, cream with 4 px ink outline | |
| `.pill` | Seg 700 | 34 (tag), 42-44 (chips) | 6 px ink border, radius 999 |
| starburst label | Seg 700 | 92 ("MỚI!"), 74 / 66 ("Minh" / "hoạ") | inside a 300-320 px burst |

Smallest text in the build: 34 px (the "Minh hoạ" tag). No text under 30 px.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  top platform UI: empty (only the orbit ornament touches y 190)
y 196  -262  "Minh hoạ" tag, left 96 (persistent, every beat)
y 290  -700  headline block (H1 two lines, or H2 + script)
y 520  -1540 content: hero circle (620-700 px) or three panels (300 px high, gap 60)
y 1540 -1620 footer chip
y 1620 -1920 bottom platform UI: empty
x 96   -984  content column, 888 px
```

Panels: x 96, width 888, height 300, tops 520 / 880 / 1240. Hero circle: 620 px at left 230 top 790 (beat 1); 700 px at left 190 top 700 (beat 3). Starburst 300-320 px overlaps the circle's upper-right edge on purpose (a sticker).

## 4. Layers, back to front

`#dots` (cream with a baked-look dot grid, 28 px pitch, drawn as a CSS radial-gradient on ONE layer at full opacity: dot colour #e6d8b4, no alpha) -> `.band` diagonal bands (teal 260 px, mustard 90 px, rotated -14 deg) -> beat containers `#s1 #s2 #s3` (content) -> `#tag` (z 50, persistent) -> `#wipe` starburst (z 60, only while a transition runs).

The profile asks for baked halftone and misregistration PNGs. This build did not bake any (the image step was skipped, see section 10); the dot grid is one CSS gradient layer. That is within the renderer limit (far below ~40 gradient elements).

## 5. Components

- **Slab headline**: caps, ink stroke 3 px, offset shadow 5x6 px ink. The key word in `--red`.
- **Ringed circle** `.circle`: 14 px ink border, then a 14 px cream rim (`box-shadow 0 0 0 14px cream`), then a 12x14 px ink drop shadow. Hero sits inside (circle fill teal or mustard).
- **Starburst sticker**: 14-point polygon (outer r 196, inner r 150 in a 400 box), red fill, 8 px ink stroke, a duplicated ink polygon offset (8,10) as shadow, cream label with ink stroke 7 px. Built in JS before the first tween.
- **Ad panel** `.panel`: cream, 8 px ink border, radius 44, offset shadow 10x12 px, a 220 px coloured numeral block on the left (orange / teal / red), title + sub on the right.
- **Pill**: 6 px ink border, cream or mustard. Used for the "Minh hoạ" tag and the footer chip.
- **Atom orbit**: a 150 px dashed ink circle with a teal dot, around a red centre dot, rotating linearly 360 deg in 3.6 s (finite).
- **Hero robot** (inline SVG, 400 x 520 viewBox, six groups `ant head body al ar lg`, flat fills, 8 px ink strokes). Pieces are addressable for the assembly gag.

## 6. Motion language (measured)

Energy 4 per the profile. Allowed eases used: `back.out(1.4-2)` (landings, slides), `bounce.out` (parts, robot, one bounce read), `power3.in` / `power3.out` (starburst wipe), `sine.inOut` (finite breathing), `none` (rotations). No shake, no flash, no elastic was needed.

| Verb | Recipe as built |
|---|---|
| Headline slide | line 1 from x -900 with skewX 14, line 2 from x +900 with skewX -14, 0.55 s `back.out(1.4)`, offset 0.15 s |
| Circle pop | scale 0 -> 1, 0.55 s `back.out(1.6)` |
| Kit assembly (signature) | six robot parts fly in from off-circle (x or y of 600-900 px, rotation -90..160 deg), 0.7 s `bounce.out`, one every 0.22 s from t 0.75; whole robot complete at 2.1 s |
| Starburst slap | scale 1.6, rotate -30, opacity 0 -> scale 1, rotate 0, opacity 1 in 0.35 s `back.out(1.8)`; then the burst shape rotates 15 deg over 1.6-2.4 s linear |
| Panel slide | panels slide in on x +-1300 with rotation +-6 deg -> 0, 0.6 s `back.out(1.6)`, staggered 0.3 s (4.65 / 4.95 / 5.25) |
| Starburst wipe | a mustard (then red) 14-point burst at the frame centre scales 0.1 -> 9 in 0.4 s `power3.in` (rotates 40 deg), the beat container swaps while it covers the frame, then it scales 9 -> 0.1 in 0.5 s `power3.out` with 90 deg total rotation; the next beat's elements start 0.1-0.25 s after the swap |
| Micro-motion in holds | robot bob y -14 px (0.5 s yoyo x3), panels 1 and 3 bob -8 px, orbit rotation, burst rotation, band drift 40 px over 3.6 s, circle scale 1.00 -> 1.03, robot arm wave -35 deg yoyo x5 (0.3 s) |

The wipe starburst needs scale 9 from a 400 px box (= 3600 px) to clear the 2200 px frame diagonal; scale 6 left corners of the old beat visible.

## 7. Scene recipes (timings of the 12.0 s build; voice not used, so no word anchors: ASSUMED that real builds anchor to `W()`)

| Beat | Time | Content | Hold |
|---|---|---|---|
| 1 Cover | 0 - 4.2 | tag pops 0.1 s; headline lines slide 0.15 / 0.3 s; circle 0.4 s; robot assembles 0.75 - 2.1 s; "MỚI!" burst 2.1 s; chip 2.3 s | full composition from 2.45 s to the wipe at 3.8 s (1.35 s) |
| wipe | 3.8 - 4.7 | mustard starburst, swap at 4.2 s | |
| 2 Steps | 4.2 - 8.4 | H2 slides from the left 4.45 s; orbit 4.55 s; three panels 4.65 - 5.85 s; numeral blocks pop 5.0 / 5.3 / 5.6 s | full composition 5.9 - 7.9 s (2.0 s), panels bob |
| wipe | 8.0 - 8.9 | red starburst, swap at 8.4 s | |
| 3 Payoff | 8.4 - 12.0 | H3a slides 8.6 s; script tagline scales in 8.9 s; circle 8.7 s; robot drops in 9.1 s (`bounce.out` 0.7 s); "Minh hoạ" burst 9.5 s; chip 9.6 s; robot waves from 9.9 s | full composition from 10.2 s to 12.0 s (1.8 s, last frame included) |

Illustrative copy used (generic; no brand, price or spec): "BỘ ROBOT TỰ LẮP", "MỚI!", "Bộ đồ chơi lắp ráp cho bé", "3 BƯỚC LẮP", "Chọn chi tiết / Vặn khớp / Bật công tắc", "TỰ TAY LẮP", "tự hào khoe!". The star claim "for kids 8+" or any part count was deliberately NOT shown: it would be a spec.

## 8. Captions

NOT EXERCISED (demo build, no voice). The profile asks: cream pill, ink border, 42 px Be Vietnam Pro 700 ink, current word mustard, bottom band. Be Vietnam Pro is not installed here; the pill component above (6 px ink border, `SegUIVar` 700) is the natural substitute. ASSUMED. Keep captions out of y 1540-1620 only if the footer chip is also used; in a voiced build drop the footer chip.

## 9. Sound

NOT EXERCISED (silent demo). Profile: swing, surf or lounge exotica 110-128 BPM; boing, ding, slide whistle, cash register. Natural hooks seen in the build: the six robot parts land on a ~0.22 s grid (about 270 BPM eighth notes, i.e. every other beat at 135 BPM), so a voiced build should snap the assembly to the beat grid instead.

## 10. Images

This build made NO agy image: the generation command was not approved in this session, and the hero is inline SVG (flat shapes), which suits the profile better than a generated picture. When an agy image is used: prompt it as "flat 1950s ad illustration, teal / cream / orange / red, heavy halftone dots, slight colour misregistration, plain cream background, no text", at most one per video, inside a ringed circle. Halftone and misregistration must be baked into the picture, never animated.

## 11. Must not

- No neon, glass, chrome, gradients on shapes or text, glow; no thin modern sans headlines; no dark palette (profile).
- No red text under 130 px; no cream text on orange without the ink outline.
- No real company, brand, price, spec, age rating or part count in generic samples; keep the "Minh hoạ" label visible on every beat (the build keeps a persistent pill plus a burst and a footer chip).
- No `segoepr.ttf`.
- No unseeded randomness; spin and bounce are finite.

## 12. Traps seen in real builds (from the t125 build, 2026-11-14)

1. **Slab headline wrapped.** "BỘ ROBOT" at 186 px in an 888 px box wrapped to two lines, so "BỘ" sat on top of the red "TỰ LẮP" (inspect: `content_overlap` at 0.67-3.33 s; the snapshot at 1.2 s showed "TỰ LẮP" printed over "ROBOT"). Fix: 150 px, `white-space: nowrap`, 900 px box; hero word 200 px at top 465. Rule: 8 caps characters at Seg 700 are about 0.62 x size wide, so 888 px allows at most about 160 px for 9 characters; size from the longest line.
2. **Orbit ornament hid the headline.** The 200 px orbit at left 820 top 270 sat under "LẮP" of the 150 px "3 BƯỚC LẮP" (inspect: `text_occluded #h2 span` at 7.33 s). Fix: headline 130 px in a 760 px box at top 350, orbit 150 px at left 850 top 190.
3. **Headline entering from y -200 / -240 sat under the persistent tag** (inspect: `text_occluded #h3a inside #tag` at 8.67 s). Fix: enter headlines from the side (x -1000 / -1100), never from above through the tag's row.
4. **Starburst wipe ghost.** At scale 6 the swap showed corners of the old beat; at scale 9 (3600 px) the frame is fully covered at the swap. The covered time is about 0.15 s around 4.2 s and 8.4 s; the full-frame mustard / red frame is the transition itself, not a ghost, but it must not be held longer.
5. **Offset text shadow plus stroke eat counters.** 3 px stroke + 5x6 px shadow at 130 px was clean; at 90 px small caps with tone marks (ẶẮ) the shadow merged with the diacritic. Keep slab text >= 130 px or drop the shadow to 3x4 px.
6. **Wave arm detaches.** Rotating the right arm -35 deg about (330, 260) swings its lower end out and leaves a gap to the body (seen at 10.5-11.5 s). Acceptable as a cartoon wave, but the arm should overlap the body by at least 10 px (arm x 290-350) to look attached.
7. **Lint warning** `overlapping_gsap_tweens` on `#wipe` (the first wipe's tail and the second wipe's start share properties). Harmless because each wipe is `fromTo` with explicit values; two warnings are expected, no error.
8. **Inspect info** `canvas_overflow` for panels sliding in from x +-1300: intentional, only at 4.67 s.
9. **Tooling.** In this session `motion_tools.py` and `frame_check.py` needed an approval that was not granted, so the frame check was done with `ffmpeg fps=2 tile=6x4` contact sheet read by eye (selfcheck). A voiced build must run the real script.

## 13. Verdict on fit (Jev t125 = 0.82)

Good fit for a toy-kit launch: the robot kit "assembles" in beat 1 (the product IS the animation), the three numbered panels are the profile's ad-panel layout, the payoff is a bouncing hero plus script tagline. The style carries a children's product better than any data story. Weak points: the Segoe substitute for Alfa Slab One, no baked halftone, and no voice or beat sync tested.
