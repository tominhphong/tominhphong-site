# Style: product-spec-film (family: brand-inspired; 9:16 Vietnamese edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), as observed in this build.** Hardware or system stories that are about parts and one or two exact numbers: a product's internal structure (exploded view), architecture reveals, engineering deep-dives, feature deep-dives with 3-5 named parts. Topic shape t132 (smartphone maker shows an exploded view of its new camera module, Jev 0.91) fits. Not for: people stories, quotes, news with a data table, hype, anything without a physical or layered object. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE real demo build (sample-t132.mp4, 12.0 s, silent). **Voice, captions, music and word timing were NOT exercised** (demo build): sections on them are the profile's rules only, untested. Content in the build is generic and labelled "Minh hoạ"; it states no real product, price or spec.

Profile: `skill/references/styles/profiles/product-spec-film.yaml` (energy 2, dark). Character: the object is taken apart with calm; layers separate along one axis, fills fade to linework, thin leader lines pin exact numbers to parts. Format 1080 x 1920, 30 fps.
Marks: **ASSUMED** = invented here, the profile gives no value. **DEVIATION** = knowingly differs from the profile.
DEVIATION 1: the profile layout is 16:9 (callouts at 180 px margins); here margins are 72 px and callout labels sit left/right on the margin.
DEVIATION 2: profile label size 20 px; 9:16 phone needs 30 px (rule: no text < 30 px except one footer line).
DEVIATION 3: profile says "Inter" and "IBM Plex Mono"; not installed, local substitutes below.
DEVIATION 4: no reassemble phase (12 s demo); the explode is followed by the x-ray dissolve instead.

## 1. Tokens (contrast measured with the WCAG formula on bg #0b0c0e, L = 0.0037)

```css
:root{
  --bg:#0b0c0e;               /* graphite */
  --ink:#e6e6e2;             /* 15.6:1 on bg: all primary text */
  --mute:rgba(230,230,226,.6);/* resolves to ~#8e8f8d, 6.0:1: secondary text (profile .5 gives 4.4:1 = FAILS, so raised) */
  --line:rgba(230,230,226,.55);/* 1.5 px plate edges and linework; not text (profile .35 = 2.7:1, too faint on a phone) */
  --accent:#74b0f7;           /* 8.7:1: highlighted part, leader lines, values, kicker */
  --warm:#f29a4a;             /* 8.8:1: used only for the "Minh hoạ" chip (profile: heat/power only; ASSUMED reuse as the label colour) */
  --plate:#15171a;            /* plate fill, only visible until the x-ray dissolve */
}
```
Rules: text only in `--ink --mute --accent --warm`. One accent. No gradients except the baked-style top light (`radial-gradient` ellipse 80% x 45% at 50% 18%, ink at 10% alpha) and a 40 px grid at 4% ink. `hyperframes validate`: 10 text elements pass WCAG AA.

## 2. Fonts (all local, Vietnamese glyphs rendered and looked at in snapshots: Â Ô Ơ Ư, ả, ộ, ẩ, ế, ọ, ủ, ừ all drawn correctly)

| File | Role |
|---|---|
| `SegUIVar.ttf` (variable, declared `font-weight: 100 900`) | headline 600, spec number 300, values 500. SUBST for Inter. Weight 300 works only because the face is declared with a weight range |
| `CascadiaMono.ttf` | uppercase labels, kicker, chip, footer; letter-spacing .08em. SUBST for IBM Plex Mono |
| `cambriai.ttf` | not used in this build |
| `segoepr.ttf` | never used (lacks Vietnamese letters). Not even copied into the project |

Uppercase Vietnamese in the mono face: "KÍNH PHỦ", "CHỐNG RUNG", "CẢM BIẾN", "MINH HOẠ" render with all marks intact at 30 px.

## 3. Type scale, safe areas and grid (1080 x 1920)

| Element | Font | Size |
|---|---|---|
| Kicker | Casc 400, +.08em, accent | 30 px, top 140 |
| Headline (2 lines) | Seg 600, -.01em | 76 px, top 200, line-height 1.08 |
| Callout label | Casc 400 uppercase, ink | 30 px |
| Callout value | Seg 500, accent | 44 px |
| Spec number | Seg 300, ink, tabular | 150 px |
| Spec unit | Seg 500 | 40 px |
| Spec sub line | Casc 400 uppercase, mute | 30 px |
| Chip "Minh hoạ" | Casc 400, warm, 1.5 px border | 30 px, right 72, top 1496 |
| Footer (the one small line) | Casc 400, mute | 26 px, top 1790 |

- Side margin 72 (content width 936). y 0-130 empty; y 140-370 kicker + headline.
- Object zone y 560-1400 (object centre y 960). Spec block y 1450-1700 (1.5 px ink rule at 1450). Footer y 1790. Nothing below 1816.
- Callout labels: left column x 72 (left-aligned), right column right edge x 1008 (right-aligned), width 400. Label sits 104 px above its leader rule; the rule runs from the margin to the dot on the plate.

## 4. Layers, back to front

1. `#root` bg. 2. `#grid` 40 px lines at 4% ink. 3. `#light` top falloff. 4. `#cam` (scale 1.00 -> 1.025 linear over the whole 12 s; the only camera) holding `#obj` (CSS `perspective: 2200px`) > `#tilt` (`rotationX 60`, `rotationZ -40`, `preserve-3d`) > 5 plates; and `#cos` (callouts: dot, rule, label) in the same `#cam` so they scale with the object. 5. Kicker, headline, spec block, chip, footer (flat, above the camera, never scaled). 6. `#fade` (bg colour, 1 -> 0 in 0.4 s).

## 5. Components

- **Plate**: 460 x 460, radius 58, fill `--plate` on a child `.pf`, 1.5 px `--line` border; inline SVG linework (strokes only, 1.5 px) on top. Fill and linework are separate nodes so the x-ray dissolve fades only `.pf`. Five plates, top to bottom: cover glass, lens stack (5 concentric circles), stabiliser frame (nested rounded squares + 4 corner squares), sensor (4x4 grid, accent strokes: the highlighted part), board (rects + traces). All drawn by hand; no image was needed (no agy call).
- **Callout**: 14 px accent dot, 1.5 px accent rule, mono label + value typed in char by char.
- **Spec block**: ink rule (draws left to right), 150 px number counted 0 -> 6, unit, mute sub line "Minh hoạ · số liệu giả định".
- **Chip**: "Minh hoạ" in warm, always on screen from 0.5 s.
- Max 4 callouts on screen at once (profile); beat 3 retires them and shows one.

## 6. Motion language

- Everything eased, nothing bounces, no beat-driven motion (silent build, no beats).
- Fade open 0.4 s `power2.out`. Headline lines rise out of an overflow mask, `power3.out` 0.6 s, stagger 0.08, finished at 0.88 s.
- **Explode**: each plate `z` from [20,10,0,-10,-20] to [340,170,0,-170,-340], `power2.inOut` 1.2 s, stagger 0.08 s, start 0.8 s, end 2.2 s. Cover glass first.
- **Leader callout** (per callout, 0.7 s apart from 2.5 s): dot scale 0 -> 1 0.2 s; rule `scaleX` 0 -> 1 0.5 s `power2.out` (origin at the label side); label typed 0.03 s/char at t0+0.4; value 0.04 s/char at t0+0.7. All four done by 5.8 s.
- **Spec number**: rule draws 4.6 s (0.7 s), text fades in 4.9 s, count 0 -> 6 over 0.9 s `power2.out` from 5.0 s (done 5.9 s).
- **X-ray dissolve** 7.7-8.8 s: `.pf` opacity 1 -> 0, `power2.inOut` 1.0 s, stagger 0.06; strokes remain. Simultaneous slow orbit: `rotationZ` -40 -> -26, `sine.inOut` 1.8 s (7.7-9.5 s). Callouts retire in 0.3 s at 7.4 s BEFORE the orbit, because they are screen-space anchored and an orbit would detach the dots.
- **Final callout** (anchor measured for the orbit end state): dot 9.6 s, rule 9.7 s, label 10.0 s, value 10.3 s (done 10.7 s). Hold to 12.0 s.

## 7. Captions, voice, sound

Not exercised (demo build, silent). Profile rules, untested: caption 40 px Be Vietnam Pro 500 ink, bottom band, no pill; sparse ambient music 70-95 BPM; mechanical ticks on callouts vol 0.15-0.25, low whoom on explode.

## 8. Scene recipe (the single sample: 12.0 s, 3 beats, one persistent object)

**B1 Explode (0-2.4 s).** Fade opens; kicker, headline, chip, footer in by 0.9 s; the assembled stack (z spacing 10 px) is on screen from frame 1; explode 0.8-2.2 s.
**B2 Callouts + number (2.4-7.4 s).** Four callouts (cover glass 0,5 mm; lens stack 6 lớp; stabiliser 4 cuộn; sensor Khối lớn: all generic, labelled Minh hoạ). Spec block counts "6 lớp thấu kính" at 5.0-5.9 s. Hold 5.9-7.4 s.
**B3 X-ray (7.4-12 s).** Callouts out, fills dissolve, orbit, one accent callout on the sensor, spec block and headline stay. The last 1.5 s (10.5-12.0 s) is the full composition.

## 9. Transitions

In 12 s only: fade-in, explode, x-ray dissolve. Profile also lists reassemble, macro-push and cross-fade: not built.

## 10. Image guidance

None needed: the object is built from CSS 3D plates and SVG strokes, which keeps edges at exactly 1.5 px (an agy image would not). If an image is ever used: flat graphite plate, no text or logo, never as the object itself.

## 11. Safe handling of facts

Generic content only; every callout value is a placeholder. "Minh hoạ" appears three times: kicker, chip, footer, plus the spec sub line. A real build must replace values with sourced ones and keep a source line.

## 12. Must not

Glow, gradient colour, thick strokes (> 1.5 px), more than 4 simultaneous callouts, bounce, hype type, text over the object linework where it can be avoided, segoepr, emoji, a camera move that detaches callout anchors.

## 13. Traps seen in real builds (this build, 2026-11-14)

1. **Profile mute at 50% alpha fails.** `rgba(230,230,226,.5)` on #0b0c0e = 4.4:1 (< 4.5). Use .6 = 6.0:1. Line at .35 = 2.7:1 reads as nothing on a phone; use .55.
2. **Plates too small, object floats.** First pass: 380 px plates, z spacing 150: object 40% of width, empty band y 1100-1450. Fix: 460 px plates, z +/-340 (spacing 170), centre y 960.
3. **Exploded stack collides with the spec block.** With z +/-400 the lowest plate reached y 1420 and crossed the spec rule at 1450. Spread must keep the object bottom <= ~1400.
4. **Callout anchors vs 3D.** Leader dots must be placed on the projected plate, not guessed: measure `getBoundingClientRect()` of each plate in the exploded state during build, synchronously (before the first tween), then restore the assembled state. Any later orbit or scale of `#obj` alone detaches the dots; scale only `#cam` (object + callouts together, 1.025 here) and retire callouts before an orbit.
5. **Left labels over the plate.** The left plate vertex reaches x ~230; labels at x 72 only fit if placed ABOVE their rule (104 px up) and kept short (<= 10 characters at 30 px mono, ~200 px). A long value ("Lớp cảm quang") crossed the sensor grid; shortened to "Cảm quang".
6. **Counter shown as "0" before it counts.** The number text is visible at 0 for ~0.1 s after its fade-in (4.9 -> 5.0 s). Fade the number in and start the count on the same time, or fade in already counting.
7. **Typed labels caught mid-type** in the 1.5 fps check sheet (frames at 3.3 and 4.0 s show "KÍ" and "T"): normal during typing (0.4-0.9 s per label) but never leave the typing running into a held frame; all labels finished by 5.8 s.
8. **Layout inspector warnings on per-character spans.** 24 `content_overlap` warnings (labels split into one `<i>` per char). Mark generated callout nodes `data-layout-allow-overlap`; then `inspect` = 0 issues.
9. **Variable font weight 300.** Without `font-weight: 100 900` in the `@font-face`, the 150 px number renders at 400.
10. **`hyperframes` needs a single root:** keep scratch snapshots in a folder outside the project (`work/`), not next to `index.html`.

## 14. Output numbers

Render `-f 30 -q standard`: 1080 x 1920, h264, 30 fps, 12.000 s, 4.04 MB, silent. lint 0/0; validate: no console errors, 10 text elements pass WCAG AA; inspect: 0 layout issues (9 samples) after the allow-overlap marks.
