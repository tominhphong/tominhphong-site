# Style: creative-suite (9:16 Vietnamese news edition, "pro creative tool" look)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** Stories whose point is a visible transformation of an image: photo, video and design app releases (masking, retouch, generative remove, colour grading), AI image tools, "how to edit X in N steps" tutorials, design tools with collaboration features, portfolio or before/after showcases. It shows change, not numbers: a story with fewer than 3 numbers fits; a story with 4+ numbers that each need a tile belongs to `saas-bento`. Not for government, finance, law, accidents or sad news (the spectral reveal reads as celebration). Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built and measured in the first real build (2026-11-11/12, video `camera-raw-19-mat-na-do-sau`, 53.4 s, plus two 10 s samples). Section 12 is "Traps seen in real builds" from that same build. Later builds append sections 13+; where two sections disagree, the later section wins.

**Clips and screenshots are optional.** This build used none: generated illustrative photos (agy) carried every scene, labelled "Minh hoạ". Never show a real app's interface, icon or panel layout (profile constraint); never fake a screenshot.

**Example videos show the visual recipe, not the niche.** Copy how it is built, not what it is about.

**Status.** Written 2026-11-12 from the first build; kept by the owner. Not yet merged into the skill folder.

Profile: `skill/references/styles/profiles/creative-suite.yaml` (energy 3, dark mode, family brand-inspired, alias "Adobe-like"). A professional studio in motion: one dark workspace (tools strip, canvas, layers/properties panel) that stays on screen from scene 2 to the end, while the artwork inside it changes through the profile's four transitions (before-after divider, brush-mask, layer-peel, spectral burst). Format 1080 x 1920, 30 fps, Vietnamese voice-over (VieNeu "Hải Đăng", about 3.9 words/s including 0.35 s scene gaps), no music, karaoke captions on estimated word times.

Marks: **ASSUMED** = the profile gives no value and this document invented one. **SUBST** = a named font is not installed, a local one replaces it. **DEVIATION** = knowingly differs from the profile.
- DEVIATION 1: the profile's layout is 16:9 ("artwork centre, layers panel right, tools strip left"). In 9:16 the layers panel moves UNDER the canvas; the tools strip stays left.
- DEVIATION 2: scene 1 is a full-bleed artwork scene with no chrome (the profile's "full-bleed artwork scenes between workspace scenes"); from scene 2 on the workspace persists and only its contents change. Full-bleed scenes between workspace scenes were not used (they broke the "one studio" continuity in a 53 s piece).
- DEVIATION 3: profile captions ask for Be Vietnam Pro 600 40 px; SegUIVar 600 44 px is used (SUBST and scaled for 9:16).
- DEVIATION 4: "brush masks baked to PNG" (constraint). The brush-mask transition is four CSS rounded bands with `overflow:hidden` whose width is tweened (see trap 12.4); no baked PNG was needed and no live blur is used.

## 1. Tokens (measured contrast, WCAG formula; `hyperframes validate` confirmed the on-bg values)

```css
:root{
  --bg:#1b1b1b;        /* profile bg (page)                                   */
  --ink:#f0f0f0;       /* profile ink   15.11:1 on bg (validate), 13.4:1 on panel */
  --mute:#9a9a9a;      /* profile mute   6.12:1 on bg (validate),  5.45:1 on panel */
  --panel:#252525;     /* profile panel: workspace frame, caption pill, chips  */
  --edge:#323232;      /* profile panel_edge: 1 px borders, empty slider track */
  --accent:#3f8cff;    /* profile accent: FILLS ONLY (rings, slider fill, mask tint, pill border) 4.68:1 on panel, 5.25 on bg */
  --accent-ink:#6aa6ff;/* ASSUMED text-safe accent: current caption word, key word in headline, chip text  6.98:1 on bg (validate), 6.21:1 on panel */
  --accent-soft:rgba(63,140,255,.18); /* ASSUMED: selection pill / active tool fill */
  --spec-a:#ff4d6d; --spec-b:#ffb000; --spec-c:#2ee6a6; --spec-d:#7a5cff; /* profile spectral: ONLY inside the baked mesh (halo, burst, shimmer) */
}
```
Rules: text colours only `--ink --mute --accent-ink`. White on `--accent` is 3.28:1 and fails: never put text on an accent fill (selection chips use `--accent-soft` fill + `--accent` border + `--ink` text). Spectral colours appear only as the baked mesh image (`mesh.jpg`) in the halo behind the finished artwork, the 0.3 s burst and the shimmer bar: never on UI chrome (profile constraint). Image overlays: depth-mask tint `rgba(63,140,255,.55)` band, LUT mask tint `rgba(63,140,255,.32)` with a 3 px dashed `--accent-ink` edge, brush marks `rgba(63,140,255,.62)`.

## 2. Fonts (local files; Source Sans 3 / Syne / Be Vietnam Pro are not installed)

| File | Role | Vietnamese check |
|---|---|---|
| `SegUIVar.ttf` (weight axis 300-700) | SUBST for Source Sans 3 and Syne: headlines 700, body 400, UI rows 500, captions 600 | every rendered frame read clean: Ặ ố ừ ữ ợ ễ ỗ đ in "Mặt nạ theo độ sâu", "Khử nhiễu", "Xoá tạo sinh", "mười chín"; the owner documents measured 0 missing glyphs with fontTools |
| `CascadiaMono.ttf` (200-700) | kicker, panel headers ("MẶT NẠ", "XOÁ TẠO SINH · HÀNG LOẠT"), file name, canvas tags (TRƯỚC / SAU / Minh hoạ), source chips | uppercase Ặ Ạ Ẫ Ổ rendered in full on frames (headers in s2-s6) |
| `cambriai.ttf` | not used (no quote in this story) | owner documents: 0 missing |
| `segoepr.ttf` | NEVER (lacks Ơ ơ Ư ư and every hooked/dotted vowel) | - |

Not run in this build: a fontTools glyph scan (custom python scripts were not permitted in this session and the local ffmpeg has no `drawtext`); the check above is a visual check of rendered frames at 1080 px. Syne 800 "creative flair" does not exist locally: result titles use Seg 700 with the key word in `--accent-ink`.

### Type scale (1080 x 1920, px)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| s1 hero title | Seg 700, -0.02em | 128 / 1.05 | "Camera Raw 19", the number in `--accent-ink` |
| `.hl` headline | Seg 700, -0.02em | 72 / 1.12 | 1 line in 5 of 6 scenes; max 2 lines; key words in `--accent-ink` |
| `.sb` sub line | Seg 400 | 40 / 1.25 | `--mute`, one line, states the claim in words |
| `.kk` kicker | Mono 600 +0.04em | 30 | s1 only ("ADOBE · NGÀY 10/11") |
| panel header `.ph` | Mono 600 +0.03em | 30 / 36 | `--mute`, uppercase |
| panel row | Seg 500 | 32 (LUT rows 30 in 42 px rows) | `--ink` |
| canvas tag `.tag` | Mono 600 | 30 in a 50 px chip | `rgba(27,27,27,.94)` fill, 1 px `--edge` |
| chip | Seg 600 / Mono 500 | 30 in a 50 px chip | |
| caption | Seg 600 | 44 / 1.3 | see section 9 |
Minimum text: 30 px everywhere (acceptance rule); no footer line was needed.

## 3. Safe areas and grid (1080 x 1920, measured on held frames)

- y 0-110: empty (platform status zone).
- Header block: s1 kicker + 128 px title + sub at top 120 (ends about y 350); s2-s6 headline + sub at top 168 (ends y 300-386).
- Workspace frame `#wsbg`: x 48-1032, y 410-1310 (984 x 900), radius 8, 1 px `--edge`, shadow `0 24px 60px rgba(0,0,0,.45)`.
  - title strip: y 410-472 (file name "anh-minh-hoa.jpg" mono 30 px + three 14 px `--edge` dots, not traffic lights).
  - tools strip: x 64-128, six 64 px tools from y 486, step 80; active tool = `#tsel` (`--accent-soft` + 1 px `--accent`) that slides 0.35 s `power3.out`.
  - canvas: x 144-1016, y 486-1086 (872 x 600), radius 6, `overflow:hidden`.
  - layers/properties panel: x 144-1016, y 1102-1294 (872 x 192), `--bg` fill, 1 px `--edge`, radius 6.
- s1 canvas (full-bleed artwork): x 48-1032, y 430-1300 (984 x 870).
- Lowest content edge at every hold: y 1294 (panel) or 1300 (s1 canvas); frame_check TOPHEAVY 0 of 107 frames.
- Captions: pill top 1400, max width 936 (x 72-1008), up to 2 lines (to about y 1560).
- y 1600-1920: empty (bottom UI zone).
- For a sample with 5 layer rows: canvas 872 x 470 (y 486-956) and panel 872 x 322 (y 972-1294), rows 52-53 px.

## 4. Layers, back to front

1. `#root` `--bg`.
2. Header groups `.ht` (one per beat; swapped with `visibility`).
3. `#halo` (x 24, y 392, 1032 x 936, radius 28): the baked spectral mesh, `opacity:0` until a result reveal, then 1 (0.25 s fade). It only shows as a 16-24 px glowing rim around the workspace.
4. `#wsg` workspace group (transform origin 580/786 = canvas centre) for the pull-back: `#wsbg`, title strip, tools, `#tsel`, panel (`.pp` per scene, `display:none` when off), `#canvas`.
5. Inside `#canvas`: `#cam` (the camera; all artwork layers, mask overlays, brush bands, cursor) and `#ovl` above it (divider, TRƯỚC/SAU tags, info tags, "Minh hoạ" tag, shimmer).
6. `#burst` (900 px circle at canvas centre, mesh, `mix-blend-mode:screen`).
7. `#caps`.
Depth: background halo (still), workspace (camera drift 0-4%), canvas content (push 1.00-1.17), cursor and tags (fastest, they travel). No live `backdrop-filter`, no live blur.

## 5. Components

- **Workspace** (`#wsbg` + strip + tools + panel): generic, no real-app icons; tool icons are inline SVG from circles, lines and rounded rects (brush, half-circle mask, sliders, stacked copies, sparkles, sun).
- **Before/after divider** `#dv`: 4 px `--ink` line with 12 px dark shadow, 64 px round handle (`--panel` fill, 3 px `--ink` ring, two chevrons). The "before" layer sits on top with `clip-path: inset(0 R% 0 0)`; the divider `left` and the clip are tweened with the same ease and duration. Tags "TRƯỚC" (top-left) and "SAU" (top-right) pop 0.5-0.6 s after the sweep starts. Before is always LEFT.
- **Mask band** (depth mask): full-width band 38% of canvas height, linear gradient transparent / accent .55 / transparent; its `top` follows a two-handle range slider in the panel (`rg` proxy object, `onUpdate` sets both knobs and the fill).
- **Range slider**: track 440 x 6 `--edge`, fill `--accent`, knobs 26 px `--ink` with 3 px `--accent` ring.
- **Segmented control** `.seg`: 46 px high, `--panel` fill; the selection pill (`--accent-soft` + 1 px `--accent`) slides 0.45 s `power3.out` (LUT "Toàn ảnh / Theo mặt nạ").
- **Layer row** (stacking signature): thumbnail swatch 40 x 36, label, amount slider; rows drop in from y -26 with `power3.out` 0.3 s, stagger 0.05 s (profile value).
- **Thumbnail strip**: three 262 x 120 thumbs at x 22 / 305 / 588 in the panel, letter tag A/B/C (mono 30 px), selection ring 3 px `--accent` sliding 0.45 s; check badges 40 px `--accent` circle with a white tick (no text on accent).
- **Option cards** (glow modes): two 404 x 120 cards with an SVG arrow diagram and a 34 px label, selection ring slides.
- **Brush cursor**: 70 px ring, 3 px `--ink`, 1 px dark outline inside and out; it leads every mask paint.
- **Canvas tags**: "Minh hoạ" bottom-left on every generated image for the whole video; info tags top-left ("Theo DPReview", "Cả 2 bản Lightroom", "Bản đồ độ sâu").
- **Source rows** (last scene panel): mono chip with the domain + `--mute` line with version/date.
- **Multiplayer cursors** (sample t115): arrow SVG with a name tag (30 px, tag fill = cursor colour); colours limited to `--accent`, `--ink`, `--mute` so no spectral colour reaches UI chrome; avatars 50 px circles with 30 px letters.

## 6. Motion language (energy 3)

- Entrances: headline groups rise y 22 to 0, 0.28 s `power3.out`; panel content fades in 0.18 s with y 14; pops `back.out(1.4)` from 0.7 (soft overshoot, energy 3); layer rows drop from y -26.
- Camera per scene (no two adjacent scenes share a move): s1 lateral drift (x 0 to -14, scale 1.00-1.04, linear); s2 static, then a cut-in push 1.00 to 1.15 (0.6 s `power3.inOut`) on the spoken "tự tạo", drifting to 1.17; s3 pull-back 1.12 to 1.00 (`power2.out` over the scene); s4 nearly static 1.00-1.02; s5 push 1.00-1.03, then a second cut-in push 1.00 to 1.15 on "Tính năng khử nhiễu"; s6 workspace push 1.00 to 1.04 then the profile's "pull back to reveal the workspace around a finished piece" 1.04 to 1.00 (0.9 s `power3.inOut`) on "Bản mười chín".
- Before/after sweep: 0.9 s `power2.inOut` (profile). Reveal from the right edge to 38-52%.
- Result moments (s1 hook, s6 end, samples at 7.2-7.7 s): spectral burst 0.3 s (scale 0.15 to 1.7, opacity 0.95 to 0, screen blend) followed by the halo fading in over 0.25 s and staying; in s6 the halo breathes scale 1.000-1.015 (`sine.inOut`, finite yoyo).
- Word anchors: `A(sid, word, nth)` = estimated onset minus 0.12 s, never before the scene start. Estimated onsets are computed in the page with the SAME formula as `motion_tools.py voice` (speech length x word length / total letters), so captions and anchors agree with `voice/timeline.json` exactly.
- Hold motion: camera drift, cursor travel, halo breathing; no frozen frame longer than about 1 s.
- Not used: shake, flash, speed lines, hard cuts, elastic.

## 7. Scene recipes (S = scene start; times from `voice/timeline.json`)

**R1 Hook - full-bleed artwork with a before/after sweep (s1, 0-7.39 s).** Frame 0: kicker "ADOBE · NGÀY 10/11", title "Camera Raw 19" 128 px, sub line, the artwork 984 x 870 showing the desaturated "before" with the divider already at 88%. On "Camera" (2.06 s): divider sweeps 88 to 38% (0.9 s), then burst + halo + TRƯỚC/SAU tags at +0.9 s; on "bản" the divider settles at 52% (0.8 s); the "19" bumps 1.12 on "chín". Lowest edge y 1300.

**R2 Workspace + depth mask (s2, 7.39-17.58 s).** Transition: the s1 artwork morphs into the canvas slot (`left/top/width/height` 0.6 s `power3.inOut`, starting S-0.12) while strip, tools and panel rise in 0.3 s with 0.03 stagger. Panel: "MẶT NẠ", row "Mặt nạ theo độ sâu" with an eye icon and accent dot, row "Phạm vi độ sâu" with the range slider. On "mặt nạ" the mask band fades in over the near ground; tags "Theo DPReview" and "Cả 2 bản Lightroom" rise on their words; cut-in push on "tự tạo" while the baked depth map fades in (0.35 s) with the tag "Bản đồ độ sâu"; the range slider moves twice (0.9 s each) and the band and brush cursor follow.

**R3 Layer stack (s3, 17.58-24.81 s).** Transition: before-after wipe right-to-left (0.72 s from S-0.6) brings the night photo in. Panel: "BẢNG TRA MÀU" + segmented control; row A present at S, rows B and C stack on "ba" (stagger 0.05) while two baked grades crossfade on the canvas (0.35 s each, 0.4 s apart); pill slides to "Theo mặt nạ" on "mỗi" and the masked half of the image is tinted; amount sliders shrink/grow on "thanh chỉnh mức độ" and the top grade layer's opacity follows the slider.

**R4 Versions + compare (s4, 24.81-32.92 s).** Transition: layer-peel, the night layer slides off left (x -980, rotation -4, 0.5 s `power3.in` from S-0.4). Panel: three version thumbs A/B/C (B and C pop on "nhiều"); selection ring moves to B on "chỉnh riêng" and the canvas crossfades to version B; divider sweeps 100 to 50% on "so sánh trước và sau" (A left, B right); chip "không nhân đôi tệp gốc" pops on "không".

**R5 Brush marks + batch result (s5, 32.92-38.7 s) and cut-in compare (38.7-43.75 s).** Transition: brush-mask, four rounded 200 px bands paint the pier in left-to-right (0.36 s each, stagger 0.14, from S-0.65). Panel: three bracketed thumbs. The cursor travels to each bird and paints a blue stroke (0.4 s apart) on "đánh dấu"; dots pop on the thumbs on "nhiều ảnh"; on "xoá tất cả" a spectral shimmer bar crosses the canvas (0.5 s), the canvas crossfades to the cleaned plate and check badges pop (stagger 0.06). Cut-in on "Tính năng": headline, panel and canvas swap together, push to 1.15, switch toggles on "khử", divider reveals the clean right half against the noisy left; format chips pop on "JPEG", "PNG", "nhiều".

**R6 Glow modes + result reveal (s6, 43.75-53.4 s).** Transition: spectral burst from S-0.05. Panel: two option cards ("Một hướng", "Hai hướng"); six screen-blended copies of the baked highlight layer spread 16 px steps one way on "kéo" and to alternating sides (24 px steps) on "hai hướng"; ring slides between cards. On "Bản mười chín": pull-back, headline "Bản 19" + sub, panel swaps to the source rows, halo fades in and breathes until the end. The last 1.5 s are a full composition (no fade-out).

**Sample recipe "N steps as layers" (t088).** Five layer rows stack one per 1.3 s, the active row pill and the active tool move with them, the canvas steps through five baked grades (step 3 painted on with the brush bands), then a raw-vs-final divider, burst and halo at 7.7 s, hold to 10 s.

**Sample recipe "multiplayer" (t115).** Three cursors glide on arcs (x `expo.out`, y `power2.inOut`), one drags a selection box, two comment cards pop with soft overshoot, a pin drops, the answer lands as a before/after sweep, the panel status changes to "đã xử lý", burst + halo + pull-back at 7.2 s.

## 8. Transitions (one per cut, all from the profile)

| Cut | Kind | Timing |
|---|---|---|
| s1 > s2 | match-move (artwork shrinks into the canvas slot) | 0.6 s from S-0.12 |
| s2 > s3 | before-after wipe | 0.72 s from S-0.6, outgoing image gone by S+0.12 |
| s3 > s4 | layer-peel | 0.5 s from S-0.4 |
| s4 > s5 | brush-mask (4 bands) | from S-0.65 to S+0.13 |
| s5 > s5b | cut-in (same scene) | instant swap + 0.6 s push |
| s5 > s6 | spectral burst | 0.3 s from S-0.05 |
Rule from this build: the canvas transition runs BEFORE the boundary so that the outgoing picture is gone within 0.15 s after the new headline appears (see trap 12.3). Headlines swap exactly on the boundary.

## 9. Captions (karaoke)

- Pill: `--panel` fill, 1 px `--edge`, radius 8, padding 14 x 30, top 1400, max width 936, centred; SegUIVar 600 44 px, line height 1.3, `--ink`; current word `--accent-ink` (6.21:1 on the pill). Unread and read words stay `--ink`.
- Visibility and highlight by `tl.set` only (no fades): no ghosts, no half states.
- Chunking (as built): split after punctuation once a chunk has 3+ words; at 7+ words split only if the next pause is more than 2 words away; hard cap 9; a 1-2 word tail is merged into the previous chunk. Result: every chunk in this build was one line except the last (2 lines, 10 words).
- Captions show the spoken words verbatim (numbers in words), so spoken and on-screen text cannot drift; headlines and panels carry the digits ("19", "3", "2").

## 10. Sound

No music and no SFX in this build (tools unavailable). Profile intent for later builds: cinematic electronic 100-122 BPM, brush swishes on mask paints, soft clicks on tool and pill moves, a shimmer on result reveals; moderate density. Voice only: mux loudnorm gives -15.4 LUFS integrated, peak -4.2 dBFS.

## 11. Images (agy) and baked variants (ffmpeg)

- Four agy images, each 768 x 1376, about 1 min each, run in parallel: a landscape with strong near-to-far depth (tree on a hill, misty ridges), a wet night street with many point lights, a pier at sunrise with exactly three gulls in a clean sky, a fictional studio portrait. Prompt pattern: "Professional ... photograph, vertical: <subject>, <light>, realistic camera photo, no people / not a real person". All four came back usable on the first call.
- Every edit state is BAKED with ffmpeg, never live CSS filters: before (`eq=saturation=0.2:contrast=0.8`), depth map (gray, blur 14, `0.45*(255-lum)+0.7*255*(Y/H)^1.3` so near = bright), versions B/C (`colorbalance` + `eq`), three LUT grades, noisy plate (`noise=alls=48`), highlight layer (`geq` keep pixels with luma > 195, blur 3), clean pier (`delogo` on the three gull boxes; result checked at 1:1, no smear visible on the smooth sky), five portrait steps (cumulative chain incl. `vignette` and `smartblur`), spectral mesh (`geq` with four Gaussian blobs in the four spectral colours at 540 x 960, scaled to 1080 x 1920).
- `-q:v 4`: 18 KB (depth) to 635 KB (noisy) per file; final.mp4 14.6 MB for 53.4 s.
- Choose source images with a smooth area where an object will be removed (sky, wall): `delogo` only works on smooth backgrounds.

## 12. Traps seen in real builds (this build, measured)

1. **Hidden panel kept showing children.** Panel pages were hidden with `visibility:hidden`, but their rows and chips had been made `visibility:visible` by their own tweens, and a visible child overrides a hidden parent: scene 4 showed scene 3's LUT rows and scene 6 showed every earlier chip. Fix: panel pages switch with `display:none/block` (`tl.set`), never `visibility`.
2. **A layer leaked into the next scene.** The depth map (opacity tweened to 1 in s2) stayed on top of the landscape in s4 (snapshot 26 s showed a grey depth map instead of the photo). Fix: reset every overlay that was faded in when its scene ends (`tl.set("#iDepth",{opacity:0}, S3+0.15)`).
3. **Outgoing scene visible 0.8-0.9 s after the cut.** The wipe and the brush transition started at the boundary, so the new headline sat over the old picture for 0.82 s (s3) and 0.45 s (s5). Fix: start canvas transitions before the boundary (S-0.6 / S-0.65 / S-0.4) so the old picture is gone by S+0.13 at the latest; tiles at 0.1 s steps confirmed it.
4. **SVG dash reveals do not animate in the renderer.** A `stroke-dashoffset` reveal on a `pathLength="1"` path, used both inside an SVG `<mask>` and as a pattern-filled stroke (stroke-width 260), rendered as a pop: nothing at 32.6 s, full picture at 32.7 s. The small brush marks pop the same way (acceptable, the cursor leads them). Fix for the brush-mask transition: four `div` bands (`height 200`, `border-radius 100px`, `overflow:hidden`, image inside positioned at -bandTop-170) with `width` tweened 0 to 1100, stagger 0.14: verified progressive at 0.1 s steps.
5. **Visibility only in the tween's FROM values disappears after a seek.** `fromTo(el,{visibility:"visible",opacity:0},{opacity:1})` worked in a straight play but, in the parallel render, comment c2 and the pin of sample t115 were missing from 3.4 s to about 5 s. Fix: put `visibility:"visible"` in the TO values too (done in all helpers: `rise`, `pop`, cursor, shimmer, burst).
6. **Caption orphan.** The 7-word cap left "bảng," at the head of the next chunk and a 9-word chunk wrapped with one word on line 2. Fix: the look-ahead chunk rule in section 9.
7. **Facts gate caught two lines after the build.** "Xoá bằng AI" and "cập nhật cùng Photoshop" were not stated by either opened page (Adobe's post never uses the word AI; its install line names Photoshop AND Bridge; DPReview's headline even says the best features "aren't AI"). Fix: "xoá tạo sinh" (Generative Remove) and "đến qua bản cập nhật Photoshop và Bridge"; voice regenerated (52.90 s), scene table and anchors updated, re-rendered. Re-open the pages for selfcheck BEFORE the final render.
8. **A text edit glued two words** ("loạt:đánh") so `A("s5","đánh")` silently fell back to the scene start. Plain `validate` only printed "4 warning(s)"; `validate --json` showed "missing word s5 đánh 1". Always read `--json` warnings after editing script text.
9. **Lint "overlapping tweens between 0.00 s and ..." warnings** are false positives for times computed from word anchors (lint cannot evaluate them); 17 such warnings, 0 errors.
10. **validate contrast false positives** on semi-transparent chips and coloured avatar circles (t115 avatar letters "1.13:1", t088 "Minh hoạ" tag "2.23:1"): the checker reads the wrong background. Real values: letters on their own circles about 5:1 and above; the tag is 94% `--bg` under `--mute` text. Use an opaque tag fill if a clean report matters.
11. **`hyperframes render -o` is relative to the current directory**, not to the project directory: `render t088 -o ../x.mp4` from `samples/` wrote to the parent folder. Run render from the folder where the file should land.
12. **Script size.** 206-208 words gave 51.5-52.9 s of voice (3.9 words/s incl. 0.35 s gaps); video = voice + 0.5 s. 6 scenes of 7.2-10.8 s; scenes over 10 s got an internal cut-in.
13. **Measured output.** Render 27-33 s for 53.4 s (standard), silent 24.3 MB, muxed 14.6 MB, -15.4 LUFS, peak -4.2 dBFS; frame_check 0 BLANK and 0 TOPHEAVY of 107 frames on silent and on final; samples 2.3 MB and 5.4 MB, 0 BLANK of 20 frames each.
14. **Still not checked.** Pronunciation of Adobe, Camera Raw, Lightroom, DPReview, Photoshop, Bridge, Creative Cloud (listed in `ear-check.txt`, default VieNeu reading, no respelling); word times are estimates; no music or SFX pass.

## 13. Must not

- Real app icons, panel layouts, logos or screenshots presented as the real product; a generated image without the "Minh hoạ" tag.
- Spectral colours on chrome (tools, pills, chips, cursors); white text on `--accent`; text under 30 px.
- Live CSS filters or blur for edit states (bake them); more than one before/after sweep per scene; before on the right.
- Shake, flash, elastic, hard cuts; a fade-out ending (last 1.5 s must be the full composition).
- Claims the opened pages do not state ("AI" for a feature the page does not call AI); predictions, advice, hype, calls to like/share/subscribe.
