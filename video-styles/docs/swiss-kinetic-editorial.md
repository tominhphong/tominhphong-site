# Style: Swiss kinetic editorial (9:16 Vietnamese edition, demo-derived)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build:** announcements and explainers that are text-first and structured as "what / how much / how": industrial and economic policy, programme or subsidy rules, event announcements, brand manifestos, three-step procedures. It rendered the topic shape t141 (industrial policy, new factory subsidies explained, Jev fit 0.73) cleanly in 12 s. Not for warm human stories, product hero shots, montage or anything that needs photos (the profile lists product-hero and montage under `avoid`). Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a 12.0 s silent 1080x1920 sample (`samples/sample-t141.mp4`, 3 beats). **Voice, caption, sound and beat-sync rules were NOT exercised** (demo build: no voice-over, no captions, no music); every rule in those areas below is the profile's text, marked ASSUMED. Layout, type, colour, motion and timing numbers are measured from the build.

**Content in the demo is generic.** "30%", the three steps and the deadlines are invented; every scene carries a "Minh hoạ" chip and a footer saying so. Copy how it is built, not what it says.

Source of values: `styles/profiles/swiss-kinetic-editorial.yaml`. Energy 3 in the profile; in practice the style reads as energy 2-3: hard snaps, no shake, no flash, no bounce.

## 1. Tokens

```css
--paper:#f2f0eb;   /* background */
--ink:#111111;     /* all primary text, rules                 16.6:1 on paper */
--red:#e30613;     /* bars, big numerals, one punctuation dot. 4.28:1 on paper, 3.87:1 on ink: LARGE TEXT ONLY (>= 120 px) and marks */
--mute:#8a8883;    /* profile value; 3.11:1 on paper: NEVER text on paper (5.34:1 on ink) */
--rule:rgba(17,17,17,0.14);  /* the 13 column rules */
/* text-safe variants added in this build (hand-computed WCAG ratios, +-0.05) */
--red-ink:#b8040f; /* red as SMALL text on paper (indices 01/02/03, row labels)   6.0:1 */
--mute-ink:#55534f;/* footers, axis labels on paper                              6.7:1 */
--red-lt:#ff4a55;  /* red as text on the ink scene (numerals 01-03, final dot)   5.7:1 on ink */
--mute-lt:#a9a7a1; /* secondary text on the ink scene                            7.9:1 */
/* paper on ink 16.6:1 ; ink on red 3.87 (do not set ink text on a red block) */
```
Rules: red only for bars, numerals, one punctuation dot per headline and the filled grid cells. Inverse scene (`#s3`) swaps paper/ink; red stays but text uses `--red-lt`. `hyperframes validate` reported "40 text elements pass WCAG AA". No shadows, gradients, radius or glow.

## 2. Fonts (2 local files; the profile's Inter Tight / Inter / IBM Plex Mono are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Display, body, row text | Inter Tight 800 / Inter 400 | `SegUIVar.ttf`, weight axis 300-700; display 700 with `letter-spacing:-0.045em`, body 400/600 (800 does not exist: 700 is the heaviest) | The 36-letter set was measured by the owner docs `style-saas-bento.md` and `style-fluent-productivity.md` (all present). In this build the check was visual only (fontTools could not be run, see selfcheck): every diacritic stack in the rendered frames (Trợ, giá, hưởng, hỗ, điều, kiện, Thẩm, định, nộp, hồ, sơ, bước, vận, Năm) is intact |
| Indices, kicker, chip, labels, footer | IBM Plex Mono 500 | `CascadiaMono.ttf`, weight axis 200-700, 500, uppercase, `letter-spacing:0.08em` | same; Ạ, Ệ, Ợ, Ấ, Ỗ rendered correctly in the uppercase kicker |
| Never | | `segoepr.ttf` (35 of 36 Vietnamese letters missing), `cambriai.ttf` (not needed: no serif in this style) | |

Declare both with `font-display: block` and variable weight ranges. Uppercase Vietnamese in mono is wide: "CHÍNH SÁCH CÔNG NGHIỆP" at 30 px is 440 px.

### Type scale (1080 x 1920 px, measured in the build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| Display (title) | Seg 700, -0.045em | 210 / 0.92 | 3 lines, widest line "nhà máy" = 765 px of 888; flush left |
| Display (inverse scene) | same | 190 / 0.92 | 2 lines, widest "nộp hồ sơ." = 830 px |
| Stat numeral | Seg 700, -0.05em, red | 450 / 0.9 | "30%" = 820 px; nowrap |
| Row text | Seg 600 | 64 (steps), 52 (stat sentence), 40 (rows, deck) | all >= 40, the contract minimum is 30 |
| Index / kicker / chip | Cas 500 uppercase | 30 | the floor for everything except the footer |
| Row numerals 01-03 (inverse) | Cas 500 | 60 | `--red-lt` |
| Footer "Minh hoạ ..." | Cas 500 | 24 | the ONE sub-30 line, `--mute-ink` |

Display to body ratio 210:40 = 5.3:1 (profile asks 6:1; 52 px stat sentence under 450 px = 8.7:1). No centred text anywhere.

## 3. Safe areas and grid (1080 x 1920; no captions in this build)

```
y 0    -170  top platform UI: empty
y 190        kicker (left) and running index "01 / 03" (right), Cas 30
y 250        2 px full-width ink rule (header rule)
y 282  -332  "Minh hoạ" chip (border 2 px, 30 px mono)
y 420  -1300 body zone (display / numeral / rows)
y 1500-1620  bottom index row (scene 1) / bar + deck (scene 3)
y 1716       footer line (24 px)
y 1750 -1920 empty (ASSUMED bottom platform UI; nothing placed below 1750)
x 96   -984  content width 888
```
12 columns: column 52 px, gutter 24 px, pitch 76 px (profile: 96 px margin, 24 px gutters; the profile's 160 px column width and 12 px baseline do not fit 888 px, so 52 / 76 are DERIVED). 13 vertical rules (1 px, `--rule`) at x = 96 + 76 n, the last one pulled in 24 px so it sits on the right margin. Rules stay visible in every scene (profile shows them in title scenes only; visible everywhere read as the "grid", no clutter at 14% opacity).

Anchors used: display columns 1-9, red bar spans 8 columns (584 px) at the title, 12 columns (888 px) on the closing scene, step text starts at column 3 (x 248) in scene 3 and at x 400 (column 5) in the stat rows.

## 4. Layers, back to front

`.scene` section (own background, full frame) -> `.cols` (13 rules) -> header (kicker, index, rule, chip) -> content -> footer. One section per beat; the next section sits above the previous one and is revealed by a clip-path wipe, so the outgoing beat is simply covered (no cross-fade, no ghost). No flash layer, no fade layer: the video starts on paper and ends on a full composition (profile has no fade-out either).

## 5. Components

- **Header strip:** kicker (left), `NN / 03` running index (right), 2 px rule. Index changes only when the scene changes (snap, no animation).
- **Chip "Minh hoạ":** 2 px border, no fill, no radius, 30 px mono, 6/18 px padding; in the inverse scene the colour is paper.
- **Display block:** one `.ln` mask per line (see Traps 1). The final full stop is the red accent (`.acc`).
- **Red bar:** 12 px tall, `transform-origin:left`; grows in whole column steps (scaleX = n/8).
- **Cell strip (data):** 10 cells, 78 x 96 px, 12 px gaps, 2 px ink border; the filled cells carry an inner red block that scales from the left. 3 of 10 red = 30%. Axis labels "0%" and "100%" in 30 px mono. Only the cells that end filled are animated (Traps 3).
- **Spec row:** 2 px rule, mono red-ink label at x 96, 40 px Seg 600 value at x 400, 106 px row pitch.
- **Step row (inverse):** 2 px paper rule at 50% opacity, mono numeral 60 px red-lt, text 64 px, 170 px pitch.

## 6. Motion language

Allowed: `expo.out` (entrances), `power2.inOut` (rules and bars), `power4.inOut` (grid shift), `power3.out` (counter), `steps(12)` (column wipe), `power2.out` snaps. Not used: elastic, back, rotation, scale bounce, shake, flash, blur. Only horizontal or vertical motion.

| Move | Values measured in the build |
|---|---|
| Line slide | each line inside its mask, `yPercent 115 -> 0`, 0.7 s `expo.out`, stagger 0.09 s |
| Rule draw | `scaleX 0 -> 1`, 0.5-0.6 s `power2.inOut` |
| Bar growth | 8 steps of 0.14 s `power2.out`, one step per 0.4 s (title, 0.5 s -> 3.3 s); on the closing scene 11 steps of 0.12 s every 0.1 s |
| Column wipe | incoming section `clip-path inset(0 100% 0 0) -> inset(0)`, 0.45 s `steps(12)`, then `clip-path: none` at +0.46 s |
| Grid shift | incoming children `x 76 -> 0`, 0.5 s `power4.inOut`, together with the wipe (exactly one column pitch) |
| Counter | `0 -> 30` in 0.7 s `power3.out`, numeral rises 60 px -> 0 in 0.5 s `expo.out`; final value held from 5.2 s |
| Row entrance | `x -40..-50 -> 0` plus opacity, 0.5 s `expo.out`, stagger 0.14-0.25 s |
| Cell fill | `scaleX 0 -> 1`, 0.2 s `power2.out`, stagger 0.12 s |

Cadence in the demo: something changes every 0.1-0.5 s inside a beat, a hard structural change (wipe) every 4.0 s on a bar line (120 BPM assumed: 4.0 s = 8 beats). No camera move other than the grid shift.

## 7. Scene recipes (S = beat start; times from the build)

### R1 Title (0-4.0 s)
Kicker, rule, chip at 0.05 s; display lines slide at 0.10 / 0.19 / 0.28 s; red bar steps from 0.5 s; deck lines at 1.0 s; bottom rule 1.5 s; index row (01 Điều kiện / 02 Mức hỗ trợ / 03 Thủ tục) at 1.7 s with stagger 0.18 s. Held complete from about 2.5 s. The index row previews the next beats.

### R2 Stat (4.0-8.0 s)
Column wipe 4.0-4.45 s; label 4.45 s; numeral 4.5-5.2 s (counter); stat sentence 5.0 s; axis labels 5.4 s; three red cells 5.5-6.06 s; two spec rows 6.2-6.9 s. Complete from about 6.9 s (about 1.1 s hold).

### R3 Steps, inverse (8.0-12.0 s)
Wipe 8.0-8.45 s (paper -> ink); headline lines 8.5 s; three rules 9.0 s then three rows 9.1 s (stagger 0.25 s); red bar fills 12 columns 9.0 -> 10.2 s; deck line 10.1 s. The last 1.5 s (10.5-12.0 s) show the full composition. The end is a hold, no fade.

## 8. Captions

Not exercised (demo build, no captions). Profile text, ASSUMED: no pill, 42 px Be Vietnam Pro 600 ink flush left at the grid margin in the bottom band, current word red; on paper the current word must use `--red-ink` (6.0:1), not `--red` (4.28:1). Be Vietnam Pro is not installed: use SegUIVar 600.

## 9. Sound

Not exercised (silent build). Profile text, ASSUMED: minimal techno 110-124 BPM, dry ticks and paper slides on column snaps; red bar one column per beat; no pulse, no flash. The demo's 0.4-0.5 s steps were written to a 120 BPM grid so music can be added later without re-timing.

## 10. Images

No generated image was used (optional, and the style is typographic). If one is needed: high-contrast monochrome photographic or geometric plate cropped to whole grid columns, never a rounded card, no text, no logos, no real people. The style's `avoid` list rules out product hero and montage. A generated picture must not look like data (see saas-bento section 10: a "skyline" returned five bars that read as a chart).

## 11. Must not

- No centred text, no rotation, no scale bounce, no drop shadow, gradient, glass or radius.
- No second accent colour; red is never small text on paper (use `--red-ink`).
- No `--mute` (#8a8883) text on paper (3.11:1).
- No element off the 12-column grid or below y 1750.
- No emoji; no `segoepr.ttf`; no serif.
- No invented figure without the "Minh hoạ" chip and a footer that says it is assumed.
- No outgoing beat left visible after its wipe (hide it at wipe end).

## 12. Traps seen in real builds (this build, 2026-11-14, 12.0 s sample t141)

1. **Descenders cut by line masks.** First render: the `g` of "giá" and the `y` of "máy" were sliced at 210 px, because the mask padding was 0.12 em bottom. Descender plus the dot of Vietnamese "ợ" need 0.30 em below and 0.20 em above. Final: `.ln { overflow:hidden; padding:0.2em 0 0.3em; margin:-0.2em 0 -0.3em }` (net layout unchanged). At 190-210 px that is 57-63 px of bottom padding. Check by looking at `g y p ợ ộ` in every display line, not at the Vietnamese capitals.
2. **Red bar crowds the display.** With the bar at y 1190 and the last line's baseline region ending at about 1175 the bar touched "mới". Moved the bar to y 1226 and the deck to y 1276 (a 51 px gap between the descender area and the bar).
3. **Staggering all ten cells then resetting seven.** First version filled all 10 cells (stagger 0.12 s over 1.08 s) and then reset cells 4-10 with `tl.set`, which showed up to 6 red cells at 6.5 s and a flickering count between 6.0 and 7.0 s (read as 30% -> 50% -> 30%). Final: tween only the first 3 cells (`.cell:nth-child(-n+3) .cf`), 0.36 s total.
4. **Counter and wipe overlap.** The numeral starts at 4.5 s (just after the wipe) and ends at 5.2 s. At the 4.5 s contact-sheet sample it read "24%", at 5.0 s "30%". Rule held: count starts after the wipe has finished and finishes within 0.8 s (0.7 s used) before anything else is read.
5. **Wipe shows the outgoing beat for 0.45 s.** On the sheet frames at 4.0 s and 8.0 s the outgoing scene is visible to the right of the wipe edge ("á / náy", "Thủ tục" fragments). That is the wipe itself, under the 0.5 s limit, and the incoming layout shifts 76 px into place at the same time. The outgoing section is set `visibility:hidden` at wipe start + 0.5 s so nothing ghosts afterwards.
6. **Frame 0 skeleton.** The first sampled frame (0.0 s) shows the headline half-revealed (lines start at 0.10 s). It is a motion frame, not a held frame, but a still thumbnail of it looks broken: pick the thumbnail from 2.5 s or later.
7. **Inspect warnings are expected.** `hyperframes inspect` reported 4 `content_overlap` warnings (t 0.67-3.33 s and 4.67-7.33 s): the `.ln` masks overlap by design (negative margins) and `#num` (450 px, line-height 0.9) overlaps the label above it by its line box, not by its glyphs. Lint 0 errors / 0 warnings, validate no console errors.
8. **Tools in this environment.** `frame_check.py` failed here (`ModuleNotFoundError: numpy`) and inline python / node were blocked, so the frame check was done by reading a 24-frame ffmpeg contact sheet (`fps=2, tile=8x3`); contrast ratios were computed by hand with the WCAG formula. Fix the python environment before relying on the scripted checks.
9. **Render numbers.** `hyperframes render` standard quality: about 15 s for 12.0 s, 1.36 MB (1080x1920, h264, 30 fps, silent, no audio track).
10. **Large red numeral is fine, small red is not.** `--red` at 450 px passes as large text (3:1 needed, 4.28 measured); the same colour at 30 px would fail. The indices 01-03 therefore use `--red-ink`.

## 13. Open questions for a real (voiced) build

- How the 0.4 s bar steps and 4.0 s wipes map onto spoken words (not tested; keep word anchors per `composition-contract.md`).
- Caption band position with the bottom of the grid occupied (the demo leaves y 1750-1920 empty; captions would take y 1370-1480 per the other docs, which collides with the bottom index row of R1 at y 1500-1620: move that row up or drop it).
- Which niche, if any, the owner assigns.
