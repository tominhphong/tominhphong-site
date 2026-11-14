# Style: blueprint-engineering (detail, written from the demo build of 2026-11-13)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** "how a physical thing is put together" stories: hardware teardown and exploded views (the test shape t132, a camera module), architecture and building-system explainers, engineering specs with one or two measured numbers, "how it works" mechanisms. Not for people stories, crowds of numbers, news with one hero figure, or anything emotional. Tier 2 never widens tier 1.

**Status.** Demo-only build: one silent 12.0 s sample (1080 x 1920, 30 fps) on shape t132 (Jev fit 0.78). Voice-over, karaoke captions, pronunciation, music and SFX were NOT exercised, so this document has no caption or sound rules measured from a build; sections 7 and 9 only restate the profile and mark it ASSUMED. Everything else carries numbers measured on this build. Profile: `skill/references/styles/profiles/blueprint-engineering.yaml` (energy 2, dark mode).

**Marks.** ASSUMED = profile gives no value and this document invented one. SUBST = a named font is not installed, a local one replaces it. DEVIATION = knowingly differs from the profile.
- SUBST: profile IBM Plex Mono -> `CascadiaMono.ttf`; Archivo condensed -> `SegUIVar.ttf` 700 uppercase; Be Vietnam Pro -> `SegUIVar.ttf`.
- DEVIATION 1: profile palette allows "no fills"; parts carry an opaque fill equal to `--bg` (an occlusion mask, invisible as a colour) so hidden lines of the part below do not show through in the collapsed stack. See trap 3.
- DEVIATION 2: profile primary stroke 2 px; at 1080 x 1920 primary strokes are 3 px and construction strokes 1.5 px (ASSUMED, 2 px read thin on a phone).
- DEVIATION 3: profile title block is "top-right"; in 9:16 the top 200 px is the platform zone, so the title block sits at y 1380-1500.

## 1. Tokens

```css
:root{
  --bg:#0d3b6e;      /* profile bg */
  --ink:#e8f1ff;     /* profile ink       9.88:1 on bg */
  --accent:#ffd166;  /* profile accent    7.80:1 on bg */
  --mute:#859fbe;    /* profile mute (ink at 55%) 4.12:1 on bg: FAILS 4.5, so graphics only (construction lines), never text */
  --mute-t:#a6bad3;  /* ASSUMED: ink at 70% over bg, 5.67:1 on bg, the only grey allowed for text (kicker, footer) */
  --hatch:#446992;   /* ASSUMED: ink at 25% over bg, flat colour for the 45 deg hatch lines, graphic only */
}
```
Contrast: WCAG relative-luminance formula, computed by hand (bg L 0.0434, ink L 0.8729, accent L 0.6782, mute-t L 0.4792, mute L 0.3348). Rules: text colours only `--ink`, `--accent`, `--mute-t`. `--mute` is for lines. Yellow appears only on the highlighted part (lens), the measurement (dimension line and numeral) and the detail circle; never on headlines. Never lighten a text token to look softer: use the real `--mute-t`.
Grid: 24 px minor at ink 10%, 120 px major at ink 22% (one full-frame `linear-gradient` layer, no baked PNG needed; 4 gradients on one element rendered fine).

## 2. Fonts (glyph coverage)

| File | Role |
|---|---|
| `SegUIVar.ttf` | headlines (700, uppercase, 88 px), the dimension numeral (700, 60 px), the footer line (500, 26 px). Variable, declare `font-weight: 100 900`. |
| `CascadiaMono.ttf` | every label, kicker, title-block cell, callout (500, 30 px, +0.04em). Declare `font-weight: 200 700`. |
| `cambriai.ttf` | not used in this style. |
| `segoepr.ttf` | NEVER (lacks Ơ ơ Ư ư and dotted/hooked vowels). A handwritten note is not part of this style anyway. |

Diacritics check: a fontTools/cmap script could not be executed in this session (script execution was blocked), so coverage was verified on RENDERED frames instead (snapshot at 1920 x 1080 scale 1x): every string below rendered with its marks in both fonts, including Ắ Ả Ế Ệ Ẩ Ấ Ộ Ụ Ỉ Ẫ Ạ Đ Ø (not the full Vietnamese set): "HÌNH 1 · LẮP RÁP", "BẢN VẼ", "TỈ LỆ", "CHI TIẾT A", "CỤM THẤU KÍNH", "KHẨU ĐỘ", "ĐỘ DÀY", "CẢM BIẾN ẢNH", "KHUNG ĐẾ", "BO MẠCH", "MINH HOẠ", "Ø". Before reusing for new copy, run a cmap test on the new strings. `hyperframes` reported "Fonts: 2 loaded" (the two used).

## 3. Type scale, safe areas and grid (1080 x 1920)

| Role | Font, px |
|---|---|
| headline (2 lines, uppercase) | SegUI 700, 88 px, line-height 1.12, x 72, y 205-400 |
| kicker ("HÌNH n . ...") | Cascadia 500, 30 px, y 160 |
| callout label, title-block cell, stamp | Cascadia 500, 30 px |
| dimension numeral (big) | SegUI 700, 60 px, accent |
| dimension numeral (small, beat 1) | SegUI 600, 40 px, accent |
| footer line (the ONLY text under 30 px) | SegUI 500, 26 px, `--mute-t` |

- Frame: border at 48 px inset (4 px stroke), tick marks every 120 px, 14 px long (a 24 px tick touched the text at x 72: trap 1).
- Side margin 72, content width 936. y 0-200 platform zone: only the 30 px kicker at y 160. Drawing zone y 470-1330. Title block y 1380-1500 (3 cells 380 / 198 / 358 px + a stamp row). Footer y 1540. y 1560-1920 left as empty sheet (grid only) for the phone UI.
- Callout lanes: left labels x 72-340, right labels x 722-1008 (mono 30 px = 17.6 px per character, so 14 characters = 246 px). Leaders are horizontal rules with the label sitting 10 px above; the dot (6 px radius) sits on the part.

## 4. Layers, back to front

1. `#grid` (CSS gradients, fades in 0-0.5 s)
2. `#svg` > `#sheet` (frame, ticks, title-block lines), `#viewB` (construction lines, dashed axis, five parts, callout rules, dimension, yellow detail circle), `#viewC` (detail view: crosshair, rings, hatch, dimension)
3. `#txt` (all HTML text: kicker, headline, labels, numerals, title-block cells, footer)
Parts inside `#viewB` are in reverse order (last part first) so an upper part covers the part below.

## 5. Components

- **Part**: group with `sil` (opaque `--bg` silhouette, fades in as the part is drawn), `body` (side lines plus the front half of the bottom outline), `top` (top face outline), `det` (inner rings or inner rhombus, 2 px). Collapsed, only part 1's `top` is drawn; the other tops stay undrawn (dashoffset 1) until the explosion. Five parts used: cover glass (ellipse rx 190 ry 62, h 22), lens (rx 160 ry 52, h 64, three inner rings), sensor (rhombus 150 x 62, h 24), board (rhombus 140 x 58, h 18), base (rx 125 ry 42, h 56). Widths decrease downward so no lower top face peeks out around an upper part.
- **Callout**: horizontal leader rule 2 px, a 6 px dot on the part, a mono label "0n NAME" typed after the rule. The highlighted part uses accent for rule, dot and label.
- **Dimension**: 2 px line with filled triangle arrowheads (7 x 16 px), 1.5 px dashed-style extension lines in `--mute`, a numeral that counts up.
- **Title block**: 936 x 120 px, cells "BẢN VẼ 01/02", "REV A", "TỈ LỆ 5:1", then a 2 px outlined stamp "MINH HOẠ" and a mute note. The sheet number swaps 01/02 -> 02/02 on the third beat.
- **Detail circle**: yellow 3 px circle around the lens (r 176), then it expands to r 300 as the outer ring of the detail view and turns ink.
- **Hatch**: annulus r 250-300, `pattern` of 45 deg lines, 2 px, colour `--hatch`.

## 6. Motion language (timings measured on the 12.0 s sample)

- Easing: draws `power2.inOut` 0.4-0.65 s; leaders `power2.out` 0.4 s; the explosion `power3.inOut` 0.8 s with 0.04 s stagger per part; the detail-circle expansion `power3.inOut` 0.85 s; headlines `power3.out` rise 36 px, 0.55 s, 0.14 s between lines. No bounce, no flash, no shake.
- Draw verb: `pathLength=1` plus `stroke-dasharray:1; stroke-dashoffset:1`, tween the offset to 0. Dashed lines (axis, crosshair) cannot use it: grow them with `attr` on `y1/y2` or `x1/x2`, then march `stroke-dashoffset` linearly during holds (-78 over 3.3 s).
- Construction first: dashed axis and a 1.5 px guide ellipse draw 0.5-1.1 s, final 3 px strokes from 1.0 s. The guide and the dimension are erased (0.25 s fade) when the explosion starts.
- Text: typeIn = one span per character, opacity stepped 0 -> 1, 0.03-0.035 s per character (a 15-character label = 0.5 s).
- Counters: proxy object tweened with `onUpdate` writing text (0 -> 6,2 mm in 0.6 s; 0 -> 24,0 mm in 0.8 s); decimal comma. Both finish at least 0.4 s before the next cut.
- Micro-motion in holds: marching dashes only (axis, crosshair). No scale push-in, because HTML labels and SVG leaders would drift apart.

## 7. Captions

NOT exercised (demo build, no voice-over). Profile says: blueprint-blue bar at 88% alpha, 1 px ink top rule, 40 px karaoke, current word accent yellow. ASSUMED for 9:16: keep the bottom band y 1560-1920 free for it; the title block already ends at y 1500.

## 8. Scene recipes (sample timings, 12.0 s, three beats)

| Beat | Window | Content |
|---|---|---|
| R1 Draw the assembly | 0-3.6 s | grid fades in, frame draws 0-0.9, title block 0.25-0.9, headline 0.6-1.3, construction lines 0.5-1.1, parts drawn top-down every 0.2-0.4 s from 1.0 s, thickness dimension 1.9-3.1 s |
| R2 Exploded view | 3.6-7.7 s | parts separate along the dashed axis 3.6-4.4 s, tops and inner rings draw 4.0-4.9 s, five callouts 4.6 s onward every 0.3 s (rule, dot, label), lens turns yellow at 6.2 s, detail circle draws 6.9-7.55 s |
| R3 Detail zoom | 7.7-12.0 s | outgoing parts, labels, kicker and headline fade in 0.25 s; the circle expands 7.75-8.6 s; crosshair 8.1 s; rings 8.5-9.35 s; hatch 9.0-9.4 s; dimension 9.25-9.9 s; numeral counts 9.6-10.4 s; two callouts typed by 10.45 s; full composition held 10.5-12.0 s |

Pattern: **draw, explode, detail.** Every beat has one yellow element at most (lens, then the aperture ring and the dimension).

## 9. Sound

NOT exercised. Profile: ambient electronic or minimal orchestral 84-104 BPM, soft pencil and ruler scratches while drawing, paper slide on pans. ASSUMED: the three beats of the sample (3.6 s, 4.1 s, 4.3 s) sit at about 4 beats each at 100 BPM, so a downbeat lands near 3.6 s (explosion) and 7.7 s (detail).

## 10. Images

None used in this build (line art is vector). If a baked paper or cyanotype texture is wanted, one agy image at 8% opacity is enough (prompt: "cyanotype blueprint paper, blue mottling, faint fibre, no text, no objects"); never generate the drawings themselves.

## 11. Must not

- No solid fills except the `--bg` occlusion mask and the 25% hatch; no gradients on parts; no glow; no glossy render.
- No yellow on headlines or on more than one part at a time.
- No `segoepr.ttf`; no text under 30 px except ONE footer line.
- No bounce or overshoot; all motion along the dashed axis, a pivot, or a draw.
- No real company, product, price or spec; the generic content must carry "Minh hoạ" on screen (stamp plus footer line in this build, visible from 1.1 s to the end).
- Do not leave a label or leader beside the frame ticks (min gap 10 px to a 14 px tick).

## 12. Traps seen in real builds (this build, measured)

1. **Ticks touched the text.** Edge ticks 24 px long ended at x 72, the same x as the kicker, headline and left labels, so "HÌNH" looked struck through at y 160-168. Fix: ticks 14 px (end at x 62); keep content at x >= 72.
2. **Callout ran into the part and the frame.** "CỤM THẤU KÍNH" (13 characters x 17.6 = 229 px) started at x 770 and ended at x 1013, past the 1008 content edge, and touched the r 300 ring (ring x at y 1070 = 754 px). Fix: start at x 752, move the rule from y 1098 to y 1140 where the ring is at x 671.
3. **Hidden lines show through without an occlusion mask.** With line-only parts, the lens side lines (x 380, y 852-885) were visible through the cover glass in the collapsed stack. Fix: each part gets an opaque silhouette in `--bg`; it fades in over 0.2 s as the part is drawn. Side effect: the grid is hidden inside parts, which reads as intended drafting occlusion.
4. **Wide lower parts peek out.** A stack where a lower top face is wider than the upper part shows an undrawn-looking rim. Fix: widths decrease 190 -> 160 -> 150 -> 140 -> 125.
5. **The first second was empty.** In the first render the body zone (y 470-1330) held nothing from 0.5 to 1.5 s while only the frame and title block drew. Fix: construction lines at 0.5 s and the first part at 1.0 s (was 1.5 s). In the second render the body has content from 0.5 s.
6. **Counter timing.** The thickness numeral read 4.8 mm at 2.5 s and 6.2 mm at 3.0 s; it finishes at 3.1 s. The big numeral reads 10,1 at 9.5 s and 23,8 at 10.0 s and reaches 24,0 at 10.4 s, 0.1 s before the final hold. Keep at least 0.1 s of margin between the end of a count and the last-1.5-s window.
7. **Inspect false positive on headline.** Line-height 1.04 made the two headline lines' boxes overlap by 3 px and the inspector warned 4 times ("content_overlap"). Fix: line-height 1.12 plus `data-layout-allow-overlap` on the headline wrapper (it contains its own lines). After that: 0 layout issues.
8. **An empty `<audio>` breaks validate.** `<audio id="mix">` without `src` fails the HyperFrames contract; a silent video must have no audio element at all.
9. **`mute` grey is not a text colour.** Ink at 55% (the profile's mute) measures 4.12:1, below 4.5. The kicker and footer use `--mute-t` (ink at 70%, 5.67:1).
10. **Tooling in this session:** `frame_check.py` could not run (no `numpy` in the available Python and other interpreters needed approval). An ffmpeg contact sheet at 2 fps (24 frames, 216 px wide) was used instead; see `selfcheck.md`. A full run of `frame_check.py` is still owed.
