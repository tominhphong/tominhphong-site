# Style: quirky-editorial (detail, first build, demo only)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY, observed in one build).** Warm, human, slightly odd small-business and community stories told with illustration and a witty punchline: workshops and classes, makers, local shops, hobby communities, brand refresh, "how it works in 3 steps" explainers. Jev fit for the tested shape (a DIY community print shop teaches screen printing on Sundays) was 0.63: usable, not a strong match. Not for urgent, financial, enforcement, spec or dark stories (the profile avoids terminal, spec, montage). Tier 2 never widens tier 1.

**Status.** Written 2026-11-15 from ONE demo build: a silent 12.0 s sample, 1080 x 1920, 30 fps, 5.3 MB, 3 beats, no images generated (all art is code-drawn SVG). **Voice-over, word timing, music and karaoke caption rules were NOT exercised** (demo build): nothing here says how captions or sound behave in this style beyond the profile. Everything marked ASSUMED is invented by this build; SUBST = font substitution.

Profile: `skill/references/styles/profiles/quirky-editorial.yaml` (energy 3, light mode). Example video shows the visual recipe, not the niche.

SUBST 1: profile asks Fraunces 700 (soft serif). Not installed. `cambriai.ttf` (Cambria Italic, only one weight, always italic) is the headline face. `font-synthesis: none` so no fake bold.
SUBST 2: Manrope / Be Vietnam Pro are replaced by `SegUIVar.ttf` (variable, weights 500-700 used).
DEVIATION 1: profile says "headline left, illustration spilling off right"; at 1080 x 1920 everything stacks (headline top, illustration below, spilling off the right edge in beat 1 only).
DEVIATION 2: profile wants baked pencil-texture and risograph grain; this build bakes one grain PNG with ffmpeg (see section 4) and uses no pencil masks.

## 1. Tokens

```css
:root{
  --mustard:#f2c230;  /* bg beats 1 and 3 */
  --ink:#1f1b17;      /* all text and all linework */
  --cream:#f6f0e4;    /* bg beat 2, chips, frame/shirt fill */
  --teal:#1a8072;     /* FILL ONLY */
  --teal-dk:#0f6357;  /* ASSUMED: chip fill under cream text */
  --coral:#f2777a;    /* FILL ONLY (card 3 background, print layer) */
  --sage:#9eb28c;     /* card 2 background, screen window */
  --mute:#6b5f55;     /* not used in this build; cream bg only */
}
```
Contrast, WCAG formula computed by hand from sRGB (HyperFrames `validate` also reported "20 text elements pass WCAG AA"):

| Pair | Ratio | Use |
|---|---|---|
| ink on mustard | 10.2 | headlines, body on mustard |
| ink on cream | 15.1 | headlines, chip text |
| ink on sage | 7.5 | card 2 text |
| ink on coral | 6.3 | card 3 text |
| cream on teal-dk | 6.3 | chip "Chủ nhật hàng tuần" |
| teal #1a8072 on cream | 4.2 FAIL | never text |
| teal-dk on mustard | 4.25 FAIL | never text |
| mute on mustard | 3.7 FAIL | never on mustard |
| mute on cream | 5.45 pass | allowed on cream only |

Rules: on mustard, coral and sage the only text colour is ink. Teal and coral are flat fills inside illustrations and card/chip fills, never a page background (profile rule; cream and mustard are the two backgrounds). Grain overlay: 1 PNG, `mix-blend-mode: multiply`, opacity 0.13 (profile says 8%; 0.13 was needed to be visible after H.264 at standard quality; ASSUMED).

## 2. Fonts (checked by rendering the real words; fontTools could not be run in this session)

| File | Role | Vietnamese check |
|---|---|---|
| `cambriai.ttf` | headlines 118-130 px, one line = one idea, letter-spacing -0.02em | Rendered correctly in snapshots: "Chủ nhật", "học in lụa", "bằng tay", "Ba bước", "một buổi sáng", "Áo lem mực", "vui thật" (hook-above, dot-below, circumflex-plus-dot all visible, none clipped) |
| `SegUIVar.ttf` | card titles 66 px 700, body 38-44 px 500, chips 42 px 700, sticker 38 px 700 | Rendered correctly: "Xưởng", "cộng đồng", "Phủ lưới", "Hình in sang lưới, chừa chỗ cho mực", "chiếc áo thành của bạn", "Minh hoạ" |
| `CascadiaMono.ttf` | declared, not used | not tested |
| `segoepr.ttf` | NOT copied into the project (lacks Vietnamese Ơ ơ Ư ư and others) | never use |

Note: the project copy of `assets/fonts` holds only the three usable files on purpose.

## 3. Type scale, safe areas, grid (1080 x 1920)

- Side margin 72. Content width 936.
- y 0-200 empty except the "Minh hoạ" sticker (right 72, top 196, 38 px, rotated -5 deg).
- Headline block top 330: beat 1 130 px x 3 lines (line-height 1.08), beat 2 118 px x 2 lines, beat 3 124 px x 2 lines at top 1090 under the picture.
- Cards (beat 2): x 72, width 936, height 270, tops 660 / 960 / 1260 (gap 30). Number badge 76 px circle at (-22,-26). Icon 200 px at left 28. Title left 268.
- Chips (beat 3): height 84, top 1470, x 72 and x 560.
- Lowest content edge: beat 1 about y 1630 (squeegee), beat 2 y 1530, beat 3 y 1554. y 1650-1920 empty (platform UI).
- Smallest text: 38 px (card sublines, sticker). No footer line was used.

## 4. Layers, back to front

1. `#root` background colour (changed by `tl.set` at each colour swap).
2. Scene sections `.sc` (z 14), one visible at a time.
3. `#xt` colour-field wipe (z 12, sits UNDER incoming scene, over outgoing background): full-frame block in the next colour with a 10 px ink top edge.
4. `#tag` "Minh hoạ" sticker (z 20), all 12 s.
5. `#grain` (z 30): baked PNG, made with `ffmpeg -f lavfi -i color=c=0x808080:s=540x960,noise=alls=60:allf=t+u,format=gray`, then scaled 2x nearest to 1080 x 1920.

Never use CSS blur or live noise filters.

## 5. Components

- **Ink illustration** (the core of the style): each shape is a closed or open polygon passed through `wob()`: edges densified every ~70 px, each point jittered +-2.6 px (seeded LCG), smoothed with Catmull-Rom to cubic bezier. Stroke 4-5 px ink, round caps and joins, flat fill of a palette colour. Always ink outline (profile constraint).
- **Boiling line:** 3 variants per illustration (different seed per variant), each variant a group with fill + stroke. Groups toggle with `display` every 0.1 s (about 10 fps; profile says "on twos"; 0.067 s felt like strobing on a held frame, ASSUMED 0.1 s). Fills boil with the strokes.
- **Card** `.cd`: radius 6, 3 px ink border, hard offset shadow `8px 8px 0 ink`, flat fill (mustard / sage / coral), number badge ink circle with cream numeral.
- **Chip**: radius 6, 3 px ink border, 5 px hard shadow, 42 px 700.
- **Sticker** "Minh hoạ": cream, 3 px ink border, radius 6, hard shadow, -5 deg.
- **Sparkle doodle**: 4-point star path, 70-90 px, ink or cream with ink stroke; wiggles +-10 deg, scale 0.9-1.1, 0.42 s yoyo.
- **Underline squiggle**: coral 10 px stroke, drawn with dashoffset 0.5 s.
- **Misregistered print:** shirt print = coral circle layer plus a teal star layer on top; the teal layer arrives 0.15 s later and 12 px off (settles to 0). A real screen-print detail and the beat-3 punchline picture.
- Icons: code-drawn from polygons (pencil, frame, squeegee), never by agy. No image was generated in this build; if agy images are added later, no text, no logos, no real people.

## 6. Motion language (energy 3)

- Headline: line mask reveal, `yPercent 118 -> 0`, rotation 5 -> 0 about the bottom-left, `power4.out` 0.6 s, stagger 0.1 s with `power1.in`. Mask `.ln` has padding .2em top / .14em bottom so Vietnamese tone marks are never cut; mask carries `data-layout-allow-overflow`.
- Line redraw: `strokeDashoffset 1 -> 0` (pathLength=1) `power2.inOut`, 0.55-0.75 s, stagger 0.07; fills flood in `opacity 0 -> 1` 0.35 s starting 0.3-0.65 s after the draw starts (overlap, profile says 0.7 s redraw).
- Cards: slide x +300, y +30, rotation 6 deg -> 0, `back.out(1.3)` 0.6 s, opacity 0 -> 1 in only 0.18 s (so no semi-transparent card on a held frame); stagger 0.32 s.
- Squeegee: x -300, y +110, rotation -16 -> 0, `back.out(1.3)` 0.75 s.
- Stamp (beat 3): `scale 1.4 -> 1`, `power3.out` 0.25 s (outside `back`, per motion-craft rule for pieces settling over a surface).
- Sparkles pop `scale 0 -> 1` with 60 deg spin, `back.out(1.3)`, then wiggle.
- Hold motion: beat 1 illustration drifts x -20 over 3.3 s; beat 2 cards sway +-0.6 deg, 0.9 s yoyo; beat 3 shirt and print sway +-1.4 deg about 50% 60%; boil runs the whole hold. Nothing is frozen.
- No flashes, no shake, no speed lines.

## 7. Captions, sound (NOT exercised)

Voice-over, karaoke captions and sound were not part of this demo. The profile says: cream box radius 6, 3 px ink outline, 42 px Be Vietnam Pro 600, current word teal. Warning from section 1: teal #1a8072 on cream is 4.2:1 and fails; a real build must use `--teal-dk` (6.3) for the current word. Not tested.

## 8. Scene recipes (the 3 beats built; 12.0 s)

**R1 Hook, 0-3.7 s, mustard.** Headline "Chủ nhật, / học in lụa / bằng tay." lineIn at 0.05; sub line (44 px, one line, `white-space: nowrap`) 0.55; screen frame outline draws 0.35-1.1, fills flood from 1.0; squeegee kicks in 1.15; sparkles 1.5 and 1.7; boil from 1.4 (frame) and 1.95 (squeegee). Text finished at about 0.75 s, picture complete at about 1.9 s.

**Transition 1: colour field swap, 3.7-4.08 s.** Cream block rises with an ink edge, `expo.inOut` 0.38 s. Background colour and scene visibility are swapped at the end of the wipe (t + 0.38); incoming entrances start the same frame.

**R2 Three steps, 4.08-7.7 s, cream.** Headline "Ba bước, / một buổi sáng." 118 px; coral squiggle draws at +0.5; three tilted cards at +0.30 / +0.62 / +0.94, each icon draws 0.3 s after its card starts, floods at +0.6, boils at +0.9; green sparkle at +0.7. Hold 3.0 s (all cards complete from about 5.7 s).

**Transition 2: mustard field swap, 7.7-8.08 s.** Same wipe.

**R3 Punchline, 8.08-12.0 s, mustard.** Shirt draws 8.08-8.63, floods from 8.38; coral print slaps at 8.83, teal print at 8.98 (12 px off, then lands); headline "Áo lem mực, / vui thật." at 8.98; chips pop at 9.88 and 10.08; sparkles 9.88 / 10.08; sway to the end. From 10.5 s the frame is complete and moving only by boil, sway and wiggle (last 1.5 s = full composition).

## 9. Transitions (this build used 1 of the 4 in the profile)

Used: colour field swap (twice). Not tried: line-redraw scene change, cut-out slide, surreal morph. A wipe covers the outgoing scene, so there is no ghost; the empty colour field lasts 0 frames because incoming content starts at the cover frame.

## 10. Image guidance

Not used. If a photo/art layer is added: loose ink drawing on flat colour, no text, no logos, no real people; cut-out objects with a white sticker border; bake grain and pencil texture to PNG.

## 11. Safe handling of facts

Demo content is generic and illustrative: no real company, price, date or spec; "Minh hoạ" sticker on screen for the full 12 s.

## 12. Must not

- Teal or coral as page background; dark or glossy 3D looks (profile).
- Text in teal or coral on any background (both fail 4.5:1 or have never been measured).
- segoepr.ttf for Vietnamese.
- `visibility: visible` set on a child of a hidden scene (see trap 1).
- Faux bold on `cambriai` (italic only, one weight).
- A hard cut; fast cutting (beats here run 3.6-4 s).
- Characters that copy a known mascot (profile).

## 13. Traps seen in real builds (this build, 2026-11-15)

1. **Hidden scene leaks through `visibility`.** The boil toggled `visibility: visible/hidden` on illustration groups. A child with explicit `visibility: visible` overrides a hidden parent, so beat 1's frame, squeegee and star showed on top of beats 2 and 3 (snapshot at 6.8 s and 11.9 s: pencil, frame and squeegee sitting under the headline). Fix: toggle boil groups with `display: inline/none`, leave `visibility` only on the scene section. Re-snapshot after the fix: clean.
2. **Empty shirt beat.** First timing (outline 0.8 s, fill at +0.55, print at +1.05, headline at +1.5) left beat 3 showing only a black outline on mustard at 8.6 s (about 0.9 s without a filled picture or text). Compressed to outline 0.55 s, fill +0.3, print +0.75, headline +0.9; the 4 fps sheet then shows a filled shirt from about 8.5 s.
3. **Orphan word in the sub line.** At 44 px in a 640 px box, "Xưởng in cộng đồng mở lớp mỗi Chủ nhật." wrapped leaving "Chủ nhật." alone. Fixed with a 940 px box and `white-space: nowrap` (the line is about 830 px wide).
4. **Teal text fails.** Teal #1a8072 on cream is 4.2:1, teal-dk on mustard 4.25:1. Use teal only as fills; text on teal is cream (6.3 with teal-dk).
5. **Overlapping GSAP tweens on the squeegee.** The slow drift (x) started at 0.4 s while the entrance (x) ran 1.15-1.9 s: lint `overlapping_gsap_tweens`. Fix: start the drift at 1.9 s.
6. **Inspect overlap on masked lines.** `content_overlap` at 8.67 s: the headline spans in their pre-reveal offset overlap each other. `data-layout-allow-overlap` on the `h1` clears it (0 issues after).
7. **Transient semi-transparent frames.** Snapshot at 10.4 s caught chip 1 mid-pop and at 9.4 s the teal print at about 50%. Both pop tweens are 0.25-0.35 s; shortened the stamp to 0.25 s and the card opacity to 0.18 s so any such frame lasts well under 0.2 s.
8. **Loose-ink corner rounding.** Catmull-Rom over densified points rounds every corner of rectangles into soft blobs; with amp 2.6 the screen frame and shirt read as hand-inked, with amp above about 4 they read as broken. Keep amp 2.4-3.
9. **Tools missing.** `frame_check.py` needs numpy, which was not installed and could not be installed here; the frame check was done with an ffmpeg 4 fps tile sheet read by eye (see selfcheck). Run the real script where numpy exists.
10. **Wrong CLI assumptions.** `hyperframes` has no `check`; the real checks are lint, validate, inspect, snapshot. `snapshot` always adds one extra end frame past the timeline (13.5 s here, plain mustard): ignore it.

## 14. What was not tested

Voice-over, captions, music, SFX, boil on twos at 0.067 s, line-redraw / cut-out / morph transitions, agy images, Fraunces. Beat 2 is a list of three cards: if the story had more than 4 items the layout would not fit.
