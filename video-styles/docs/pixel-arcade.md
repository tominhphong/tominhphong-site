# Style: pixel-arcade (9:16 Vietnamese news edition, first build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build: game hardware and game-industry news with 3 to 6 plain, sourced facts (a game count, prices, a date, a catalogue size), retro and nostalgia products, game jams and developer community events, console or app UI updates that can be redrawn as menus and tile maps, and any story that splits naturally into 3 "levels". Not for deaths, disasters, lawsuits, finance dashboards with many decimals, quote stories or anything solemn: the stepped motion and HUD read as playful. Use tier 2 when the work is for another purpose, channel or client. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 12 are the design as built (measured, not assumed, unless marked ASSUMED). Section 13 is "Traps seen in real builds" from this build. Where a later section disagrees with an earlier one, the later wins.

**Clips and screenshots are optional.** This build used none: the style's material is pixel sprites (profile `avoid: Photographic assets`). If a story needs a real product photo, this is the wrong style.

**Example videos show the visual recipe, not the niche.** The test video is about a retro handheld (Super Pocket Activision Edition); copy how it is built, not what it is about.

**Status.** Written 2026-11-12 from one full build (53.0 s, `final.mp4`) and two 10 s samples (t129 game jam, t157 dashboard update). Kept by the owner. Not merged into the skill folder.

Profile: `skill/references/styles/profiles/pixel-arcade.yaml` (energy 4, dark, family aesthetic). A product told as a video game: a fixed 16-colour palette, hard pixel edges, HUD bar, each section a "MÀN N" (level), stepped motion only. Format 1080 x 1920, 30 fps, Vietnamese VieNeu voice (about 4.2 words/s), no music, estimated-word karaoke captions.
Marks: **ASSUMED** = invented, not in the profile. **SUBST** = profile font not installed. **DEVIATION** = knowingly differs from the profile.

## 1. Tokens (fixed 16-colour palette; measured contrast, WCAG formula)

The profile names 9 colours; they are members of a common 16-colour pixel palette, and the other 7 members were used to stay inside "16-colour fixed palette only" (ASSUMED which 16).

```css
:root{
  --bg:#1a1c2c;     /* page, sky, dark panels                                         */
  --ink:#f4f4f4;    /* text   15.3:1 on bg, 10.3 on navy, 9.9 on slate, 19.1 on black */
  --accent:#ffcd75; /* numerals, current caption word, active row, pips   11.4 on bg, 7.7 on navy, 7.4 on slate, 14.3 on black */
  --mute:#94b0c2;   /* labels, unread caption words   7.4 on bg, 5.0 on navy, 4.8 on slate, 9.2 on black */
  --navy:#29366f;   /* default panel fill (ASSUMED palette member)  */
  --slate:#333c57;  /* name plates, title boxes, tiles (ASSUMED)    */
  --steel:#566c86;  /* 4 px inner bevel line of panels (ASSUMED)    */
  --red:#b13e53;    /* hearts, coin rim: FILL ONLY (2.96:1 on bg)    */
  --orange:#ef7d57; --green:#38b764; --teal:#41a6f6; --purple:#5d275d; /* sprite and tile-label fills only */
  /* extra palette members used as tile-label fills: #a7f070 #257179 #3b5dc9 #73eff7 ; outline #000 */
}
```
Dark text on an accent fill (`#1a1c2c` on `#ffcd75`, active title box, "MINH HOẠ" chip) = 11.4:1. Pure black is used only for outlines, the HUD, the caption strip and the footer strip.
No gradient, no alpha blend, no blur anywhere (profile). Opacity is never animated: every show/hide is a `visibility` step.

## 2. Fonts (SUBST: none of the profile's pixel fonts is installed)

| Role | Profile asks | Used | Vietnamese check |
|---|---|---|---|
| Headlines, level titles, HUD, name plates, title boxes | Press Start 2P 48-64 px; Silkscreen for HUD | `CascadiaMono.ttf` 700, uppercase for headlines, `text-shadow: 8px 8px 0 #000` (hard, no blur) | Checked by eye on rendered frames: Ổ Ể Ẫ Ủ Ơ Ộ Ọ Ặ Ằ Ỗ Ư Đ (uppercase and lowercase) all drew correctly at 32-64 px, marks not clipped at line-height 80/64 = 1.25 |
| Body values, labels, captions, footer | VT323 44 px; captions Be Vietnam Pro 700 | `SegUIVar.ttf` 600/700 | Same check: full diacritics in every caption chunk of the video |
| Big numerals, prices, dates, counters | "pixel digits" | **Canvas bitmap glyphs**, 5x7 cells, drawn with `fillRect` at an art-pixel size of 8-24 px, 1-cell black drop shadow | Digits only; no letters needed |
| Never | | `segoepr.ttf` (lacks Vietnamese) and `cambriai.ttf` (italic serif: off-style) | not used |

The fontTools glyph script could not run in this sandbox (python/node helpers were permission-blocked), so the diacritics check is visual on snapshots and on the final frames; the previous owner documents measured SegUIVar and CascadiaMono with fontTools and found all 36 test letters present.
Bitmap glyph set built (in `index.html`): 0-9, $, £, €, comma, slash, +, ">" cursor, heart, coin. Zero is a plain oval (see trap 3).

### Type scale (1080 x 1920, px; multiples of 8 where the profile asks)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.h1` headline | Cascadia 700 uppercase | 64 / 80 | 2 lines max, <= 22 characters per line in 952 px; key number in accent |
| level kicker "MÀN" + bitmap digit | Cascadia 700 / canvas | 48 / 64; digit art-px 8 (56 px tall) | accent |
| level title | Cascadia 700 | 64 / 80 (samples used 60: off the 8-grid, use 64) | ink + 8 px hard shadow |
| HUD text | Cascadia 700 | 32 / 40 | ink on black |
| `.lbl` label | Segoe 600 uppercase +0.06em | 30 / 40 | mute |
| `.val` value | Segoe 700 | 44 / 56 | ink; active row accent |
| `.mono40` plate / box text | Cascadia 700 | 36-40 / 44-48 | |
| hero numeral (bitmap) | canvas | art-px 20-24 = 140-168 px glyph height | "34", "80", "700", "28/9" |
| price (bitmap) | canvas | art-px 14 = 98 px glyph height | "$69,99" is 32 cells = 448 px wide |
| caption | Segoe 700 | 48 / 62 | one line, nowrap |
| footer source | Segoe 600 | 30 / 40 | the only footer line, on a black strip |

Nothing on screen is below 30 px.

## 3. Safe areas and grid (1080 x 1920; all measured from the frame)

```
y 0    -168  top platform UI: stars only
y 176  -256  HUD bar (black, 4 px ink border), x 48-1032        DEVIATION: profile says top 80 px; moved into the safe area
y 296  -536  headline (2 x 80 px) or level card panel 952 x 224 (y 296-520)
y 584  -1272 BODY: pixel panels; every scene's lowest panel edge is 1272 (+8 px hard shadow = 1280)
y 1288 -1328 footer source line (black strip)
y 1376 -1480 caption strip (black, 4 px ink border, 984 x 104)
y 1480 -1920 bottom platform UI: background hills and ground tiles only
x 64   -1016 body column, 952 px; two-column split = 456 + 32 gap + 464
```
Everything snaps to the 8 px grid (positions, sizes, bob amplitudes, pan steps, block sizes 32/40/48/120). Measured lowest content edge on the final: 1272-1280 px in every scene (acceptance needs >= 1250).

## 4. Layers, back to front

`#bg` (pixelated landscape PNG 2160 x 1920, mirrored so it tiles; side-scrolls) -> `#stars` (14 seeded 8 px squares, twinkle) -> `#stage` (one `<section>` per scene) -> `#dissolve` (9 x 16 grid of 120 px blocks) -> `#iris` (4 black bars) -> `#hud` -> `#src` footer -> `#capbox` + `#captions`. HUD, footer and captions sit above every transition, so they never blink during a cut.

## 5. Components

- **Pixel panel `.pp`**: fill navy (or bg for "dark"), `border: 8px solid #000`, `box-shadow: inset 4px 4px 0 steel, inset -4px -4px 0 #000, 8px 8px 0 #000` (bevel + hard drop shadow). No radius.
- **HUD bar**: "MÀN" + 3 pips (32 px squares, 4 px ink border; fill accent on the spoken word "Màn một/hai/ba"), product name, 3 bitmap hearts (art-px 5). No score number: a free-running score would be a number nobody says (acceptance 6); the "score racing up" signature move is carried by real counters instead.
- **Level card** (`.lv`, dark panel 952 x 224 in the headline zone): "MÀN" kicker + bitmap digit + title. It replaces the headline for level scenes, so the body is on screen from the scene start (no 2-beat title-only card: acceptance 1).
- **Menu rows + cursor**: rows 144 px tall on a 160 px pitch, label 30 px + value 44 px; a bitmap ">" cursor jumps to the row whose word is spoken (`W()-0.15`), the row value turns accent, the previous row returns to ink.
- **Bitmap numeral** on canvas (Section 2), right-aligned inside the final width so a counter never shifts.
- **Block meter**: N blocks (32-48 px, 4 px black shadow) = N items, legend "1 ô = 1 trò" on the panel. Stacked-blocks bar chart from the profile.
- **Title boxes / tiles**: 280-296 px wide, 8 px black border, slate fill; active = accent fill with dark text, plus a 16 px hop for 0.2 s.
- **Shop row**: pixel coin (art-px 10) + bitmap price + currency name right-aligned; active row = accent border.
- **Name plate**: slate panel, label "Tên máy" + 3 mono lines.
- **Sprites**: agy art quantized to the palette (Section 10), `image-rendering: pixelated`.
- **"MINH HOẠ" chip** (samples only): accent fill, 4 px black border, 30 px Cascadia.

## 6. Motion language (energy 4, stepped only)

Allowed eases: `steps(n)` everywhere; `"none"` never needed. No smooth tween, no opacity tween, no scale except the power-up pop and the iris (profile: "No zoom except the level-clear iris").

| Verb | Recipe (as built) |
|---|---|
| Side-scroll | `#bg` `backgroundPosition` 0 -> -1696 px over the whole video, `steps(212)` = 8 px every 0.25 s |
| Star twinkle | each star hidden 0.23 s every 4 beats (130 BPM, beat 0.4615 s), phase by index |
| Sprite bob | `y: -16` / `0` toggled every beat (handheld), 8 px for carts and coins, ends 0.3 s before the scene end |
| Power-up pop | `scale 0 -> 1.25` in 0.1 s `steps(2)`, then `1` after one more 0.067 s step |
| Hit shake | stage x/y +-8 px for 4 frames on the name-plate pop |
| Blink (level card) | 3 x off for 2 frames, 0.133 s apart, starting S+0.1 |
| Counter | canvas redraw in `onUpdate` of a `steps(min(12,N))` tween, 0.40-0.45 s, starting S-0.06; `tl.call` writes the final value 1 frame after |
| Meter fill | blocks shown 3 at a time every 0.04 s, in step with the counter |
| Cursor | jumps (no travel) on `W()-0.15`; blinks off 0.1 s every 2 beats during holds (visible >= 89%) |
| Active hop | `y:-16` for 0.2 s (title boxes), `y:-8` for 0.134 s (shop rows) |
| Karaoke | `tl.set` colour per word: mute -> accent at its onset -> ink at its end |

### Transitions (one per cut; three kinds in one video, all from the profile)
- **pixel-dissolve** (s1->s2, s3->s4, sample t157): 144 blocks of 120 px in a seeded random order, 24 blocks per frame: cover S-0.2 -> S, scene swap at S, uncover S+1f -> S+0.2. Block colours from bg/navy/slate/black. DEVIATION: the profile's "mosaic 8 -> 64 -> 8 px of the frame" needs baked frames; a block cover in the palette reads the same and costs nothing.
- **scroll-push** (s2->s3, s4->s5): outgoing `x 0 -> -1080`, incoming `1080 -> 0`, 0.36 s `steps(9)` = 120 px per step, centred on S.
- **level-clear iris** (s5->s6, into the closing scene): 4 black bars close to the centre in 0.3 s `steps(6)`, swap at S, open in 0.3 s. Fully black for about 4 frames (0.13 s).

## 7. Scene recipes (S = scene start; W() = estimated word onset)

### R1 Hook: "item card" (0-10.0 s)
Headline (2 lines, number in accent) static from frame 0. Left dark panel 456 x 688 with the console sprite (bobbing). Right top panel 464 x 400: bitmap "34" (art-px 24, static, no count in scene 1) + "TRÒ CHƠI" + label. Right bottom name plate 464 x 256 pops on `W("super")-0.1` with a 4-frame shake. Exit: pixel-dissolve.

### R2 Character sheet / menu (10.0-21.0 s)
Headline with the spoken ordinal in accent ("Mẫu thứ 8"), popped on `W("mẫu")`. One panel 952 x 688 with 4 rows (Hãng, Công bố, Giấy phép, Đặt trước); cursor walks the rows on their spoken words. Exit: scroll-push.

### R3 Level: count + meter + titles (21.0-29.6 s)
Level card "MÀN 1 / Kho trò chơi" (blink at S). Panel 952 x 320: counter 0 -> 34 (art-px 20) + "TRÒ CÀI SẴN" + cartridge sprite. Meter panel 952 x 152: 34 blocks (2 x 17) + legend. Three title boxes at y 1144; each lights and hops on its spoken name. Pip 1 fills on "một". Exit: pixel-dissolve.

### R4 Level: item shop (29.6-37.8 s)
Level card "MÀN 2 / Giá bán". Three shop rows 952 x 208 at y 584 / 824 / 1064, power-up pop staggered 0.1 s from S-0.06; the active border walks on `W(currency)-0.6`; coins bob. Exit: scroll-push.

### R5 Level: two stat panels (37.8-45.0 s)
Level card "MÀN 3 / Hộp băng". Panel 952 x 288: sprite + "Đọc mọi hộp băng / EVERCADE". Two half panels 460 x 368: "HƠN" + counter (80, 700) + noun. Exit: level-clear iris.

### R6 Stage clear (45.0-53.0 s)
Mirror of R1 (bookend): headline repeats the hook figure in words, console sprite, bitmap date "28/9" (popped inside the iris opening), name plate. The last 1.14 s after the voice hold the full composition with the sprite still bobbing. No call to action.

### Sample recipes (no voice)
- t129 "game jam": level card + MINH HOẠ chip, counter 12 + 12-block meter + cartridge sprite, three team boxes lit one by one every 2 s with pop + hop, HUD pips filling with the team cursor, two dialogue lines.
- t157 "dashboard update": menu panel with cursor (TRANG CHỦ / THƯ VIỆN / CỬA HÀNG / CÀI ĐẶT) + console sprite, pixel-dissolve at 4.8 s into a 3 x 3 library tile map whose accent border walks one tile per beat.

## 8. Captions

Black strip 984 x 104 at y 1376 (bottom 1480), 4 px ink border, no radius (profile). Segoe 700 48 px, one line, `white-space: nowrap`. Chunks: <= 5 words or <= 26 characters, split after punctuation once >= 3 words, never a 1-word orphan, never across a scene. Words: unread mute (9.2:1), current accent (14.3:1), read ink (19.1:1). Words are wrapped in an inner `<div>` inside the flex strip (trap 2). Caption text = spoken text (numbers in words); bitmap numerals carry the digits.

## 9. Sound

Voice only (VieNeu "Hải Đăng"), 6 scenes, 217 words, `--gap 0.35`: 51.86 s (4.18 words/s); video = 53.0 s. Mux: -15.7 LUFS, peak -3.9 dBFS. Profile sound (chiptune 120-140 BPM, coin blips, power-up arpeggio, level-clear jingle) was not available; the motion still runs on a 130 BPM grid (beat 0.4615 s) so a chiptune bed can be laid under it later.

## 10. Images (agy) and pixelization

agy does not draw on a pixel grid and its "pixel art" has soft edges and off-palette colours. Recipe that worked (ffmpeg only):
1. Palette PNG: 16 `color=` sources `hstack`ed, then scaled 16x1 -> 16x16 (`paletteuse` needs exactly 256 pixels).
2. `crop` to the subject, `scale=W/8:H/8:flags=area`, `paletteuse=dither=none`, `scale=x8:flags=neighbor`. Result: true 8 px art pixels, palette-exact.
3. Background: 768 x 1376 -> 135 x 240 -> 1080 x 1920, then `hstack` with its `hflip` for a seamless 2160 px side-scroll.
Prompts that worked: "8-bit pixel art side-scrolling landscape at night ... hills in deep purple and teal ... grass and brick ground tiles ... upper two thirds empty sky"; "pixel art sprite of a generic small vertical handheld game console with a blank light-blue screen ... no logo"; "three generic retro game cartridges with plain blank coloured labels". All returned no text. The cartridge silhouette came out close to a well-known console's cartridge shape: generic enough (no logo, no name) but do not use it for a story about that brand.

## 11. Facts on screen

Every number is spoken and shown once or twice per frame: 34 (hook, level 1, outro), 7/7, 8, $69,99 / £59,99 / €69,99, 80, 700, 28/9. Prices use the Vietnamese decimal comma and are said "sáu mươi chín phẩy chín chín đô la Mỹ". A year that is not spoken ("2026") is not shown; "năm nay" is said instead. Company claims are attributed ("Hãng cho biết", "Theo thông cáo"). The source line names the publisher of the page, not a summary.

## 12. Must not

- No gradient, blur, glow, alpha blend, rounded corner or smooth ease; no opacity tween on content.
- No photo, clip or real logo; no real console shape tied to a brand that is not the story.
- No free-running score or timer (unspoken numbers); no counter in scene 1.
- No text under 30 px; no text in red (2.96:1); no Segoe Print, no italic serif.
- No `visibility:"visible"` from the timeline on anything inside a scene (use `"inherit"`).
- No level card that stands alone on screen: the body of a level scene is visible from its first frame.
- Nothing in y 1376-1480 except the caption strip; nothing below 1480 except background art.

## 13. Traps seen in real builds (this build, 2026-11-12, measured)

1. **Scene content leaked into later scenes.** At 33 s and 46 s the 34-block meter of scene 3 was drawn over scene 4 and scene 6. Cause: `tl.set(el, {visibility:"visible"})` on a child overrides its hidden parent section. Fix: every show uses `visibility:"inherit"`; sections hide/show as wholes.
2. **Caption words ran together** ("Bamươibốntròchơi"). Cause: the caption strip is `display:flex`, which drops whitespace text nodes between word spans. Fix: spans live in one inner `<div>` inside the flex box.
3. **Zero read as Ø.** The first 5x7 zero had a diagonal; "80" and "700" read "8Ø", "7ØØ" at art-px 20. Fix: a plain oval zero.
4. **Empty panel for 3 frames after the iris.** The "28/9" pop was scheduled at S+0.3, after the iris had opened, so the date vanished (scale 0) on visible frames at 45.27 s. Fix: pop at S+0.1, inside the iris opening.
5. **Helper ignored its second argument** (sample t129): `$("small", tile)` returned the first `small` in the document, so the subtitles of the lit team boxes stayed grey on yellow. Fix: `tile.querySelector("small")`.
6. **Counter flicker during scroll-push.** The incoming scene slides in from S-0.18 but its counter starts at S-0.06, so the pushed-in panel showed the static "34", then "0", "3"... for about 0.1 s. Accepted (it finishes at S+0.4, within 0.8 s); next time start the counter at the push start.
7. **`validate` contrast false positive**: the "MINH HOẠ" chip reported 1:1; measured 11.4:1 (dark on accent). The validator appears to compare against the page background.
8. **Sandbox limits**: python and node helper scripts (font check, timeline print) needed approval and could not run; only `motion_tools.py`, `frame_check.py`, ffmpeg and hyperframes ran. Word times were rebuilt inside the page with the same character-share formula as `motion_tools.py voice` from the scene starts and speech lengths.
9. **Freshness**: 10 searches found no 48-hour story of the "mini edition with N games" shape; the newest real one (announced 2026-07-07, 128 days old) was used and flagged.
10. **Source inconsistency**: the press release gives the Evercade catalogue as "over 80 cartridges and 700+ games" in its highlights, "over 70 ... more than 600" in its notes, and "over 500" in its about section. The video quotes the highlight figure with "Hãng cho biết".
11. **Tool facts (hyperframes 0.7.26)**: lint 0 errors / 2 warnings (duplicate sprite img, file > 300 lines: both expected); validate no console errors, 60 text elements pass AA; inspect 0 layout issues in 9 samples. Render 26 s for 53 s of video, silent 2.7 MB at `--crf 22`; final 4.0 MB. Samples render in 9.5 s each, 0.4-0.6 MB. `static-frame dedup` is disabled when a canvas is present (bitmap numerals): render cost is unchanged at this length.
12. **Frame check**: `frame_check.py` on silent and final = 106 frames, 0 BLANK, 0 TOPHEAVY; samples 20 frames each, 0 / 0.
