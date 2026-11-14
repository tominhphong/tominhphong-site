# Style: Music editorial (9:16 Vietnamese year-in-review edition)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build:** "year in review" and "most-X" ranking stories with one huge headline number plus a top-3 list: most streamed songs and artists in a region (Jev 0.81 for shape t127), annual stats of a music, video or game app, culture campaigns, personalised-stats recaps. Not for dense multi-series data, serious/enforcement news, or stories with many equal numbers. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample (`sample-t127.mp4`, 1080x1920, 30 fps, 2.3 MB). **Voice-over, captions, word timing and music were NOT exercised** (demo build): sections 7 and 8 are ASSUMED from the profile only. Content in the sample is generic and labelled "Minh hoạ".

Source of values: `styles/profiles/music-editorial.yaml` (energy 4). Anything not in the profile is **ASSUMED** or **MEASURED** (this build).

Character: three full-frame saturated colour blocks, one per beat; huge tight uppercase type; a giant stat; chunky bars. Blocks change by a wipe, never a dissolve.

## 1. Tokens

```css
--ink:#141416;    /* text on pink, yellow, green; chips */
--white:#ffffff;  /* text on blue and on ink */
--pink:#ff4fa3; --blue:#4238b5; --yellow:#f7e14b; --green:#2ad19a;   /* blocks and marks */
```
Contrast, hand-computed with the WCAG formula (the script runs were blocked in this build, so numbers are from manual arithmetic, +-0.05) and `hyperframes validate` ("5 text elements pass WCAG AA"):

| Pair | Ratio | Use |
|---|---|---|
| ink on pink | 6.05 | body, sub-headline on pink |
| ink on yellow | 13.9 | all text on the yellow block |
| white on blue | 8.5 | all text on the blue block |
| yellow on blue | 6.4 | the giant stat |
| white on ink | 18.4 | chip, rank 3 bar |
| white on pink | 3.04 | LARGE text only (>= 240 px); never small |
| blue on pink | 2.80 | FAILS even large; do not use (first draft did, see traps) |

Rules: pink / green are marks and giant type only, never small text. One saturated block + at most 2 other colours per scene (profile: max 3): beat 3 = yellow + pink + blue/ink.

## 2. Fonts

| Role | Profile asks | Used | Vietnamese check (36 letters + đ) |
|---|---|---|---|
| Headlines, stat, labels | Archivo 900 / 700 | `SegUIVar.ttf` weight 700 (Archivo not installed; 900 does not exist) | all present, rendered correctly in snapshots (Ạ, Ỉ, Ệ, Ợ, Ẫ ok) |
| Mono | none | `CascadiaMono.ttf` was tried for the number and dropped | present |
| Never | | `segoepr.ttf` | lacks Vietnamese letters |

Declare `font-display: block`; `font-weight: 300 700` for the variable file. Uppercase via `text-transform` keeps tone marks: set line-height >= 0.9 only with >= 245 px of line pitch (see traps).

## 3. Type scale (1080 x 1920 px, MEASURED in this build)

| Token | Size / line | Notes |
|---|---|---|
| `.giant` hook words | 240 / 0.9, -0.04em, uppercase | 3 lines, pitch 240 px (g1 top 320, g2 585, g3 825) |
| stat number | 380, -0.04em, tabular-nums | "12,4" fills 640 px |
| stat unit | 200 | "tỉ" |
| ranking title row | 150 (rank), 52 (name), 38 (artist) | |
| label | 44-56 / 1.15-1.2 | sub-headline 46, stat caption 56 |
| chip "MINH HOẠ" | 30 / 52 px pill | the only text at 30 px, plus footer 30 |

## 4. Safe areas and grid

```
y 0    - 170  top platform UI: empty
y 190  - 242  "MINH HOẠ" chip (persistent, left 80)
y 320  - 1040 hook stack / y 380 - 1130 stat card / y 300 - 1400 ranking
y 1100 - 1220 sub-headline (beat 1);  y 1240 - 1480 cover-art tiles (beat 1) / wave (beat 2)
y 1480 - 1920 bottom platform UI: empty
x 80 - 1000   one column, 920 px
```

## 5. Layers, back to front
Scene sections (each its own full-frame block colour) -> `#wipe` full-frame colour block (z 40) -> chip (z 50). No flash, no shake layer in the demo.

## 6. Components
- **Hook stack**: three uppercase words, ink / white / ink, pink block.
- **Cover-art tile**: 240 px flat square with one flat geometric shape (circle, rect+circle, triangle). No real covers, no logos, no shadow.
- **Story card**: label (44 px, +0.1em) -> giant number -> unit -> caption -> waveform bars (16 bars of 48 px, 10 px pitch, alternating pink / green, seeded heights).
- **Ranking bar**: radius 24, 210 px tall, widths 920 / 760 / 600 (the width IS the data); rank numeral 150 px, name 52 px, artist 38 px. Colours pink / blue / ink with ink / white / white text.

## 7. Motion language (MEASURED) and recipes
Energy 4 but no music/shake in the demo. Per beat:
1. **Hook 0-3.7 s (pink).** Words rise 160 px with expo.out, 0.55 s, eased stagger (0.14 s), starting 0.1 s; sub-headline 0.75 s; tiles pop with back.out(1.6) from 0.95 s; three tile scale hits 1 -> 1.07 at 1.6 / 2.1 / 2.6 s (stand-ins for kicks); words drift 14 px through the hold.
2. **Wipe 1 (3.3-3.99 s).** Blue block power3.inOut 0.32 s in, old scene hidden at 3.62 when fully covered, block exits left 3.66-3.98.
3. **Stat card 3.66-7.7 s (blue).** Number counts 0 -> 12,4 over 1.3 s (power2.out) from 3.9 s, finished at 5.2 s and held 2.4 s; unit slides in at 4.9 s; caption 5.3 s; bars grow 5.0 s then pulse (yoyo x3) until 7.2.
4. **Wipe 2 (7.3-7.99 s).** Yellow block, same recipe.
5. **Ranking 7.66-12 s (yellow).** Headline rises 7.8 s; bars scaleX 0 -> 1 (expo.out 0.55 s) at 8.15 / 8.29 / 8.43 s; text fades in 0.2 s after each; footer 9.0 s. From 9.0 s the composition is complete; it holds 3 s with a 10 px drift and a 4% push-in on the headline.

Cadence: a visible change every 3.7-4.3 s. Counters finish at least 2 s before the next wipe.

## 8. Captions and voice
**Not exercised (demo build).** Profile says: solid black box radius 8, 42 px, white, current word accent. The ranking and stat card keep y 1100-1480 free of the stat so a caption pill can sit at y 1370-1470 ASSUMED. In beat 1 the tiles occupy that band: move them up or drop them when captions are on.

## 9. Sound
Not exercised. Profile: pop/dance 110-130 BPM, vinyl scratch-lite on reveals, whoosh on wipes. At 120 BPM a beat is 0.5 s: the wipes (3.3, 7.3 s) and tile hits are spaced to fit bars of 8 beats (3.7 s is 7.4 beats; if music is added, retime wipes to 4.0 / 8.0 s).

## 10. Images
None used (optional agy images skipped). Cover art is drawn as flat SVG. If agy images are added: duotone pre-baked PNG, no text, no logos, no real people or real covers.

## 11. Must not
- Real artist, song, label or app names or real figures; the demo uses "Bài hát A", "Nghệ sĩ A", "12,4 tỉ" and the on-screen label "Minh hoạ" (chip on every beat plus footer).
- Dissolves, thin type, muted palettes. Text below 30 px except one footer line.
- Blue text on pink. White text below 200 px on pink.
- A new block colour without a wipe; a wipe longer than 0.7 s.

## 12. Traps seen in real builds (this build, 2026-11-14)
1. **Tone-mark collision at line-height 0.9.** With 260 px words on a 236 px pitch, the dot under Ạ (NHẠC) landed on the Ă of TEXAS (read as "TEXAS" with a stray dot). Fix: 240 px words with a 240-260 px pitch (g2 moved 566 -> 585). Check every Vietnamese hook stack at 100% zoom.
2. **Contrast of the signature duotone.** Blue on pink, the profile's example pair, is 2.80:1 even at 240 px; I switched to white (3.04:1, large text only). `validate` still said "5 pass" because it samples text elements, so measure the giant words yourself.
3. **Sub-headline wrapped to 2 lines** and hit the tile row (first snapshot: overlap at y 1180). Vietnamese runs long; size boxes for 2 lines (110 px) and leave a 20 px gap.
4. **Mono comma gap.** `CascadiaMono` made "12,4" read "12 , 4" at 400 px (fixed-width comma cell). Use the proportional face with `tabular-nums`.
5. **`inspect` flags tight stacks** (content_overlap on line-height .9 boxes). The overlap is by design: mark with `data-layout-allow-overlap`; also give the number box 50 px of clearance below its label.
6. **Wipe frames are empty panels** (pure blue / yellow). They last 0.32 s each (well under 0.5 s), but keep the incoming block's content starting >= 0.1 s after the block lands.
7. **Frame-check script blocked:** `frame_check.py` could not run (python not approved in this session), so the check was done with `ffmpeg fps=2.5,tile=10x3` and by eye; automated numbers are missing (see selfcheck.md).
8. **Bottom band.** Tiles at y 1240-1480 touch the 1480 safe edge; no spare room for captions in beat 1 (section 8).
9. **Missing Archivo 900.** Segoe 700 is lighter than the profile's headline weight; the blocks of colour carry the loudness instead.
