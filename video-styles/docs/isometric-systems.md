# Style: isometric-systems (9:16 Vietnamese system-explainer edition)

## 0. Read this first: niche, status, what was and was not exercised

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build:** "how the parts of a platform fit together" stories: low-code and no-code platforms, integrations, architecture and infrastructure explainers, onboarding flows, anything with 3 to 5 named parts connected in a chain and a reusable-layers payoff. Jev fit for topic shape t169 ("Low-code platform lets teams snap together apps from reusable blocks") = 0.82. Not for people stories, quotes, breaking one-number news, dense number dashboards (use saas-bento), or mood pieces. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE real 12 s demo build (`samples/t169`). There was no owner document before this one. Everything below is measured on that sample unless marked **ASSUMED** (profile gives no value, this document invented one) or **SUBST** (a font named by the profile is not installed).

**Not exercised (demo build):** voice-over, word timing, karaoke captions, music, SFX, pronunciation, images from agy, counters, multi-scene transitions of a full 45-60 s video. Sections 8 (captions) and 9 (sound) are the profile's rules restated and are UNTESTED. Do not treat them as verified.

Profile: `skill/references/styles/profiles/isometric-systems.yaml` (energy 2, light mode, aesthetic family). Calm, orderly: a miniature world at 30 degrees, systems assemble block by block, data cubes glide along a route, a stack explodes vertically to show layers.

DEVIATION 1: the profile's typefaces (Space Grotesk, IBM Plex Mono, Be Vietnam Pro) are not installed. SUBST: SegUIVar (headline) and CascadiaMono (labels).
DEVIATION 2: the profile says headline 64 px. In 1080 x 1920 it is 82 px.
DEVIATION 3: the profile says data cubes "move along paths". Cubes that run on the floor were rejected (trap 7); they hop from block top to block top instead.
DEVIATION 4: the projection is exactly 2:1 (dx 88, dy 44 per cell), which is the profile's "dx:dy = 2:1" axis rule; true 30 degrees would be 1.73:1. The profile itself uses 2:1 for camera pans, so 2:1 is used everywhere to keep one projection.

## 1. Tokens (contrast computed by hand with the WCAG formula; the validator's own readings are in trap 2)

```css
:root{
  --bg:#eef2f8;      /* profile bg */
  --ink:#1e2a3b;     /* 12.9:1 on bg, 14.5 on white. headline, labels */
  --mute:#475569;    /* ASSUMED; 6.7:1 on bg. inactive step text */
  --accent:#3b6cff;  /* 3.9:1 on bg: FILL / route / blocks ONLY, never small text. white on it 4.4:1 */
  --accent-dk:#2a50c4; /* ASSUMED; 6.1:1 on bg. accent words in the headline */
  --top:#ffffff; --left:#d5deeb; --right:#b7c4d8;  /* neutral block faces; --right is 1.6:1 on bg: borders only */
  --green:#2fbf8f;   /* 2.1:1: block fill only */
  --amber:#f5a524;   /* 1.8:1: block fill only */
}
```
Face tones per block (one hue, three faces): neutral `#ffffff/#d5deeb/#b7c4d8`; amber top `#ffc965` left `#f5a524` right `#c9821a`; green `#6fdcb8/#2fbf8f/#1f9170`; blue `#7a9bff/#3b6cff/#2a50c4`; blue slab 2 `#9db6ff/#5b86ff/#3a63d6`; blue slab 3 (screen) `#ffffff/#7a9bff/#4a76f0`. Edge: 1.5 px `rgba(30,42,59,.2)`. Ground shadow: footprint offset by (h x 0.22, h x 0.12), `rgba(30,42,59,.10)`. Top-face highlight on a beat: `#eaf0fa` (neutral), `#ffe0a0` (amber), `#b2f0da` (green), `#b4c7ff` (blue), `#e6edff` (screen slab).
Rule kept: accent marks only the route, the packets and the active "app" block; every other block uses its own hue.
Text colours allowed: `--ink`, `--mute`, `--accent-dk`, white on `--ink`. No text in accent, green or amber.

## 2. Fonts (glyph claim comes from the existing owner documents; verified visually on this build's frames, not with fontTools: python was not runnable in this session)

| File | Role | Vietnamese |
|---|---|---|
| `SegUIVar.ttf` | headline 82 px / 700; accent words same weight in `--accent-dk` | TÀI LIỆU NÓI (style-saas-bento / fluent-productivity: 0 missing). Frames show correct stacked marks in "Ghép ứng dụng", "Dữ liệu chạy theo đường đã nối", "Khối dựng một lần" |
| `CascadiaMono.ttf` | chip, block labels, step buttons, 32 px / 500-600 | frames show "Biểu mẫu", "Quy tắc", "Dữ liệu", "Ứng dụng", "Giao diện", "Quy trình", "Kết nối", "Minh hoạ" correctly |
| `cambriai.ttf` | not used in this build | n/a |
| `segoepr.ttf` | NEVER used: 92 Vietnamese glyphs missing | |

Mono labels are 18.8 px per character at 32 px; pill width = chars x 19 + 44 px (measured against frames: no clipping).

## 3. Type scale, safe areas and grid (1080 x 1920)

| Item | Size | Where |
|---|---|---|
| Headline | 82 px / 700, line 1.1, 2 lines, manual `<br>` | x 72, y 270-450, width 936 |
| "Minh hoạ" chip | 32 px / 500 mono, white on ink, radius 12 | x 72, y 196, present for the whole video |
| Block label pill | 32 px / 500 mono, ink on white, 2 px `--right` border, radius 12, height 52 | above the cluster, y 540-620 (before camera move) |
| Step buttons | 32 px / 600 mono, height 68, 3 equal cells with 20 gap | x 72, y 1340, width 936 |

No text below 32 px anywhere; no footer line was needed because the chip is already 32 px.
- y 0-190 and y 1480-1920: kept empty of content (platform UI zones); the last content is the step strip ending y 1408.
- Iso grid: tile = 176 x 88 px diamond (dx 88, dy 44), floor 5 x 5 cells = 880 x 440 px, origin (540, 720) = back corner. Floor slab thickness 26. Cluster occupies y 640-1170, x 100-980.
- Projection: `P(i,j,z) = (540 + (i-j)*88, 720 + (i+j)*44 - z)`.
- Cell map used: A (0,3) neutral h90, B (2,3) amber h120, C (2,1) green h110, D (4,1) accent stack 3 x 44. Low neutral decor at (1,4) h40, (3,4) h40, (4,4) h60, all in FRONT of the route so no label leader crosses a decor block.

## 4. Layers, back to front
1. `#bg` iso grid pattern, 176 x 88, 1.5 px ink lines at 5% (profile asks 8% for floor lines; the floor lines use 8%).
2. `#drift` wrapper (settle scale 1.00 to 1.02) holding `#iso` camera group: floor slab, accent route (16 px, round joins), blocks layer L0 (A, C), blocks layer L1 (B, D stack, decor), label pills and leaders, data cubes.
3. `#fg` four floating cubes (24-34 px) with parallax 1.6 x the camera move, bobbing +-14 px.
4. HTML: chip, headline (three stacked divs), step strip.
Draw order inside the cluster is by depth (i+j). Data cubes sit on the TOP layer so they never need depth sorting.

## 5. Components
- **Block:** three polygons (left, right, top) of one hue + ground shadow + 1.5 px edge. Built by one function `box(parent,i,j,w,d,z0,h,tone,shadow)`; the top polygon is returned so it can be brightened.
- **Stack (the "app"):** three 44 px slabs of the same footprint, tones blue / blue2 / blue3; top slab carries two 6 px accent lines (a screen).
- **Route:** one polyline from block centre to block centre along grid axes, drawn with stroke-dashoffset, under all blocks.
- **Data cube:** 36 px iso cube, faces `#7a9bff/#3b6cff/#2a50c4`, 2 px white outline so it reads on any top face.
- **Label:** vertical 3 px leader (ink at 60%) from the block top centre with a 6 px dot, ending in a pill. Screen-aligned, never skewed. Pill heights alternate (620 / 540) so neighbours 176 px apart never overlap.
- **Step strip:** active = ink fill + white text; inactive = transparent + `--mute` text + 2 px `--right` border.

## 6. Motion language
Energy 2: no shake, no flash, no bounce. Eases: entrances `power3.out`, camera `power2.inOut`, hops `power1.inOut` on x with `power2.out`/`power2.in` halves on y (an arc), pulses `power2.out` then `power2.in`.
- **tile-build:** blocks rise from y +44 to 0 with opacity 0 to 1, 0.5 s, `power3.out`, starting at 0.15 / 0.32 / 0.5 / 0.68 s, then the three slabs at 0.9 / 1.1 and decor at 1.5-1.74 s (build is complete at 2.24 s).
- **Hold with life (2.9-3.8 s):** the top faces of A, B, C and the screen slab brighten in a chain, 0.18 s up and 0.3 s down.
- **Beat switch (3.85-4.35 s):** old headline out 0.15 s `power2.in`; new headline in at 4.0, y 20 to 0 and opacity, 0.35 s `power3.out`; step button colours swap in 0.2 s. Gap with no headline: 0 s.
- **axis-pan (4.0-4.9 s):** `#iso` x +50, y +25 (dx:dy = 2:1), scale 1 to 1.08, 0.9 s `power2.inOut`; foreground cubes move +60/+30.
- **Route draw:** 4.2-5.1 s. **Labels:** 4.75 s, then +0.14 s each, y 14 to 0, 0.35 s.
- **Data cubes:** 3 cubes at 4.9 / 5.5 / 6.1 s. Each pops in on block A (scale 0 to 1, 0.15 s `back.out(1.6)`), hops A to B to C to D (0.55 s per hop, apex 70 px above the higher top, 0.1 s rest), top face of the landing block pulses (0.12 s up, 0.3 s down), and the cube shrinks into D. Last cube is gone at 8.2 s.
- **Beat switch (7.85-8.35 s):** labels and headline out in 0.15 s, new headline in at 8.0.
- **layer-lift (8.0-9.75 s):** camera pans to x -80, y -40, scale 1 over 1.0 s; mid slab lifts 70 px (8.8 s), top slab 140 px (8.95 s), 0.8 s `power3.inOut`; three stack labels at 9.5 s +0.14 s each (x -14 to 0).
- **Final hold (9.9-12.0 s):** `#drift` scale 1.00 to 1.02 (linear), top slab glow loop (4 yoyo half-cycles of 0.5 s from 10.2 s), foreground cubes bob. The 12.0 s timeline ends on a full composition.

## 7. Scene recipes (S = beat start)
### R1 Build (S 0-4 s, "1 Ghép")
Frame 0 already shows headline, chip, floor slab and step strip; blocks rise from 0.15 s. Headline: "Ghép ứng dụng từ / các khối có sẵn". No labels yet: the beat is about assembly.
### R2 Connect (S 4-8 s, "2 Nối")
Headline: "Dữ liệu chạy theo / đường đã nối". Pan + route + four labels (Biểu mẫu, Quy tắc, Dữ liệu, Ứng dụng) + three data cubes. Focal point: the moving cube.
### R3 Reuse (S 8-12 s, "3 Dùng lại")
Headline: "Khối dựng một lần, / dùng lại mọi nơi". Pan, exploded stack with labels Giao diện / Quy trình / Kết nối, quiet hold.
Rule for a longer video (UNTESTED): one beat = one idea; 2-4 s of builds, hold until the spoken keyword, pan on a bar line.

## 8. Captions (NOT exercised: demo build has no voice)
Profile rule restated, unverified: white bar `rgba(255,255,255,.9)`, radius 12, 42 px Be Vietnam Pro 600 ink (SUBST: SegUIVar), current word in `--accent-dk`, bottom band. In 9:16 the platform covers about the bottom 440 px, so the captions go at bottom 440 as in the skeleton, which means the step strip (y 1340-1408) must move up or be dropped when captions exist.

## 9. Sound (NOT exercised)
Profile: minimal electronic or ambient 88-104 BPM, soft ticks on block placement, light whoosh on pans, low density. Data-cube hops and top-face pulses are the natural beat anchors.

## 10. Images (none used)
Not needed: every object is vector. Baked ambient-occlusion PNG under clusters is optional (profile); skip it unless the shadow looks flat on a real device.

## 11. Must not
- No text on the iso plane, no skew on text. No rotation of the projection. Camera moves only along dx:dy = 2:1 plus a zoom <= 1.08.
- No more than ~40 blocks (this build: 12 block groups + 3 cubes).
- No accent colour on blocks that are not the active path or the app.
- No empty-floor hold: the floor never stays alone longer than 0.15 s (rise starts at 0.15).
- No leader line crossing another block; no decor block under a leader.
- No data cube that runs on the floor.
- No label or foreground cube within 40 px of a label pill, and nothing within 20 px of the frame edge during any camera pose.
- No Vietnamese in segoepr. No emoji. No real company, product or price; keep the "Minh hoạ" chip on every illustrative video.

## 12. Traps seen in real builds (this build, 2026-11-14)
1. **Floor-level cubes are occluded by blocks.** In the first plan the data cubes ran on the floor between blocks. A cube at cell (1.2, 3.5) is in front of block A (so it must overdraw A's right face) but behind block B (so B must overdraw it), and the legs are only 0.7 cell (about 60 px) long. Fix: cubes hop between block tops on a top layer; no depth sorting needed.
2. **Validator contrast false positives.** `hyperframes validate` printed 10 warnings "1.12:1 (need 3:1)" for `#chip` and `#st1` (white on the ink fill, real ratio 14.5:1). Cause not confirmed (it probably samples the page background behind the element). Visual check of frames confirms the text is legible. Do not "fix" it by lightening the chip; re-check the real colours instead.
3. **Foreground parallax cube hit a label pill.** At 6.8 s the green foreground cube (930, 500) moved +60 px in the camera pan and sat on the "Ứng dụng" pill (pill right edge about 899 + pan). Moved the foreground cubes to the bottom band (y 1120-1260) and the left cube to x 250.
4. **Pan cut the floor corner.** First final pose x -110 pushed the floor's left corner to x -10. Pan reduced to x -80 (left corner at x about 20 with the 1.02 settle).
5. **Stack labels overflowed the frame.** Pills at x 936 + 210 = 1146 minus the 80 px pan left a 14 px margin. Leader shortened to 24 px (pill at x 916-1126), margin about 34 px in the final pose. `hyperframes inspect` reports 4 info lines `canvas_overflow #labs` for the hidden (opacity 0) beat-3 labels at earlier times: harmless; the group is measured with its invisible children.
6. **Headline orphan.** "Khối dựng một lần, dùng / lại mọi nơi" wrapped after "dùng". Manual `<br>` in all three headlines.
7. **Beat-1 label gap.** With labels held back to beat 2, y 450-840 is empty at 0-4 s (about 390 px). Accepted because the headline and floor are present; if the gap looks weak on a phone, raise the cluster (`OY`) or show one label early.
8. **Tooling in this environment:** `frame_check.py` needs numpy, which was missing, so the frame check was replaced by an ffmpeg 6 x 4 sheet at 2 fps read by eye (see selfcheck.md). `sed -i`, `cp -R` and python were refused by the sandbox: copy the three font files by name.
9. **Hand-set label coordinates.** Leader anchors (block top centres) were typed as numbers; moving `OY` by -80 meant editing every number. Compute them from `P()` in the next build.

## 13. Measured result
12.0 s, 1080 x 1920, 30 fps, h264, silent, 2.3 MB, rendered in 11.2 s (HyperFrames 0.7.26). Lint: 0 errors, 0 warnings. Validate: 0 errors, 10 contrast false positives (trap 2).
