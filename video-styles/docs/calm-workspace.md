# Style: calm-workspace (first detail document, written from the demo build of 2026-11-15)

## 0. Read this first: niche, status, what was and was not exercised

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** thoughtful "how it works" explainers about an abstract mechanism that can be drawn as stacked text blocks: a context window, a queue, a document structure, a note-taking or planning flow, a knowledge-base feature. Calm, low energy (1). Not for urgent news, one big number, enforcement, bad news, dense multi-series data, or anything that needs fast cutting. Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: one silent 12.0 s sample (`samples/sample-t030.mp4`, topic shape t030 "how a large language model uses a context window", Jev fit 0.65). Voice-over, captions, word timing, music and sound were NOT exercised; sections 7 and 9 are profile-derived and unverified. Content is generic illustration, labelled "Minh hoạ" on screen; no real product, number or spec.

Profile: `skill/references/styles/profiles/calm-workspace.yaml` (energy 1, light). Marks: **SUBST** = font not installed, local one used. **ASSUMED** = profile gives no value. **DEVIATION** = knowingly differs from the profile.
- SUBST: profile says Fraunces 600 for headings and Inter for body. Not installed. Heading = `cambriai.ttf` (Cambria Italic, a serif, only italic and weight 400), body = `SegUIVar.ttf`, labels = `CascadiaMono.ttf`.
- DEVIATION 1: profile layout is 16:9 (column 1100 px, doodle to the right). For 1080 x 1920 the column is 936 px wide (margins 72), the doodle shrinks to a 150 px corner icon at the heading's right.
- DEVIATION 2: profile caption style (Be Vietnam Pro 40 px on highlight band) not built (no captions in a demo).

## 1. Tokens (contrast measured with the WCAG formula, computed by hand because python was blocked in this session; rounded to 2 decimals)

```css
:root{
  --bg:#fbfbfa;      /* profile bg */
  --ink:#191919;     /* 16.98:1 on bg, 17.58 on white, 15.28 on --hl */
  --mute:#7c7a73;    /* profile mute: 4.15:1 on bg  -> FAILS 4.5, never text */
  --mute-dk:#66645d; /* ASSUMED: 5.72:1 on bg, 5.93 on white, 5.15 on --hl: the only muted text token */
  --hair:#e8e6e1;    /* borders and empty cells only */
  --accent:#3a6fe0;  /* profile link blue: 4.47:1 on bg -> FAILS 4.5 by 0.03; 4.63 on white. fills and bars only */
  --accent-dk:#2a5bc4; /* ASSUMED: 5.98 on bg, 6.19 on white, 5.38 on --hl. accent TEXT */
  --hl:#fbeed0;      /* the one highlight block */
}
```
Rules: text colours only `--ink --mute-dk --accent-dk`. Max one colour highlight (`--hl`) per scene: in this build the only highlight is the closing callout; role colour on rows is a 8 px bar, not a fill. `hyperframes validate` reported "480 text elements pass WCAG AA".

## 2. Fonts (Vietnamese check)

| File | Role | Result |
|---|---|---|
| `cambriai.ttf` | heading only, 100 px italic, -0.01em | Vietnamese "Cửa sổ ngữ cảnh" with ử, ữ, ả stacked marks rendered correctly in snapshots |
| `SegUIVar.ttf` | body 38-40 px (500/600) | all marks rendered ("đính kèm", "nhường", "Câu trả lời") |
| `CascadiaMono.ttf` | labels 30 px | "Người dùng", "KHUNG NGỮ CẢNH", "Minh hoạ", "ô" rendered |
| `segoepr.ttf` | NOT used | lacks Vietnamese letters |

The glyph-table test with fontTools could not be run (interpreter blocked); the check was done by reading the snapshot PNGs and the 2 fps / 3 fps contact sheets. `font-synthesis: none` so no fake bold on the italic. Cambria Italic has no 600: headline weight 400.

## 3. Type scale, safe areas and grid (1080 x 1920)

- Margins 72, column 936. y 0-160 empty. Chip "Minh hoạ" y 170-226 (mono 30 px, 1.5 px ink border, radius 4).
- Heading y 262, 100 px, ~680 px wide (one line, "Cửa sổ ngữ cảnh"). Doodle 150 x 150 at x 862, y 236. Subtitle y 410, 40 px, up to 2 lines.
- Evicted slot y 560-688. Window y 720-1380 (936 x 660, radius 10, 3 px ink outline). Header 30 px mono y 740. Rows from y 812, x 104, width 872. Meter cells y 1414-1466 (8 x 105 px, gap 12). Callout y 1506-1644 (38 px).
- Everything ends at y 1644; y 1650-1920 empty (bottom UI zone). Smallest text 30 px (mono labels).
- Scale: 100 heading, 40 sub and row titles, 38 callout, 30 mono labels.

## 4. Layers (back to front)
1. `#root` bg. 2. `#world` camera wrapper, scale 1.000 to 1.012 over 12 s (`none` ease, the only continuous motion). 3. page blocks: heading, sub, doodle. 4. window fill + SVG outline + header. 5. rows (R1..R4). 6. `#sweep` reading line. 7. meter cells, callout (highlight under text). No caption layer. Three depth levels are flat by design: this style has no parallax.

## 5. Components
- **Row (block)**: white, 1.5 px hair border, radius 4, 8 px role bar at the left (ink = user, `--mute-dk` = document, `--accent` = model), title 40 px 600, mono sub 30 px, mono size tag at right ("2 ô"). Height = 64 px per cell (R 2 cells 128, 3 cells 192): a block's height equals its token cost, so 8 cells = 544 px = the window's inner height.
- **Window**: white fill, hand-drawn feeling 3 px ink round-cap outline drawn with stroke-dashoffset (0.7 s `power2.inOut`).
- **Meter**: 8 cells, hair outline empty, filled with the role colour.
- **Evicted block**: dashed 2 px `--mute-dk` border, title in `--mute-dk`, sub "Ngoài khung · mô hình không thấy".
- **Callout**: `--hl` block radius 4 wipes in (scaleX 0 to 1, 0.45 s) then its text types.
- **Doodle**: monoline 3 px ink icon (window + 3 lines + 2 corner brackets) drawn with stroke-dashoffset, 5 paths staggered 0.12 s.
- **Reading sweep**: 6 px accent line travels down the window rows (0.8 s `power2.inOut`), then fades 0.15 s.

## 6. Motion language
- Typing: one span per character, opacity step at 0.07 s (heading), 0.02 s (subtitle, callout), 0.03-0.04 s (row titles). Frame 0 is clean; every typed line is complete 0.2 s or more before its hold.
- Rows rise 28 px with fade (0.45 s `power3.out`) while their title starts typing 0.15 s later. No bounce, no elastic.
- Drag-and-settle: new block enters from x +1100 (0.8 s `power3.out`) with a light shadow (`0 10px 24px` at 16%) that fades over 0.4 s once it lands; old block moves up 252 px (0.75 s `power3.inOut`), widens 872 to 936 and changes border from solid to dashed; surviving blocks scroll up 144 px (0.7 s `power3.inOut`). Page-scroll feel without moving the page.
- Doodle-draw then settle; micro-motion is only the 1.2% page drift and the sweep line. Nothing flashes, shakes or pulses.

## 7. Captions (NOT exercised in this build)
Profile: no pill, 40 px Be Vietnam Pro 500 ink on a highlight underline band, left-aligned to the column. Untested; check the band does not collide with the callout at y 1506-1644 (a vertical caption would need y 1650+, which is the bottom UI zone).

## 8. Scene recipe used (t030, 12.0 s, three beats, one continuous page)
**Beat 1 (0-2.4 s) blank page to heading.** Chip "Minh hoạ" visible from frame 0. Heading types 0.3-1.35 s, doodle draws 0.7-1.9 s, subtitle "Mô hình chỉ đọc được phần nằm trong khung." types 1.7-2.54 s.
**Beat 2 (2.1-5.7 s) the window fills.** Window outline draws 2.1 s; blocks "Câu hỏi đầu tiên" (2 ô) 2.4 s, "Tài liệu đính kèm" (3 ô) 3.3 s, "Câu trả lời của mô hình" (3 ô) 4.0 s; counter text "2/8 ô, 5/8 ô, 8/8 ô" changes with a discrete swap at each block; meter cells fill; the sweep reads the whole window 4.9-5.85 s.
**Beat 3 (5.9-12 s) the window is full.** The oldest block leaves to a dashed slot above the window (5.9-6.65 s), "Câu hỏi mới" (2 ô) slides in 6.4-7.2 s, meter recolours, callout "Khung đầy: mô hình bỏ phần cũ nhất để nhường chỗ cho phần mới." wipes and types 7.6-9.2 s, second sweep 9.2-10.15 s, then a full-composition hold to 12.0 s (last 1.5 s = complete page, all text finished, only the 1.2% drift moves).

## 9. Transitions and sound (NOT exercised)
No scene cuts: the whole piece is one page, beats are handed over by scroll and drag. Profile lists page-scroll, block-type, doodle-draw, soft fade 0.5 s. Sound: none in this build (profile: lo-fi or solo piano 70-95 BPM, key taps).

## 10. Images
No image generated (optional; the page is typography and monoline). If one is made for agy: flat off-white, monoline ink doodle, no text, no people, no logos; agy draws mood only, never windows or blocks (those are CSS/SVG).

## 11. Must not
- `--mute` or `--accent` as text colour (4.15 and 4.47 fail on bg).
- More than one `--hl` highlight in a scene; shadows heavier than the 16% lift shadow, shown only while a block is in flight.
- Bounce, elastic, shake, flash, neon, dark mode, emoji, segoepr, real brands or figures; labels without "Minh hoạ" when content is generic.
- Text smaller than 30 px; anything below y 1650.

## 12. Traps seen in real builds (this build, measured)
1. **Accent blue fails as text.** Profile `#3a6fe0` = 4.47:1 on `#fbfbfa` (needs 4.5). Profile mute `#7c7a73` = 4.15:1. Fix: `--accent-dk #2a5bc4` (5.98) and `--mute-dk #66645d` (5.72).
2. **Typing spans visible at frame 0.** First version scheduled `tl.set(chars, opacity 1)` and `opacity 0` at time 0; the callout showed fully at 5.3 s, 2.3 s before it should start. Rely on CSS `opacity:0` and only schedule the reveal `set`s.
3. **Empty window panel.** Window drawn at 2.5 s with first block at 3.4 s = 0.9 s empty (3 of 24 samples at 2 fps). Fix: window 2.1 s, first block 2.4 s (0.3 s empty).
4. **Inspect noise.** Off-canvas entering block (x +1100) and the crossfading two sub-labels produced 56 info and 1 warning; cleared with `data-layout-allow-overflow` on `#r4` and `data-layout-allow-overlap` on the two sub-labels, final inspect 0 issues.
5. **Lint overlap warning.** Two tweens on `#sweep` y overlapped by 0.15 s; fix: tween only opacity in the `fromTo`, reset y with a `set` 0.05 s earlier.
6. **Left-over gaps are real.** A 3-cell block (192 px) with two text lines leaves the lower half of the card blank; accepted as the token-height metaphor, but it reads emptier than the 2-cell blocks.
7. **Tools.** `frame_check.py` needs numpy, absent from the python3 used here, so the frame check was done by hand (see selfcheck.md). Run `frame_check.py` from the repo root with a relative path.
8. Output size 1.0 MB at `-q standard`; render 12 s for 360 frames.

## 13. Not yet decided / weak spots
- Tier-1 niche not yet assigned. - Fraunces and Inter are unavailable (SUBST). - Voice, captions, sound, bottom-band caption fit unverified. - No image used. - Hold from 10.2 s to 12.0 s is quiet by design; add a 0.5 s page fade only if a full video needs an outro.
