# Style: functional-playful (9:16 Vietnamese how-to edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** A practical step-by-step "how it goes together" story that can be told as 3-5 numbered jobs with 2-5 plain numbers each: assembly guides, checklists, paperwork steps, "how a factory-built thing is put together on site", "snap apps together from blocks". The story must come with a real instruction document (a manual, a checklist page) so every step and quantity can be traced. Not for deaths, crashes, enforcement, code stories, mood pieces, or a story whose only numbers are statistics. Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the design as built. Section 12 "Traps seen in real builds" is written from THIS build (the first build of the style) with measured numbers; where 12 and an earlier section disagree, 12 wins.

**Clips and screenshots are optional.** This build used none. Never fake or pad media.

**Status.** Written 2026-11-12 from one real build (video `giay-sach-billy-14-buoc-4-viec`, 54.0 s) plus two 10 s samples. No owner document existed before. Source of values: `styles/profiles/functional-playful.yaml`; anything the profile does not give is marked **ASSUMED**.

**Character in one line.** Instruction-sheet clarity with a wink: white pages, 3 px ink outlines, numbered pictogram panels, blue and yellow as solid blocks, yellow tags with a punched hole that swing in, scenes that rearrange into the next scene. Energy 3.

## 1. Tokens

```css
--bg:#ffffff; --ink:#111111; --blue:#1f4fb0; --yel:#f5b416; --birch:#e8d5b5; --sage:#b7c9a8;
--mute:#595959;   /* ASSUMED text-safe grey. The profile's #767676 is only 4.54:1 on white and 3.16:1 on birch */
```

Measured with the WCAG relative-luminance formula (computed by hand in this build, not by a tool; `hyperframes validate` does not report these pairs):

| Pair | Ratio | Use |
|---|---|---|
| ink on white | 18.88 | everything |
| ink on yellow | 10.27 | tag text, caption text, warning card |
| ink on birch | 13.14 | tile numerals, rows |
| ink on sage | 10.72 | tile numerals |
| blue on white | 7.49 | accent words, big numerals, kicker |
| white on blue | 7.49 | badges, tile 13-14, current caption word |
| blue on birch | 5.21 | allowed |
| mute #595959 on white | 7.00 | labels, source line |
| mute #595959 on birch | 4.87 | allowed |
| mute #595959 on sage | 3.98 | **forbidden** (use ink) |
| blue on yellow | 4.07 | **forbidden as text** (this is why the caption's current word is white on a blue chip, not blue on the yellow block) |
| blue on sage | 4.26 | **forbidden as text** |
| yellow as text on white | about 1.9 | **forbidden**; yellow is a block colour only |

Colour rules: blue and yellow only as solid blocks, tags, numerals (blue) and marks; birch and sage as fills; no gradient, no shadow, no glow. The five hues map to meaning in the build: birch = parts and wood, sage = ground and wall, yellow = tags, warnings, ticks, blue = the thing the viewer should read (numerals, badges, accent word).

## 2. Fonts (the profile's Be Vietnam Pro is not installed)

| Role | Profile asks | Used | Vietnamese check |
|---|---|---|---|
| Headline, labels, captions, tags, chips | Be Vietnam Pro 800 / 700 / 400 | `SegUIVar.ttf`, weight axis 300-700, used at 700 (600 for the source line); 800 does not exist | The owner documents record a fontTools test of all 36 test letters (ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ) as present. In this build no tool was available to rerun it, so the check is visual: the 7 scenes and ~50 caption chunks rendered every tone mark used in the script (for example ấ, ế, ệ, ặ, ử, ư, ơ, đ) with no tofu |
| Numerals, step badges, tile numbers | none | `CascadiaMono.ttf` (weight 700) for badges and the tile numbers 1-14 | present; its decimal comma is wide and low, so numerals with a separator ("17.800", "44%") use Segoe 700 with `font-variant-numeric: tabular-nums` instead |
| Never | | `segoepr.ttf` (no Vietnamese letters), `cambriai.ttf` (not needed) | |

Declare both faces with `font-display: block`.

### Type scale (1080 x 1920 px; ASSUMED where marked)

| Token | Size / line | Notes |
|---|---|---|
| `.kick` | 30 / 1.2, 700 uppercase, +0.1em | blue, with a 18 px yellow square before it |
| `.tag` ("VIỆC 1") | 40 / 1.1, uppercase | yellow block, 3 px ink border, radius 10, punched hole 22 px at left |
| `.h1` | 80 / 1.12, -0.02em, max 2 lines | 960 px wide; one `<em>` word in blue; each line <= 21 characters |
| `.sub` / `.sub2` | 34 / 1.2 | mute |
| `.lab` | 36 / 1.15, centred | ink; `.lab2` 30 / 1.15 mute 600 |
| numerals (hero) | 130-210 | Segoe 700 tabular, ink or blue; one hero numeral per panel |
| badge numeral | 44 in a 72 px square | Casc 700 white on blue |
| tile numeral | 84 in a 225 x 176 tile, 40 in a 76 px tile | Casc 700 |
| `.src` | 30 / 1.2, 600 | the only footer line; one line, <= 62 characters (the first 72-character version overflowed) |
| caption | 44 / 1.3, 700 | see section 7 |

No text below 30 px anywhere.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170   platform UI: empty (the yellow tag may start at y 166)
y 176  -236   kicker or tag (+ right-aligned .sub "bước 1-7")
y 246  -430   .h1 (1 or 2 lines of 80 px)
y 450  -1250  BODY, margin 60 (x 60-1020, 960 px wide), panels radius 28, gap 20-40
y 1296 -1326  .src line
y 1344 -1480  caption block (bottom edge 1480)
y 1480 -1920  platform UI: empty
```

The body always ends at y 1250 (lowest panel edge) so the lowest content edge of every hold is 1250-1262, and the source line at 1296-1326 is below it. Layouts used (x, y, w x h):
- 3 x 2 cells: 300 x 380 at x 60/390/720, y 450 and 870 (tools).
- hero panel 960 x 400 (y 450) + 3 tiles 300 x 370 (y 880).
- 2 x 2 pictogram panels: 470 x 400 at (60, 450) and (550, 450) + one wide 960 x 380 at (60, 870).
- hero 960 x 500 (y 450) + lower cards 960 x 270 at y 980, or 960 x 150 and 960 x 100 at y 980 / 1150.
- stat panel 960 x 390 at y 450 + panel 960 x 380 at y 870.
- tall panel 470 x 800 + 2 tag cards 460 x 250 + a 460 x 260 checklist.
- 4 bands 960 x 180 at y 470 / 674 / 878 / 1082 (the grouped list).

Nothing but the caption sits in y 1344-1480.

## 4. Layers, back to front

`.sc` scene sections (white, one per voiced scene, stacked in DOM order) -> inside each: kicker/tag, `.h1`, `.cam` wrapper (all body elements, scaled 1.00 -> 1.02 over the scene, linear, as the micro-motion), `.src` -> `#wipe` (70 px blue bar) -> `#caps` (captions). No flash layer, no shake layer, no fade layer: the first and last frames are full compositions.

## 5. Components

- **Panel** `.pnl`: white, 3 px ink border, radius 28, no shadow. (The profile says 2 px outlines; 3 px reads better on a phone: ASSUMED.)
- **Yellow tag** `.tag`: swings in (rotation -12 -> 0, y -34 -> 0, `elastic.out(1,0.5)`, 0.7 s), transform-origin at the hole. Used for the job number ("VIỆC 1-4"), "2 người", and one warning card.
- **Step badge** 72 px blue rounded square with a white mono numeral (steps 8, 9, 11 in the 2 x 2 panels).
- **Numbered tile** (hook): 225 x 176 in the list, 76 x 76 in the band; fill by group (birch, sage, yellow, blue).
- **Group band** `.band`: 960 x 180, blue badge "VIỆC n" at left, group name 38 px, step range 30 px right.
- **Pictograms** (inline SVG, 3 px ink stroke, round joins, flat fills): five tools, two neutral figures (round head, blob body), a frame that assembles from six parts, a board with pencil marks, a back panel sliding over an outline, a hammer on a pivot, a leaning shelf with a wall and an L-bracket, a warning triangle that becomes a yellow tick circle, 100 small figures (44 filled blue), a shelf with 16 pins and 4 shelves.
- **Checklist row** 56 px: blue number square, 34 px label, yellow stamp tick that lands (scale 1.8 -> 1, `power3.out` 0.25 s).
- **Source line**: always "Nguồn: <maker>, <document>, trang N" and, for a derived grouping, "cách gom nhóm: của chúng tôi".

## 6. Motion language

Energy 3. Allowed eases: `back.out(1.4)` (panels pop, y 26-40 px, scale .82 -> 1, 0.42 s, stagger 0.1), `power3.out`, `power2.inOut`, `power3.inOut` (rearrange, 0.7 s), `expo.out` (travel), `elastic.out(1,0.5)` (tags and the bracket snap only), `bounce.out` (shelves dropping), `sine.inOut` (idle sway, finite repeats sized to the hold), `none` (camera settle). No shake, no flash, no glitch.

| Verb | Recipe |
|---|---|
| Pop-in | panel `fromTo` {autoAlpha 0, scale .82, y 26-40} -> 1, 0.42 s, 0.1 s steps; starts at scene start + 0.12 |
| Tag swing | see section 5 |
| Rearrange (signature) | 14 tiles tween x, y, width, height, fontSize, radius from a 4 x 4 list into 4 colour bands, 0.7 s `power3.inOut`, 0.04 s stagger; bands fade in 0.2 s after the first tile starts |
| Assemble | six parts fly in from six sides (`power3.out` 0.6 s, 0.1 s steps) while dashed guide lines fade out |
| Stamp | tick scale 1.8 -> 1 |
| Drop | `bounce.out` 0.55 s, 0.3 s apart |
| Snap | the leaning shelf (rotation 14 -> 0, `elastic.out(1,0.45)`) as the bracket arrives; the warning triangle fades to a tick |
| Highlight pulse | the spoken object scales 1 -> 1.05-1.1 -> 1 in 0.4 s |
| Idle | tools sway +-2.5 deg, tag sway +-2 deg, tiles +-1.2 deg; camera settle 1.00 -> 1.02 |

Transition (one language for the whole video): **blue block wipe**. The incoming scene is revealed with `clip-path: inset(0 100% 0 0) -> inset(0)` over 0.3 s `power2.inOut`, starting 0.1 s before the scene start, while a 70 px blue bar rides the boundary; the incoming kicker and headline are part of the revealed section, the body pops in 0.12-0.7 s later. Clip-path is set back to `none` 0.02 s after the end and the outgoing scene hidden. The profile's other transitions (flat-pack fold, tag flip) were not used; "room rearrange" is used inside scene 1 and as the recipe of the t171 sample.

## 7. Captions

Yellow block `rgba(245,180,22,0.95)`, radius 4, padding 10 x 18, 44 px 700 ink, centred, bottom edge y 1480, max width 980. Chunks <= 6 words, split after punctuation once >= 3 words. The current word gets a blue chip with white text (7.49:1); the profile's "current word blue" is rejected because blue on yellow is 4.07:1. First chunk 0.02 s before its first word.

## 8. Scene recipes (S = scene start; word anchors from the estimated timeline)

| Scene | Recipe |
|---|---|
| R1 Hook | kicker, 2-line headline "14 bước, gom lại / thành 4 việc", 14 numbered tiles already in a 4 x 4 list on frame 0 (final, no counting); at the word "gom" - 0.35 s the tiles rearrange into the 4 colour bands; the second "bốn" pulses the accent word |
| R2 Inventory | 3 x 2 grid of 300 x 380 pictogram cells (5 tools + a "2 người" cell), pop-in 0.1 s apart from S+0.12, tag on the word, one cell pulses on its spoken word |
| R3 Job with quantities | tag "VIỆC n" + sub "bước a-b", assembling pictogram in a 960 x 400 hero, three quantity tiles (numeral 140 px + label) that pulse on their spoken number |
| R4 Pictogram panels | 2 x 2 grid (two small panels + one wide), each with a step badge, one figure or tool performing one action; the wide panel carries the quantity (190 px blue numeral) and the repeated action (hammer taps, 18 dots pop) |
| R5 Diagram + warning | hero diagram (leaning shelf, wall, bracket) over one card; at the word that starts the warning (-0.1 s) the card is replaced (0.12 s out, 0.3 s in) by a yellow warning card and a beige card |
| R6 Statistic | stat panel (numeral 210 px + 2 label lines) + 100-figure pictogram panel with the share filled blue on the spoken number |
| R7 Closing | the last job's construction (pins pop, shelves drop) + two quantity tags + a 4-row checklist whose first three ticks stamp at S+0.7/0.9/1.1 and the fourth when the last shelf lands; last 1.6 s hold the full composition |

## 9. Sound

Not built (no music tool in this build). The profile's sound (light Scandinavian pop or whistling, 100-115 BPM; wooden knocks, allen-key clicks, tape rip on folds) is untested. The video is voice only; the mux normalised it to -15.7 LUFS, peak -4.2 dBFS (target was -14 LUFS; the shorter-than-expected mux gain came from `loudnorm` on a speech-only file).

## 10. Images

The tool `image` (agy) returned one bookshelf illustration (97 s). Flat colours were right (birch, sage, thin ink outline) but the geometry was wrong (a floating top board, shelves of different depth, arrows in the sides) and it showed 6 boards where the source sheet has 4 loose shelves, so it would contradict a number on screen. It was NOT used. Every picture in the video is inline SVG drawn for the style. Guidance for agy in this style: "flat vector, 2 px dark outline, birch and sage fills, white ground, no gradients, no shadow, no text"; keep the subject simple (one object, front view) and never place a generated object next to a count.

## 11. Must not

- No gradient, glow, shadow, glossy 3D, neon, emoji, hard cut (use the wipe).
- No blue text on yellow or sage; no yellow text; no mute grey on sage.
- No empty panel and no counter: numerals are final from the moment their panel appears (the hook has none).
- No text under 30 px; no more than one footer line; nothing below y 1480; nothing but captions in y 1344-1480.
- No number or part name a page does not state. A visual reading of a pictogram (e.g. "chốt gỗ" for the ribbed dowel) is allowed only when the page prints the quantity; a material the page does not state ("kim loại") is not.
- A derived grouping says so on screen ("cách gom nhóm: của chúng tôi").
- No real product name outside the one named source; no catalogue pages, logos or brand fonts.
- No advice, no prediction, no hype.

## 12. Traps seen in real builds (this build, 2026-11-12, 54.0 s, 217 spoken words)

Measured results first: `frame_check.py` on silent and on final = 108 frames, 0 BLANK, 0 TOPHEAVY; lowest content edge 1250 (panels) / 1262 (hook bands) with the source line at 1296-1326; lint 0 errors / 2 warnings (file longer than 300 lines, expected); inspect 0 layout issues after the fixes below; render 25 s for 54 s, silent 6.3 MB at `--crf 24`, final 7.8 MB.

1. **GSAP overwrites an SVG `transform` attribute.** The pencil, figure, screwdriver, hammer and warning triangle each had `transform="translate(...)"` on the same `<g>` that GSAP tweens (x, y, rotation). The first snapshot showed them jumped to the panel's top-left corner and the hammer detached. Fix: an outer `<g transform=...>` for the fixed position, and tween only the inner `<g>`. Check every animated SVG group in the first snapshot.
2. **A 72-character source line overflowed the 960 px box** (cut at "gom" in the hook, seen at 0 s in the contact sheet). 30 px Segoe 600 fits about 62 characters; the hook line was shortened to "Nguồn: IKEA, BILLY, bản 6/10/2021 · cách gom nhóm: của chúng tôi".
3. **A big numeral beside a grid collided with it.** In the wide panel of recipe R4 the 190 px "18" overlapped the last column of nail dots (seen in a transition frame at 28.7 s). Fix: dots start at x 385 with 52 px pitch and the board narrows to 330 px; the numeral keeps `right:50px; top:80px`.
4. **`inspect` flagged `container_overflow` on every `.cam`** (the 1.02 settle grows the wrapper 4-21 px past the frame) and `content_overlap` between a 140-210 px numeral line box and its 36 px label. Both are intentional: `data-layout-allow-overflow` on `.cam`, `data-layout-allow-overlap` on `.num` / `.lab2`. In the samples, blocks travelling over each other raised `text_occluded` at 2.78 s: `data-layout-allow-occlusion` on the moving blocks.
5. **Contrast validator noise.** `hyperframes validate` reports 15 warnings, all in three kinds: tile "13"/"14" "1:1" and the caption word "Mười" "1.78:1", at the times (5.4, 16.2, 27, 37.8, 48.6 s) when the page is sampled while the scene or the caption is hidden or mid-switch. The same frames in the snapshots show white on blue at 7.49:1. Accepted; do not "fix" by changing colours.
6. **Estimated word times.** `voice/timeline.json` spreads each scene's speech over its words by character count, so anchors can be 0.3-0.6 s off in the 10 s scene. Design so that an anchor miss is harmless: panels appear at scene start, not on a word; only pulses, tags and the warning swap hang on words (scene 5 swap at the word "Tờ" - 0.1 s). A word-level forced alignment would let the snap and the 16-pin pop land exactly.
7. **A fact slipped into the first script and was caught in review.** The first script said "thanh góc kim loại" (metal bracket); no opened page states a material. Fixed to "thanh góc" (script, on-screen card, anchor word), voice re-run: 52.85 s -> 52.45 s, scene starts after scene 5 moved by -0.40 s and were updated in the page. Re-run the voice step and re-read the page text whenever one word of the script changes.
8. **Quantities are read from drawings.** The manual has no text labels for parts, only counts next to pictures (22x, 12x, 18x, 12x, 16x, 2x). Part names on screen are descriptions of the pictures; the selfcheck lists each as "read from the drawing". Total cam locks (12) was derived by adding 4 + 2 + 6 from three steps; it equals the 12x in the parts list.
9. **Wipe frames.** A 0.3 s wipe shows two scenes split by a blue bar; `frame_check.py` samples every 0.5 s and found no BLANK frame. Frame 215 (7.17 s) shows the split; no frame shows a semi-transparent ghost.
10. **Frame 0.** Hook frame 0 shows the finished kicker, headline and 14 tiles (no mask, no fade-in). The last frame (1619) shows the full closing composition with all four ticks.
11. **Sample clips.** A generic "Minh hoạ" scene needs no research but still needs a real recipe: the t171 sample (4 modules from a "nhà máy" row rearrange into a 2 x 2 house on a "khu đất" plot, tag "Ghép xong", 3 chips) leaves the factory panel empty after 4.0 s; accepted because the scene is full elsewhere, but a labelled "đã chuyển" ghost would be cleaner.
12. **Do not use `rm` or compound shell lines in the build folder.** This environment only allowed single commands; helper Python scripts could not be run, so all timing is computed in the page from the voice timeline numbers (scene start and speech length pasted by hand).
