# Style: monochrome-luxury (9:16 Vietnamese fashion-house edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**

**Status.** Written 2026-11-14 from ONE 12 s silent demo (`samples/sample-t126.mp4`, 1080x1920, 30 fps, 4.6 MB). There is no earlier owner document. **Voice-over, captions, pronunciation, word timing and music were NOT exercised** (demo build): the caption and sound rules in sections 9 and 10 are taken from the profile and are marked **ASSUMED**. Values marked "measured" come from this build; everything else is **ASSUMED**.

**Example video shows the recipe, not the niche.** The demo content is generic and labelled "Minh hoạ" on screen.

Energy 1 (profile). Source of values: `styles/profiles/monochrome-luxury.yaml`.

## 1. Tokens

```css
--bg:     #0a0a0a;  /* stage black */
--ink:    #f4efe6;  /* ivory: 17.28:1 on bg (computed by hand, WCAG formula) */
--accent: #c8b79a;  /* champagne: 10.09:1 on bg; ONE hairline or monogram per beat; may be small text */
--mute:   #9a958c;  /* labels and footer: 6.65:1 on bg */
--hair:   #4a4741;  /* frame hairline, graphic only (not text) */
```
The profile's `mute` is `rgba(244,239,230,0.45)`, which composites to about #737170 = about 4.1:1 on #0a0a0a (fails 4.5). Replaced by the solid #9a958c (6.65:1). A solid colour is also used for hairlines, so nothing sits below 90% opacity on a held frame. `hyperframes validate` reported "5 text elements pass WCAG AA".
Light variant (profile: bg #f4efe6, ink #0a0a0a) was not built; the 17.28:1 pair is the same.

## 2. Fonts (local files; the profile's Playfair Display, Cormorant Garamond and Be Vietnam Pro are NOT installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Display italic, Latin and Vietnamese | Playfair Display 400 / italic | `cambriai.ttf` (Cambria Italic, weight 400, real italic) | owner docs measured all 36 letters present; seen in the render: ộ ư ậ ã ó ờ ắ ả đ drawn correctly at 96 and 150 px (the fontTools run was blocked in this build, so the check is by eye on snapshots) |
| Small caps label, footer | Cormorant Garamond 500, +0.32em | `SegUIVar.ttf`, weight 500, uppercase, `letter-spacing:.32em` | present (owner docs); "BỘ SƯU TẬP MÙA MỚI" rendered correctly |
| Never | | `segoepr.ttf` (35 of 36 Vietnamese test letters missing), `CascadiaMono.ttf` (no numbers in this style) | |

Declare faces with `font-display: block`. Cambria Italic has no bold and no roman: do not set `font-weight` above 400 and do not use it for small labels (hairlines of its thin strokes vanish below 60 px).

### Type scale (1080 x 1920 px, measured in this build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.lab` label | Segoe 500 uppercase, +0.32em, `--mute` | 32 / 1.3 | letterspace-open from +0.6em; 18 characters = about 540 px wide |
| `.disp` hero | Cambria italic, -0.01em, `--ink` | 190 / 1.15 ("Lookbook" = 8 letters, about 640 px wide) | one word only |
| `.disp` line | Cambria italic | 150 / 1.15 (end card, 2 lines of up to 11 characters, about 690 px wide); 96 (one 19-character caption line, about 780 px wide) | max 11 characters per line at 150 px in a 1080 px frame with 64 px frame inset |
| `#foot` "Minh hoạ" | Segoe 500, +0.2em, `--mute` | 30 / 1.3 | the one footer line; never below 30 px |
| monogram letter | Cambria italic | 96 | inside a 200 px champagne circle, 1.5 px stroke |

Profile says display 120-200 px: 190 and 150 sit inside; 96 for the caption line is below it on purpose (a sentence, not a word).

## 3. Safe areas and grid (1080 x 1920) (measured in this build)

```
y 0    - 64    outside hairline frame: empty (frame inset 64 px, 1 px, #4a4741, present in every beat)
y 236  - 292   label + champagne hairline (beat 2)
y 330  - 1290  look plate 780 x 960 at x 150 (beat 2)
y 760  - 1130  title block (beat 1: label y 760, word y 850-1040, hairline y 1130)
y 652  - 1290  end card: monogram 200 px at y 600-800, two lines at y 930 and y 1110
y 1356 - 1450  caption line under the plate (beat 2)
y 1738 - 1770  footer "Minh hoạ"
```
Axis: everything centred on x 540 (mask boxes are full width with `text-align:center`). More than 50% of the frame is empty in every beat (profile rule). Content sits between y 236 and y 1450; the lower 470 px are empty except the footer, and the frame-check "TOPHEAVY" note (info only) would fire: it is the style, not a defect.
Tracking adds a trailing gap, so centred small caps sit about 0.16em to the left; fixed with `padding-left` equal to the tracking.

## 4. Layers, back to front

`#root` bg -> `.beat` (b1, b2, b3; each holds one `.cam` group that carries the camera move) -> `#frame` (SVG hairline rectangle, static, z 30) -> `#foot` -> `#sweep` (light-sweep bar, z 38) -> `#vig` (baked-look radial vignette, CSS gradient, z 40) -> `#grain` (PNG, z 41).
Grain: made with ffmpeg `geq` (10% of pixels white, alpha 45/255), shown at 50% layer opacity (about 1% effective); static, no animation. Vignette 0 -> 0.75 black at the edges. The camera group moves; frame, footer, vignette and grain never move, so the frame stays at its 64 px inset during pushes.

## 5. Components

- **Label** `.lab`: small caps, letterspace-open +0.6em -> +0.32em with opacity 0 -> 1, 1.2-1.4 s `power2.out`.
- **Display line** inside a mask: `.mask` has `overflow:hidden`, `padding 36px 0 30px`, `margin -36px 0 -30px` (room for ế ộ ậ and descenders p g), carries `data-layout-allow-overflow`; the inner span starts at `yPercent:115` and rises to 0.
- **Champagne hairline** `.hr`: 1 px high, 160-200 px wide, `scaleX` 0 -> 1 from the left, 1.2 s `power2.inOut`.
- **Plate** (the "product"): 780 x 960, `#12110f`, 1 px `#5a564d` border, built from 6 CSS gradient folds plus a top-light radial gradient (no image). It stands in for a garment: a drape of ivory highlights on black. Labelled "Minh hoạ" by the footer.
- **Monogram**: SVG circle r 98, `stroke-dasharray 616`, drawn with `strokeDashoffset` 616 -> 0 over 1.3 s; a single italic letter inside. Letter "M" is generic.
- **Footer** `#foot`: "Minh hoạ", fades in at 0.8 s and never leaves.

## 6. Motion language

Energy 1: no shake, bounce, elastic, flash or `back` ease. Eases used: `power2.out` (reveals), `power2.inOut` (hairlines, circle), `sine.inOut` (sweep, drift), `power2.in` (fade out), `none` (push). The profile bans motion faster than 0.6 s except cuts to black: shortest used = 0.12 s outgoing fade hidden under the sweep and 0.3 s fade to black.

| Verb | Recipe (measured) |
|---|---|
| light-sweep | `#sweep` bar 520 px wide, `skewX(-18deg)`, ivory alpha 0 -> 0.32 -> 0, `x` 0 -> 2700 over 1.2 s `sine.inOut` (3.9-5.1 s); the beat swap happens under its centre |
| mask-rise | inner span `yPercent` 115 -> 0, 1.0-1.2 s `power2.out` |
| letterspace-open | see Components |
| fade-through-black | beat 2 out 0.3 s `power2.in` (8.1-8.4), beat 3 in at 8.4; black gap about 0.3 s with the frame and footer still visible |
| hairline draw | 1.2 s |
| camera | beat 1 push `scale` 1.00 -> 1.03 over 4.6 s (`none`); beat 2 lateral drift `x` +22 -> -22 px over 3.7 s (`sine.inOut`; profile limit 40 px); beat 3 pull-out 1.03 -> 1.00 over 3.6 s. Adjacent beats never share a move |
| parallax in the plate | back fold 0 px, mid folds -16 to -26 px, thin highlights -44 px over 3.7 s (ratio about 0 : 1 : 2) |
| inner sheen | a 220 px skewed bar crosses the plate in 1.2 s at 6.3 s, alpha 0.30 |

Every hold carries micro-motion (push, drift or pull-out); nothing is frozen.

## 7. Scene recipes (the 12 s demo: 3 beats; times are absolute seconds)

### R1 Title (0 - 4.6), type `title`
0.0 label opens (visible from about 0.3 s); 0.4 "Lookbook" rises out of its mask (done 1.6); 1.3 champagne hairline draws (done 2.5); footer in at 0.8; hold with push to 3.9; 3.9-5.1 light sweep; beat 1 fades out 4.42-4.54. First frame is the hairline frame only; by 0.4 s the label shows at about 30%, by 1.0 s title is rising.

### R2 Look plate (4.4 - 8.4), type `product-hero`
Beat 2 visible from 4.4 under the sweep; plate fades up 4.45-5.45; label "Look 01" opens 4.55; hairline draws 5.1-6.3; caption line "Đường cắt tinh giản" rises 5.5-6.5; sheen crosses the plate 6.3-7.5; hold with lateral drift to 8.1.

### R3 End card (8.4 - 12.0), type `outro`
8.1-8.4 beat 2 fades to black; 8.4 circle starts drawing (done 9.7); 8.6 "M" fades in and "Bộ sưu tập" rises (done 9.6); 8.8 "đã lên sóng" rises (done 9.8). The composition is complete from 9.8 s and holds 2.2 s with a slow pull-out. There is NO fade to black at the end (the acceptance rule wants a full composition in the last 1.5 s); a long black hold before the end card, from the profile, is replaced by a 0.3 s black.

Words on screen: beat 1 = 5 (4 label + 1 title), beat 2 = 6 (2 + 4), beat 3 = 6 (5 + the letter M); footer "Minh hoạ" is a label line and not counted. Profile maximum is 6.

## 8. Transitions (profile set)

Used: light-sweep (beat 1 -> 2) and fade-through-black (beat 2 -> 3). Not used: mask-rise as a transition (used only as an entrance), letterspace-open (entrance only). Do not add a third language in 12 s.

## 9. Captions and voice

**Not exercised in this build (no voice-over).** The profile asks: no pill, 40 px Be Vietnam Pro 500, ivory, +0.02em, centred bottom band, unread words mute. **ASSUMED**: use `SegUIVar` 500 at 44 px (the 40 px minimum of other styles is 30; 44 reads better on a phone), unread `#9a958c`, read and current `#f4efe6`; the footer "Minh hoạ" lives at y 1738, so the bottom band must sit above it (bottom edge 1480, as in the other styles) and the 64 px frame must not be crossed.

## 10. Sound

**Not exercised.** Profile: sparse piano or dark ambient 60-84 BPM, almost no SFX (one soft shimmer on the light sweep, one fabric swish per section). Beats only time reveals; here the sweep at 3.9 s would take the one shimmer.

## 11. Images (agy)

**No image was generated in this build**: the `motion_tools.py image` call (agy) was refused by the permission layer, so the plate is CSS gradients. If a still is wanted: one image, no text, no people, "black silk garment on an invisible hanger, matte black studio, one soft top light, deep falloff, empty black around it, centred in the middle 55% of the height". Place it inside the 780 x 960 plate, `scale` 1.00 -> 1.04 (Ken Burns) instead of the folds. Never ask for a model's face or a real person.

## 12. Must not

- No colour except ivory, champagne and the black ramp; no gradient on text; no glow; no bounce, elastic or overshoot; no shake or flash.
- No more than 6 words on screen (footer excluded); no stats tile, chart, list, UI or terminal.
- No `rgba` text colours: use solid tokens (contrast must be computed on a solid).
- Champagne only on one hairline or the monogram circle per beat; never on large text.
- No text under 30 px; the only footer line is "Minh hoạ" at 30 px.
- No brand name, real price, real spec or real company: the demo is generic and labelled "Minh hoạ".
- No fade to black as the last frames; no empty panel longer than 0.5 s.
- No `segoepr.ttf`.

## 13. Traps seen in real builds (this build, 2026-11-14)

1. **Monogram letter not centred in its circle.** First render put the "M" at the bottom of the circle: the letter box was placed with `top:690` for a circle centred at y 700, but a 96 px line box is 96 px tall, so its centre was 738 (38 px low). Rule: letter `top` = circle centre y - font-size/2 (here 700 - 48 = 652). Fixed and verified on the final render.
2. **Sparse stretch at the end-card start.** In the first version the end card began at 8.55 s with a 1.5 s circle draw and text from 9.1 s: frames 8.4-9.1 were black except for a tiny arc and the footer (about 0.7 s, over the 0.5 s limit). Fix: beat 3 starts at 8.4, the text rises at 8.6 and 8.8, and the circle draws 1.3 s from 8.4. Measured after the fix on the render: the black gap is about 0.3 s (8.4-8.7 s).
3. **Profile `mute` fails contrast.** `rgba(244,239,230,0.45)` on #0a0a0a is about 4.1:1. Use the solid #9a958c (6.65:1).
4. **Container overflow warnings.** The 6 plate folds are taller than the plate (overscan so drift never shows an edge): `inspect` printed 8 `container_overflow` warnings. Fix: `data-layout-allow-overflow` on `#plate`; second `inspect` = 0 layout issues.
5. **Frame check script needs numpy.** `frame_check.py` could not run (python was not permitted in this session); the check was done with ffmpeg contact sheets (`fps=2` tile 8x3, and `fps=10` over each transition) plus reading them. Re-run the script before a full build.
6. **Beat swap leaves two beats visible for 0.12 s.** Beat 1 fades 4.42-4.54 while beat 2 is set visible at 4.4: overlap 0.14 s, under the 0.15 s ghost limit and hidden by the sweep bar. A longer crossfade would show the old title ghosting through the plate.
7. **Tracking shifts the centre.** A letter-spaced centred label sits about 0.16em left of the axis (5 px at 32 px). Fix with `padding-left` = tracking; during letterspace-open the offset moves by up to 19 px for 1 s: accepted.
8. **Style is top-heavy by design.** The content sits y 236-1450 and the lower quarter is empty. A "TOPHEAVY" flag from the frame-check script is informational; do not fill the space.
9. **Tool facts (hyperframes 0.7.26).** lint 0 errors / 0 warnings; validate no console errors, 5 text elements pass WCAG AA; inspect 0 issues after the fix; render 17.7 s for 12 s, `--crf 22` gave 4.6 MB (file limit 15 MB). GSAP is inlined from the CDN at render time. Do not use `sed -i` or cp with flags in the build folder (permission prompts): use the edit tool and plain `cp file file`.
10. **Gradient-only "product".** CSS folds read as satin curtain more than a garment. Fine for a demo; a real lookbook needs real photography supplied by the owner, because agy cannot be trusted with drape geometry.
