# Style: cinematic-technology (9:16 demo edition, shape t111)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Product news where the product is an image-maker's tool and the feeling matters more than the numbers: a lens, camera, monitor, microphone or audio launch (shape t111: "camera maker launches a cinema lens with anamorphic look", Jev fit 0.89), premium brand films, creator tools. Works with one hero object plus 3 spec readouts. Not for data dashboards, charts, code or terminals (profile `avoid`), enforcement or sad stories. Tier 2 never widens tier 1.

**Status.** Written 2026-11-13 from ONE 12 s silent demo (`samples/sample-t111.mp4`). There is no owner document before this one. Voice-over, captions, sound and word timing were NOT exercised (demo build): sections 8 and 9 are the profile's rules, untested. Everything marked ASSUMED is invented here; MEASURED means taken from this build.

Profile: `skill/references/styles/profiles/cinematic-technology.yaml` (energy 3, dark). Format 1080 x 1920, 30 fps. Content on screen is generic and labelled "MINH HOẠ"; no real brand, price or spec.

DEVIATION 1: profile typography names Manrope / IBM Plex Mono / Be Vietnam Pro; none installed. SUBST: SegUIVar (weights 300 and 600), CascadiaMono, no third font.
DEVIATION 2: profile says letterbox 2.0:1 on film shots. In 9:16 a 2:1 band is only 540 px tall; the film shot is full-bleed vertical and the letterbox idea survives only as the shutter-close bars (section 7).
DEVIATION 3: profile headline 64 px; this build uses 80 px (the profile maximum) for a phone screen.

## 1. Tokens

```css
:root{
  --bg:#050608;     /* 17.8:1 with ink; page and void */
  --ink:#f0f0f0;    /* 17.8:1 on bg (hand-computed, WCAG formula) */
  --sub:#c9cbcd;    /* sub-line, 12.4:1 on bg */
  --mute:#8e9093;   /* SOLID colour, not rgba: 6.2:1 on bg; labels and footer */
  --accent:#4da3ff; /* 7.7:1 on bg; readout values and streaks only */
  --warm:#f2a65a;   /* 10:1; bokeh fill only, never text */
  --hair:#4a4e55;   /* 1 px frames; decoration, no contrast need */
}
```
Contrast values are hand-computed (no script could run in this session); `hyperframes validate` reported "15 text elements pass WCAG AA". Imagery carries the colour (teal and orange grade); the accent blue is used only for the streak, the readout numbers and the focus box. Mute is a solid hex: an rgba mute dips under 90% opacity on a bright frame and a text colour must never be an animated-opacity element at rest.

## 2. Fonts

| File | Missing glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 for every word on screen (seen rendered: Ố, ệ, ạ, ỷ, ẩ, ư, ơ all correct in snapshots; fontTools test not run) | headlines weight 300, labels weight 600 |
| `CascadiaMono.ttf` | 0 for the digits, "T", "mm", "×", "MINH HOẠ" (seen rendered) | readout values 84 px, footer label 30 px |
| `cambriai.ttf` | not used | free for one quoted line, unused here |
| `segoepr.ttf` | 92 missing | never used |

Declare the variable font with `font-weight:100 900` in `@font-face`, otherwise weight 300 snaps to regular. Headlines carry `letter-spacing:.04em` (credit-like). Uppercase "MINH HOẠ" in mono with `.12em` tracking keeps the dot-below under the Ạ legible at 30 px.

### Type scale (1080 x 1920, MEASURED from CSS)
| Role | Font | px | Weight |
|---|---|---|---|
| Headline (credit) | Seg | 80 (max by profile) | 300 |
| Sub-line / kicker | Seg | 44 | 300 |
| Readout label | Seg | 34 | 600 |
| Readout value | Casc | 84 | 400 |
| Footer "MINH HOẠ" | Casc | 30 | 400 |
Nothing is under 30 px. The profile's 64 px is too small on a phone; 80 px light still reads because of 17.8:1 contrast.

## 3. Safe areas and grid
- Side margin 72, content width 936. y 0-200 empty. Kicker y 206.
- Credit block (headline + sub-line): left 72, top 1390 (was 1260 and collided with the lens barrel, see traps). Ends about y 1600.
- Viewfinder frame y 330-890 (936 x 560); readout frame y 960-1520 (3 rows x 186).
- Footer label y 1716. y 1780-1920 empty (platform UI). Right rail x 960-1080: no text.

## 4. Layers, back to front
1. `#cam` camera group: the lens still (agy, 1200 x 2120 oversized box, `object-fit:cover`), dolly 1.0 to 1.06.
2. `#vig` radial vignette, `#dim` black layer (opacity 0 to 0.62 behind the panel).
3. `#streak` baked PNG 2400 x 120 (ffmpeg `geq`, blue core, no live blur), `#streak2` the same PNG, 936 px wide.
4. Beat A credit, beat B panel, beat C credit.
5. Shutter bars `#barT`, `#barB` (960 px each).
6. `#grain` baked noise PNG 540 x 960, screen blend 7%, position jittered with discrete `tl.set` every 0.1 s.
7. `#fade` black start fade, `#foot` label (z 50, above the bars so "MINH HOẠ" never disappears).

## 5. Components
- **Thin frame:** 1 px `--hair` border, no fill, no radius, no shadow (profile: "no cards").
- **Viewfinder:** dark `#0a0c10` field, three stretched ovals (anamorphic bokeh: 200 x 300, 90 x 140, 110 x 170, radial gradients, warm / blue / teal), focus box = four 44 px corner brackets, 3 px ink.
- **Readout row:** 186 px high, label left (mute 34 px), mono value right (84 px, accent number + ink unit), 1 px hairline below.
- **Streak:** one baked PNG used horizontally only.

## 6. Motion language (MEASURED)
- Easing: entrances `expo.out`, handoffs `power2.inOut`, counters `power3.out`, streak `power2.inOut`, camera `none` (dolly) or `power1.inOut` (pan). No bounce, no overshoot.
- Camera: beat A scale 1.00 to 1.06 over 4.6 s; beat B panel scale 1.00 to 1.03 over 3.4 s; beat C x pan 0 to -40 px over 3.7 s. Adjacent beats never repeat the same move.
- Rack focus: image `blur(0) -> blur(12px)` and panel `blur(12px) -> blur(0)` in the same 0.8 s window (3.9-4.7 s). Only two filtered layers exist at any time; the panel's filter is set to `none` at 4.75 s and the image's blur is cleared at the shutter cut.
- Counters: three values tick through `onUpdate` on a proxy object (T 8.0 to 2.0, 18 to 50 mm, 1.0 to 1.8x), 0.8 s each, staggered 0.15 s, all final by 6.0 s and then held 2.2 s.
- Focus box: scale 1.3 to 1 in 0.3 s `power3.out` at 5.0 s, then drifts with the subject (x +30, y +20 over 1.8 s).
- Streak flare: 1.0 s sweep, fades 0.25 s after; used at 0.45 s (opening), 6.0 s (inside the panel, 0.7 s, width 936) and 8.9 s (closing).
- Shutter close: bars to centre in 0.28 s `expo.in` (8.05 s), content swaps under black at 8.36 s, bars open in 0.45 s `power2.out` from 8.5 s. Black-ish time is about 0.2 s.

## 7. Scene recipes (S = beat start; every tween start clamped at 0)
Whole sample = 3 beats, 12.0 s.

### R1 Opening hero (0-3.9 s)
Black fade 0.7 s over the lens still; streak sweeps across the lens axis at 0.45 s; credit headline rises out of its mask at 0.9 s (0.9 s `expo.out`), sub-line at 1.1 s; hold (dolly keeps moving) until 3.75 s; both lines exit up in 0.3 s.

### R2 Spec panel with rack-focus handoff (3.9-8.0 s)
Handoff as section 6. Kicker "Nhìn qua kính anamorphic", viewfinder with focus box, three readouts. A mid-panel streak at 6.0 s. The lens still stays behind the panel at 62% black dim and 12 px blur (a background, not a ghost).

### R3 Shutter close and calm ending (8.05-12.0 s)
Shutter close, image un-blurred, headline "Nhìn như phim." and sub-line, one closing streak at 8.9 s, then 2.1 s of held composition with the pan still running. The last 1.5 s (10.5-12.0 s) is the full composition: lens, credit, footer.

## 8. Captions
NOT exercised (demo, silent). Profile rule, untested: no pill, 42 px Be Vietnam Pro 500 (here the replacement would be SegUIVar 600) with soft shadow, bottom band. Because the credit sits at y 1390-1600, a caption band must go at y 1620-1700, under the credit and above the footer, or the credit must move up.

## 9. Sound
NOT exercised (demo, silent). Profile: cinematic ambient with piano and strings, shutter-click SFX on the shutter close, soft whooshes on streaks. The streak at 0.45 s, 6.0 s, 8.9 s and the shutter at 8.05 s are the natural sync points.

## 10. Images (agy)
One agy still, 71 s: matte black cinema lens, three-quarter, blue anamorphic streak across the glass, teal-orange grade, empty black top and bottom. The prompt asked for the streak IN the image; after `cover` scaling by 1.5625 it lands at y about 959, so the baked streak PNG sits at top 900 (centre 960) and passes exactly through it. Always read the generated still and align the overlay to it. No text, logo or real person was in the image.

## 11. Must not
- No headline above 80 px, no bold weight above 600, no bounce or elastic.
- No more than two blurred layers at once; never leave a filter on when the tween ends.
- No neon palette, no flat vector illustration, no cards with fill and shadow.
- No live CSS blur on streaks, grain or bokeh; bake them to PNG.
- No chart, code or terminal scene.
- No real brand, price or spec on screen; "MINH HOẠ" visible on every frame.
- No text colour that is an rgba with alpha under 0.9.

## 12. Traps seen in real builds (this build, 2026-11-13, 12.0 s sample)
1. **File size.** The HyperFrames render was 25.9 MB, over the 15 MB limit, because of fine grain on a dark frame. Re-encoding with `ffmpeg -crf 25 -preset slow -pix_fmt yuv420p` gave 1.6 MB with no visible loss on the contact sheet. Rule: always re-encode the render; do not raise grain above 7%.
2. **Credit collided with the hero.** At top 1260 the headline overlapped the lens barrel's lower ring (visible in the 2.5 s and 10.5 s snapshots). Moved to top 1390, clear of the lens (lens ends about y 1300 at 1.06 scale).
3. **Streak misaligned with the image.** The first guess (top 870, centre 930) was 30 px above the streak painted in the still (y about 959). Rule: compute the position after cover-scaling and camera scale, not from the raw image.
4. **Inspect false errors on masked entrances.** `hyperframes inspect` reported 4 errors and 2 warnings at t = 0.67 s and 8.67 s ("clipped_text", "content_overlap") although `data-layout-allow-overflow` was on both the mask and the text; these are lines waiting below their mask before the rise. Hold frames (2.5, 5.2, 6.5, 10.5, 11.8 s) were clean. Fix tried: `visibility:hidden` until entry and `display:none` on the outgoing credit block (this removed the A-versus-panel overlap warnings but not the pre-entrance ones). Decide by looking at snapshots.
5. **Overlapping tweens.** Lint warned twice that the streak's fade-out overlapped its sweep (1.25 s vs 1.45 s, 9.70 s vs 9.90 s). Fix: start the fade exactly at the end of the sweep (1.46 s, 9.91 s).
6. **Handoff ghost.** The lens stays visible behind the panel for the whole beat B (blur 12 px, 62% dim); the outgoing credit is gone in 0.3 s (3.75-4.05 s), inside the 0.15 s ghost budget only after the 4.1 s hidden set; one contact-sheet frame at about 4.05 s shows the sub-line half-masked. It lasts about 2 frames.
7. **Black frame at the shutter.** 1 s sampling shows one fully black frame (about 8.0-8.4 s window): by design, about 0.2 s with the footer still on top. It would fail a stricter "no empty frame" check; if so, shorten the hold under the bars.
8. **Counters mid-count.** At 4.7-4.9 s the panel shows the start values (T 8.0, 18 mm, 1.0x) for 0.2 s before ticking; counting is finished by 6.0 s. Start the count the moment the panel sharpens, not 1 s later (the focus box already waits for 5.0 s).
9. **Tooling.** `frame_check.py` needs `numpy`, which was not installed, so it did not run; the check was done by hand on a 1 fps contact sheet and a 10 fps handoff sheet (`samples/t111/fc-sheet.jpg`, `fc-handoff.jpg`). Install numpy before the next build.
10. **Text overlap by streak.** The mid-panel streak (6.0-6.9 s) crosses the "Tiêu cự" label for about 0.3 s. Move it to the gap between the viewfinder and the readouts (y about 925).
