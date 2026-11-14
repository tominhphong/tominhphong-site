# Style: Modular build (9:16 Vietnamese brick-assembly edition)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in one build:** products or ideas that are built from parts and explained step by step: kits and toys for kids, product assembly, onboarding steps, "building blocks" of a platform, DIY how-tos. It gets its charm from one object assembling in front of the viewer, so it needs ONE hero object with 6 to 12 parts. Not for news with numbers, quotes, bad news, enforcement, money, or anything serious (the bright primaries and stepped hops read as play). Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from one DEMO-ONLY build: `samples/sample-t125.mp4`, 12.0 s, 1080x1920, 30 fps, silent, topic shape t125 "toy company releases a build-it-yourself robot kit for kids", content generic and labelled "Minh hoạ". **Voice-over, word timing, music and captions were NOT exercised**; sections 8 and 9 are the profile's values, untested. No agy image was used (all art is CSS). Source of values: `styles/profiles/modular-build.yaml`; anything the profile does not give is **ASSUMED**.

The look: cream instruction paper, flat primary-colour cuboid "bricks" with a lighter top and a 18% darker side face, numbered instruction-manual steps, a parts tray with counts, bricks that drop and snap on twos (15 fps steps), and a tile-pop transition. Energy 4 (profile) but the juice is stepped, never floaty.

## 1. Tokens (contrast measured with the WCAG formula, by hand)

```css
--bg: #fef9e7;      /* cream paper                                   */
--ink: #1b1b1b;     /* text, outlines, hard shadows: 16.33:1 on bg, 17.2 on white */
--red: #d8462c;     /* brick / fill ONLY: 4.12 on bg, white on it 4.35 (fails small text) */
--red-ink: #b83a22; /* red AS TEXT or badge fill: 5.43 on bg, white on it 5.73 */
--yellow: #f2aa1a;  /* brick, chip fill: ink on it 8.64 */
--blue: #2a4fb8;    /* brick, pill fill: white on it 7.22, 6.85 on bg */
--green: #1f8a5c;   /* brick, check box (graphic only): white on it 4.33, ink on it 3.98 -> never small text on green */
--mute: #6d6e70;    /* footer line: 4.84 on bg, 5.10 on white */
```
Rules: only red, yellow, blue, green and white bricks. Face shading is computed, not designed: top = colour mixed 22% to white, side = colour x 0.82, all faces get `inset 0 0 0 3px rgba(27,27,27,.45)` so white bricks stay visible on cream. Text never uses `--red`, `--green` or `--yellow`.

## 2. Fonts (local files)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, step label, pills, counts' labels | Archivo Black / Archivo 600 / Be Vietnam Pro | `SegUIVar.ttf` weight 700, `letter-spacing:-0.02em`, uppercase titles | Rendered in the sample: Ă Ắ Ầ Ố Ồ Ủ Ả Ơ Đ ê â ư ạ all drew correctly in 12 snapshots (visual check; the font was fully checked with fontTools in the other owner docs) |
| Counts "x2" | none | `CascadiaMono.ttf` 700 | digits and x only |
| `cambriai.ttf` | | not used | |
| `segoepr.ttf` | | never: lacks Vietnamese letters | |

Archivo Black is not installed; Segoe 700 is lighter than Archivo Black. It reads fine but is less "toy-box". If a heavier face is installed later, swap the `--h` font only; sizes hold.

### Type scale (1080 x 1920, px, as built)

| Token | Size / line | Notes |
|---|---|---|
| `.h1` scene-1 headline | 84 / 1.15, uppercase | 2 lines, max 14 chars per line (about 770 px wide) |
| `.h2` step label | 76 / 1.15, uppercase | 2 lines, max 12 chars per line (about 600 px) |
| step number in `.sbox` | 160 / 212 | in a 200x220 white box |
| `.kick` | 34, +0.08em, uppercase, `--red-ink` | "BƯỚC 1 / 3" |
| count `.cnt` | 76 mono | "x2" |
| card label `.lab` | 38 | |
| pill | 34 | "1  Chân" |
| sub line | 44 | |
| chip "Minh hoạ" | 30 | |
| footer | 24 (the one allowed line under 30) | |
| arrow badge number | 36 | |

Line-height 1.15 or more: Ủ, Ồ, Ắ tone marks on capitals are not clipped at 1.15.

## 3. Safe areas and grid (1080 x 1920, as built)

```
y 0    - 170   platform UI: empty
y 176  - 232   chip "Minh hoạ" (x 96, 56 px high)
y 262  - 510   scene-1 headline (2 x 84)   |  y 284 - 534 step header (box 200x220 + kicker + 2-line label)
y 516  - 544   colour strip of 10 squares (scene 1 only)
y 560  - 1300  tray panel / build panel (888 x 740, 4 px ink border, 8 px hard shadow)
y 1338 - 1400  sub line (scene 1)  |  y 1340 - 1412 progress pills (scenes 2-3)
y 1430 - 1454  footer line (24 px)
y 1480 - 1920  platform UI: empty
x 96 - 984     content column (888 px)
```
Consequence: content ends at 76% of the frame height, so a naive "top-heavy" check will flag the whole video. This is the platform-UI safe area, not a defect. A bigger robot could not fit the panel without leaving the column.

## 4. Layers, back to front

`#root` cream bg -> `#chip`, `#foot` (always on) -> `#s1` (headline, strip, `#tray`, sub line) -> step headers `#hd1..#hd4` (stacked, one visible) -> `#panel` (build panel) -> `#stage` (all bricks, arrows and confetti in absolute frame coordinates) -> `#prog` pills -> `#tiles` (66 transition tiles, on top). No flash layer, no shake, no music-driven pulse.

## 5. Components

- **Brick** `brick(parent, {x, y, w, h, d, c, inner})`: three flat divs. Front `w x h`. Top: `height d`, `transform-origin: 0 100%`, `skewX(-45deg)`. Side: `width d`, `transform-origin: 0 0`, `skewY(-45deg)`. This is a cabinet-oblique view (front, top and right faces visible), not true isometric. Plain tops, no studs. Draw order = DOM order; for a body part that touches another, the one that must cover goes later (left arm, legs, body, right arm, head, eyes, antenna). Right arm must sit at least `d` px right of the body (x 750 vs body 350+300), otherwise its front face overlaps the body's side face.
- **Baseplate**: one flat green brick 640 x 34, depth 90, under the build. It gives a ground and fills the panel from frame 0 of scene 2.
- **Panel**: white, 4 px ink border, radius 12, hard 8 px shadow, one 48 px grid drawn with a single CSS gradient element.
- **Step box** `.sbox`: 200x220 white, 4 px border, 8 px hard shadow, 160 px number. The last state is the same box in green with a white check (SVG polyline, stroke 22).
- **Parts card**: 418x220, cream, 4 px ink border; a mini brick on the left (bottom-aligned at y 196, centred at x 105), count and label on the right (x 226).
- **Instruction arrow**: a 64 px red-ink circle with the step number (36 px white) and a 40 px ink triangle pointing down at the target. Shows 0.25-0.3 s before the piece drops and bobs 10 px on twos. Marked `data-layout-allow-overlap`.
- **Progress pill**: 280x72, three states: idle (white, ink), active (`--red-ink`, white), done (`--blue`, white). Both coloured states pass 5.7:1 or better.
- **Confetti**: 16 squares 34 px in the four colours, falling 580 px in 1.2 s on `steps(10)`.
- **Transition tile**: 6 x 11 grid of 180x176 flat colour squares with an inset 10 px darker bottom edge.

## 6. Motion language

- Everything is stepped: drops use `steps(3)` over 0.2 s (3 positions = on twos at 30 fps), the snap is a 4 px bounce for one step (0.067 s, `steps(1)`), hops are `steps(3)` up and down, page turns are `steps(2)` over 0.1 s. No `back`, no `elastic`, no easing curves on bricks.
- Drop distance rule (measured): the falling brick must start inside its panel. Head dropped from 240 px above its spot crossed the step headline at 7.2 s (trap 1). Allowed start: spot top minus drop distance >= panel top (560) + 10. Used: legs 200, body 240, arms 240, head 70, eyes 120, antenna 40.
- Arrows lead each drop by 0.25-0.3 s and vanish on the drop frame; the next arrow starts on the same frame (overlap, not queue).
- Holds carry motion: scene 1 hops each card and strip square in turn (12 px, 0.4 s each); scene 3 hops the robot twice (46 px, 8.55 and 9.05 s) then the pupils look left and back (10.6 and 11.2 s). The profile's "celebratory spin" was replaced by a hop: the cabinet-oblique faces cannot rotate in CSS 2D without breaking.
- Transition between scene 1 and 2: **tile pop**: 66 tiles scale 0 to 1 on `steps(2)` 0.134 s, diagonal stagger 0.02 s per cell plus up to 0.05 s random (seeded), full cover at about 3.5 s, swap at 3.52 s, uncover in the opposite diagonal, clean at about 4.05 s. Total 1.05 s. Brick crumble, brick build and page turn from the profile were not used except the page turn (below).
- Between steps: **page turn** of the whole header group: `scaleX` 1 to 0 and back over 0.1 s each, hidden for one frame.

## 7. Scene recipes (S = scene start; times as built; all tween starts are non-negative)

### R1 Parts list (0 - 3.5 s, hook)
Headline "BÉ TỰ LẮP / ROBOT CỦA MÌNH" visible at frame 0. Ten colour squares pop in under it, one per 0.04 s from 0.04 s. Six parts cards drop on twos, one every 0.18 s (0 - 0.9 s); tray 2 x 3: Chân x2, Thân x1, Tay x2, Đầu x1, Mắt x2, Ăng-ten x1 (9 pieces, matches the sub line "9 mảnh ghép, 3 bước lắp"). 1.75 - 3.0 s: cards hop in turn. 3.0 s: tile pop.

### R2 Instruction steps (4.05 - 8.4 s, 3 steps of about 1.5 s)
Step box and label per step; the progress pill of the step turns active; per piece: arrow 0.3 s, then drop. Step 1 legs at 4.45 and 4.75. Step 2 (page turn 5.2): body 5.6, left arm 5.9, right arm 6.2. Step 3 (page turn 6.75): head 7.15, eyes 7.4 and 7.65, antenna 7.95. The number of pieces dropped in a step equals the counts in the tray.

### R3 Finished build (8.4 - 12.0 s)
Page turn to the green check box and "XONG RỒI! / ROBOT CỦA BÉ"; all three pills done (blue); robot hops twice; confetti lands on the baseplate by 9.65 s (its 16 pieces rest there). 10.2 - 12.0 s: full composition, only the pupils move. Held 3.6 s in total.

## 8. Captions

Not exercised (silent demo). Profile value, untested: white box, 4 px ink border, hard 6 px shadow, 42 px Be Vietnam Pro 700 ink, current word red (use `--red-ink`, not `--red`: 5.43 vs 4.12 on white... on white `--red-ink` gives 5.73). The bottom band y 1330 - 1480 is free in this layout except the pills (y 1340 - 1412) and the footer (y 1430): a caption pill would collide with both; moving the pills up or dropping them in a captioned build is needed.

## 9. Sound

Not exercised. Profile value, untested: upbeat pop with claps 115-125 BPM, plastic click on every snap, rattle on crumbles. The build has natural click points: 9 drops at 4.45 - 7.95 s and 6 card drops at 0 - 0.9 s.

## 10. Images

None used. All art is CSS bricks. If an agy image is wanted, it may only be decoration (no text, no logos, no real toy brand, no studs).

## 11. Must not

- No real toy logos, minifigures or studded-brick shapes (profile). Plain cuboids only.
- Only red, yellow, blue, green, white bricks; no gradients, no soft shadows (hard 0 offset shadows only).
- No eased or floaty brick motion; always `steps()`.
- `--red`, `--green`, `--yellow` never as small text; use `--red-ink` or ink.
- A falling piece never crosses text.
- No testimonial or quote scenes (profile). No real company, price or spec in illustrative content; every illustrative video carries the "Minh hoạ" chip and a footer line for its whole length.
- No camera shake or flash (profile: "No flashes").

## 12. Traps seen in real builds (this build, 2026-11-14)

1. **A dropping brick crossed the headline.** At 7.2 s the head, dropping 240 px, covered "LẮP ĐẦU, MẮT VÀ ĂNG-TEN" for about 0.2 s. Cause: drop distance larger than the gap between the panel top (y 560) and the brick's spot. Fix: head 70 px, eyes 120, antenna 40 (rule in section 6). The head's arrow had the same problem: its badge sat at y 514 - 578, inside the header zone (y to 534); moved the arrow tip onto the head's own top face (tip at y 700).
2. **Tray empty at frame 0.** The first card started at 0.1 s so the 740 px panel was empty at t = 0. Fix: first drop starts at 0.0 s, one card per 0.18 s. Still, the panel is only part-filled until 0.9 s (under the 0.5 s limit per empty state, but cards 4 - 6 are missing for 0.7 s).
3. **Scene 2 opens with an almost empty panel.** From the end of the uncover (4.05 s) to the first drop (4.45 s) the panel holds only the green baseplate and one arrow (0.4 s, under the 0.5 s limit; one more beat would break it). Start the first arrow at 4.05 or shorten the uncover.
4. **Overlap warnings from `inspect` on a full-frame stage.** The 1080x1920 `#stage` layer reported overlaps with the chip and the header text at 8.67 - 11.33 s (3 warnings, 0 errors after marking `data-layout-allow-overlap` on `#stage`). Alternative: size the stage to the panel.
5. **Brick overlap order.** A right arm at x 660 (inside the body's side face, x 650 - 740) looked glued to the wrong plane. Moved to x 750. Left leg's side face (x 470 - 540) overlaps the right leg's front by 10 px with a 60 px gap and 70 px depth; looks like a shadowed seam, kept.
6. **Tile pop frames look like stray squares.** At 3.3 s and 4.0 s snapshots show loose coloured squares over the old or new scene. They are tiles mid-scale (0.134 s per tile), not leftovers; judge a transition only from the 2 fps sheet, not from one snapshot. Total transition 1.05 s of a 12 s clip: heavy; for a short use a 0.6 s spread.
7. **Content ends at y 1454 of 1920.** A top-heavy check will flag it; it is the safe area (section 3).
8. **White on `--red` is 4.35:1.** `validate` passed 20 text elements, but only because the white-on-red badge uses `--red-ink` (5.73). Using `--red` for the badge would fail.
9. **Tools missing.** `frame_check.py` needs numpy and could not run in this environment (`ModuleNotFoundError`); the check was done with an ffmpeg 2 fps contact sheet (24 frames, 8 x 3) read by eye, plus `inspect` and `validate`.
10. **Renderer cost.** 66 tiles with only flat backgrounds and inset shadows rendered without black frames; render time about 16 s for 12 s at 30 fps; file 0.56 MB.
