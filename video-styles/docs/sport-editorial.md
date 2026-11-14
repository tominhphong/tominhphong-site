# Style: sport-editorial (9:16 Vietnamese limited-drop edition, family brand-inspired)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build (topic shape t084, Jev fit 0.82): a launch or drop of ONE physical product with a small number of facts (a limited sneaker drop, a collection, a ticketed event, a culture or lifestyle campaign). Works when the story is "what, how few, when". Not for dense numbers (use saas-bento), not for sad or enforcement stories, not for spec or terminal content (profile `avoid: terminal, code, spec`). Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12 s sample (`samples/sample-t084.mp4`, 1080x1920, 30 fps). **Voice-over, word timing, music, captions and SFX were NOT exercised** (demo build). Sections 8 and 9 are therefore taken from the profile and marked ASSUMED. Everything with a measured number was measured in this build. No owner document existed before; this one is a first draft.

**Clips and photos are optional.** The sample uses no photo: the product is a flat hard-edged SVG built in code. A real photo or cut-out would improve it (see Traps 7).

Character: part sports magazine, part street poster. Paper off-white, a visible 12-column rule grid at 15% alpha, hard-edged rectangular panels, big uppercase grotesk headlines that break raggedly across columns, small mono index numbers (01/03). Energy 4 (profile) but delivered as rhythm, not shake: panel wipes and splits carry the energy.

## 1. Tokens

```css
--bg:#efece6;       /* paper */
--ink:#111111;      /* text, dark panels     16.0:1 on bg (hand-calculated, WCAG formula) */
--accent:#0047ff;   /* one accent per scene: headline word, blue panel, button.  5.33:1 on bg (ok for large text 100+ px); white on accent 6.28:1 */
--mute:#7a766f;     /* profile value: 3.83:1 on bg = FAILS for text. Never use for text. */
--mute-ink:#57534d; /* ASSUMED text-safe mute, 6.48:1 on bg: footer line */
--signal:#ff5a1f;   /* sticker fill ONLY: 2.65:1 on bg, so never text; ink text on signal 6.06:1 */
--panel:#1a1a1a;    /* dark panel / inverted scene; paper on panel 14.8:1 */
```
Rules: paper and ink dominate; one accent per scene; dark panels invert type to paper (`#efece6` on `#111`, 16.0:1). Signal appears once, as a flat sticker, in the last beat only. No gradients, no glow, no radius, no shadows. `hyperframes validate` reported "15 text elements pass WCAG AA" on the final composition.

Grid rules: 13 vertical 1 px lines, ink at opacity 0.15, x = 72 + 78 i (i 0..12), full height, drawn under the scenes (hidden under the full-bleed dark scene).

## 2. Fonts (2 local files; profile fonts Archivo / Space Mono / Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headlines, sub lines, button, sticker | Archivo 800 wdth 75 uppercase | `SegUIVar.ttf` weight 700 uppercase, letter-spacing -0.02em (-0.04em on the 3-digit number). No width axis, so headlines are wider than Archivo condensed: size them smaller (see scale) | Rendered and looked at in snapshots: Ả Á À Ở Ợ Ẫ Ỗ Ặ Ắ Ị Ạ Ơ Ư Ế all drew correctly in `BẢN PHÁT HÀNH GIỚI HẠN`, `MỞ BÁN THỨ SÁU`, `MỖI SIZE MỘT LƯỢT MUA`, `ĐẶT LỊCH NHẮC`. Not a full 36-letter fontTools run (python was not available for ad-hoc scripts in this build) |
| Index numbers, chips, footer | Space Mono 400 | `CascadiaMono.ttf` weight 600 (500 footer) | Chip `MINH HOẠ`, `QUY MÔ`, `NGÀY MỞ BÁN`, `PHIÊN`, `GIỚI HẠN` drew correctly |
| Never | | `segoepr.ttf` (no Vietnamese letters), `cambriai.ttf` not needed | |

Declare faces with `font-display: block`; variable weight ranges `300 700` and `200 700`.

### Type scale (1080 x 1920, px, measured in this build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| Cover headline | Segoe 700 upper | 160 / pitch 150 (lines at y 300, 450, 600) | 3 ragged lines indented 0, 78, 234 px (1 and 3 columns); the last line in accent. Widest line `PHÁT HÀNH` = about 832 px at 160 |
| Hero headline (inverted scene) | Segoe 700 upper | 200 / pitch 180 | 2 lines, indent 0 / 78; `THỨ SÁU` fits at 200 (about 830 px) |
| Panel headline | Segoe 700 upper | 112 / pitch 138 | `MỘT LƯỢT MUA` = 12 chars does not fit 936 at 132 |
| Number | Segoe 700, -0.04em | 150 | `250` in a 312 px panel; 176 touched the panel edge |
| Panel small caps | Segoe 700 upper | 50 | `ĐÔI / DUY NHẤT` in a 312 px panel (64 clipped) |
| Sub line | Segoe 600 | 44 / 1.2 | sentence case |
| Button | Segoe 700 upper | 56, bar 120 px high | white on accent |
| Index / chip / panel letter | Cascadia 600 | 30, tracking 0.04-0.06em | chip: 48 px high, ink on paper (inverted on dark) |
| Footer | Cascadia 500 | 26 | the ONE line under 30 px: `Minh hoạ · nội dung giả định, không phải sản phẩm thật` |

Line masks need `padding-top: 34px; margin-top: -34px` so tone marks above capitals (Ở, Ẫ, Ắ) are not cut.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  top platform UI: empty
y 176  -224  index row: kicker (left, x 72) and MINH HOẠ chip (right, x 1008 edge)
y 290  -830  headline block (cover: 300-760; inverted scene: 290-650)
y 850  -900  sub line
y 930  -1400 panel row / product panels (cover: 980-1400 = four 234 px panels; split: 290-1050)
y 1130 -1400 panel headline (split scene)
y 1340 -1460 button (last scene)
y 1500 -1530 footer line
y 1530 -1920 empty (bottom platform UI)
x 72   -1008 content column, 936 px = 12 columns of 78 px, no gutters
```
Everything snaps to the 78 px columns: indents 78 / 234, split panel 312 + 624 (4 + 8 columns), button full width. The lower 390 px stay empty on purpose; a TOPHEAVY flag from the frame check there is expected.

## 4. Layers, back to front

`#root` paper -> `#grid` (13 rules) -> scenes `#s1 #s2 #s3` (one visible at a time; `#s3` carries its own `#111` background) -> `#strips` (4 ink panels, 270 x 1920, for the panel wipe) -> `#hT` / `#hB` (two 1080 x 960 ink halves, for the split). No flash layer, no shake layer, no beat pulse (no music).

## 5. Components

- **Index row**: mono kicker `NAME / 01/03` + `MINH HOẠ` chip. Fades in 0.15 s (`ease none`). The index changes per beat (01/03, 02/03, 03/03).
- **Panel**: hard rectangle, no radius, no border. Cover: four 234 x 420 panels (ink, accent, paper-grey `#d8d3c8`, panel) with mono letters A-D in the bottom-left corner. Split: ink 312 x 760 + accent 624 x 760.
- **Product**: one `<symbol>` SVG sneaker (viewBox 600 x 300): paper body, ink 8 px outline with mitre joins, accent toe cap, ink collar patch, three short lace marks, double sole line. Used 3 times at different sizes. No diagonal stripe motif (profile constraint).
- **Sticker**: flat signal rectangle, ink 50 px text, rotated -5 deg.
- **Button**: accent bar, no radius, white 56 px text, grows from the left (`scaleX 0 -> 1`, origin left).
- **Footer**: the "Minh hoạ" disclaimer, 26 px.

## 6. Motion language

Allowed eases: `expo.out`, `power4.out` (entrances), `power3.inOut` (wipes, splits, panel rises), `power3.out`, `sine.inOut` (micro drift), `none` (fades). No bounce, no elastic, no blur, no gradient.

| Move | Values measured in this build |
|---|---|
| Line rise (masked) | `yPercent 115 -> 0`, 0.55 s `expo.out`, lines offset 0.07 s |
| Panel rise | `yPercent 100 -> 0`, 0.5 s `power3.inOut`, stagger 0.06 s |
| Product slide-in | x +700 (cover), +760 (split), -800 (last) -> 0, 0.7-0.75 s `expo.out` |
| Product micro drift | y 0 -> -18..-22, 1.2-1.6 s `sine.inOut`, yoyo, repeat 1 (keep total inside the video length) |
| Number | opacity 0 -> 1 and scale 1.25 -> 1 over 0.3 s `power4.out` (a counter would have to be held mid-count; none used) |
| Sticker stamp | scale 1.6 -> 1, rotation -12 -> -5, 0.3 s `power4.out` |
| Panel-wipe transition | 4 strips y 1920 -> 0, 0.45 s `power3.inOut`, stagger 0.06; scene swap at the first frame when all are covered; then y 0 -> -1920 with the same stagger |
| Split transition | two halves close from top and bottom 0.4 s, swap at 7.95, open 0.45 s |

### Transition rules
Cover starts 3.5, full cover 4.13, swap 4.15, clear at 4.84. Split closes 7.5-7.9, swap 7.95, open to 8.4. The outgoing scene is hidden at the swap frame, so no ghost of an outgoing beat exists (0 frames measured by eye on the 2 fps sheet). Swap only while the panels cover the frame.

## 7. Scene recipes (S = beat start; sample timings at 120 BPM feel, beat = 0.5 s)

**R1 Cover (0 - 4.15).** Frame 0 already shows paper, grid and the index row; headline lines rise 0.05 / 0.12 / 0.19 s, sub fades 0.5 s, four panels rise from 0.45 s, product slides in at 0.95 s and drifts from 1.7 s. Everything is settled by 1.65 s; 2.5 s of hold with the product drift as micro-motion.

**R2 Number + product split (4.15 - 8.0).** Dark number panel grows from its bottom edge (scaleY 0 -> 1, 0.5 s), blue panel opens by clip-path inset from the right (0.5 s), `250` stamps at 4.65, small lines at 4.95, product slides in at 4.8 and tilts -3 -> 0 deg, headline lines rise at 5.1 / 5.2. Hold 5.7 - 7.5 with drift.

**R3 Inverted launch + CTA (7.95 - 12).** Dark scene: `MỞ BÁN` 8.15, `THỨ SÁU` 8.25, sub 8.6, product slides from the left 8.5, button grows 9.0, sticker stamps 9.3. All settled by 9.75. The last 2.25 s hold a full composition (product and sticker drift only).

Total: 3 beats, 2 transitions, 12.0 s. Something changes at least every 3.5 s.

## 8. Captions
NOT exercised (silent demo). ASSUMED from the profile: ink block on paper with no radius, 40 px Be Vietnam Pro 700 in paper colour, current word accent; Be Vietnam Pro is not installed, so use `SegUIVar.ttf` 700 at 44 px and check it against `captions-vi.md`. Keep captions out of y 1500-1530 (footer) and below.

## 9. Sound
NOT exercised. Profile (ASSUMED): UK garage / house / hip-hop 100-125 BPM, paper swipes and shutter clicks on panel moves; the sample's timings sit on a 0.5 s grid so they can be bar-aligned later.

## 10. Images
This build made no agy image: the command needed approval and was not given, so the product is the SVG above. Recommended for a real video: one agy cut-out or panel photo per beat, no text, no logos, no real people, hard-edged rectangle in a panel, 8 px paper outline on cut-outs, image drift 30-60 px inside the panel. Label generated pictures as illustration. Baked paper grain / halftone PNGs from the profile were not used.

## 11. Must not
- Rounded corners, gradients, glass, shadows, blur anywhere.
- Parallel diagonal stripe motifs, logo-like stripe patterns (the sneaker has none).
- Free-floating cards: every block snaps to the 78 px grid (the sticker is the only rotated item).
- `--mute #7a766f` as text (3.83:1) and `--signal` as text (2.65:1).
- A second accent colour in one scene; signal more than once in the video.
- A counter held mid-count; an empty panel visible > 0.5 s.
- Real brand, product, price, spec, logo, person. Demo content is labelled `MINH HOẠ`.
- Terminal, code or spec scenes.

## 12. Traps seen in real builds (this build, 2026-11-14, measured)

1. **Fixed-height line masks overflow.** Masks sized 190 / 210 px with a 34 px top padding made `inspect` report 20 px (160-176 px text) and 34 px (200 px text) of overflow on every headline line. Rule: mask height auto (padding 34 + font-size), `data-layout-allow-overflow` and `data-layout-allow-overlap` on the mask and its text child because tight leading overlaps the boxes by design.
2. **Widest line cut by its own mask.** `PHÁT HÀNH` at 176 px overflowed the canvas right by 57 px and the last H showed cut at 0.3-3.2 s. Fix: 160 px, mask width extended to the frame edge (930 instead of 858), text ends at about 982 px. Test the widest Vietnamese line, not the first.
3. **Two-word panel headline too wide.** `MỘT LƯỢT MUA` at 132 px was clipped at 936 px on every held frame; 112 px fits (about 800 px). `DUY NHẤT` at 64 px was cut by the neighbouring blue panel inside a 312 px panel; 50 px fits.
4. **Number touching the panel edge.** `250` at 176 px ended at 818 of 821 px in the panel. 150 px leaves 28 px padding. Rule: the number plus 28 px padding on both sides must fit the panel.
5. **Timeline longer than the video.** A yoyo with `repeat: 2` on the last product (9.3 s start, 1.3 s each way) ran to 13.2 s, so `snapshot` added an end frame at 12.8 s. Render length was still 12.0 s because of `data-duration`, but the drift never finished. Rule: start + duration x (repeat + 1) x 2 for yoyos must be <= video length; use repeat 1.
6. **Tools missing in the build environment.** `frame_check.py` needs numpy and PIL; neither was available and installing was not permitted, so the frame check was done with an ffmpeg 2 fps tile sheet read by eye (see selfcheck). Archivo was not installed (Segoe UI Variable has no width axis), so every headline is wider than the profile intends.
7. **Flat SVG sneaker reads as a slide sandal.** The low, hard-edged shape without laces or a raised heel looks like a sandal. If no photo is available, make the upper taller and add a visible lace area and heel counter. A photo or cut-out is the real fix.
8. **Wipe overlaps are transient.** `inspect` flags the panel row overlapping the footer at 0.67 s (panels still rising). Harmless because it is mid-motion; do not fix by shortening the move.
9. **Lower fifth empty.** Footer at y 1500 and nothing below leaves 390 px of paper; frame-check TOPHEAVY would fire. This is the platform-UI zone and is intended. Do not stretch content to fill it.
10. **Before delivery** check: frame 0 has the index row and grid (0.05 s of empty paper before the row fades in is acceptable), the last 1.5 s are a full composition, nothing under 90% opacity after 0.2 s.
