# Style: newsprint editorial (9:16 Vietnamese front-page edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY).** Observed in this build (topic shape t138, "a century of the Texas oil industry: boom, bust and the workers", Jev fit 0.72): a history-with-a-curve story told over 3 "pages" works well: a loud cover, one illustrative curve, one human page. Breaking one-number stories fit even better (profile `best_for`). Not for warm, soft human stories (the stamp and caps are loud) and not for many equal numbers. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample at 1080 x 1920, 30 fps, no voice-over, no word timing, no music. **Voice, caption and sound rules were NOT exercised**; sections 7 and 8 are the profile's values, marked ASSUMED. Everything else is measured on `samples/sample-t138.mp4`.

**Reading order.** Sections 1-11 are the design as built; section 12 holds the traps seen in this build with numbers; where they disagree, section 12 wins.

**Example videos show the recipe, not the niche.** The sample content is generic and labelled "Minh hoạ" on every page: no real company, price or figure.

Source of values: `styles/profiles/newsprint-editorial.yaml` (energy 4). Anything the profile does not give is marked **ASSUMED**.

## 1. Tokens

```css
--bg: #f1e8d4;      /* aged cream page                         */
--cream: #f8f2e3;   /* chart panel, text on dark chips          */
--ink: #1b1916;     /* headlines, body, rules, dark chips       14.4:1 on bg, 15.7:1 on cream */
--charcoal: #3a3733;/* creases, secondary rules (not used for text here)  9.71:1 on bg */
--accent: #b3201c;  /* stamp, ONE key headline word per page    5.49:1 on bg, 5.99 on cream */
--mustard: #e0a526; /* highlighter label, closing band: MARK ONLY  1.80:1 on bg (never text); ink on mustard 8.0:1 */
--desk: #2b2723;    /* dark surface visible only while a sheet spins (ASSUMED) */
```

Ratios are hand-computed with the WCAG relative-luminance formula (no script could be run in this build) and agree with `hyperframes validate`: "15 text elements pass WCAG AA". Accent on mustard is 3.05:1: never put red text on the highlighter. Text colours allowed: ink, cream-on-ink, accent (large only, >= 64 px or the stamp). No gradients, no glow.

## 2. Fonts (3 local files; Anton, Old Standard TT, PT Serif, IBM Plex Mono are not installed)

| Role | Profile asks | Used here | Notes |
|---|---|---|---|
| Stacked headlines | Anton (condensed) | `SegUIVar.ttf` 700, uppercase, `letter-spacing:-0.02em`, line-height 1.02 | NOT condensed: Segoe caps run about 0.62 em per letter, so every headline is sized by width (section 3). Do not fake a condensed face with `scaleX`. |
| Deck (one pull sentence) | Old Standard TT 700 | `cambriai.ttf` (Cambria Italic, 400 only) | 54 px / 1.2. Real italic, no bold exists |
| Column body, labels, masthead | PT Serif 400 | `SegUIVar.ttf` 600, 30 px / 1.42 | sans body instead of serif; accepted substitution |
| Datelines, captions, footer | IBM Plex Mono 500 | `CascadiaMono.ttf` 500-600 | 30 px datelines and chart captions, 24 px footer only |
| Never | | `segoepr.ttf` | lacks Vietnamese letters |

**Vietnamese diacritics check.** The fontTools glyph test (36 letters ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ) could NOT be run in this build (script execution was refused). It was replaced by reading rendered snapshots and a 48-frame sheet of the final MP4: every tone-marked word on screen (MỘT THẾ KỶ, DẦU MỎ, BÙNG NỔ, SUY THOÁI, NGƯỜI LAO ĐỘNG, TRANG, CON NGƯỜI, Nét viền: chỗ trống) drew correctly in SegUIVar, Cambria Italic and Cascadia Mono, with no tofu and no clipped marks. Run the fontTools test before a real edition.

Declare faces with `font-display: block`, variable ones with `font-weight: 300 700` / `200 700`. The renderer embedded all three as data URIs (1808 + 363 + 872 KB).

### Type scale (1080 x 1920, px)

| Token | Size / line | Notes |
|---|---|---|
| `.mast` masthead | 54 / 1.2 (44 on pages 2-3), tracking +0.24 em | between a 3 px and a 1 px ink rule |
| `.dateline` | Cascadia 30 / 1.2, with a `.chip` "MINH HOẠ" (cream on ink) | on every page |
| Cover headline | 128 (line 1), 196 (red key word), 236 (last word, 5 letters) | each its own line mask |
| Page 2 / 3 headline | 150 + 112 (page 2), 112 + 104 (page 3) | key word red |
| `.deck` | Cambria Italic 54 / 1.2 | max 2 lines |
| `.col` | Segoe 600 30 / 1.42 | 2 columns of 430 px, 3 lines max, lines are separate `nowrap` spans |
| Stamp | 60 px 700 caps, 8 px red border, tracking +0.06 em | rotated -8 deg |
| Band | 44 px 700 caps, +0.14 em, on mustard | closing page only |
| Footer | Cascadia 24 / 1.3 | the one line allowed under 30 px; always says "Minh hoạ: nội dung chung, không phải số liệu thật." |

Width rule measured in this build: at 700 weight Segoe caps need about 0.62-0.64 em per letter. "DẦU MỎ" overflowed 888 px at 236 px and fits (about 800 px) at 196; "NGƯỜI LAO ĐỘNG" (14 characters) overflowed at 150 and spans 905 px at 104 (17 px into the right margin, still inside the frame). Size every headline line = 888 / (characters x 0.63).

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -166  platform top: empty (rule at 166)
y 166  -302  masthead block: rule, masthead, thin rule, dateline, rule
y 322  -690  headline stack (page 2/3) ; page 1: y 350 - 1000
y 600  -1160 chart panel (page 2) ; y 900-1040 pictogram row (page 3)
y 1108 -1296 deck (page 1) ; y 1150-1410 columns and rules
y 1410 -1506 closing band (page 3 only)
y 1560       footer line (24 px)
y 1620 -1920 empty (platform UI, and reserved for captions in a full video: ASSUMED)
x 96   -984  content column, 888 px; two text columns of 430 px with a 14 px gap and a 2 px column rule at x 540
```

All page elements are absolute children of the sheet's `.inner` layer, so the numbers are absolute frame coordinates.

## 4. Layers, back to front

`#root` (desk colour) -> `.sheet` (one per beat, full frame, cream, `visibility:hidden` until its spin) -> `.grain` (baked noise PNG 540 x 960 scaled to the frame, opacity 0.07) -> `.crease` (4 px charcoal line at y 958, opacity 0.10) -> `.inner` (all content; this is the layer that gets the push-in and the shake). No flash layer, no wipe layer: the transition is the sheet itself.

## 5. Components

- **Masthead strip**: thick rule, spaced caps title, thin rule, dateline row (left label, right "MINH HOẠ" chip), thick rule.
- **Headline line mask** `.ln` (`data-layout-allow-overflow`): `overflow:hidden; padding-top:.16em; margin-top:-.16em; padding-bottom:.1em; margin-bottom:-.1em`. The padding keeps Ầ, Ệ, Ỏ tone marks inside the mask.
- **Stamp**: red border and red caps, transparent inside, rotated, slammed once per cover.
- **Highlighter label**: mustard box, ink text, 34 px caps. **Ink label**: ink box, cream text.
- **Column**: lines are explicit `span.tl` blocks (never auto-wrapped) so a typing clip can address each line.
- **Chart panel**: cream, 4 px ink border, one CSS `radial-gradient` dot halftone (16 px pitch, ink at 0.16 alpha), an SVG baseline and one 10 px ink curve. Illustrative only: no ticks, no values, captioned "Đường vẽ minh hoạ, không có số liệu."
- **Pictogram figure**: 64 x 140 px, built from three `<i>` boxes (hard hat in mustard, head, body). A filled figure is "present", an outlined one is "gone"; the fill fades to the page colour, the ink border stays.
- **Closing band**: full-width mustard strip with ink borders and one caps line.

## 6. Motion language

Energy 4. Allowed eases: `expo.out` and `power4.out` (entrances, spin), `power3.in` (spin out), `power2.inOut` (curve draw), `back.out(1.4)` (labels, figures), `steps(22)` (typing), `none` (holds). No elastic.

| Verb | Recipe as built |
|---|---|
| spinning-page in | sheet `scale .08 -> 1`, `rotation 540 -> 0`, 0.6 s `expo.out`; it is visibly settled by about 0.35 s |
| spinning-page out | previous sheet `scale 1 -> .25`, `rotation 0 -> -140`, 0.15 s `power3.in`, then hidden; the incoming sheet starts 0.1 s after the out starts |
| Headline lines | `yPercent 115 -> 0`, `rotation 3 -> 0`, 0.5 s `power4.out`, stagger 0.09 s, starts 0.5 s after the sheet starts spinning |
| Stamp slam | `scale 2.4 -> 1`, `rotation -24 -> -8`, 0.2 s `expo.out`, on 1.25 s; then a seeded 6-frame shake on `.inner` (amplitude 12 px decaying, `set` per frame, back to 0 at frame 7) |
| Typing columns | each line `clip-path inset(0 100% 0 0) -> inset(0)` over 0.32-0.34 s in `steps(22)`, lines overlapped at 80% |
| Curve draw | SVG path with `pathLength=1`, `stroke-dashoffset 1 -> 0`, 1.9 s `power2.inOut`; labels pop (`back.out(1.4)`) as the curve passes their point; red circle draws 0.4 s |
| Figures | rise 50 px + fade, `back.out(1.4)`, stagger 0.07 s; three of eight then fade their fill to outline at 10.0 / 10.1 / 10.2 s |
| Band | `scaleX 0 -> 1` from the left, 0.4 s `expo.out`, text fades in 0.25 s later, small shake |
| Hold (camera) | `.inner` `scale 1 -> 1.03`, `ease:none`, from the headline start to the sheet's exit |

Timeline of the 12.0 s sample (3 beats): beat 1 cover 0.0-4.15 s (sheet spin 0.0, headline 0.5, stamp 1.25, deck 1.55, columns 2.0-3.4); beat 2 chart 4.1-8.15 s (spin 4.1, headline 4.6, panel 4.8, curve 5.1-7.0, labels 5.55 / 6.4, columns 6.3); beat 3 workers 8.1-12.0 s (spin 8.1, headline 8.6, deck 8.85, figures 9.1-9.7, columns 9.6, band 10.1). Everything is settled by 10.6 s, so the last 1.4 s is a full held composition. Do not add `repeat:-1` loops: the timeline is paused and seeked.

## 7. Captions (NOT exercised in this build; profile values, ASSUMED)

Cream strip with an ink rule above, 42 px bold ink text, current word red, bottom band. This demo has no captions. If a voice is added, keep y 1370-1480 free and shift the footer line.

## 8. Sound (NOT exercised; profile values)

News-theme percussion at 108-128 BPM; SFX: typewriter on the columns, press roll on the spin, stamp hit with the shake. The sample is silent.

## 9. Scene recipes

### R1 Cover (beat 1, about 4 s)
Masthead strip, three stacked caps lines (ink / red key word / ink), red stamp "MINH HOẠ" across the corner of the deck rule, a Cambria deck, two typed columns, footer. Order: sheet spins in, masthead drops 24 px, headline lines rise, stamp slams with shake, deck, columns type.

### R2 Curve page (beat 2, about 4 s)
Two-line headline (red key word first), chart panel with the drawn curve, highlighter label on the peak with a red circle, ink label in the trough, mono axis words ("đầu thế kỷ", "nay"), two short columns, mono caption stating the line is illustrative.

### R3 People page (beat 3, about 4 s)
Two-line headline (red key word second), deck, row of 8 hard-hat figures where 3 turn to outlines, one mono caption, two columns, mustard band as the closing line, footer. The band lands last, so the final frame is the most complete.

## 10. Images

None used (optional in the brief): the halftone is one CSS dot pattern and the grain is a baked PNG. Make the grain with `ffmpeg -f lavfi -i color=c=0x808080:s=540x960 -vf noise=alls=40:allf=t+u,format=gray -frames:v 1 grain.png` (393 KB). If a hero halftone photo is added later, bake the halftone into the PNG (profile constraint) and keep generated images free of text, logos and real people.

## 11. Must not

- No emoji, gradients on text, glow, glass, rounded friendly UI, script fonts, `segoepr.ttf`.
- Red only for the stamp and ONE key word per page (the chart's red circle counts as the stamp-family mark and appears on the page whose key word is also red: keep it to one extra mark).
- No mustard text; no red text on mustard.
- No number on screen that is not stated by a source. A "Minh hoạ" chip in every dateline and a footer line are mandatory when content is illustrative.
- No text clipped by a mask on a held frame; no outgoing sheet visible more than 0.15 s after the next sheet starts.
- Shake is seeded and decays within 6 frames; no shake on text that is still typing.

## 12. Traps seen in real builds (this build: t138 demo, 2026-11-14, 12.0 s, 7.8 MB)

1. **Segoe is not condensed.** The first pass used the profile's Anton sizes (236 px for "DẦU MỎ", 150 px for "NGƯỜI LAO ĐỘNG"); the snapshot showed "DẦU MỎ" cut to "DẦU MC" and "NGƯỜI LAO Đ" at the right edge. Fixed at 196 px and 104 px (section 2). Always check the widest headline on a snapshot, not in the CSS.
2. **Caption line wrapped under a rule.** A 61-character mono caption at 30 px wrapped to two lines and sat on the next rule. Shortened to 33 characters ("Nét viền: chỗ trống sau suy thoái.").
3. **`inspect` content_overlap warnings (4) are the line masks.** The negative-margin `.ln` wrapper makes each headline line overlap its own mask. Lint: 0 errors, 0 warnings; validate: no console errors; inspect: 0 errors, 4 warnings, all of this kind, accepted.
4. **A class toggled with `tl.call` is not seek-safe.** The outline state of the figures was first written as `classList.add` at a timeline time; replaced by a tween of `backgroundColor` to the page colour (`rgba(241,232,212,0)`), which renders the same on any seek.
5. **The spin makes a short "empty desk" moment.** With the out (0.15 s) and the in (starts 0.1 s later, `scale .08`), the dark desk shows for about 0.2 s and the new page has only its masthead for about 0.5 s before the headline rises (headline starts 0.5 s after the spin). That is the longest sparse stretch and stays within the 0.5 s limit; do not delay headlines further.
6. **`frame_check.py` needs numpy**, which the machine lacked, so the check was replaced by an ffmpeg contact sheet (48 frames at 4 fps, 216 x 384 tiles) read by eye. Install numpy to run the scripted check.
7. **Font glyph test could not run** (section 2); diacritics were verified visually only.
8. **Render facts (hyperframes 0.7.26).** `render . -o ../sample-t138.mp4 --quiet`: 360 frames, 5 workers, 13.6 s wall, 7.8 MB, h264 1080 x 1920. `--resolution portrait` is not needed when the root is 1080 x 1920. GSAP was inlined from the CDN by the compiler (needs network at render time).
9. **Sizes under 30 px.** Only the 24 px mono footer; all other text is 30 px or more.
10. **Not measured:** counters (none in this build), caption timing, sound, ghosting beyond visual review.
