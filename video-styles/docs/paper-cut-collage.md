# Style: paper-cut-collage (detail, written from the demo build of 2026-11-14)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), as observed in this build.** Warm, tactile, human, local stories where the subject is a gathering of makers: zine fairs, craft markets, neighbourhood events, small shops, parks, schools, community programmes. It worked well on topic shape t133 ("Underground zine fair in Austin: bands, printers and tickets", Jev fit 0.79) because the subject IS paper, print and tickets, so the material and the story agree. Not for enforcement, specs, dense numbers or finance dashboards (the build had no number at all and the style never missed one). Tier 2 never widens tier 1.

**What was exercised and what was not.** This is a DEMO-ONLY build: one silent 12.0 s sample, 1080 x 1920, 30 fps, 3 beats, no voice-over, no word timing, no music, no captions, no full video. Everything about voice, pronunciation, karaoke captions, SFX sync and music is NOT covered by this document; section 7 and 11 say what the profile claims, untested. All numbers below are measured on that one sample or computed by hand (marked).

**Reading order.** Sections 1 to 6 are tokens and layout; 7 to 9 motion and scenes; 10 to 12 images, sound, must-not; 13 the traps from this build.

**Status.** Written 2026-11-14 from a real render (`samples/sample-t133.mp4`, 10.6 MB). Not merged into the skill folder. Profile: `skill/references/styles/profiles/paper-cut-collage.yaml` (energy 3, light mode, bpm 92-110, no detailed `style-*.md` existed before this file).

Marks: **SUBST** = a named font is not installed, a local one replaces it. **ASSUMED** = the profile gives no value and this document chose one. **DEVIATION** = knowingly differs from the profile.

- SUBST 1: profile asks for Archivo Black (headline), Fraunces 600 (subheads), Caveat 700 (notes), Be Vietnam Pro 700 (captions). None is in `assets/fonts`. Used: Segoe UI Variable (`SegUIVar.ttf`) at weights 600-800 for headlines and body, Cambria Italic (`cambriai.ttf`) for handwritten-style notes and the "Minh hoạ" tag. `segoepr.ttf` (the only handwriting face) lacks Vietnamese letters and was never loaded.
- DEVIATION 1: the profile says "UI screens printed on paper cards"; this sample has no UI screen, the cards carry flat SVG icons instead.
- DEVIATION 2: profile pacing bpm 92-110; this silent build uses a 100 bpm grid (beat 0.6 s) for timing only. No audio exists to confirm it.
- ASSUMED: every layout number in sections 3 to 5 (the profile gives none for 9:16).

## 1. Tokens

```css
:root{
  --bg:#f3ead8;        /* profile bg (paper)                    */
  --card:#fbf6e9;      /* ASSUMED: lighter stock for cards, strips, tiles */
  --ink:#231f1a;       /* profile ink     13.7:1 on --bg, 15.2:1 on --card (hand-computed WCAG) */
  --accent:#e4572e;    /* profile accent  FILL ONLY: 3.1:1 on --bg, ink on it 4.4:1 (fails 4.5) */
  --accent-dk:#b23a17; /* ASSUMED: accent for TEXT: 5.0:1 on --bg, 5.5:1 on --card */
  --mustard:#f2b134;   /* ink on it 8.7:1 */
  --sage:#7fa37a;      /* ink on it 5.8:1 */
  --sky:#6fa8dc;       /* ink on it 6.5:1 */
  --kraft:#c9a26b;     /* ink on it 6.9:1 */
  --tape:rgba(250,240,200,.82);   /* decorative only, never behind text */
  --shadow-rest:drop-shadow(0 6px 12px rgba(35,31,26,.25));   /* profile */
  --shadow-air:drop-shadow(0 34px 26px rgba(35,31,26,.14));   /* ASSUMED: piece in the air, before landing */
}
```

Contrast rules measured in this build:
- Ink on every paper colour passes 4.5:1 (lowest: sage 5.8). Use ink for all text on mustard, sage, sky, kraft, cream.
- The accent `#e4572e` must not carry small text. Cream `#fbf6e9` on it is 3.4:1: allowed only for the 176 px tile letter "Ợ" (large text, needs 3:1). Ink on it is 4.4:1, which fails; do not use. Text in the accent hue uses `--accent-dk` (stamp lettering "ĐỘC LẬP", 56-58 px).
- `hyperframes validate` reported "5 text elements pass WCAG AA" (it samples only some elements; the table above is the full list, computed by hand with the WCAG formula, not by a tool).
- A full-frame grain layer (`multiply`, opacity .55) sits on top of everything; its effect on contrast was NOT measured. Ratios above are before grain.

Colour rule seen to work: one flat colour per piece, at most 5 paper colours on screen in a beat, the accent only on the stamp and one tile (never a whole card).

## 2. Fonts (glyph test on the real script plus Vietnamese capitals and lower case)

| Role | File | Used at | Notes |
|---|---|---|---|
| Cut-out letters, titles, body | `SegUIVar.ttf` (variable) | 176 px / 800 (tiles), 78 px / 800 (card title), 66 px / 700 (strips), 42 px / 600 (card body) | substitutes Archivo Black and Be Vietnam Pro |
| Notes, tag | `cambriai.ttf` (italic only) | 46 to 64 px / 400 | substitutes Fraunces and Caveat; there is no bold italic, never set `font-weight` above 400 here or the browser fakes bold |
| (not used) | `CascadiaMono.ttf` | - | the style has no mono role |
| (never) | `segoepr.ttf` | - | no Vietnamese letters |

**Vietnamese diacritics check.** The planned fontTools glyph test could not be run (the session refused Python, see section 13 trap 9). Replacement evidence: the render and the snapshots show every accented form used in the copy drawn by the intended face (not a fallback): Ợ, Ầ, Ạ, Ố... in "CHỢ ZINE NGẦM", "NHẠC", "VÀO CỬA", and lower-case ạ, ả, ấ, ồ, ỏ, ở, ặ, ẩ, ề, ự, ứ in the notes. `hyperframes snapshot` printed "Fonts: 2 loaded". Stacked marks (Ầ with a grave over a circumflex) were read by eye at 176 px and are not clipped. Rule for the next build: run the fontTools coverage test on both files before writing copy.

## 3. Grid and safe areas (1080 x 1920)

- Side margin 60 px minimum (cards 70 px, strips 60-110 px). Nothing but tape and torn sheets may touch the frame edge.
- Top 0-150: the permanent "Minh hoạ" tag (left 56, top 64, 300 x 76). Body from y 170.
- Bottom: no caption band was built (demo, silent). If captions are added later, the profile's torn white strip needs about y 1590-1760; the three final-beat rows end at y 1630, so beat 3 would have to move up about 150 px first. Not tested.
- Beat 1: headline block 3 rows x 262 px, gap 16, from y 250 to y 1090; sub-strip y 1130; note y 1330; stamp y 1300.
- Beat 2: header strip y 170-320; three cards 940 x 330 at y 470, 830, 1190 (gap 30); sticky note y 1590.
- Beat 3: top strip y 190; ticket 900 x 560 at y 420; chips y 1170-1220; note and stamp y 1440-1630.
- Pieces are deliberately rotated -4 to +3 degrees and offset 4-10 px at random (seeded). A 10 px jitter on a 262 px tile still reads as hand-cut; 20 px read as sloppy in an early look.

## 4. Layers, back to front (z-index)

0. Paper: `--bg` plus the baked grain PNG on top (z 50, see below).
1. Halftone corner (CSS radial-gradient dots 22 px pitch, masked to one corner; one element only).
2. Backdrop sheet: kraft (beat 1), sage (beat 2), kraft (beat 3). Each is a torn-edge piece AND the wipe that brings the next beat in.
3. Content pieces (tiles, strips, cards, ticket, chips) z 6-14, each with its own shadow.
4. Tape strips and stamps z 8-20 (tape lands 0.3 s after its piece).
5. Confetti scraps (beat 3): z 3, BEHIND all content (see trap 3).
6. "Minh hoạ" tag z 60, grain z 50 (pointer-events none).

Structure of every piece: `.piece` (entry transform + `filter: drop-shadow`) > `.b` (boil jitter) > `.art` (the colour, `clip-path: polygon(...)` torn edge). The shadow must be on the OUTER element, because `clip-path` also clips a shadow drawn on the same element.

## 5. Components

- **Torn edge.** A seeded polygon: points every 30 px around the rectangle, each pulled inward by `rng() * amp` (amp 5-6 px on small pieces, 10 px on full sheets). Built in JS before the first tween. About 30 clipped pieces existed in total, at most about 20 visible at once; no black frame (blackdetect found none).
- **Cut-out letter tile.** 212 x 262 px, one letter, 176 px, 800 weight, ink on a paper colour, rotation -6 to +6, colours cycle cream, mustard, accent, sage, sky.
- **Strip.** Cream torn strip, text 54-66 px / 700, rotation -1.5 to 1.5.
- **Card.** 940 x 330: 250 px colour block with a flat SVG icon (note, printer, ticket) + title 78 px / 800 + body 42 px / 600 on two lines.
- **Sticky note.** Mustard torn rectangle, Cambria Italic 54-62 px, rotation 2.5 to -4.
- **Tape.** 150 x 46, `--tape`, rotation up to 38 degrees, never over text.
- **Stamp.** 300 px circle, 12 px border and text in `--accent-dk`, cream fill at 92%; no shadow.
- **Ticket.** 900 x 560 mustard rectangle, side notches from two radial-gradient masks, dashed 6 px perforation, stub text in Cambria Italic.
- **"Minh hoạ" label.** Mustard torn tag, Cambria Italic 46 px, on screen from 0.05 s to the end.
- **Doodles.** Inline SVG strokes (star, speed lines, hand-drawn underline), 7-8 px, drawn with `strokeDashoffset` in 0.4-0.5 s.

## 6. Baked textures

Only one texture was baked: `img/grain.png`, 540 x 960, made with ffmpeg (`color=c=0xeeeeee` + `noise=alls=24:allf=t`), shown at 1080 x 1920 with `mix-blend-mode: multiply`, opacity .55 (1.2 MB). Halftone is a CSS gradient on one element, under the 40-element renderer limit. Torn edges are generated polygons, not baked masks (deviation from the profile's "baked PNG masks": cheaper and exactly repeatable). No paper-fibre PNG and no generated art: `motion_tools.py image` was not run (section 13 trap 9).

## 7. Motion language

| Move | Values measured in this build |
|---|---|
| Drop (default entrance) | from y -300 to -500 and rotation -9 degrees off, `back.out(1.4)`, 0.40-0.46 s; shadow `shadow-air` to `shadow-rest` over the same time (`power2.in`) |
| Letter-tile stagger | 0.06 s per tile, 11 tiles, whole headline in about 1.0 s |
| Tape-on | scale 1.5 to 1, rotation +10 to 0, 0.14 s `power3.out`, 0.3 s after its piece lands |
| Stamp slap | scale 1.55 to 1, rotation +8 to 0, 0.2 s `expo.out` |
| Doodle draw | 0.4-0.5 s `power2.inOut` |
| Boil (stop-motion) | seeded, on `.b`: rotation +/-0.4 to 0.8 degrees, x and y +/-1.5 px, new value every 1/8 s (8 fps); only after landing, cleared before the beat's exit |
| Hold drift | backdrop sheet 14 px over 3.4 s; halftone 24 px over 11 s, linear |
| Transition (torn reveal) | a full-frame torn sheet slides in over 0.6 s `power2.in` (beat 1 to 2 from the right, 2 to 3 from below); the sheet is the NEXT beat's backdrop, so nothing fades and nothing is rebuilt from empty |
| Confetti | 24 seeded scraps, linear drift 140-260 px over about 3.4 s, behind content |

Juice level matches energy 3: soft overshoot only, no shake, no flash. No beat pulse was built (no music).

Timeline hygiene that held: all DOM built before the first tween; `visibility` set to visible at each entrance time (pieces never use opacity below 1, so nothing sits at partial opacity); scene containers hidden with `display:none` after their cover sheet has landed; one seeded `rng` (mulberry32, seed 1334); `tl.set({}, {}, 12)` ends the timeline.

## 8. Scene recipes (3 beats in 12.0 s; this is a sample, a full video would hold 5-9 such beats)

| Beat | Time | Recipe |
|---|---|---|
| 1 Hook | 0.0-4.2 | Kraft sheet slides in (0.5 s). 11 cut-out tiles spell "CHỢ ZINE NGẦM" in 3 asymmetric rows. Sub-strip "Ban nhạc · Nhà in · Vé vào cửa" at 1.3 s, hand underline 1.7 s, note "Austin, Texas" 1.8 s, doodle star 2.0 s, stamp "ĐỘC LẬP" slaps at 2.4 s. Hold 1.2 s with boil. Torn sage sheet covers it 3.7-4.3 s. |
| 2 Three things | 4.2-8.4 | Header strip 4.4 s; three cards drop at 4.6, 4.95, 5.3 s (one per 0.35 s), tape after each; sticky note 6.0 s; hold with boil about 1.8 s. Torn kraft sheet rises 7.9-8.5 s. |
| 3 Payoff | 8.4-12.0 | Top strip 8.55 s; ticket drops 8.65 s; three chips 9.3, 9.48, 9.66 s; note 9.9 s; stamp slaps 10.2 s; confetti throughout; the full composition holds from 10.6 s to 12.0 s (1.4 s of boil and drift). |

Rule from the build: a beat should reach at least half of its final content within 1.0 s of its start (beat 2 needed a faster stagger after the first look, see trap 7).

## 9. Transitions

Used: torn-reveal twice (profile value 0.5 s; built 0.6 s). Profile also lists slide-in stack, paper-flip and tape-on; not used here. The covering sheet and its drop-shadow (`-10px 0 18px`) are what makes a wipe read as paper rather than a plain slide; without the shadow it looked like a flat colour wipe.

## 10. Image guidance for agy

Not used in this build (0 images). The sample is built from generated paper, SVG and type only, and that was enough; generated art is optional for this style. If used later: one overhead tabletop photo prompt, "kraft paper, torn edges, halftone print texture, tape, cut-out look, muted cream / tomato / mustard / sage palette", no text, no logos, no people; bake it to a halftone, torn-edge cut-out before animating. Never place a raw photo edge-to-edge; the style wants a visible paper border and a shadow.

## 11. Voice, captions, sound (NOT exercised)

Demo build: silent, no voice-over, no word timing, no captions, no music. Profile claims, untested: captions as a torn white strip, 42 px Be Vietnam Pro 700 (substitute Segoe UI Variable 700), current word in accent (use `--accent-dk` for text, section 1); sound acoustic indie or light hip-hop 92-110 bpm with paper-rustle, tear and tape SFX. Nothing here validates them.

## 12. Must not

- No glass, chrome, neon, or perfectly clean vector edges on any paper piece (profile).
- No `Math.random`; seeded only.
- No tape over text; no confetti above text; no accent-coloured small text.
- No opacity fades for entrances (pieces drop in; they never dissolve).
- No text below 30 px on a held frame (smallest in this build: 42 px).
- No real company, product, price or spec; the label "Minh hoạ" stays on screen for the whole sample.
- Do not use `segoepr.ttf`.

## 13. Traps seen in real builds (this build, 2026-11-14)

1. **A drop shadow on a clipped element disappears.** `clip-path` cuts the shadow. Fix: shadow on the outer wrapper, `clip-path` on the inner `.art` (section 4). Found while planning, confirmed by the lit edges in the first snapshot.
2. **Hiding a scene container does not hide children that were set visible.** `visibility:hidden` on `#s1` is overridden by children with `visibility:visible`. Use `display:none` for containers (fixed before the first render).
3. **Confetti above text.** First snapshot at 11.9 s: a green and a red scrap sat on top of "zine" in the top strip. Fix: scraps z 3, behind every piece. Check every held frame for scraps and tape over letters.
4. **Tape over the note's first letter.** Snapshot at 11.9 s: the "B" of "Ban nhạc, nhà in," was half covered. Fix: tape moved to the left of the note, 100 px clear of the first letter.
5. **Cream gap at the bottom of beat 2.** The sage sheet is 2100 px tall at top -90; tweening it by -90 px lifted its bottom edge to y 1920 and left a 30 px cream sliver at 7.0 s. Fix: tween only 0 to -24 px.
6. **Layout checker noise.** `hyperframes inspect` first gave 47 warnings (stacked scene containers and pieces landing on pieces) plus 4 canvas-overflow notes (the oversize sheet), then 3 `text_occluded` errors at t=0.11 s, 4.71 s, 8.75 s (a card or the ticket passing under the tag and strip while still falling). All are transient and intentional. They were silenced with `data-layout-allow-overlap / -overflow / -occlusion` on every piece, which also hides any real future overlap: after changing layout, re-run `inspect` with those attributes temporarily removed, and read a contact sheet.
7. **Slow build-up read as empty.** First contact sheet: at 0.5 s the kraft sheet showed 2 tiles; at 4.9 s the lower 55 % of beat 2 was bare sage (cards started at 4.85, 5.45, 6.05 s). Fix: tile stagger 0.075 to 0.06 s starting at 0.02 s; cards at 4.6, 4.95, 5.3 s. After the fix the longest near-empty span is about 0.3 s (4.3-4.6 s, the header falling in from above the frame).
8. **Boil must stop before the exit and never touch the entry tween.** Boil is applied to the inner `.b`, the entry to `.piece`; the same element would make the two fight. `freezedetect` (noise 0.001, 0.2 s) found only three short stills of 0.27, 0.30 and 0.40 s (1.03-1.30, 3.67-3.97, 7.80-8.20 s), all before a wipe; boil lifts motion in the rest of the holds.
9. **The tools that the brief lists were refused in this session.** `python3 motion_tools.py image / probe` and `python3 frame_check.py` returned "requires approval" and could not be run; fontTools was refused too. Substituted: `ffprobe` and `ffmpeg` (contact sheet at 2 fps, `blackdetect`, `freezedetect`), snapshots read by eye, hand-computed contrast. The "ink % / BLANK / TOPHEAVY" numbers of `frame_check.py` were therefore never produced. If this style is rebuilt with those tools, re-run the check; expect a TOPHEAVY flag at 4.3-4.9 s unless beat 2 starts with cards.
10. **Renderer limit watch.** About 30 clip-path pieces and up to 20 drop-shadow filters live in one file, 360 frames rendered in 15.6 s with 5 workers, 10.6 MB (about 7.1 Mbit/s); no black frame. Do not exceed about 40 simultaneous clip-path or filter elements.

## 14. Fixes to carry into the next build

- Run the fontTools coverage test first (trap 9) and write copy afterwards.
- Add a pencil arrow or one low doodle in beat 2 so the lower half is never bare while cards land.
- Add a 4-6 px paper-fibre PNG overlay on the sheets (only grain exists now).
- Add captions and sound as a separate, tested step; this document does not cover them.
