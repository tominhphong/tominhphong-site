# Style: cinematic product launch (9:16 Vietnamese edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** One hero object with one idea per shot: flagship hardware or a premium feature reveal (a camera lens, a device, a materials or finish story), brand promos, a "one thing, done beautifully" announcement. Needs a hero that can be drawn or shot cleanly on a quiet stage. Not for: dense feature lists, comparisons with many numbers, news with sourced figures, hype or loud energy, anything where text must carry more than about 8 words per beat. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built. Section 12 holds the traps seen in this build. Later builds append numbered fix sections; the newest wins.

**Status.** Written 2026-11-14 from ONE demo build: `samples/sample-t111.mp4`, 12.0 s, 1080 x 1920, 30 fps, silent, topic shape t111 (camera maker launches a cinema lens with an anamorphic look; Jev fit 0.75). **Voice, caption and sound rules were NOT exercised** (demo build, no voice-over, no music); sections 8 and 9 repeat the profile and are marked ASSUMED. All content on screen is generic and carries the label "Minh hoạ".

The look: a pure black stage, one soft blue vignette, one lens drawn in CSS on the centre axis, a horizontal blue-white streak through it (the anamorphic flare, the style's one light gesture), and at most one centred text block. Energy 2: no shake, flash or bounce.

## 1. Tokens

```css
--bg: #000000;                      /* flat stage + one vignette (accent at 7% alpha, ellipse 760 x 900 at 50% 37%) */
--ink: #f2f1ee;                     /* headlines          18.6:1 on bg (WCAG formula, computed by hand) */
--accent: #4a86ff;                  /* streak, brackets, ONE highlighted headline line   6.1:1 on bg (ok as large text) */
--mute: rgba(242,241,238,0.56);     /* sub line, tag      = #878785 on black, 5.8:1 */
--hair: rgba(242,241,238,0.12);     /* thinnest lens ring */
```
Measured contrast (hand-computed with the WCAG relative-luminance formula, black bg): ink 18.6, accent 6.1, mute (0.56 alpha) 5.8. `hyperframes validate` reported "20 text elements pass WCAG AA". Ink on an accent fill is only 3.0: never put ink text on an accent fill; black on accent is 6.1.
Three colours only (bg, ink, accent). Every grey is an ink alpha step (lens rings use alpha 0.06 to 0.32). Light variant (bg #f2f1ee, ink #1a1b1f, accent #1f5fd6) was not built.

## 2. Fonts

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headlines, sub, tag | Inter 600-700, Be Vietnam Pro for captions (neither installed) | `SegUIVar.ttf`, weight axis 300-700; headlines 700, `letter-spacing:-0.03em`; sub 400 with 0 tracking; tag 600 | The owner docs measured all 36 test letters present with fontTools. In this build fontTools could not be run (the shell blocked Python), so the check was visual: ó ệ ả ạ ầ ố ộ ờ ế rendered correctly in the 1080 x 1920 snapshots (Góc nhìn điện ảnh, Ống kính, Khung hình rộng, Nén ngang, ánh sáng kéo thành vệt, nội dung giả định, Minh hoạ) |
| Numerals | none | not used (no counters in the demo); `CascadiaMono.ttf` copied but unused | not needed |
| Never | | `segoepr.ttf` | lacks Vietnamese letters |

Declare `font-display: block`; the variable face with `font-weight: 300 700`. The profile's "Inter" is not installed: SegUIVar is the stand-in, so every px size below is tuned to Segoe's width.

### Type scale (1080 x 1920, px)

| Token | Size / line | Notes |
|---|---|---|
| `.t1` hero line | 108 / 1.12 | 2 lines of <= 9 characters ("Góc nhìn" / "điện ảnh"), centred, -0.03em |
| `.t2` spec line | 88 / 1.12 | 2 lines; second line in `--accent` ("2,39 : 1") |
| `.t3` end word | 150 / 1.1 | ONE word, "Anamorphic" is 10 letters and measured about 790 px wide at 150 px, inside the 888 px column |
| `.sub` | 40 / 1.25, 400, `--mute` | one line, at most 40 characters ("Nén ngang 2×, ánh sáng kéo thành vệt" is 36) |
| `#tag` footer | 30 / 1.2, 600, `--mute`, +0.02em | "Minh hoạ · nội dung giả định"; the ONLY text under 38 px |

Line-height >= 1.1 so Vietnamese tone marks are not clipped; no `overflow:hidden` on any text box (the build uses no line masks).

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  top platform UI: empty
y 344  -1056 lens stage (lens 560 px, centre x 540; centre y 700 in B1 and B3, 640 in B2; scale 0.62-1.27)
y 454  -826  2.39:1 frame (888 x 372, x 96-984), B2 only, centred on the lens
y 1000 -1220 B2 text block;  y 1090 -1400 B1 text block;  y 1130 -1290 B3 word
y 1440 -1470 #tag footer
y 1480 -1920 bottom platform UI: empty
x 96   -984  text column (888 px), always centred (text-align:center)
```
Empty space measured by eye in the snapshots: about 55-60% of the frame is black at every held moment (profile asks >= 40%). Only one text block is on stage at a time.

## 4. Layers, back to front

`#vig` (one static vignette) -> `#lens` group (halo, barrel ring, knurled grip ring, two hairline rings, glass with oval highlight, focus dot and light sweep, then the streak on top) -> `#frame` (2.39:1 hairline rectangle with four accent corner brackets, SVG strokes drawn with `stroke-dashoffset`) -> three text blocks `#b1 #b2 #b3` -> `#tag`. No flash, no pulse, no caption layer, no fade layer: the video starts and ends on a full composition.

## 5. Components

- **Lens (the hero).** 560 px; all CSS: ring borders in ink alpha, a `repeating-conic-gradient` grip (1.5 deg on / 3.5 deg off) masked to a ring, a glass disc with a radial accent gradient and an inset accent glow, and a VERTICAL OVAL highlight (50 x 150 px, rotated 14 deg): the oval, not a round bokeh, is what says "anamorphic". One light sweep (70 x 420 px band at 22 deg, 30% ink) crosses the glass twice in the video.
- **Streak.** A 6 px line, 1500 px wide (overscan beyond the 1080 frame), gradient transparent / accent / ink at the centre / accent / transparent, plus a 120 px tall soft halo under it. It lives inside the lens group, so it travels and scales with the lens. Its `scaleY` grows 1 -> 1.5 -> 2.2 as the story advances.
- **Frame.** 888 x 372 (2.39:1), `--mute` 2 px stroke, corner brackets 5 px in accent; drawn with `pathLength=1` and dashoffset 1 -> 0.
- **Text blocks.** Centred, never in a corner, at most 3 lines (two headline lines plus one sub).

## 6. Motion language

Energy 2. Allowed eases: `expo.out` (streak sweep), `power3.inOut` (lens moves), `power3.out` (text rises, bracket draw), `power2.in` (exits), `power2.out` (final push-in), `sine.inOut` (holds). Nothing is linear and nothing bounces.

- **One persistent hero (match-move).** The same lens element moves through all three beats: scale 0.94 -> 1.02 (hold), 0.62 (spec slot), 1.2 -> 1.27 (end). It never cuts or rebuilds. 
- **Hold with micro-motion.** Every hold has something alive but quiet: lens push of 0.04-0.08 in scale over 3-4 s, the oval drifting 14 px, a light sweep. No frame is fully frozen.
- **Rise with overlap.** Text enters `y 50 -> 0`, opacity 0 -> 1 and blur 8 px -> 0 in 0.7 s `power3.out`, children staggered 0.08 s; blur is removed with `clearProps:"filter"` on complete.
- **Exits.** 0.5 s, `y -30`, opacity 0, `power2.in` (about 70% of the entrance).
- **Transitions as built.** B1 -> B2 (3.2-4.5 s): text leaves while the lens match-moves to its smaller slot and the 2.39:1 frame draws around it. B2 -> B3 (6.9-8.2 s): scale-through; the frame grows 1 -> 1.5 and fades while the lens grows 0.65 -> 1.2, and the end word settles from scale 1.04. Zero hard cuts.

## 7. Scene recipes (12.0 s total; times measured from the build)

### R1 Hero (0.0-3.6 s)
Frame 0 is already finished: lens, thin streak, headline "Góc nhìn điện ảnh", sub, tag. The streak sweeps 10% -> 100% width in 1.2 s `expo.out` from t = 0 and the lens pushes 0.94 -> 1.02 over 3.35 s. Text leaves 3.2-3.7 s.

### R2 Spec (3.6-7.4 s)
Lens match-moves to scale 0.62, y -60 (3.35-4.5 s). Frame draws 3.9-4.9 s, brackets 4.3-4.9 s, streak thickens (scaleY 1.5). Text rises from 3.95 s ("Khung hình rộng" / "2,39 : 1" / sub), settled by about 4.8 s, then holds about 2 s until 6.9 s. One idea: the wide frame.

### R3 End card (7.4-12.0 s)
Scale-through at 7.0-8.2 s; the single word "Anamorphic" rises from 7.7 s and is fully settled by 8.6 s; then a 3.4 s hold with the lens easing 1.2 -> 1.27 (`power2.out`, decelerating) and a second light sweep at 9.0 s. The last 1.5 s (10.5-12.0 s) show the full composition: lens, streak, word, tag.

## 8. Captions (ASSUMED, not exercised: demo build has no voice)

Profile: no pill, 44 px (the vertical bottom band here would be y 1370-1480), ink with soft shadow, unread words mute, current word ink. Not built or measured. Note the conflict seen: the end word sits at y 1130-1290 and the tag at y 1440, so a caption band at 1370-1480 collides with the tag; a real build must move or drop the tag line.

## 9. Sound (ASSUMED, not exercised)

Silent build. Profile: 90-110 BPM family, about one soft cue per scene, subtraction audit. The three reveal moments (streak sweep 0 s, frame draw 3.9 s, end word 7.7 s) are the natural cue points.

## 10. Images

No agy image used; the hero is drawn in CSS because geometry must be exact (concentric circles, a true 2.39:1 box). If a photo is wanted later: "a cinema lens on a pure black stage, centred, soft contact shadow, anamorphic blue streak flare, no text, no logo, no person". Never a real brand.

## 11. Must not

- No emoji; no corner text; no kicker or HUD chrome; no second colour besides the accent; no glow beyond the one accent halo and glass inset; no glass cards; no orbs, grids or patterns on the stage.
- No shake, flash, bounce, elastic or linear motion; at most 2 hard cuts (this build used 0).
- No real company, product, price or spec: invented values are labelled "Minh hoạ".
- No text under 38 px except the single 30 px footer line.
- Do not use `segoepr.ttf`.
- Do not put ink text on an accent fill (3.0:1).

## 12. Traps seen in real builds (from THIS build)

1. **Text gap between beats.** First render had no text on screen at 3.7-4.3 s and 7.4-8.0 s (0.6 s each) because the next block waited for the lens move to finish. Rule: start the next block's rise at most 0.25-0.3 s after the previous one ends (fixed: B2 at 3.95 s, B3 at 7.7 s); the lens carries the gap, but keep it under 0.5 s.
2. **Overlapping tweens on the persistent hero.** The lens scale tweens overlapped by 0.15 s and 0.6 s (lint `overlapping_gsap_tweens`, 2 warnings). Rule: end each push-in tween 0.05 s before the next move starts (3.5 -> 3.35 s and 2.6 -> 1.95 s); lint then reported 0 warnings.
3. **Frame 0 must be finished.** Starting with the headline faded in would give a black first frame. Rule: text and tag are visible at t = 0; only the streak and push-in animate from the first frame.
4. **Blur left on text.** A blur tween leaves `filter` set; the held frame is then slightly soft. Rule: `clearProps:"filter"` in `onComplete`, and keep blur <= 10 px.
5. **Streak on a scaled hero.** The streak inside the lens group scales with it, so at 0.62 it is only 3.7 px thick and nearly vanishes; it was compensated with `scaleY 1.5` at 4.3 s. Rule: re-thicken the streak whenever the lens scale drops.
6. **Weak sub line.** The 40 px mute sub (5.8:1) is legible but visibly weaker than the headline in the contact sheet; keep it to one line and do not shrink below 40 px.
7. **Tools.** `hyperframes@0.7.26`: lint 0 errors 0 warnings (after fix 2), validate no console errors, inspect 0 layout issues across 9 samples, render 12.0 s in about 10 s, 1.6 MB. In this environment `frame_check.py` failed (no `numpy`) and `motion_tools.py probe` was not permitted to run, so the frame check was done with ffmpeg contact sheets read by eye and probing with ffprobe. Compound shell commands (`cd && ...`, `;`) and `sed -i` were blocked: run tools as single commands and edit with the Edit tool.
