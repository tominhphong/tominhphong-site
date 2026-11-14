# Style: saas-bento (aesthetic family; 9:16 Vietnamese feature-tour edition)

Written 2026-11-14 from the demo build `samples/sample-t131.mp4` (12.0 s, 1080x1920, 30 fps, silent, topic shape t131
"team chat app adds threads, emoji reactions and integrations"). Profile source: `skill/references/styles/profiles/saas-bento.yaml`.
Everything not measured in this build is marked ASSUMED.

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
  chooses one, an agent working on the owner's channels does not pick this style by taste: ask the orchestrator.
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build.** The style carries a story of 3 to 4 named things that each
  deserve one tile and one small animated micro-demo: product feature releases and changelogs (threads, reactions,
  integrations), settings or plan tours, dashboards of 4 to 8 numbers. In this build three features plus a recap strip fitted
  a 888 x 840 px grid with every tile filled. Not for quote stories, one-number stories, hype, or anything that needs a
  long uninterrupted take. Tier 2 never widens tier 1.

**Status of what was exercised.** Demo-only build: ONE silent 12 s sample. Voice-over, word timing, karaoke captions, music and
SFX were NOT exercised, so this document has no verified voice or caption rules (section 8 and 9 are ASSUMED and short).
Everything else (tokens, type, grid, tile expand and collapse, stagger-fill, ring hand-off, packets on connectors, recap) was
built, rendered and frame-checked.

**Content rule for demos.** On-screen content is generic and labelled "Minh hoạ" in three places (kicker, a peach chip in the
strip, the footer line). No real company, product, price or spec.

## 1. Tokens

```css
--bg:#f5f6f8; --ink:#0f172a; --tile:#ffffff; --line:#e2e8f0;
--accent:#6366f1;      /* rings, connectors, avatar fill; NOT text (4.47 on white) */
--accent-ink:#4f46e5;  /* accent as text and as chip fill; white on it 6.29 */
--mute:#64748b;        /* tile labels on WHITE only (4.76) */
--mute-ink:#475569;    /* any muted text on the grey page or on a grey chip (7.01 on bg, 7.58 on white) */
--mint:#10b981; --mint-ink:#047857;   /* mint = mark; mint-ink = text on #ecfdf5 */
--peach:#fb923c; --peach-ink:#c2410c; /* peach = mark; peach-ink = text on #ffedd5 */
```

Contrast: the ratios above are from the WCAG formula as already measured in the owner reference for the same hex values (I did not
get to re-run my own script: Python scripts needed approval that this run did not have). Measured in THIS build:
`hyperframes validate` reported "20 text elements pass WCAG AA" on the final composition. Not measured separately (covered only by
that validate pass): peach-ink on #ffedd5, mint-ink on #ecfdf5, ink on #e0e7ff (the highlighted reply bubble).
White initials on the avatar fills #6366f1 / #10b981 / #fb923c are large 30-40 px bold labels; white on #fb923c is the weakest
(about 2.3:1 by formula, ASSUMED) and passes only the large-text rule if at all: use ink initials or a darker peach when this matters.

Material (profile, kept): tile radius 28, 1 px `--line` border, shadow `0 12px 32px rgba(15,23,42,.08)`; active tile = 3 px accent ring
drawn as a separate element 4 px outside the tile (radius 31) so it can fade and breathe independently.
Light mode only; the dark variant was not built.

## 2. Fonts

| Role | Profile asks | Used | Vietnamese check |
|---|---|---|---|
| Headline, labels, chips, bubbles, pills | Manrope 800/700 | `SegUIVar.ttf`, weight 300-700; headline 700, -0.03em | The fontTools 36-letter table check was NOT run (Python needed approval this run). Visual check only: every Vietnamese glyph that is on screen (ư, ơ, ồ, ể, ả, ờ, ợ, ạ, ế, ỗ, đ and others in the text list of selfcheck.md) rendered with correct marks in the final frames. Run the table check before relying on a letter that was not on screen |
| Numerals / counts | JetBrains Mono 500 | `CascadiaMono.ttf`, weight 600, count chips only | digits only in this build |
| Editorial line | none | `cambriai.ttf` | not used in this build |
| Never | | `segoepr.ttf` (lacks Vietnamese letters) | not copied into the project |

Copy only the three fonts into `assets/fonts/` of the project; declare each `@font-face` with `font-display: block`.

## 3. Type scale (1080 x 1920 px; all measured from the build)

Rule from the acceptance bar: nothing under 30 px except ONE footer line.

| Token | Size | Weight | Use |
|---|---|---|---|
| kicker | 30 px, +0.12em, uppercase | 700 | `--mute-ink`, 14 px accent dot |
| h1 | 78 px / 1.1, -0.03em | 700 | 2 lines, <= 24 chars each; key words in `--accent-ink` |
| tile label | 32 px | 600 | `--mute` on white, top-left, 28 px padding |
| bubble text | 30 px (grid) / 36-40 px (expanded) | 500 | ink on `--bg` bubble, radius 20-24 |
| chip / strip chip | 32 px | 700 | idle `--mute-ink` on `--bg`; lit white on `--accent-ink` |
| count | 32 px mono | 600 | reaction counts |
| step pill | 40 px | 600 (key word 700 accent-ink) | one phrase of <= 38 chars |
| expanded counter | 48 px | 700 | "N trả lời" |
| footer line | 24 px | 500 | the only text under 30 px; always begins "Minh hoạ" in a demo |

Vietnamese runs long: "Một kênh chat, ba tính năng mới" is 31 chars and fills a 40 px pill to about 650 of 888 px.

## 4. Safe areas and grid

```
y 0-170    empty (platform UI)            y 1308-1332 footer line (24 px)
y 176-206  kicker                         y 1370-1470 step pill (bottom 1470)
y 228-410  h1 (2 lines of 78 px)          y 1480-1920 empty (platform UI)
y 450-1290 BENTO GRID, 840 px             x 96-984 grid column (888 px), gap 20 px
```

Slots used (persistent; every tile snaps to them): T1 2x2 `96,450 434x324` threads; T2 2x2 `550,450 434x324` reactions;
T3 4x2 `96,794 888x324` integrations flow; T4 4x1 `96,1138 888x152` strip of chips + the "Minh hoạ" chip;
XP (expanded) `96,450 888x840`. Measured: with 4 tiles and no empty slot the content ends at y 1470 (77% of the frame height),
so a frame check that flags content ending above 55% does not fire. The grid is sized for three features; a fourth feature
needs a 4x3 reflow, not a new row (ASSUMED).

## 5. Layers, back to front

`#bg` flat grey -> `#grid` (4 tiles, rings inside each tile) -> `#xp` (expanded tile, hidden until needed, overflow hidden) ->
head (kicker + h1, above the grid in y) -> footer line -> step pills. No flash, no shake, no beat pulse, no fade layer: frame 0 is
already a finished headline.

## 6. Components

- **Tile**, **ring**, **bubble** (grey rounded message), **avatar** (circle with 3 px white border, one initial), **reaction chip**
  (56 px pill: 28 px SVG mark + mono count), **flow node** (60 px rounded rect; the centre node is solid accent-ink and 72 px high),
  **connector** (2-3 px accent path, `pathLength=1` + dash offset to draw), **packet** (14 px dot riding a connector),
  **strip chip** (52 px pill; lights up), **step pill** (white pill with the current phrase).
- **No emoji.** Reactions are drawn marks: a peach heart, a mint check, an accent four-point spark (inline SVG paths).
- Avatars in a stack must not overlap in the DOM: overlapping avatars made the inspector flag text_occluded (initial under the
  next avatar). Use 6 px gaps (60 px circles on a 66 px pitch).

## 7. Motion language (energy 3)

Eases: `power2.out` for entrances, `power3.inOut` for expand/collapse, `back.out(1.4)` for chips, nodes and avatars, `sine.inOut` for
hold breathing, `expo.out` for the particle burst, `none` for opacity and colour holds. No elastic, no shake.

| Verb | Measured recipe in this build |
|---|---|
| stagger-fill | 4 tiles, scale .92 -> 1 and opacity 0 -> 1, 0.45 s, stagger 0.07 s (all four tiles full by 0.66 s); labels rise 12 px |
| ring hand-off | ring opacity 0 -> 1 in 0.25 s on the new tile; the old ring leaves in 0.1 s; one active tile at a time except in the recap |
| tile-expand | `#xp` starts on T1's rect and tweens left/top/width/height to XP, `power3.inOut` 0.6 s (1.5 to 2.1 s); the content fades in at 1.62 s (0.22 s) INSIDE the clipped xp so it is cut by the growing rect, not floating over neighbours |
| reply cascade | 3 replies at 2.3 / 2.95 / 3.6 s, each rise 24 px + 16 px slide, 0.4 s; the thread line draws down (scaleY, 1.5 s); counter text "1/2/3 trả lời" is three stacked spans swapped by visibility, each with a 1.12 -> 1 pop (0.3 s) |
| tile-collapse | content fades 5.28 s (0.12 s), rect shrinks 5.4 to 5.85 s (0.45 s), grid content comes back at 5.6 s while the xp background fades out (0.25 s) |
| reaction burst | 3 chips pulse 1.12 (0.2 s yoyo) staggered 0.1 s; count 4 -> 5 by swapping two spans with a 1.4 -> 1 pop; 6 seeded peach dots fly 50-80 px, `expo.out` 0.55 s |
| flow draw | 4 connectors draw 0.5 s staggered 0.12 s; nodes pulse 1.06; 3 packets (0.18 s per segment, `none`) travel the paths from 8.2 s |
| recap | rings come back on T1 (9.0 s) and T2 (9.45 s), strip chips light at 9.0 / 9.45 / 9.9 s with a 1.08 pop; the three rings then breathe 1.012 and the whole grid drifts 6 px up during the last 2 s |

Dimming the inactive tiles to 60% (profile) was NOT used: it breaks the "nothing below 90% opacity for more than 0.2 s on a held
frame" bar. The ring alone carries focus. If a dim is wanted, dim with a colour (a lighter tile fill), not opacity.

## 8. Scene recipes (beats of the 12 s sample)

| Beat | Time | What happens |
|---|---|---|
| 1 Fill | 0.0-1.5 | finished h1 at frame 0; tiles stagger-fill; footer line and the first step pill arrive; ring on T1 with avatars bouncing |
| 2 Expand demo | 1.5-5.85 | T1 expands to full grid, three replies cascade, counter 1-2-3, collapse back into its slot |
| 3 Reactions + flow | 5.85-8.95 | ring to T2: chips pulse, count 4 -> 5, burst; ring to T3: connectors draw, packets travel |
| 4 Recap | 8.95-12.0 | rings and strip chips light in sequence; held full composition for the last 2.1 s with ring breathing |

Captions (assumed, not exercised): a bento video with voice would put its karaoke pill in the same y 1370-1470 band the step pill uses;
the step pill and a karaoke pill must never be on screen together.

## 9. Sound (ASSUMED, not exercised)

Profile asks for light corporate electronic at 104-122 BPM with soft UI clicks. 12 s = 24 beats at 120 BPM; the expand (1.5 s),
collapse (5.4 s), ring hand-offs (5.95, 7.45, 9.0 s) would sit near downbeats if re-timed to a 0.5 s grid. Not verified.

## 10. Images

None used. Tile illustrations are drawn in CSS and inline SVG. If an agy image is added, it goes inside T1 or T2 as decoration, no
text, no logos, no real people.

## 11. Must not

- No empty tile on screen for more than 0.5 s; tiles that have no content are not shown.
- No emoji; no dimming by opacity; no accent colour as small text (use accent-ink); no mint or peach as text.
- No text under 30 px except the single footer line; no text in a tile that is clipped on a held frame.
- No free-floating card: everything snaps to a slot or to XP.
- No real brand, price or spec in a demo; the "Minh hoạ" label stays on screen to the end.

## 12. Traps seen in real builds (from THIS build, with numbers)

1. **Expanded tile arrives empty.** First render: the expanded tile showed a blank white rect from 1.5 to about 1.95 s and again
   from about 5.4 to 5.9 s (3 sampled frames at 0.1 s steps each, about 0.45 s), right at the 0.5 s limit. Fix: fade the content in
   at 1.62 s (inside the growing rect) and bring the grid content back at 5.6 s while the xp background fades out. Result: blank
   time down to about 0.3 s each way.
2. **Content of the expanded tile ghosting over the neighbours.** The "Kênh gọn hơn" chip (absolute at x 520, y 706 inside a 434 px
   wide tile) showed on top of the Minh hoạ chip and the integrations tile while the rect was still growing (frames at 1.8-1.9 s).
   Fix: `overflow:hidden` on `#xp` with `data-layout-allow-overflow`, and set the xp ring inset to 0 so it is not clipped.
3. **Strip chips overlapping.** At 32 px bold with 24 px side padding, "Luồng" is about 130 px, "Biểu cảm" about 175 px and "Tích hợp"
   about 160 px wide. First positions (28 / 170 / 354) made the first two overlap by about 30 px. Fixed pitch: 28 / 190 / 395 and a
   270 px "Minh hoạ" chip at 590. Always position chips from measured widths in the browser, not by guess.
4. **Overlapping avatars flagged as occluded text.** `hyperframes inspect` gave 2 errors (text_occluded L under M, M under H) for a
   stack with 38 px pitch on 60 px circles. `data-layout-allow-overlap` did not clear text_occluded; a 66 px pitch did.
5. **Inspector sees the covered grid.** While `#xp` covers the grid, inspect reported 11 errors and 13 warnings (content_overlap,
   text_occluded for tiles under it). Setting `#grid` to `visibility:hidden` at 2.02 s (xp covers it) and back at 5.4 s removed
   them except samples taken at exactly 2.0 s (the boundary): the last run still lists 1 error + 7 warnings at t=2 s only. The
   rendered frames show nothing wrong there; hide the grid a hair earlier (1.95 s) if a clean inspect is required, at the cost of a
   32 px sliver of the right tile popping out of view.
6. **Dim to 60% vs the 90% opacity bar.** The profile's "others dim to 60%" would hold below 90% opacity for seconds; ring only.
7. **Counters.** The reply counter is three spans swapped at 2.4 / 3.05 / 3.7 s and the count 4 -> 5 at 6.75 s: no digit is ever
   held mid-count (acceptance: no counter held mid-count). Do not tween a number through intermediate values.
8. **Tooling.** `frame_check.py` needs numpy and Pillow, which were not installed and could not be installed in this run; the
   check was done with ffmpeg contact sheets read by eye (6x4 sheet at 2 fps, plus 10 fps strips around 1.5 and 5.2 s). Install
   the two modules before the real run so the BLANK and TOPHEAVY flags are machine-checked.
9. **Frame 0.** Tiles start at opacity 0 with the headline already finished; at 0.1 s two tiles are partly filled (the grid is
   empty for about 0.3 s). A clean-colour start with headline only would be the alternative; the fill is under the 0.5 s limit.
