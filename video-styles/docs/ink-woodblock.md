# Style: ink woodblock (9:16 Vietnamese ink-and-seal history edition)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** slow history and heritage stories told as a sequence of 3 stages (origins, expansion, today): trade routes, a craft, a region's past, a cultural or philosophy explainer, a calm heritage promo. Strong with generous negative space and 2-4 short lines per scene. Not for numbers, charts, dashboards, breaking news, enforcement or anything loud. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample on topic shape t122 ("history of the Mekong delta rice trade told with ink illustrations", Jev fit 0.74). **Voice-over, word timing, captions and music were NOT exercised** (demo-only build). Everything about captions and sound below is from the profile, marked ASSUMED. No agy image was used (the image tool needs approval that was not available); all art is inline SVG with solid fills.

Content in the sample is generic and labelled "Minh hoạ" on screen (chip top-left on every frame, plus a line on the last scene). No real figure, date, company or price.

Profile source: `styles/profiles/ink-woodblock.yaml` (energy 2, light mode, BPM 64-88, signature moves: brush writes headline, seal stamp, scroll unroll). Anything the profile does not give is **ASSUMED**.

## 1. Tokens

```css
--bg:#efe6d4;     /* rice paper. L=0.783 */
--ink:#151311;    /* all text: 14.7:1 on bg */
--accent:#c0301f; /* vermilion: seals + ONE key word, >= 100 px or as seal fill. 4.52:1 on bg (hand-calculated, borderline: never below 48 px) */
--wash:#6d6a64;   /* 4.27:1 on bg: FAILS 4.5 -> shapes only (near mountain), never text */
--mist:#d9d2c3;   /* far mountain, mist band, rice-paper fibre tint #e4d9c2: shapes only */
--mid:#b9b2a4;    /* mid mountain: shape only */
/* paper (#efe6d4) on accent seal = 4.52:1 for the 56 px seal characters */
```
Ratios are hand-calculated with the WCAG formula (the helper scripts could not run); `hyperframes validate` reported "25 text elements pass WCAG AA". Jade (#4f7a68) was not used.
Rules: no gradients, no glow, no hard shadow. Mist and mountains are SOLID fills (no opacity below 100) so no held frame is under 90% opacity. Vermilion appears only as a seal and one word ("Tây", "bến").

## 2. Fonts (local files; the profile's Ma Shan Zheng, Cormorant Garamond, Noto Serif are not installed)

| Role | Profile asks | Used | Vietnamese check (ắằẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ đ) |
|---|---|---|---|
| Headlines (the "brush" voice) | Cormorant Garamond 600 / brush CJK | `cambriai.ttf` Cambria Italic 400 | renders all marks in the sample (Hạt, miền, Tây, chặng, Khai khẩn, phù, Chợ nổi, thuyền, ruộng, bến); not re-run with fontTools |
| Body, kicker, chip, seal text | Noto Serif / Be Vietnam Pro | `SegUIVar.ttf` weight 500-700 | all marks in the sample render (ạ, ơ, ư, ố, ẻ, ổ) |
| Never | | `segoepr.ttf` (no Vietnamese), `CascadiaMono` (not needed) | |

Honest note: no true brush font exists locally, so the "brush" feel comes from the italic serif plus a feathered left-to-right wipe and one drawn brush stroke, not from letterforms. A real brush display font would raise the style a lot.
Declare faces with `font-display: block`. Line-height >= 1.15 so tone marks are not clipped (headline 200 px / 1.15 held fine).

### Type scale (1080 x 1920, px)

| Token | Font | Size | Notes |
|---|---|---|---|
| `.tag` "Minh hoạ" chip | SegUI 600 | 32 | 3 px ink border, radius 8; top-left (96, 200), on every frame |
| cover headline | Cambria italic | 200 / 1.15 | 2 lines, "miền Tây" is 8 chars and fits 888 px |
| cover sub | SegUI 600 | 42 / 1.4 | 2 lines, width 860 |
| scene title | Cambria italic | 104 | one line ("Ba chặng của hạt lúa" fits) |
| kicker | SegUI 700 +0.1em caps | 32 | ink, not accent |
| entry title | Cambria italic | 70 / 1.2 | |
| entry body | SegUI 500 | 38 / 1.35 | width 700, one line each in the sample |
| finale headline | Cambria italic | 112 | 2 lines |
| seal | SegUI 700 | 56 in a 132 px square | inner 4 px paper outline at 112 px |
| footer line | SegUI 600 | 32 | the only small line ("Minh hoạ: không phải số liệu thật") |

Nothing below 32 px.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  platform top: empty (tag chip at y 200)
y 200  -1480 all text lives here
y 1480 -1920 platform bottom: decoration only (mountains, river, boat); no text except the 32 px footer at y 1432-1470
x 96   -984  text column (margin 96); timeline spine at x 150, text at x 240 (width 740)
```
Cover: headline y 380-830, brush stroke y 880, sub y 950-1070, land (mountains) from y 1230. Subject in the upper third; the lower third is land. Timeline: title y 320, three blocks at y 490 / 830 / 1170 (340 px pitch, last ends about y 1380), spine y 560-1240. Finale: scroll panel x 66-1014, y 260-1410 with 30 px ink rods at y 240 and 1394.

## 4. Layers, back to front

Each scene is a full-frame layer with its own solid paper background (`#s1`, `#s2`, `#s3`), so a scene reveal fully replaces the previous one. Inside a scene: paper fibre (34 short strokes, seeded rng, `#e4d9c2`) -> land (far mountain, mist ellipse, mid mountain, mist ellipse, near mountain, two ink pines) -> text -> seal. Global on top: `#tag` chip, `#ring` (ink-bleed edge). No flash, shake, fade-to-black or beat layer.

## 5. Components

- **Wipe text** `.wipe`: CSS mask `linear-gradient(90deg,#000 70%,transparent)` at `mask-size:400% 100%`; GSAP tweens `mask-position` 100% to 0% (power2.out, 0.8-1.3 s). Reads as ink flowing along a brush. Fully opaque at the end (position 0% shows the 70% solid part across the whole text).
- **Brush stroke**: a tapered closed SVG path (thick centre, pointed ends) revealed with `clip-path: inset(0 100% 0 0)` to 0 in 0.9 s.
- **Seal** `.seal`: vermilion 132 px square, radius 10, paper inner outline, 1 word of 3 letters ("Gạo"), rotated -3 deg. Stamp = visible at t, scale 1.4 to 1 and rotation -6 to -3 in 0.22 s `power3.in` (accelerates INTO the paper, no bounce).
- **Spine** (timeline): ink 8 px round path, `pathLength=1`, dashoffset 1 to 0 over 2.6 s `power1.inOut`; nodes are 40 px ink dots (scale 0 to 1, 0.3 s, power2.out).
- **Sampan**: ink silhouette (hull path + conical hat triangle) drifting on an ink river line; linear `none` ease, 4.4 s across.
- **Scroll**: two 30 px ink rods and 3 px ink side lines around a paper panel; unroll = `clip-path: inset(0 0 100% 0)` to `inset(0)` top to bottom.

## 6. Motion language

Energy 2. Eases: `power2.out` (reveals), `power2.inOut` (scroll), `power1.inOut` (spine), `power3.in` (seal only), `sine.inOut` (mist drift), `none` (boat, drift). No elastic, back, shake, flash or bounce. Mist bands drift continuously the whole time (sine.inOut over 12 s, +/- 100-200 px) so held frames are never dead; there is no beat pulse.

### Transitions used (profile vocabulary)
1. **Ink-bleed** (cover to timeline, 3.7-4.6 s, 0.9 s): next scene is clipped by `circle(r at 900px 366px)` (the seal's centre), r 0 to 1500 px, power2.out, with a 12 px ink ring of the same radius riding the edge. Driven by one tween on an object with `onUpdate` (works when seeked).
2. **Scroll-unroll** (timeline to finale, 8.5-9.4 s, 0.9 s power2.inOut).
Two languages in 12 s is the maximum; never add a third.

## 7. Scene recipes (S = scene start; sample timings)

### R1 Cover (0-4.6 s)
Land is on screen at frame 0 (no empty panel). Headline line 1 writes 0.3-1.5 s, line 2 0.8-2.1 s (feathered wipe). Brush stroke draws 2.0-2.9 s. Seal stamps 2.4 s. Sub wipes 2.6-3.6 s. Mist drifts throughout. Ink-bleed out from the seal at 3.7 s.

### R2 Three-stage timeline (4.2-8.9 s)
Title wipes 4.2-5.2 s. Spine draws 5.0-7.6 s. Entries at 5.2 / 6.3 / 7.4 s: dot pops, kicker fades 0.3 s, title wipes 0.8 s (+0.15), body wipes 0.8 s (+0.45). Sampan crosses the river at the bottom 4.4-8.8 s. Complete by 8.2 s, held 0.3 s before the unroll.

### R3 Scroll finale (8.5-12.0 s)
Unroll 8.5-9.4 s. Headline wipes 9.0 and 9.4 s ("bến" in vermilion). Boat drifts 9.0-12.0 s. Seal stamps 10.3 s. The last 1.5 s (10.5-12.0) hold the full composition with boat and mist still moving.

## 8. Captions (NOT exercised in this build)

Profile only (ASSUMED): no pill; 42 px (the 9:16 contract uses 56 px) 600 weight ink on a soft paper wash, current word vermilion (but vermilion is 4.52:1: keep it at 56 px, bold), bottom band y 1480 or higher up per `composition-contract.md` (bottom 440 px reserved). The finale panel bottom (rod at y 1394, footer at 1432-1470) is the only area near that band and must be moved up if captions are added.

## 9. Sound (NOT exercised)

Profile only (ASSUMED): guzheng, erhu or shakuhachi at 64-88 BPM; SFX brush stroke, paper unroll, one gong; seal stamps on downbeats. This sample is silent.

## 10. Images

No generated image was used. If one is added: agy ink-wash on cream paper, empty top third, no text, no faces, then place it inside the scroll panel only; never behind headlines. Keep pure SVG mountains as the fallback (they rendered at 0.9 MB for 12 s).

## 11. Must not

- Vermilion on anything but seals and one key word; never as text under 48 px.
- `--wash` (#6d6a64, 4.27:1) as text.
- Opacity fades on mist or mountains (use solid fills and move them).
- Bounce, shake, flash, fast cuts, neon, glass, gradients, charts, terminals, code, UI demos.
- A third transition language; a fade to black.
- `segoepr.ttf`.
- Child `visibility:visible` inside a hidden scene (see traps).

## 12. Traps seen in real builds (this build, 12.0 s sample)

1. **A child's own `visibility:visible` overrides a hidden parent.** The cover seal was set `visibility:hidden` at start and turned `visible` by its stamp tween; hiding `#s1` at 4.65 s did NOT hide it. `inspect` reported `text_occluded #seal1 inside #panel` at t=10-11.33 s and a content overlap with the timeline title at 4.67-8.67 s. Fix: add an explicit `tl.set("#seal1",{visibility:"hidden"},4.65)`. Re-render, the error disappeared from the sheet.
2. **Scene-3 art placed by guess left the scroll empty.** First build put the mountains at panel y 700 so about 340 px (y 800-1150) of the finale was blank and the footer line landed on the river. Moved the art svg to panel y 600, the boat to top 872, the seal to (780, 780) and the footer line below the panel (y 1432). Still about 270 px of intentional negative space between the headline (ends y 730) and the mountains (start y 1030): acceptable for this style, but check on the held last frame.
3. **Flat mist bands read as pills.** Rounded rects (1500 x 110, rx 55) looked like stickers on the mountains. Replaced by ellipses (rx 760, ry 48): reads as mist.
4. **Inspect noise.** `hyperframes inspect` gave 20 `container_overflow` warnings for intentionally oversized mountain paths, the river line, the drifting boat and fibre strokes (up to 758 px past the frame while the boat is off-screen). They are decoration that is meant to bleed; mark with `data-layout-allow-overflow` in a real build.
5. **Feathered mask wipes look like a ghost for 1 s.** While a wipe runs, the leading 30% of the text sits at partial opacity; at 1.0 s the cover sub is half-faded. All wipes end by 8.2 s (timeline), 3.6 s (cover), 10.4 s (finale), so held frames are solid. Do not hold a wipe-in-progress as a still.
6. **Contrast tokens.** Profile `wash` (#6d6a64) measures 4.27:1 on paper and `accent` 4.52:1: the first cannot be text, the second only at large sizes or as a seal fill with paper letters.
7. **Tooling.** In this environment `python3` and `node` scripts (including `frame_check.py`, `motion_tools.py image`) needed an approval that was not available, so frame checking was done by an ffmpeg contact sheet (1.5 fps, 27 tiles) and `hyperframes snapshot`/`inspect`. The renderer inlines GSAP from the CDN, so rendering needs network.

## 13. Measured result

1080x1920, 30 fps, h264, 12.000 s, 905 KB, silent. `hyperframes lint`: 0 errors, 0 warnings. `validate`: no console errors, 25 text elements pass WCAG AA. `inspect` after fix 1: see trap 1 (the error was fixed; the overflow warnings remain, trap 4).
