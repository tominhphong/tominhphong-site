# Style: wpa-screenprint (detail, written from the demo build of 2026-11-14)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Calm, civic, "an event opens / a place is worth visiting" stories where a landscape, a map or a route is the natural picture: museum and exhibit openings, history stories, parks and public-service announcements, travel promos. The style carries topic shape t080 ("museum exhibit on ancient maps opens this month", Jev fit 0.67) well because a map is itself a flat printed layer. Not for urgent, bad-news, number-heavy, UI/code or fast-energy stories (profile `avoid`: terminal, code, ui-demo). Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: one silent 12.5 s sample (1080x1920, 30 fps, 2.9 MB), `samples/sample-t080.mp4`. NOT exercised: voice-over, word timing, music, karaoke captions, any full 45-60 s video, generated images (agy was not used; all art is flat SVG). Sections on captions and sound are therefore profile-derived, not tested. Contrast ratios in section 1 were computed by hand with the WCAG formula (python and node were not runnable in this session); the HyperFrames `validate` contrast audit reported false positives, see traps.

Profile: `skill/references/styles/profiles/wpa-screenprint.yaml` (energy 2, light). Marks: **ASSUMED** = invented here, the profile gives no value. **SUBST** = font substitute. **DEVIATION** = knowingly differs from the profile.
- SUBST: Big Shoulders Display / Stardos Stencil / Libre Franklin are not installed. SegUIVar 800 caps replaces the display caps (a stencil look was not possible), CascadiaMono the kicker and label, cambriai italic the one slogan line.
- DEVIATION 1: the profile says "three inks per scene". Each scene here has 3 body inks plus the accent spot colour plus the ink for panels and silhouettes (see section 5).
- DEVIATION 2: the profile wants the title panel above a caption band. There was no caption band in the demo, so the panel sits at y 1210-1650.

## 1. Tokens (contrast measured by hand, WCAG formula)

```css
:root{
  --paper:#eadfc6;   /* bg, L 0.743 */
  --ink:#2b2a28;     /* L 0.023 ; 10.8:1 on paper; paper on ink 10.8:1 */
  --accent:#c4572f;  /* sun, route, ONE key word. 3.35:1 on paper, 3.24:1 on ink: text >= 100 px only */
  --accent-dk:#8f3a1c; /* ASSUMED: accent for small text, 5.7:1 on paper (unused in the sample) */
  --sage:#6f8a6a;    /* FILL ONLY: ink on sage 3.8, paper on sage 2.9 */
  --slate:#3f5a6b;   /* fill; paper on slate 5.5:1 */
  --sand:#d8b77a;    /* fill and sand-on-ink text; ink on sand 7.5:1; sand on ink 7.5:1 */
}
```
Rules: small text only ink on paper, ink on sand, paper on ink, sand on ink (all >= 7.5). Accent text only at 124 px on the ink panel (3.24:1 clears the 3:1 large-text bar). Never put text on sage or on accent. Never lighten a token.

## 2. Fonts

| File | Role | Vietnamese check |
|---|---|---|
| `SegUIVar.ttf` | caps titles 800 (76-124 px) | variable wght axis, weight 800 renders bold; every letter in the on-screen text (Ả Ồ Ổ Ể Ư Ờ Ạ and lower case) rendered correctly in snapshots; `hyperframes snapshot` said "Fonts: 3 loaded". A fontTools glyph dump was NOT run (python blocked). |
| `CascadiaMono.ttf` | kicker and "MINH HOẠ" label, 32 px, +0.06-0.08em | rendered correctly (Ể Ã Ạ visible) |
| `cambriai.ttf` | the one italic slogan, 48 px | rendered correctly (ì ê ự visible) |
| `segoepr.ttf` | NOT used (lacks Vietnamese letters) | - |

Declare the real italic with `font-style:italic` in `@font-face`, otherwise the browser fakes it.

## 3. Type scale, safe areas and grid (1080 x 1920)

- Paper border: 44 px paper strip plus a 6 px ink line (`#frame1`, `#frame2`, z 30/31). Everything inside it; layers are 1320 px wide, offset -120 px, so parallax drift never shows an edge under the border.
- Label chip "MINH HOẠ": x 90, y 96, 32 px mono, sand on ink. Top 0-200 otherwise empty.
- Art zone y 200-1200. Title panel: x 60, width 960, 6 px ink border plus a 6 px sand inner rule (outline offset -22). Panels at y 1210-1650 (S3), 1230-1630 (S1), 1290-1620 (S2).
- Bottom 1650-1920: art only (ink foreground hills), no text.
- Type: kicker 32 px mono; title 124 px SegUI 800 caps (one line, `white-space:nowrap`); S2 two-line panel 76 px; slogan 48 px italic. No text below 32 px. Widest line: "BẢN ĐỒ CỔ" at 124 px is about 750 px wide, inside the 872 px inner width.

## 4. Layers, back to front

1. `#root` paper. 2. Scene art: S1 `#clouds`, `#sun1` (rays group + disc), `#far` (sand), `#mid` (slate), `#hill` (sage), `#fg` (ink, 4 pines). 3. S2/S3 `#s2bg` (full paper rect), `#s3lay` (`#s3sun`, `#s3hill` sage + slate, `#s3fg` ink), `#map` 900 x 980 (slate sea, sage and sand land, paper graticule, dashed accent route under an SVG mask, compass). 4. Panels `#p1 #p2 #p3`. 5. `#chip` (z 40). 6. `#grain` (z 35, baked `img/grain.jpg`, `mix-blend-mode:multiply`, opacity .16; white base plus ffmpeg `noise`, so it only darkens). 7. Border frames.

## 5. Components

- **Layered landscape**: 5 flat SVG layers, each one ink, no shadows, no gradients. Sun = accent disc plus 18 sand triangle rays (built in JS before the timeline).
- **Title panel**: solid ink (S1, S3) or sand (S2), kicker + caps + optional italic line.
- **Map sheet**: slate sea, sage and sand land, paper 2 px graticule at 45 %, 8 short paper wave strokes, 16 px ink border, compass (paper disc, ink 4-point star, accent hub).
- **Route**: 12 px accent, dash 26/20, revealed by animating a white 30 px stroke in an SVG `mask` with `pathLength=1`. Start dot filled accent, end dot paper ring.
- **Ink count (DEVIATION 1)**: S1 = sand, slate, sage + accent sun + ink foreground; S2 = slate, sage, sand + accent route + ink border. It still reads as three muted inks because accent is one spot and ink is the line colour.

## 6. Motion language (energy 2)

- **Ink-layer print**: each layer `fromTo` opacity 0 to 1, y 4 to 0, 0.3 s `power2.out`, staggered 0.3 s (sun 0.0, far 0.3, mid 0.6, hills 0.9, foreground 1.2).
- **Parallax drift** over the scene, linear: clouds -30 to +40 px, sun -6, far +20 to -8, mid +40 to -16, hills +70 to -30, foreground +100 to -44 (about 0.2 : 0.5 : 1 : 1.4 of the hill value). Rays rotate 5 deg over 5 s (the profile says 2 deg per bar).
- **Panel rise**: `y 800 to 0`, 0.8 s `expo.out`. Panel exit: 0.3 s `power3.in` to y 800 (must start at 800, see traps).
- **Scene change S1 to S2**: panel drops (4.6), paper rect fades in over 0.14 s (4.84), S1 hidden at 5.0, then the map prints (opacity 0.3 s).
- **Match-move S2 to S3** (8.8): map scales 1 to 0.62 and moves y +20 over 0.9 s `power3.inOut` while panel 2 drops; sun, hills, foreground print behind it (9.3, 9.6, 9.9), panel 3 rises at 9.8. Then map creeps 0.62 to 0.65 until the end, rays rotate 4 deg, hills drift 50 px: nothing is frozen in the last 1.5 s.
- No bounce, shake, flash, slam. Only `expo.out`, `power2.out`, `power3.out/in/inOut`, `sine.inOut`, `none` (drift).

## 7. Captions (not exercised)

No captions in the demo. Profile says: solid ink panel, paper-colour 42 px text, current word in accent, bottom band. Untested; accent on ink is 3.24:1, so a current-word accent must stay at large sizes or use sand (7.5:1) instead. Voice and pronunciation rules were not exercised.

## 8. Scene recipes (the t080 sample, 12.5 s)

| Beat | Time | Content |
|---|---|---|
| 1 Poster hook | 0-4.8 | Landscape prints layer by layer 0-1.5; panel rises 1.9-2.7: "TRIỂN LÃM / BẢN ĐỒ CỔ / Hành trình trên giấy và mực". Held 2.7-4.6 with drift. |
| 2 Map route | 5.0-8.8 | Map sheet prints 5.0-5.9, route draws 6.0-8.4, compass pops 6.3, panel rises 6.3: "TUYẾN ĐƯỜNG / LẦN THEO TỪNG ĐƯỜNG BIỂN", end dot 8.3. |
| 3 Final poster | 8.8-12.5 | Map shrinks into the poster over a setting sun; panel: "TRIỂN LÃM BẢN ĐỒ CỔ / MỞ CỬA / THÁNG NÀY" (accent). Full composition from 10.7 to 12.5 (1.8 s). |
Label "MINH HOẠ" on screen the whole 12.5 s.

## 9. Transitions

Ink-layer print (the next scene prints layer by layer), panel drop then panel rise, and one match-move (map shrinks into the next poster). Cross-dissolve is only the 0.14 s paper rect. Never a hard cut, never a flash.

## 10. Image guidance for agy

Not used. If used: flat three-ink silkscreen, no gradient, no text, grain baked; prefer SVG layers as done here because they are crisp, tiny and deterministic.

## 11. Must not

Gradients, neon, shadows, bounce or shake, fast cuts, text on sage or accent, accent text under 100 px, text below 32 px, `segoepr.ttf`, a real company, place, price or spec (label content "Minh hoạ"), panels left at y 520 (visible), live CSS blur.

## 12. Traps seen in real builds (this build, measured)

1. **Offscreen panel still visible.** Panels start at y 1210-1290 and the first version parked them at `y:520`, so the top 170-230 px stayed inside the 1920 frame (a stack of 3 panels showed in every snapshot). Park at y >= 800 (1230 + 800 = 2030 > 1920). Same for the exit.
2. **Title wraps.** "BẢN ĐỒ CỔ" at 150 px needs about 910 px, the inner width was 792 px, so it wrapped to two lines and "Ổ" collided with the slogan. Fix: panel 960 wide, 124 px, `white-space:nowrap`. Budget 0.6 em per caps glyph for SegUI 800.
3. **Hidden scene never shown.** `#s2` was `visibility:hidden` in CSS and the first run only showed `#s2bg`; the map was missing. Every scene toggled by CSS needs its own `tl.set(...visible)`.
4. **Validate contrast false positives.** `hyperframes validate` flagged "BẢN ĐỒ CỔ" at 1.03:1 and the chip at 1.44:1 at t=1.25, 3.75, 6.25, 8.75, 11.25 s. Cause: the sampler reads the multiplied grain layer or an offscreen panel, not the real background. Measured by hand the pairs are 10.8:1 and 7.5:1. Do not "fix" by lightening text; check the snapshot.
5. **Tween overlap warning.** The map scale tweens 0.62 (ends 9.7) and 0.65 (starts 9.7) overlapped at one instant (lint `overlapping_gsap_tweens`); starting the second at 9.75 fixed it.
6. **Inspect overflow info.** `inspect` reports panels parked below the frame as `canvas_overflow` and stacked offscreen panels as `content_overlap` (3 warnings, 8 info). They are intentional; do not mark them off in a real build without checking the held frames.
7. **Print layers are translucent for 0.3 s.** Each layer print passes through partial opacity (sheet frames at 5.0-5.3 s and 9.3-10.2 s). This is the style, but it is the only time anything is below 90 % opacity; no held frame is.
8. **Blank beat at the cut.** Between the paper rect (4.84-4.98) and the first map print (5.0) the frame is paper plus chip for about 0.15 s. Do not lengthen it: the limit for an empty panel is 0.5 s.
9. **Rays crossing the mountains.** The sun rays sit in the same layer as the disc, below the far range; at the mountain peaks they poke between peaks. Looks intended, keep the rays shorter than the sky gap if peaks are lowered.
10. **frame_check.py could not run** (no numpy in the default python); the check was done with an ffmpeg contact sheet at 1.5 fps plus a 4-frame-step sheet around both transitions. Install numpy before a real build.
11. **Fonts in the render.** The CDN GSAP loaded fine in the renderer (render 13 s for 375 frames, 2.9 MB).

## 13. Output

`render -q standard`: 1080x1920 h264, 12.5 s, 2.9 MB. Lint 0 errors / 1 warning (fixed to 0), validate 0 errors (10 false contrast warnings), inspect 0 errors.
