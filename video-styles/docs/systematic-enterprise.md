# Style: systematic-enterprise (9:16 Vietnamese data-report edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** dense, sober, trustworthy reports with 3 to 6 sourced numbers plus a ranked list or a short series: quarterly results, enterprise or data-platform explainers, B2B research stories, backlog or pipeline tables, benchmark rankings. The grid, the table sort and the column-mask cut make "rigour" the feeling. Not for warm human stories, hype, breaking one-number news, or anything that needs mood. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE 12 s silent sample (`samples/sample-t026.mp4`, 1080x1920, 30 fps, 1.0 MB). **Voice-over, captions, word timing, sound and music were NOT exercised (demo build);** those rules below are carried from the profile and marked ASSUMED. No owner document existed; the profile is `skill/references/styles/profiles/systematic-enterprise.yaml`. Only generic illustrative content was used and it is labelled "Minh hoạ" on screen.

**Reading order.** Sections 1-12 are the design as built. Section 13 is the traps from this build with numbers.

**What the sample shows (3 beats, 12.0 s):**
1. 0-4.47 s dark chapter: three KPI tiles (revenue, gross margin, backlog), counters, sparklines drawn in, accent bar lighting tile by tile on the beat (100 BPM, 0.6 s).
2. 4.47-8.2 s light chapter (column-mask cover cut in): revenue bars on grid axes, margin line below.
3. 8.2-12.0 s dark chapter (hard cut): backlog hero count, a 5-row table fills row by row, then sorts with rows gliding; two recap cells flip in.

## 1. Tokens

All contrast values are WCAG, computed by hand in this run (Python and numpy were blocked), and `hyperframes validate` reported "40 text elements pass WCAG AA".

```css
:root{
  --bg:#15171a;       /* dark chapter ground */
  --ink:#f3f2ef;     /* 16.0:1 on bg, 13.4 on layer */
  --mute:#a6a8ad;    /* 7.6:1 on bg, 6.3 on layer, 5.8 on layer-on */
  --layer:#25272b;   /* square tiles */
  --layer-on:#2c2f34;/* active tile (lit on a downbeat) */
  --accent:#3a4fe0;  /* FILL ONLY on dark: 2.9:1 on bg, 2.4 on layer. Text on it: ink 5.6:1. On light bg as text: 5.6:1 */
  --accent-l:#8a9cf5;/* text and data marks on dark: 7.0:1 on bg, 5.8 on layer */
  --cyan:#3ec6e0;    /* data series only (7.4:1 on layer); unused in the sample */
  --magenta:#e0587a; /* data series only: 3.2:1 on light bg (graphics ok, text not), 4.2 on layer */
  --lbg:#f3f2ef; --link:#15171a; /* 16.0:1 */
  --lmute:#5b5f66;   /* ASSUMED token, 5.7:1 on lbg; the dark --mute (2.4:1) fails on light */
  --lgrey:#7d8088;   /* ASSUMED: de-emphasised bars on light, 3.5:1 */
  --rule:#2e3035; --lrule:#d4d3cf;
}
```
Rules: dark scenes put data marks and small accent text in `--accent-l`, never `--accent`. Light scenes use `--accent` for the hero bar and text, `--lmute` for secondary text. Cyan and magenta only for the 2nd and 3rd chart series. Solid colours only: no rgba rules, no gradients, no opacity on resting elements. Chapters alternate dark / light / dark.

## 2. Fonts (substitutes; IBM Plex is not installed)

| File | Role | Notes |
|---|---|---|
| `SegUIVar.ttf` | all read text, 300 for display, 500 for table names, 600 for emphasis and numbers | declared `font-weight: 300 700`; the weight axis rendered correctly (300 vs 600 visibly differ in the snapshots). SUBST for IBM Plex Sans |
| `CascadiaMono.ttf` | labels, axis ticks, chips, kicker (30 px), footer (24 px) | SUBST for IBM Plex Mono |
| `cambriai.ttf` | not used | |
| `segoepr.ttf` | NEVER (lacks Vietnamese letters) | |

**Vietnamese diacritics check (visual).** `fontTools` and ffmpeg `drawtext` were not available, so no full glyph-table audit was run. Checked by eye on snapshots and the render: "Quý III", "biên lợi nhuận", "Nhóm khách hàng", "Số liệu giả định, không phải dữ liệu thật", "TÓM TẮT QUÝ III", "BÁO CÁO QUÝ III · CÔNG TY AI", "Minh hoạ", "tăng", "bốn quý liên tiếp", "Biên lợi nhuận gộp, % (trục từ 50)" all rendered with correct stacked marks in both fonts. Untested letters (Ơ Ư and their tone variants) remain an open check. Avoid arrows and special symbols (the glyph "↑" could not be verified in Cascadia); use "+" and "·" only.

### Type scale (1080x1920, px, as built)
| Use | Font | Size | Weight |
|---|---|---|---|
| Hero number, scene 3 | SegUI | 240 | 300 (unit 80, 600) |
| Tile number | SegUI | 168 | 300 (unit 64, 600) |
| Headline | SegUI | 96 / line-height 112 | 300, emphasis words 600, -0.01em |
| Recap cell number | SegUI | 96 | 300 (unit 44, 600) |
| Table value | SegUI | 56 | 600 |
| Table name, chart value | SegUI | 44 | 500 / 600 |
| Labels, chips, axis, kicker, table header | Cascadia | 30 | 400 |
| Footer disclaimer (the one small line) | Cascadia | 24 | 400 |

Nothing else is under 30 px. The profile's 96-128 px display was kept at 96 because three lines must fit 992 px.

## 3. Safe areas and grid (1080 x 1920)

- 16 columns, margin 44, column 47, gutter 16: pitch 63, so column n starts at x = 44 + (n-1) x 63; k columns span 63k - 16 px; all 16 = 992. This gives integer pixels. The profile's 32 px gutter was scaled to 16 for the narrow frame.
- Tile edges, chart bars (2 columns = 110 px at cols 3, 7, 11, 15), the table value column (col 13, x 800), recap cells (8 + 8 columns, x 44 and x 548) all sit on columns. Inner padding of tiles is 16 (one gutter), so tile text starts at x 60 (deviation, accepted).
- y 0-90 empty; chip and kicker row y 96-152; headline y 190-526; body y 440-1632; progress rule y 1744; footer y 1780. No captions in this build, so nothing is reserved at y 1330-1650 (a captioned edition must reserve it; ASSUMED).
- Left-aligned always; no centred text.

## 4. Layers, back to front
1. `#root` ground.
2. Scene sections `.sc` (visibility toggled, one visible at a time); light scene has a baked 8 px dot-grid PNG (`img/dots.png`, 2x2 px dot, about 6%).
3. Scene content: tiles / chart / table.
4. `#xt` column-mask strips (z 40).
5. `#prog` 4 px progress rule across 992 px for the whole video (z 30), the permanent micro-motion.
Depth is two layers plus the rule; the profile is locked-off so no parallax. Holds are kept alive by beat-synced lighting, node pulses, the stepping row marker and the progress rule.

## 5. Components
- **Minh hoạ chip:** 236 x 56, 2 px border, mono 30, `--accent-l` on dark and `--accent` on light, at x 44 y 96, present in every scene. Plus the 24 px footer on every scene.
- **Tile:** 992 x 340, radius 0, `--layer`, 4 px top bar (transparent until active, then `--accent-l`; the profile's 1 px is too thin for a phone). Label mono 30, number 168, delta chip (accent fill, ink text, 52 px high).
- **Sparkline / mini bars:** 346 x 220, 5 px stroke in `--accent-l`, square 14 px end node; mini bars are squares of 56 px.
- **Chart axes:** 1 px solid rule lines, mono 30 tick labels in `--lmute`; bars start at zero; the line chart axis starts at 50 and says so in its title.
- **Table row:** 136 px high, 1 px bottom rule, name 44, bar 40 px high (scale 116 px per unit), value 56; header row mono 30 with a rule.
- **Active-row marker:** `--layer` block with a 4 px `--accent-l` left bar, steps down one row on each downbeat (0.12 s).
- **Recap cell:** 488 x 200, `--layer`, 4 px accent top bar, flips in on rotationX 90 to 0.

## 6. Motion language
- Productive moves 0.1-0.26 s (chips, rule draws, marker steps, label fades); expressive 0.4-0.5 s (tile reveal, bar growth, row sort, headline lines). Never mixed within one element.
- Eases: `power3.out` entrances and counters, `power2.out` small items, `power3.inOut` for the sort, `power2.inOut` for line drawing. No back, elastic or bounce (obeyed).
- Tile reveal: clip-path inset right to 0, 0.4 s, 0.14 s stagger; clip-path set to `none` right after.
- Counters: `power3.out` over 0.9 s, ending by 1.5 s, final value forced in `onComplete`.
- Bars: `scaleY` from the baseline, 0.5 s, 0.1 s stagger. Line: `strokeDashoffset` via `pathLength=1`, 0.8-0.9 s.
- Downbeat lighting (100 BPM, beat 0.6 s): active tile bg + top bar switch with `tl.set` (hard, no tween), the end node pulses 1 to 1.5 to 1 in 0.25 s.
- Exits: none animated except the column cover.

### Transitions (as built)
- **Column-mask cover (dark to light):** 8 strips of 135 px (full-bleed, not on the 16 columns), colour of the incoming ground, `scaleY` 0 to 1 from the top, 0.24 s `power2.out`, 0.04 s stagger, starting 3.95 s; complete at 4.47 s, then the scenes swap under it and the strips are reset. Total 0.52 s. Outgoing content is covered column by column, so no ghost lasts over 0.24 s.
- **Hard cut (light to dark)** at 8.2 s: the profile's chapter change.
- Not built in this sample: tile-flip scene transition (used only as the recap cells' entrance), slide by one module.

## 7. Scene recipes (S = scene start)
**R1 KPI tiles (S1, dark).** Frame 0 already holds chip, kicker and headline (static, no reveal, so the first frame is not a skeleton). t 0.15/0.29/0.43 tiles clip in; counters start 0.30/0.44/0.58, 0.9 s; sparklines draw 0.45 and 0.59, mini bars 0.73 (0.06 stagger); delta chips slide 28 px + clip at 1.25 (0.12 stagger); downbeat lighting from 1.8 s at 0.6 s steps (tile 1, 2, 3, 1). Hold to 3.95.
**R2 Chart (S2, light, 3.73 s).** Headline lines rise out of line masks (y 120 to 0, 0.5 s, 0.08 stagger) at S+0.05; titles clip in; gridlines fade 0.2 s; bars grow from S+0.4, value labels S+0.75, then the 2nd chart: gridlines S+0.9, line draws S+1.2 over 0.9 s, nodes pop, labels step in 0.28 s apart. Full chart held from S+2.4 (about 1.3 s), last node pulses on beats. The last bar is `--accent`, earlier bars `--lgrey`.
**R3 Table (S3, dark, 3.8 s).** Hero counts 0 to 9,4 over 0.7 s from the first frame; chip S+0.5; header S+0.3; rows fill at S+0.4 + 0.03 x i (y 24 to 0, opacity, 0.24 s; bars grow 0.4 s); the table is readable until S+1.1 = 9.3 s; sort: each row tweens y to its rank, 0.5 s `power3.inOut`, 0.03 s stagger by rank; marker appears at S+1.8 on rank 0; recap cells flip at S+1.8 and S+1.9 (0.4 s); marker steps at S+2.6 and S+3.2. Full composition from 10.5 s to the end (1.5 s).

## 8. Captions
Not exercised (demo, silent). ASSUMED from the profile: a square layer-grey block with a 3 px accent left bar, 40 px ink, left-aligned, in a bottom band; a captioned edition must also move the recap and table up (content already ends at y 1632).

## 9. Sound
Not exercised. ASSUMED from the profile: minimal electronic or modern classical at 90-112 BPM, precise ticks and data blips, low density. The 100 BPM downbeat lighting in the sample is a stand-in for a beat grid and would be retimed to the real music.

## 10. Images
None used: the style is flat and the data is drawn in CSS/SVG. The only baked asset is the 8 x 8 dot-grid PNG (ffmpeg `drawbox`). If agy is used, only for a decorative still; never for charts, rows or icons (a generated "skyline" reads as fake bars).

## 11. Safe handling of facts on screen
Every number in the sample is invented and labelled: "Minh hoạ" chip on all three scenes plus the footer "Minh hoạ: số liệu giả định, không phải dữ liệu thật." Real use needs a source chip or line per number and a stated derivation for derived values (here the recap numbers repeat tile 1 and 2; the table rows sum to 9,4 = the hero).

## 12. Must not
- Radius other than 0; gradients; glow; bounce, back or elastic eases; shake, flash, speed lines; centred text.
- `--accent` for text or thin marks on dark; cyan or magenta outside data series; text in `--mute` on the light chapter.
- Anything off the 16-column grid (tile edges, bars, table columns); text under 30 px except the single footer line.
- Emoji, logos, real company names, special arrow glyphs not verified in the font.
- Non-zero baseline on bars; a dual axis; a chart that appears before its first data.

## 13. Traps seen in real builds (this build, 2026-11-14)
1. **Light chapter inherited the dark ink.** `body{color:#f3f2ef}` made the scene 2 headline and every unstyled text near-invisible (about 1.1:1) on `#f3f2ef`; found only in the first snapshot sheet (`hyperframes validate` did not flag it because the text was mid-animation). Fix: `.light{color:var(--link)}`. Rule: set the text colour on each chapter's section, not on body.
2. **Accent on dark fails.** `--accent #3a4fe0` measured 2.9:1 on `--bg` and 2.4:1 on `--layer`; unusable for sparklines or bars on dark. Use `--accent-l` (7.0 / 5.8) and keep `--accent` as a fill under ink text (5.6).
3. **Dark mute on light fails.** `--mute #a6a8ad` is 2.4:1 on `#f3f2ef`; added `--lmute #5b5f66` (5.7). De-emphasised bars needed `#7d8088` (3.5) to stay a visible mark.
4. **Magenta is a graphic, not text.** 3.2:1 on light: fine for a 6 px line and 14 px squares, so all values beside it are ink.
5. **Inspect false positives.** `inspect` flagged `.lbl` overlapping the inline numeral (the 168 px span's line box reached into the label) until the number moved from top 62 to 78 with line-height 160; 3 residual warnings remain on the counter span and are a measuring artefact (visible gap in the render). Line masks need `data-layout-allow-overflow data-layout-allow-overlap`. One header ("Backlog, tỷ $" at col 14, 216 px wide) overflowed the canvas by 11.5 px: move the column to col 13 (x 800).
6. **Sort crossing.** During the 0.5 s row sort, rows pass through each other and two names overlap in a frame at 9.5 s ("Nhóm E" over "Nhóm D"). Acceptable as motion (under 0.5 s, not a held frame); reduce by staggering by rank (0.03 s) as built.
7. **Marker touching text.** The 4 px left bar of the active row sat on the "N" of the row name at x 44; row names moved to x 60 (table header too).
8. **Counters show mid-count in a 2 fps sheet** (3,3 / 49 / 4,9 at 0.5 s; 0,7 at 8.2 s). They finish by 1.5 s and 8.9 s; no held frame is partial. Final values are forced in `onComplete`.
9. **Column strips are not on the 16 columns** (8 x 135 px across 1080). Only the full-bleed cover; documented deviation.
10. **Tooling in this run.** `python3` for anything but `motion_tools.py` was blocked, so no fontTools glyph audit; `frame_check.py` could not run (no numpy); ffmpeg has no `drawtext`. The check was replaced by `hyperframes lint / validate / inspect / snapshot` and an ffmpeg 2 fps contact sheet (8x3, 216 px tiles) viewed by eye.
11. **Frame 0.** A first version of this layout (headline masked in at t 0) would give an empty frame 0; the built version keeps the headline static and animates only the tiles.
