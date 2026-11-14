# Style: Joyful pop (9:16 Vietnamese celebration-campaign edition)

Written 2026-11-14 from ONE demo build (sample t090, 12.5 s, silent). Everything marked **ASSUMED** was not exercised.

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build.** A bold, warm, celebratory campaign shape: a consumer product or seasonal moment told as "hook headline, shared moments, pop and end card" (the tested shape: an ad campaign for a sparkling water brand, Jev fit 0.8). Good for seasonal greetings, community and event promos, brand-anthem style pieces. Not for numbers, charts, code, enforcement, bad news or dense information (profile `scene_types.avoid`: terminal, code, spec, chart). Tier 2 never widens tier 1.

**Status and scope of evidence.** Demo build only: one silent 10-15 s sample, text plus motion. **Voice-over, word timing, music, captions (karaoke pill) and the pronunciation rules were NOT exercised.** Section 7 and 9 give profile values only, marked ASSUMED. Content in the sample is generic and labelled "Minh hoạ" (no real brand, product, price or spec).

**Reading order.** Sections 1-6 are what was measured. 7-9 mix measured recipes with profile values. 12 is the traps from this build.

Source of values: `styles/profiles/joyful-pop.yaml` (energy 4, red field, white hero colour). Everything the profile does not give is **ASSUMED**.

## 1. Tokens (contrast measured with the WCAG formula, hand-computed)

```css
--bg:    #e8503a;  /* field; white on it = 3.72:1 -> LARGE text only (>= 100 px here) */
--white: #ffffff;  /* hero colour */
--deep:  #a8321f;  /* pills, labels, ink on white/cream.  white on deep 6.68; deep on white 6.68; deep on cream 6.13 */
--cream: #fff4e0;  /* photo borders, end card (L 0.914) */
--gold:  #f5c242;  /* sparkles and confetti ONLY (2.2:1 on bg, 4.03 on deep: never text) */
--dark:  #1a0b0b;  /* shadows only */
/* ASSUMED inner-art reds for polaroid pictures */ #a8321f, #c93f2a, #8f2a1a
```

Rules proven in the build: any text below 100 px on the red field sits in a deep pill (6.68:1) or on cream/white; text straight on `--bg` is only the 122-200 px headline (3.72 passes the 3:1 large-text rule, not 4.5). `hyperframes validate` reported "5 text elements pass WCAG AA". A vignette (`rgba(120,26,14,.38)` at the edge) darkens the corners, so white-on-bg is slightly better there, never worse.

## 2. Fonts (3 local files; profile fonts DM Serif Display, Nunito, Be Vietnam Pro are not installed)

| Role | Profile asks | Used here |
|---|---|---|
| Headlines, labels in cards, end card | DM Serif Display 400 | `cambriai.ttf` (Cambria Italic, declared `font-style: italic`, 400). Italic only: there is no upright, so the whole style reads as warm italic serif. |
| Pills, chips, kicker, footer | Nunito 700 | `SegUIVar.ttf`, weight 700 |
| Captions | Be Vietnam Pro 700 | not used (no captions); would be SegUIVar 700 (ASSUMED) |

`segoepr.ttf` lacks Vietnamese: never used. **Vietnamese check:** the scripted 36-letter fontTools test could NOT be run in this build (python execution was blocked in the sandbox). Instead every glyph used on screen was verified by eye on the 1080x1920 snapshots and the rendered video: Ế Ị Ù È, ủ ọ ả ạ ắ ở ờ ặ ế à â ê ô ư ơ đ, with no tofu or fallback font. Run the full test before using letters not in the sample.

## 3. Type scale (px, measured in the build)

Headline hook 200 (3 lines, line-height 1.0) · headline beat 2 122 · speech-bubble line 1 150, line 2 104 · end card 62 · polaroid label 58 · pills 38-40 · chips 40 · "Minh hoạ" badge 34 · footer line 30 (the single line allowed below 40; nothing is under 30).

## 4. Safe areas and grid (1080 x 1920)

- Side margin 72, content width 936. y 0-200 top zone: only the "Minh hoạ" badge (x 56, y 120).
- Content zone y 230-1650. Bottom 270 px empty (platform UI). Measured: lowest element (footer) ends at y 1618.
- Hook block: kicker y 430, headline y 540-1140, sub pill y 1300. Beat 2: headline y 240-480, three 400x500 polaroids at (70,560), (610,660), (340,1140). Beat 3: kicker y 250, speech bubble 880x460 at (100,480), chips y 1120, end card 936x220 at y 1290, footer y 1580.
- Polaroids overlap each other by up to ~50 px on purpose: `data-layout-allow-overlap`.

## 5. Layers, back to front

1 `#vig` vignette (one radial gradient, the only one) · 2 `#fizz` bubbles (34 circles, clipping layer, `data-layout-allow-overflow`) · 3 scene sections `.sc` (one visible at a time via `autoAlpha`) · 12 `#conf` confetti (40 scraps) · 20 `#bb` burst circle · 21 `#ring` pop ring · 30 `#mh` "Minh hoạ" badge, above the burst so it never disappears.

## 6. Components

- **Bubble**: flat circle, fill `rgba(255,255,255,.16)`, 3 px border `rgba(255,255,255,.7)`, a small solid highlight dot as `::before`. No gradients (renderer limit on radial-gradient count). Sizes 36-190 px, four 120 px larger ones.
- **Pill**: deep fill, white text, radius 999, padding 20 x 40.
- **Polaroid**: cream 400x500, radius 18, 20 px border, 360 px SVG picture, label 58 px deep italic, shadow `0 18px 40px rgba(26,11,11,.35)`. Pictures are drawn in SVG (tumbler, heart, star outlines plus dots) so there are no photos, bottles or people. Doodle strokes are drawn on with `pathLength=1` and `strokeDashoffset`.
- **Speech bubble**: white, radius 100, 120 px square tail rotated 45 deg; text deep italic. The tail must sway together with the bubble (`sway` on both).
- **Underline bar**: straight 16 px bar, radius 8, `scaleX 0 -> 1`, origin left, under the key words ("vui cả", "bọt vui", "bọt vui" in red on white).
- **Sparkle**: 4-point star SVG, gold or white, 60-90 px.
- **Confetti scrap**: 22x34 rect (every third a 24 px circle), colours white, gold, cream, deep.

## 7. Motion language (measured in the build; beat 120 BPM ASSUMED, music not used)

- Entrances overshoot: `back.out(1.4-1.8)` 0.45-0.65 s, with scale 1.2-1.25 or a rotation of 3-4x the final angle, from 40-70 px below (text) or 520-900 px above (polaroids).
- Hold: a 10 px sine float (period 2.8 s) on the headline, +-1.6 deg sway on cards, a 0.82-1.0 scale pulse on sparkles, bubbles rise linearly (150-310 px/s) with +-14 px sway. Nothing is frozen.
- Beat bump: headline scale 1.03 for 0.18 s at 2.0 s.
- Bubble accelerate on kick, choir/clap sync: **not exercised** (no music).

## 8. Scene recipes (3 beats, 12.5 s; starts on 120 BPM beats 0 / 4.0 / 8.0)

**R1 Hook (0-4.0).** Kicker pill drops in at 0.04; three headline lines "Sủi bọt / vui cả / ngày hè" (200 px) pop in 0.16 s apart from 0.08; underline under "vui cả" at 0.9 (0.5 s); sub pill at 1.0. Full composition from 1.0 s; 3.0 s of hold with float.
**Transition (bubble burst).** One white 400 px circle scales 0 -> 6.6 over 0.45 s `power2.in` ending exactly at the swap (3.55-4.0), outgoing scene hidden by `tl.set` at 4.0 under full cover, then the circle grows to 8.4 and fades to 0 in 0.32 s while a 22 px ring expands (`expo.out`, 0.5 s). Incoming content starts at 4.12. Same burst at 8.0.
**R2 Shared moments (4.0-8.0).** Headline 2 lines (122 px) 4.12; three polaroids toss in at 4.35 / 4.6 / 4.85 (0.65 s `back.out(1.4)`, rotation settles to -7 / +5 / -3 deg); underline 5.0; doodles drawn on 5.5 / 5.8 / 6.1 (0.7 s each). Final held frame 6.8-8.0.
**R3 Pop and end card (8.0-12.5).** Speech bubble pops 8.1 (scale 0.2 -> 1, `back.out(1.8)`), text lines 8.4 / 8.55, confetti burst on 8.55 (40 scraps, `expo.out` 0.75 s, seeded angle in the upper half-circle, fall from 9.3, hidden at 11.0 when off-screen), sparkles 8.7, chips 9.2 / 9.34 / 9.48, end card 9.7, footer 10.0. Last 1.5 s (11.0-12.5): full composition, only floats.

## 9. Captions, sound (not exercised)

Profile values, ASSUMED and untested: white pill radius 26, 44 px SegUIVar 700 `--deep`, current word `--bg` (note: `--bg` on white is 3.72, below 4.5, so use `--deep` for the current word with scale 1.04 instead). Sound: uplifting pop anthem 110-120 BPM, fizz and pop SFX on bubbles, chimes on confetti. Voice and word timing were not part of this build.

## 10. Images

None used (one allowed, skipped: SVG doodles carry the polaroids). If agy images are added: warm shared moments, no text, logos, real people or bottle shapes; always crop into the cream polaroid frame.

## 11. Safe handling of facts

Generic content only; "Minh hoạ" badge visible on every frame (top-left) and a 30 px footer line in beat 3. Never show a price, claim, real brand or health promise in this style without a source.

## 12. Must not

No script-lettered logo imitation, bottle shape, real slogan (profile). No ribbon, wave or swoosh sweeping the frame. Red field or red accents in every scene. Seeded rng, capped counts (bubbles 34 <= 60, confetti 40). No cold palettes, no dense UI, no grunge. No gold text. No white text on `--bg` below 100 px. No 30 px-or-smaller text except one footer line.

## 13. Traps seen in real builds (THIS build, 2026-11-14)

1. **Timeline longer than the video.** Bubble sway used `repeat = ceil(DUR/d) | 1`, so yoyo segments ran to ~18.6 s; snapshot reported an end frame at 18.61 s. Fix: `repeat = floor(DUR/d) - 1`; the end frame then read 12.71 s and the render is exactly 12.5 s.
2. **CSS transform vs GSAP.** `transform: scale(0)` in CSS on `#bb` and `#ring` is a lint ERROR (`gsap_css_transform_conflict`). Start state goes in `gsap.set`, tweens use `fromTo` with `immediateRender:false` for shared layers. Residual lint warning `overlapping_gsap_tweens` on `#bb` (burst out-tween vs the next burst's in-tween, 0.00-0.32 s) is false: the tweens are 3.55 s apart; accepted.
3. **Bubbles trigger 215 `container_overflow` warnings** in `inspect` at t=4.86 s (they rise out of the frame by design). Mark `#fizz` with `data-layout-allow-overflow`: result 0 layout issues across 9 samples.
4. **Speech bubble too tall.** First version 880x560 with text at the top left the lower 45 % white and empty (seen on the snapshot at 12.0 s). Fixed to 880x460 with the text block centred; the tail had to move with it (870 px).
5. **White on `--bg` is 3.72:1.** Only 122-200 px headlines may sit directly on the field; everything else goes into a deep pill (6.68:1).
6. **Burst timing.** The white circle needs scale >= 5.5 to cover 1080x1920 (diagonal 2204 px); 6.6 gives margin. The scene swap must be a `tl.set` at the cover time, otherwise the outgoing scene ghosts. Measured result: sheet frames at 3.5 s (small dot) and 4.0 s (cards already falling) show no ghost; the empty window is about 0.35 s.
7. **Frame-check tooling.** `frame_check.py` needs numpy, which the default python3 lacked; `python3.12` and ad-hoc python scripts were blocked by the sandbox. Substitute used: `ffmpeg -vf "fps=2,scale=270:-1,tile=5x5"` contact sheet read by eye. The automatic BLANK list was therefore not produced.
8. **Confetti over the footer.** Confetti still falls across the end card until about 10.8 s and crosses the 30 px footer; hide it at 11.0 s so the last 1.5 s are clean (done).
9. **Doodles start undrawn.** Polaroid pictures show only dots for 1.0-1.7 s before the strokes draw on (5.5-6.1 s); acceptable (not empty), but draw the first doodle at 4.9 if the beat needs a full picture sooner.
10. Decorative bubbles are translucent by design (fill 16 %), so "nothing below 90 % opacity on a held frame" applies to content, not to the fizz layer.

## 14. Result of the build

lint 0 errors / 1 known warning; validate no console errors, 5 text elements pass WCAG AA; inspect 0 layout issues; render 12.3 s, 5.3 MB, h264 1080x1920 30 fps, 12.5 s, silent.
