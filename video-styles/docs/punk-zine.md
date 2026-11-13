# Style: punk-zine (detail, written from the first real build, 2026-11-13)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), as observed in this build.** Counterculture and DIY community stories with a date, a place and a "who is there" list: zine fairs, indie music and print culture, all-ages shows, maker markets, small-press and bookstore nights, protest or manifesto pieces. Works because every fact can be a taped strip or a ransom tile and the scene cuts are hard. Not for: dense numbers (more than 3 per scene), money or legal stories, sad news, anything calm or official, anything that needs a chart (the profile itself says avoid chart, spec, ui-demo). Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the design as built. Section 12 lists the traps seen in THIS build with measured numbers; where 12 disagrees with 1-11, 12 wins.

**Example videos show the visual recipe, not the niche.** The video that tested this document is a Vietnamese news piece about the 10th Lone Star Zine Fest (Austin, 56.1 s, 7 scenes). Copy how it is built, not what it is about.

**Status.** Written from one 56.1 s build plus two 10 s samples. No owner has reviewed it. Profile: `skill/references/styles/profiles/punk-zine.yaml` (energy 5, mixed palette, aliases zine, xerox).
Marks: **ASSUMED** = profile gives no value, this document invented one. **SUBST** = the named font is not installed, a local font replaces it. **DEVIATION** = knowingly differs from the profile.

Deviations in one list: (1) fonts SUBST (section 2); (2) no music and no SFX (the tools were not available; voice only); (3) captions highlight in the scene's fluorescent, not a fixed colour (section 8); (4) photocopy flash is 0.07 s at 90% white instead of "1 frame"; (5) the profile's 12 fps letter jitter runs at 8 fps because 12 fps tripled the tween count for no visible gain (ASSUMED); (6) the profile's caption font Be Vietnam Pro is SUBST by SegUIVar 700.

## 1. Tokens

```css
:root{
  --bg:#f2f0ea;     /* profile bg (paper)        */
  --ink:#0d0d0d;    /* profile ink               17.05:1 on bg, 19.44:1 on --paper */
  --pink:#ff2e88;   /* profile accent: FILL ONLY on paper (3.07:1 on bg); text on it is ink 5.55:1 */
  --acid:#c6ff00;   /* profile acid: FILL ONLY (1.04:1 on bg); ink on acid 16.39:1 */
  --paper:#fbfaf6;  /* ASSUMED: card and tile paper, lighter than --bg so cards lift */
  --grey:#e1ded5;   /* ASSUMED: third tile tone (ink on it about 14:1) */
}
```
Measured with the WCAG formula (python). Rules, all measured:
- Text colours only: `--ink` on paper/bg/grey/acid/pink (5.55 to 19.44), white `#fff` on ink (19.44), `--pink` on ink (5.55, caption highlight in pink scenes), `--acid` on ink (16.39, caption highlight in acid scenes).
- FAIL as text: pink on bg 3.07, acid on bg 1.04, profile `grey #8c8c8c` on bg 2.95 and on ink 5.78 (passes on ink only; never used). White on pink 3.5 fails: never white text on a pink tile.
- ONE fluorescent per scene (profile rule): scenes alternate pink, acid, pink, acid, pink, acid, pink (s1..s7). The scene's `data-fluo` attribute sets `--fluo`; tiles, stickers, strips, stamp accents, scrawl arrows and the caption highlight all read it. A scene never shows both.
- Ink scrawls are always `#0d0d0d` (or the scene fluorescent on an arrow over paper); never grey.

## 2. Fonts (glyph test of 115 Vietnamese capitals and lower-case letters, PIL notdef-mask method)

| File | Missing glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 | ransom tiles (700), strips (700-800), stickers (800), captions (700 44 px). SUBST for Anton / Rubik Mono One / Be Vietnam Pro |
| `CascadiaMono.ttf` | 0 | kicker tape, typewriter body, addresses (700, 32-56 px). SUBST for Special Elite |
| `cambriai.ttf` | 0 | the italic third of the ransom tiles (Abril Fatface stand-in); never body text |
| `segoepr.ttf` | many (no Vietnamese hooks) | NOT used. There is no Vietnamese-safe marker font installed, so "marker scrawl" is SVG strokes (circle, underline, arrow, cross), not text |

Method note: `fontTools` could not be installed (network install denied); the check renders each of the 115 letters with PIL at 60 px and compares the mask with the mask of U+E123 (a code point no font has). Result: 0 of 115 equal the notdef mask in all three fonts.
Ransom tile fonts: each letter picks sg / cm / cb with the seeded rng (roughly 1/3 each). CascadiaMono has no italic and weight steps: use weight 700 only.

### Type scale (1080 x 1920 px, all ASSUMED; profile gives only 30 px body and 60 px scrawl)
- Ransom tile: fixed width 0.8 em, height 1.2 em, size = floor(936 / ((letters + 0.45 per space) * 0.8)). Built sizes: 181 px ("VÀO CỬA", "NĂM SAU", "THỨ SÁU"), 157 ("MIỄN PHÍ"), 138 (4+4 letter lines), 250 (two-digit date numerals), 117 (a ten-letter word), 104 (inside a card).
- Strip text 58 px SegUIVar 700 (fall back to 50 / 42 / 40 when the line is long; a 28-character caps line fits 936 px at 50 px, 34 characters at 40 px).
- Sticker 64 px 800; stamp 96 px 700; card heading 104-110 px 800; hero money figure 140-150 px 800.
- Kicker 32 px mono; typewriter body 34-44 px mono; notes 32 px; captions 44 px. Smallest text anywhere: 32 px (rule: nothing under 30 px except one footer line; none was needed).

## 3. Safe areas and grid (1080 x 1920)

- Margin 72 px, content width 936 px. Everything is deliberately off-grid by tilt (-6 to 6 deg on tiles, -4 to 4 deg on cards and strips) but the unrotated boxes sit on the 72 / 936 grid.
- y 0-90: empty (platform status). Kicker tape y 96-140.
- Headline block y 170-650 (two ransom lines). Body y 650-1330. **Hold rule: the lowest content edge is at y >= 1250 at every hold**; built holds measured 1301-1331 (section 12 has the table).
- Captions: black tape strip top y 1400, up to 2 lines, y 1400-1570. Body never goes below y 1340. y 1570-1920 empty.
- Photos: white border 16 px, hard shadow `0 6px 0 rgba(0,0,0,.6)`, two grey staples (44 x 10 px) at opposite corners.

## 4. Layers, back to front

1. `#root` `--bg` (flat paper; grain is a separate layer).
2. `#world` (z auto): camera wrapper that the seeded shake moves (+-10 px, +-0.8 deg for 6 frames after each cut).
3. Scene sections `.sc` (`class="clip"`, `data-start`/`data-duration` from `voice/timeline.json`, one per scene). Inside: photo, strips, tiles, stickers, then the SVG scrawl layer `.scr` (z 9) so marker strokes lie on top of paper.
4. `#grain` (z 30): baked 1080 x 1920 RGBA PNG: toner speckles (about 1.5% of pixels, alpha 0.25-0.7 before the 0.7 scale), 9 vertical streaks, edge dirt. 1.2 MB after scaling. Never a live CSS or SVG filter.
5. `#caps` (z 35).
6. `#flash` (z 40): white, 0.9 to 0 in 0.07 s at every cut (not at t = 0).

## 5. Components

- **Ransom line**: `.rline` holds one tile per letter, tiles at fixed 0.8 em pitch with a +-1.5% jitter, tile y jitter +-4% of the size, rotation uniform in -6..6 deg, tile paper = 30% black / 15% grey / rest paper, and the scene fluorescent on only 1-4 chosen tiles per headline (the keyword). Hard shadow `0 5px 0 rgba(0,0,0,.6)`. Set the line width to its content width (see traps).
- **Strip** `.strip`: one line of caps on ink, paper or fluorescent, 5 px hard shadow, tilt +-1.5 deg, padding 0 28 px. The workhorse for every spoken fact ("12 GIỜ TRƯA -> 6 GIỜ CHIỀU").
- **Sticker** `.sticker`: fluorescent, 64 px 800, tilt +-4 deg, one per scene at most (the loud claim: "PHÁ KỶ LỤC NGƯỜI THAM DỰ").
- **Stamp** `.stamp`: ink block with a white word and a fluorescent numeral ("LẦN THỨ 10").
- **Card** `.card`: paper rectangle, 36 px padding, tilt -1 deg, optional tape (200 x 44 px, translucent) on the top edge. `.card.dark` for a negative or an absence.
- **Photo** `.photo`: agy image baked to black and white (autocontrast cutoff 2, contrast x1.6, Gaussian noise sigma 14), white border, stapled. agy draws mood and props only (zine stack, staple gun and scissors); no text, no people.
- **Torn bar** `.bar`: ink rectangle with a zig-zag `clip-path` on the right end; width proportional to the number (a $25 bar next to a $350 bar is 67 px next to 936 px) and a stated ratio line ("Thanh vẽ đúng tỉ lệ 25 : 350") because a derived length needs its derivation on screen.
- **Scrawl**: SVG path, `pathLength=1`, `stroke-dasharray:1`, offset 1 to 0 in 0.3 s, linear, stroke 12-16 px round caps. Kinds: wobbly ellipse (22 points, overshoots 1.1 turns), wobbly line, arrow (line plus two 46 px barbs), X (two lines). The path starts at opacity 0 and is set to 1 at its draw start (see traps).
- **Cassette** (sample t172): paper rectangle with 8 px ink border, label, ink tape window, two reels (finite 540-degree rotation over 9 s, linear), tape slot. Built from divs, no image.

## 6. Motion language

- Everything is a hard event. Entrances are **slams**: `fromTo` scale 1.5 to 1 (1.35 / 1.2 for big blocks) and opacity 0 to 1 over 0.1 s (3 frames), `ease:"none"` (string). No eases, no fades, no back/elastic.
- **Letters assemble one tile at a time**: step 0.05 s (long lines), 0.06-0.07 s (headlines), 0.1 s (two numerals). A 13-tile headline finishes in 1.0 s.
- **Cut = jump cut + photocopy flash + shake**: new scene sections start on the voice scene boundary with no overlap (so no ghost frames); flash 0.9 to 0 white in 0.07 s; `shake()` moves `#world` for 6 frames at 30 fps (+-10 px, decay 1 to 1/6, seeded by the cut time), then resets to 0.
- **Boil** (the "alive" micro-motion on every hold): every 1/8 s each headline tile gets a new seeded rotation (base +-0.9 deg) and y (+-2.5 px); photos and cards boil +-0.35 deg at 6 fps. Nothing on screen is frozen.
- **Marker scrawl** draws 0.3 s linear, started on the keyword (circle on "miễn phí", underline on "tự in", cross on "ban nhạc", arrow after the address).
- Word anchors: `Wt(sid, key, nth)` = estimated word onset minus 0.15 s (clamped to the scene start). Word times from `motion_tools.py voice` are ESTIMATED (share of characters), so a reveal is early, never late.
- Early-fill rule (section 12, trap 5): the lower body is occupied by a photo or a card within 0.5 s of the cut; only the numbers wait for their words.

## 7. Scene recipes (built, 7 scenes; S = scene start)

**R1 Hook (6.19 s).** Kicker tape; "VÀO CỬA" (static from frame 0, ink/paper tiles) and "MIỄN PHÍ" (pink tiles slamming at S+0.15, step 0.05); stapled photo of a zine stack at y 860-1300 (already in at frame 0); pink sticker "PHÁ KỶ LỤC NGƯỜI THAM DỰ" slams on "kỷ lục"; ink ellipse around "MIỄN PHÍ" on "miễn phí".
**R2 Title + definition (9.31 s).** Two ransom lines "LONE STAR / ZINE FEST", ink stamp "LẦN THỨ 10", taped definition card (zine = tạp chí nhỏ, người viết tự làm, tự in, tự đóng ghim) with an ink underline on "tự in", tools photo at right (in at S+0.2), acid strip "TỔ CHỨC AUSTIN ZINE FRIENDS" (y 1140-1290).
**R3 When and where (9.23 s).** Two giant tiles "10" "11" (250 px, the second pink), ink strip "THÁNG MƯỜI", paper strip "12 GIỜ TRƯA -> 6 GIỜ CHIỀU", address card (ransom "BLUE GENIE / ART BAZAAR" at 104 px, mono "6100 AIRPORT BLVD"), pink arrow pointing at the card corner (never across text).
**R4 Tickets and fees (7.87 s).** "MIỄN PHÍ" in acid tiles, paper strip "MỌI LỨA TUỔI ĐỀU VÀO", ink strip "NGƯỜI BÁN · GIÁ THUÊ MỘT BÀN", photo at the bottom (in at S+0.3), torn bars with "$25" and "$350" slamming on their spoken words, ratio note.
**R5 Who is there (9.79 s).** Five strips (ink / paper alternating, pink for the last list item), pink sticker "GÓC TỰ LÀM ZINE", paper strip "DẠ HỘI THẬP NIÊN 80", a stapled photo (in at S+0.3) with a dark card "BAN NHẠC ?" over its lower part and a pink cross drawn on "BAN" when the voice says the official page names no band.
**R6 Friday and after (7.39 s).** Acid ransom "THỨ SÁU", strips "9 THÁNG MƯỜI" and "6 - 8 GIỜ TỐI", "GẤP + GHIM ZINE KHỞI ĐỘNG", "HẾT HỘI CHỢ" with an ink arrow down to the photo, ransom "BREWTORIUM" over the photo, strip "quán bên cạnh".
**R7 Soft ending (6.27 s).** Pink ransom "NĂM SAU / TRỞ LẠI", card "ĐƠN ĐĂNG KÝ BÀN MỞ / cuối xuân hoặc đầu hè / 2027" (pink number box), photo and a source card (domains in 32 px mono) already in at S+0.5. No flash-out, no fade: the last 1.5 s is a full composition.

**Sample recipe (key scene of the style, 10 s, no voice): "headline assembling + physical prop + sticker slap on a photocopy flash + marker circle".** t172: ransom "BĂNG MỚI / CASSETTE", CSS cassette with turning reels, pink "ALL AGES" sticker on a flash at 2.4 s, ellipse at 3.2 s, arrow at 4.0 s, ink strip at the bottom edge. t174: ransom "ĐÊM ZINE / NGƯỜI VIẾT TRẺ", stapled zine photo, taped note "cắt. dán. ghim. viết.", acid sticker on a flash at 2.6 s, underline and ellipse. Both carry "MINH HOẠ" in the kicker and the bottom strip.

## 8. Captions (Vietnamese)

- Black tape strip (`--ink`, 5 px hard shadow), padding 18 x 30, SegUIVar 700 **44 px**, white text, centred, top y 1400, max width 936, up to 2 lines. Chunks of at most 6 spoken words, split after punctuation once 3 words are in; a 1-word orphan is merged into the previous chunk. Caption text is the spoken text (numbers in words); the numerals live in the tiles.
- Current word = the scene's fluorescent (pink 5.55:1 or acid 16.39:1 on ink), set by `tl.set` at the estimated word onset +0.02 s and reset at the next onset. DEVIATION from the profile's single highlight colour, so the one-fluorescent-per-scene rule also holds for the captions.
- Chunk visibility toggled with `tl.set` (no fades). The first chunk of the video starts at 0.15 s.

## 9. Sound

Voice only (VieNeu, about 4.1 words/s; this build 230 words in 56.05 s with `--gap 0.35`; final mux -15.5 LUFS, true peak -4.2 dBFS). The profile calls for 150-180 BPM punk with staple, tape and photocopier SFX; none were available. When music is available: cuts on the bar, flash on the kick, SFX on every slam. Estimated word times drifted up to about 0.3 s on 9 s scenes; the 0.15 s early anchor absorbed it.

## 10. Images (agy)

- Prompt recipe that worked twice (about 1 min each): "High-contrast black and white photocopied xerox photograph of a messy stack of stapled handmade zines and loose paper flyers on a table, top-down, heavy toner grain, harsh flash, cut-out zine look, no text no letters" and "... a table with a staple gun, scissors, glue stick and torn paper scraps, top-down ... no people".
- Output 768 x 1376 JPG. Bake to grayscale (PIL autocontrast cutoff 2, contrast x1.6, Gaussian noise sigma 14) so the grey never looks like colour footage; crop by `object-fit:cover` and `object-position` in the frame (zine stack 50% 30%, tools 50% 40-55%).
- The images are atmosphere, not proof; they show no real event. Reuse is fine (the zine photo appears in s1, s5, s7 at different crops; lint did not object).
- Never ask agy for lettering or a poster: all words are tiles and strips.

## 11. Must not

- No smooth easing, no fade, no blur, no gradient, no glass, no soft shadows (only the hard `0 Npx 0 rgba(0,0,0,.6)`).
- No centred tidy layout: tilt every block and offset strips by 40 px on alternate rows.
- No second fluorescent in a scene; no pink or acid as text colour on paper; no white text on pink.
- No emoji; no cut-off tile (check Vietnamese stacked marks: line box 1.2 em holds them); no text under 30 px.
- No invented number, band, price or lineup. If the source names no band, the screen says so ("BAN NHẠC ?" crossed out, with the sentence) instead of filling the gap. No call to action.
- No live CSS filters for grain; bake PNG. No unseeded randomness.
- No photo of real people or a real place presented as the event.

## 12. Traps seen in real builds (this build, measured)

1. **Story shape did not match the rank-1 shape.** The shape wanted bands, printers and tickets. The only story in 48 h to 33 days was the 10th Lone Star Zine Fest: free entry, table fees, no named band, no printer. Fix: the video says so on screen (free; "Trang chính thức không nêu ban nhạc nào") and states only what the pages state. Cost: the "tickets" beat became a fee comparison ($25 vs $350 table fees).
2. **No story in the last 48 h.** 8 searches (Austin zine fest, fair, bands, printers, tickets, Chronicle, 10th annual) found none; the newest is the event of 10-11 Oct 2026 (33 days old on 2026-11-13). Austin Chronicle calendar pages returned 403 and count as not opened.
3. **Voice too long on the first draft.** 245 words gave 60.21 s; trimming 15 words (shorter date phrases, "Sau bàn bán" cut) gave 230 words = 56.05 s. About 4.1 words/s, so budget 225 words for 55 s.
4. **Missing fonts.** No Anton, Abril Fatface, Special Elite, Rubik Mono One, Permanent Marker. Three local fonts at fixed 0.8 em tile pitch gave an acceptable ransom look; the marker font was replaced by SVG strokes.
5. **Empty lower half until the word arrives.** At S+0.5 the first render showed only the headline for 1.4 s in s4 and s5 (lowest content y 546 in s2 at S+0.5). Fix: a photo or card in the bottom area slams within 0.5 s of every cut; numbers still wait for their words. After the fix: S+0.5 lowest edges 1190-1332 (s2 later moved its photo to S+0.2).
6. **Round-cap dash dot.** With `stroke-dasharray:1` and offset 1 the round cap draws a visible dot ("-" under "MIỄN PHÍ" at 3.0 s). Fix: path opacity 0 until its draw start.
7. **Ransom line width.** `.rline` at width 1080 inside a 936 card overflowed 168 px (inspect `container_overflow`). Fix: set the line width to its content width after building the tiles.
8. **Strips overflowing.** "NGƯỜI BÁN · GIÁ THUÊ MỘT BÀN" at 58 px and the source domains at 34 px mono ran past the box (cut by the card). Fix: 50 px for the strip; the source card 468 px wide at 32 px (21 mono characters = about 395 px). In the samples the 31- and 34-character strips needed 42 px and 40 px.
9. **Card too short.** The "2027" number box was cut by the card bottom (height 260, content about 300); the dark card's 130 px heading overflowed. Fix: card height 300 and heading 110 px.
10. **Frame 0 skeleton.** First render at t = 0 showed only the first tile. Fix: the first headline line and the photo are visible from frame 0; only the second line slams.
11. **File size.** First silent render 33.6 MB and final 27.2 MB (over 25). Cause: full-frame grain over moving content. Fix: grain alpha x0.7 and `render --crf 26`; final 18.3 MB (the mux re-encodes at crf 20 from the cleaner source).
12. **Measuring the lowest edge.** Toner streaks fooled a naive row test (every row "had ink", y 1374). Fix: pixels differing more than 110 from paper and at least 60 such pixels in the row. Result at holds: s1 1313, s2 1301, s3 1311, s4 1314, s5 1330, s6 1331, s7 1320 (all >= 1250); samples 1347 and 1363.
13. **frame_check false BLANK.** `frame_check.py` flagged 6.0 s and 24.5 s (cut frames, first 1-2 frames of a scene) as BLANK; no run of 1.0 s or more. Judged by eye: not a defect (a flash frame or a frame with only the first slam).
14. **Marker circle on the wrong line** in the first t174 sample (placed under the headline, 120 px low). Fix: re-centred the ellipse on the line (cy 490). The stroke still crosses tile tops, which is intended.
15. **Hyperframes lint/inspect.** `timeline_track_too_dense` (7 scene sections on one track) accepted; inspect reports `content_overlap` for the kicker tape over the ransom line box and for the intended photo-under-card layering (6 warnings), no errors. `render` took about 80 s for 56 s at `--crf 26`.
16. **Caption chunk wrapping.** A 6-word chunk containing "Brewtorium" wrapped to two lines at 44 px (ok, band is 170 px tall).
17. **Unknown English words** went to `ear-check.txt` for a native listener's ear (Austin is in the dictionary; Lone, Star, Zine, Fest, Friends, Blue, Genie, Art, Bazaar, Airport, Brewtorium are not). No respelling was applied.
