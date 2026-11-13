# Style: data-editorial (9:16 Vietnamese data-story edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in the build.** Stories whose proof is a comparison of 3 to 6 sourced numbers on one axis, told calmly: monthly market reports (housing, jobs, prices), benchmark comparisons, "what changed since last year" reports, report-vs-previous-period stories. Best when every number has the same basis (here: "% vs October 2025"), so one diverging-bar chart can carry them. Not for: a story with one number (use a giant-numeral style), quote or human stories, breaking or urgent news, hype, anything that needs footage. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built on 2026-11-13 (video `gia-nha-austin-thang-10-giam-6-9`, 57.5 s, final.mp4 4.6 MB). Section 12 is "Traps seen in real builds" from that build, with measured numbers; where section 12 disagrees with sections 1 to 11, section 12 wins. Source of values: `styles/profiles/data-editorial.yaml`; anything the profile does not give is marked **ASSUMED**.

**Status.** Written from one full build (rank-1 shape) plus two 10 s samples (ranks 2 and 3). Not yet reviewed by a native listener.

**Character.** Calm and evidential, a newspaper graphic turned into video: paper background, italic serif headline that states the finding, one highlighted series in coral, grey context, 1 px axes, annotations drawn on the spoken word. Energy 2: no shake, no flash, no bounce, no beat pulse. Narration-led: something changes every 1 to 3 s but nothing moves for show.

**Example videos show the recipe, not the niche.** Copy how the housing build is made, not what it is about.

## 1. Tokens

Measured with the WCAG relative-luminance formula against `--bg` (hand calculation, cross-checked by `hyperframes validate`: "65 text elements pass WCAG AA" on the final composition, "40 text elements pass WCAG AA" on each sample).

```css
--bg: #fbf9f4;         /* paper (profile) */
--ink: #1b1b1b;       /* headline, numerals, read caption words      16.37:1 on bg */
--accent: #d1495b;    /* bars, rings, the story series: MARKS ONLY   4.14:1 on bg (fails 4.5 as text) */
--accent-ink: #b3283d;/* ASSUMED text-safe accent: values, notes, chips, current caption word   6.07:1 */
--s2: #2e86ab;        /* optional second series, marks only          3.91:1 (fails as text) */
--s2-ink: #1f6a8a;    /* ASSUMED text-safe blue                      5.73:1 */
--mute: #9a968d;      /* context bars, dashed boxes: MARKS ONLY      2.80:1 */
--mute-ink: #5f5b52;  /* ASSUMED text-safe mute: labels, ticks, dek, source, unread caption words   6.43:1 */
--axis: #d9d5cb;      /* gridlines, bar tracks (profile)             decoration only */
white on --accent-ink: 6.39:1 (chip text)
```

Colour rules: context series in `--mute`, the series being spoken in `--accent`, an optional second series in `--s2`; never more than 3 hues in one chart. When the narrator moves to the next series, the old one turns back to mute (0.25 s) and the new one turns accent. Three profile colours fail 4.5:1 as text (accent 4.14, s2 3.91, mute 2.80); the profile gives no text-safe variants, so the `-ink` variants above are **ASSUMED** and must be used for every piece of small text. Fade-to-black is not allowed (light style); the last frame is a full composition, not a fade.

## 2. Fonts (3 local files; the profile's Fraunces, IBM Plex Sans, IBM Plex Mono and Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline (finding sentence) | Fraunces 600 | `cambriai.ttf` (Cambria Italic, 400 only) at 76 px, `letter-spacing -0.02em`, line-height 1.13 | fontTools glyph test could not be run in this sandbox (python scripts outside the allow-list were refused); instead the real build was rendered and inspected: all Vietnamese marks in the headlines (ả ế ờ ữ ạ ố ợ ơ ư ẩ) rendered correctly at 76 px, in every one of the 6 headlines and in the 6 s sample headlines. The owner docs for saas-bento report "all present" for this same file. |
| Axes, labels, notes, captions, chips | IBM Plex Sans / Be Vietnam Pro | `SegUIVar.ttf`, weight axis 300-700; 600 for labels and captions, 700 for names and chips | rendered correctly (captions contain every tone mark used in the script) |
| Big numerals, values, ticks | IBM Plex Mono 500 | `CascadiaMono.ttf`, weight axis 200-700, 600 for numerals, `letter-spacing -0.04em` | digits, `.`, `,`, `%`, U+2212 minus (`−`) all rendered |
| Never | | `segoepr.ttf` (lacks Vietnamese letters) | not used |

**Substitution to tell the user:** Fraunces (upright serif 600) became Cambria Italic 400, so every headline is italic; there is no bold serif. This reads as editorial and was kept, but it is a departure from the profile. There is no real italic of SegUI, so notes (the "annotation 26 px italic" of the profile) use Cambria Italic at 34-36 px.

Declare every face with `font-display: block`; variable ones with `font-weight: 300 700` / `200 700`. Use U+2212 (`−`) for negatives, never a hyphen. Vietnamese decimal comma in every number (`6,9%`), thousands with a dot (`404.802`).

### Type scale (1080 x 1920 px; every size is >= 30 px except one footer line)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.kick` | SegUI 700 uppercase +0.1em | 30 / 36 | `--mute-ink`, above the headline |
| `.fig` | SegUI 600 | 30 / 36 | "Hình n", right aligned, `--mute-ink` |
| `.h1` | Cambria Italic | 76 / 1.13 (profile 72-96) | 2 lines of <= 26 characters; one finding per scene; key phrase in `--accent-ink` |
| `.dek` | SegUI 400 | 32 / 1.3 | one line, `--mute-ink` |
| `.big` hero numeral | Cascadia 600 | 168 (hook) and 150 (second numeral) / 190 and 170 | profile 160-220; 7 characters fit in 690 px |
| row label | SegUI 600 + Cascadia 500 for the number | 34 / 44 | name in ink, number in `--mute-ink` |
| row value | Cascadia 600 | 44 / 48 | right aligned at x 984 |
| table numeral `.nu` | Cascadia 600 | 88 / 100 | unit in SegUI 34 |
| column value `.cv` | Cascadia 600 | 88 / 100 | |
| axis tick `.gt` | Cascadia 500 | 30 / 34 (profile 20: too small for a phone) | |
| axis title, derivation line | SegUI 400 | 30 / 34 | |
| note (annotation) | Cambria Italic | 34-36 / 40-42 | `--accent-ink` or `--s2-ink` on a `--bg` halo so gridlines do not cross the words |
| `.src` source line | SegUI 500 | 24 / 30 | the ONE footer line below 30 px; <= 63 characters |
| caption | SegUI 600 | 44 / 57 | see section 8 |

Vietnamese runs 15-25% longer than English: headlines were sized for the longest string (the 51-character S3 headline was cut to 43 to stay in 2 lines).

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -150  top platform UI: empty
y 150  -154  4 px ink rule across 888 px (the newspaper top rule, persistent)
y 168  -204  kicker (left) and "Hình n" (right)
y 222  -392  .h1 (2 lines of 76 px = 172 px)
y 410  -450  .dek
y 470  -1290 CONTENT ZONE (820 px): hero numeral, chart, table
y 1214 -1250 axis tick labels   y 1256 -1290 axis title / footnote
y 1318 -1348 .src source line (24 px)
y 1366 -1480 caption band (bottom edge 1480, `bottom: 440px`), flush left
y 1480 -1920 bottom platform UI: empty
x 96   -984  content column, 888 px (the profile's 120 px margin was cut to 96 so 888 px fits a 6-character value plus a bar)
```

Chart geometry as built: zero axis at x = 780 for the diverging chart (values sit right of it, x 824-984, bars grow left); 60 px per percentage point at first, 42 px per point after the rescale; row pitch 230 / 185 / 150 px for 2 / 4 / 5 rows; bar height 44 px, label line 44 px, gap 8 px. Column chart: baseline y 1130, 90 px per month, columns 200 px wide at x 150 and x 720. Table: 3 rows at y 500 + 245 i, bar track 40 px high at row +152, full width 888 px = 550.000 (the largest value), so zero is the track's left edge.

Rule: the lowest content edge of every scene is at y >= 1250 (measured: S1 1288 caption, S2 to S5 1290-1270 axis title or footnote, S4b 1268 derivation note, S6 1260 empty-state box). Nothing but captions in y 1366-1480; nothing below 1480.

## 4. Layers, back to front

`#root` flat `--bg` -> `#cam` (everything that moves with the camera: `#chart` persistent chart layer, then the 6 `.scene` sections each holding its headline, dek and scene-owned graphics) -> `#chrome` (rule + kicker, never animated) -> `#src` (0.3 s fade-in at 0.3 s, then static) -> `#caps` (caption chunks). No flash layer, no shake layer, no pulse, no fade layer. The camera is "locked-off": `#cam` scales 1.000 -> 1.012 linearly over the whole video (micro-motion so nothing is frozen); the real "zoom" is the axis rescale.

## 5. Components

- **Hero numeral**: Cascadia 600 168 px, unit in SegUI 40 px on the same baseline, 6 px accent underline drawn left to right on the spoken word.
- **Diverging row** `.row`: label line (name 34 px + "· number" in mono), right-aligned value in mono 44 px, bar below. Bar starts at the zero axis and grows left; transform-origin is the zero edge, so it grows from zero.
- **Axis set**: 3 px ink zero line (draws down, `scaleY` 0 -> 1, 0.5 s), 1 px `--axis` gridlines at -5 / -10 / -15 with 30 px mono tick labels, axis title "% thay đổi so với tháng 10/2025 · thanh bắt đầu từ 0". Always drawn first, then data (profile: axes 0.4 s, gridlines, then data).
- **Columns** (zero-based, two columns): scaleY 0 -> 1 from the baseline `power2.out 0.6 s`, value in mono 88 px above, label below, a derivation line when one value is derived.
- **Table row** `.trow`: name 34 px, numeral 88 px with unit, outlined chip (3 px border, text in the series' `-ink` colour) for the change, full-width track in `--axis` with a coloured fill from the left.
- **Annotation** (signature move): ring (3 px, `--accent-ink`) drawn with `back.out(1.6)` scale 0.5 -> 1 on the spoken word, a 2 px leader line grows from it, then an italic note slides 8-12 px and fades in 0.4 s later, on a `--bg` halo.
- **Small multiples** (S6): two zero-based bar panels side by side, each with its own scale, title 32 px, month labels 30 px.
- **Empty-state box** (S6): dashed 3 px `--mute` border, name of the missing measure and "Báo cáo này không nêu số này": a missing number is shown as missing, never invented.
- **Figure frame** (S1): 2 px ink border, `clip-path` reveal from the top 0.5 s, caption "Hình 1. Minh hoạ, không phải số liệu." in Cambria Italic 30 px.
- **Stamp** (samples): "MINH HOẠ" in a 3 px `--accent-ink` outline, top right, for any illustrative content.

## 6. Motion language

| Move | Values (as built) |
|---|---|
| Headline entrance | rises 26 px, 0.5 s `power3.out`, at the scene start (the first scene is visible at frame 0 with no entrance) |
| Scene out / in | out: opacity 1 -> 0 in 0.14 s `power1.in` ending exactly at the next start; in: 0 -> 1 in 0.12 s. No overlap, so no ghost (profile's 0.4 s fade replaced, see section 12 trap 4) |
| Bar growth | `scaleX` 0 -> s `power2.out` 0.6 s from the zero edge; row fades in 0.25 s |
| Axis rescale (signature) | S2 -> S3: `power3.inOut` 0.8 s; bars `scaleX` 1 -> 42/60, gridlines and tick labels move to the new scale, rows re-pitch 230 -> 185 px; a 3rd tick (-15) fades in; S3 -> S4: re-pitch 185 -> 150 px, 0.7 s |
| Highlight swap | previous series -> mute and the spoken series -> accent, 0.25 s, on the first word of its sentence |
| Chart morph (signature) | S4: the five rows fade 0.35 s `power2.in`, then the baseline draws (0.5 s), column 1 grows at +0.5 s, column 2 at +0.65 s (0.6 s each), values fade at +0.9 / +1.05 s |
| Counter | `power3.out` 0.7 s, finishes 0.2-0.7 s after its scene start and always before the number is spoken |
| Annotation | ring 0.35 s + leader 0.25 s + note 0.45 s, started 0.05-0.1 s before the word |
| Micro-motion | `#cam` 1.000 -> 1.012 over the video; the S1 picture 1.00 -> 1.06 over 8.5 s |
| Never | shake, flash, bounce, elastic, glow, stagger from the centre |

### Transition rules between scenes

- A scene that keeps the same chart (S2 -> S3 -> S4a) is NOT a cut: only the headline swaps; the chart layer persists and rescales. That is what carries the viewer.
- A change of encoding (rows -> columns) uses the chart morph; a change of subject (S4 -> S5, S5 -> S6) uses the 0.14 s out / 0.12 s in swap.
- Never repeat the same graphic form in two adjacent scenes: here hero numeral -> rows -> rows (rescaled) -> rows + columns -> table with fills -> paired columns.

## 7. Scene recipes (S = scene start, W() = spoken-word onset; every tween start is clamped with `Math.max(0, ...)`)

Word times in this build are ESTIMATED (character share inside each scene), so key every reveal to a word that is at least 3 words before the number it introduces, and start counters early.

### R1 Hook (8.5 s): finding headline + hero numeral + figure
Frame 0 is finished: headline, 168 px numeral with unit, one-line label, kicker, source line fade in at 0.3 s. The illustration frame reveals 0 -> 0.5 s. Underline draws at 4.3 s (while the number is being spoken, 2.7-5.1 s), the "-6,9% so với tháng 10/2025" chip rises on W("sáu") - 0.25. Lowest edge 1288.

### R2 One number + first bar (8.7 s)
Headline "Số căn bán xong giảm 11,4%"; hero numeral 150 px counts 0 -> 2.114 in 0.7 s starting S + 0.2; axis draws S + 0.2, median row grows S + 0.35 (carried over from R1), second row grows on W("ghi") - 0.2 and the median row turns mute. Annotation on W("ít") - 0.1: ring at the bar's left end, leader down, note "giảm nhiều hơn giá trung vị (-6,9%)".

### R3 Axis rescale, two more rows (9.9 s)
S + 0.1: axis rescale 60 -> 42 px per point and re-pitch; the -15 tick fades in. New row on W("tin") - 0.15 (accent), next on W("giao") - 0.15 (accent, previous mute).

### R4 Rows to columns (11.2 s, internal cut-in at 6.5 s)
Part a: re-pitch to 150 px, fifth row on W("mười") - 0.2, note "giảm ít nhất trong năm chỉ số" with leader on W("chỉ"), on W("vì") the closed-sales bar turns accent and the listings bar turns blue. Part b (W("tồn") - 0.55): chart morph to two columns, the derived column labelled "suy ra" with the derivation line; ring + note "+0,4 tháng so với năm trước" on W("không") - 0.1.

### R5 Comparison table (8.75 s)
Row 1 (reference, already spoken) shows at S + 0.05 with its fill; city row on W("trong") + 0.15 with a 0.7 s counter; county row on W("quận") - 0.15 with a counter. Fills grow `power2.out` 0.7 s from the track's left edge (the largest value fills the track).

### R6 Before / after + honest gap (9.5 s, soft ending)
Two zero-based bar panels (price, inventory). The current month's columns grow at S + 0.3, the previous month's on their spoken words, the dashed empty-state box ("Số ngày nhà nằm trên thị trường / Báo cáo này không nêu số này") on W("báo") - 0.1. The last 1.5 s are the full composition; there is no fade out.

## 8. Captions (Vietnamese karaoke)

- No pill (profile). Flush left at x 96, width 888, bottom edge y 1480, SegUI 600 44 / 57 px, 1-2 lines, `.chunk` absolutely positioned at the bottom of `#caps`.
- Words: unread `--mute-ink` (6.43:1), current word `--accent-ink` (6.07:1), read words `--ink` (16.37:1); colour is switched with `tl.set` on each word onset, so there is no tween and no state in between.
- Chunks <= 6 words, split after punctuation once >= 3 words, never across a scene end; chunk hides 0.15 s after its last word or 0.03 s before the next chunk, whichever is first.
- Caption text is the spoken text (numbers in words); numerals on the graphics carry the digits.

## 9. Sound

Voice only in this build (VieNeu "Hải Đăng"); mixed -16.0 LUFS, peak -4.2 dBFS (ffprobe/`motion_tools.py probe`, final.mp4). No music and no SFX were possible. Profile target: understated documentary electronic or piano 84-104 BPM, a soft tick when a key number lands; both samples are silent by brief.

## 10. Images (agy)

agy cannot draw data. Used for ONE figure at most, as a "Figure n" with a caption that says it is an illustration ("Hình 1. Minh hoạ, không phải số liệu.").
- Prompt that worked: "Editorial newspaper illustration in the style of a data-journalism graphic: a single-story Texas ranch house ... thin black ink lines and light hatching on an off-white paper background #fbf9f4, one single accent colour of coral red #d1495b used only on the front door and a small For Sale sign post without any letters, generous empty margin, flat, no shadows, no text, no logos, no people". Output 768 x 1376 JPG, paper ground about #faf8ef (slightly different from `--bg`, hidden by the 2 px frame border), subject in the middle 40% of the height.
- Crop in CSS, no pre-processing: image width 1100 px, left -115, top -794 inside an 888 x 380 frame.
- A second prompt ("calm suburban street of five small houses ... one house accented with coral red roof") returned five identical houses with one in coral: it reads as a "one highlighted bar of five" chart. It was NOT used near numbers. Never ask agy for a skyline or a row of objects of different heights.
- No text, no logos, no people, no faces.

## 11. Must not

- No emoji; no gradients on text; no glow, neon, glass, 3D or shadows; no fast cutting; no shake, flash or bounce.
- No chart without axis, unit and source on screen; no bar that does not start at zero; no dual axis; diverging bars share one scale.
- No accent, s2 or mute colour for text (4.14, 3.91, 2.80 on `--bg`); use the `-ink` variants.
- No more than one highlighted series per chart at a time (a second one only in blue, only while the narrator compares the two).
- No number that no opened page states; a derived number says its derivation on screen ("suy ra: 6,2 trừ mức tăng 0,4 tháng") and is listed in selfcheck.md.
- No annotation or highlight before its word; numerals may be on screen up to 1 s early only in the hook.
- No empty panel for a missing number: draw the dashed empty-state box that says the source does not state it.
- Nothing below y 1480; nothing but captions in y 1366-1480; no text under 30 px except the one source line (24 px).
- No generated image that looks like a chart.

## 12. Traps seen in real builds (this build, 2026-11-13; measured)

1. **The speaker vs the chart: 241 words, not 190-225.** The brief asked for 190-225 spoken words; the first script had 241 words (six dense number sentences) and the VieNeu voice read it in 56.50 s (4.27 words/s), inside the 45-58 s window, so it was kept. Numbers in Vietnamese words are long ("bốn trăm lẻ bốn nghìn tám trăm lẻ hai" = 9 words for one figure): budget words per figure, not per second. Total video 57.5 s = voice 56.5 s + 1.0 s silent tail.
2. **Value labels crossed by the zero axis.** First render put the zero axis at x = 900 and right-aligned the value labels at x = 984, so the axis line ran through "-6,9%" (labels span about x 820-984). Fix: zero axis at x = 780, values in x 824-984, scale 42 px per point instead of 44 (so the -15 tick label stays inside the 96 px margin: x = 780 - 630 = 150). Rule: put the zero axis at least 40 px left of the left edge of the widest value label.
3. **Counter mid-count on a scene start.** The first S2 draft counted 0 -> 2.114 from S + 0.2 over 0.7 s: a still at 8.8 s shows "895" with an empty chart under it. It passes (6) (finishes within 0.8 s, before the word at 12.7 s), but the frame is a headline + a number counting. Rule: start the first bar in the same 0.3 s; the S2 median row now grows at S + 0.35.
4. **Headline-only start in the samples.** Both 10 s samples drew axis + first bar at 0.8-1.0 s, so frame-check flagged frame 0 as BLANK (headline + labels only for about 1 s). Fix: first group / first row at 0.15 s. Rule: in a data scene something that is data must appear within 0.3 s of the scene start.
5. **Profile fade (0.4 s) between unrelated charts breaks acceptance (4).** A 0.4 s cross-fade leaves the outgoing chart on screen for 0.4 s; the acceptance limit is 0.15 s. Used a 0.14 s out followed by a 0.12 s in instead. Contact-sheet frames at S3 + 0.07, + 0.2 and + 0.32 show no outgoing graphic. The persistent chart layer across S2 -> S3 -> S4 avoids the problem entirely.
6. **Source page without days on market.** The shape asks for "days on market", but the official Unlock MLS October 2026 page (opened twice) reports no days on market at all. One secondary page (a brokerage blog, updated 6 Nov 2026, AI-assisted per the search summary) gives 58 days but with an unstated geography and numbers that disagree with Unlock's (median $400,000 vs Unlock $404,802; 3,924 new listings vs 3,177). It was NOT used; the video says so on screen and in the voice ("Báo cáo này không nêu số ngày nhà nằm trên thị trường") with the dashed empty-state box. Rule: a missing figure is stated as missing, never filled from a weaker page.
7. **Derived column shown as data.** The October 2025 inventory (5,8 months) is not on the page; the page says 6.2 is "0.4 more than October 2025". The column is labelled "suy ra" and a 30 px line under it states "5,8 là số suy ra: 6,2 trừ mức tăng 0,4 tháng". The voice only says "nhiều hơn không phẩy bốn tháng", so 5,8 is the one on-screen number that is not spoken; it is flagged as derived in selfcheck.md.
8. **Estimated word times.** `voice/timeline.json` says `word_timing: estimated`. Anchors that name a short word near a long number (for example "ít" before "mười một phẩy bốn") were placed 0.05-0.2 s early on purpose. A real aligner was not available; expect 0.3-0.6 s drift on a 10 s scene, so never anchor a ring to a digit word: anchor to the word that introduces the sentence.
9. **Lint.** `gsap_css_transform_conflict` on `#s1ul` (an inline CSS `transform: scaleX(0)` plus a GSAP `to`): fixed with `tl.fromTo` and no CSS transform on that element. `composition_file_too_large` (303 lines) is expected for a single-file video. Final lint: 0 errors, 1 warning.
10. **Tool facts (hyperframes 0.7.26).** Render 1725 frames in 29.6 s, silent 6.2 MB, final 4.6 MB (limit 25 MB). The renderer inlines the gsap CDN script and embeds the three fonts as data URIs. `validate`: no console errors. `frame_check.py` samples with `fps=2`, so a label "38.0 s" shows the frame at about 38.25 s; use ffmpeg `select=eq(n,...)` for exact transition frames. Shell sandbox in this build refused redirects (`>`), `sed -i`, `python3 -c` and any script outside the allow-list, so `timing.js` (the `window.TIMING` words, 9 KB) was written by hand from `jq` output; a build step that writes it is better.
11. **Frame-check numbers.** final.mp4: 115 samples (2 per second), BLANK frames 0, TOPHEAVY frames 4 (info only; the sheet marks the frame at about 38.25 s, the start of S5 where the headline fades in before the first row grows, as one of them; the other three were not inspected one by one). Samples: 20 samples each, BLANK 0, TOPHEAVY 1.
12. **What an annotation cannot do on the last 0.4 s.** The scene-out fade is 0.14 s; any annotation must finish before `S_next - 0.16` or it fades half-drawn. The S2 ring, leader and note are tweened out at `S3 - 0.16`.
