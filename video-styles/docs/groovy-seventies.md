# Style: Groovy Seventies (9:16 Vietnamese news edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY, observed in this build).** Warm nostalgia and place stories: a diner or restaurant reopening, a retro anniversary, a community craft class, a food or culture feature with 3-6 plain facts (a year, an address, a short menu, hours, one quote). Not for earnings, enforcement, specs, bad news, or dense numbers. Tier 2 never widens tier 1.

**Reading order.** Sections 1-12 are the recipe, measured on one real build (video `paris-coffee-shop-mo-lai`, 56.5 s, 1080x1920, 30 fps, 10.8 MB). Section 13 lists the traps of that build. Where they disagree, section 13 wins.

**Status.** Written 2026-11-13 from the first build of this style. No earlier owner document. Source of values: `styles/profiles/groovy-seventies.yaml`; anything the profile does not give is marked **ASSUMED**. Energy 3: soft overshoot, no shake, no flash.

Character: mustard, orange, rust and brown wavy stripes, a fat slanted serif with a 3-step offset shadow, cream rounded cards with a brown rim and a hard offset shadow, a slowly turning sunburst, riso-grain paper. Motion is loose and lazy: type wobbles, discs roll in, stripes slide across the cut.

## 1. Tokens (contrast measured with the WCAG formula, python)

```css
--bg:#f5e6c8;     /* paper; ink on it 11.75:1 */
--cream:#fbf1dc;  /* cards, caption pill; ink on it 12.91:1 */
--ink:#3b2416;    /* all body text */
--accent:#d35f1f; /* FILLS, rings, stripes only: 3.45:1 on cream (fails small text) */
--rust:#a8400c;   /* ASSUMED text-safe accent: 5.50:1 on cream, 5.01 on bg; current caption word, quote credit */
--mustard:#e3a52b;/* fills; ink on mustard 6.68:1 */
--brown:#7a4a2a;  /* rims, shadows, footer text: 6.00:1 on bg; cream on brown 6.59:1 */
--avo-dk:#4f5a1f; /* ASSUMED: sign panel; cream on it 6.65:1 */
--avocado:#7d8a3c;/* fill only (3.36:1 on cream: never text) */
--avo-lt:#c9d27a; --peach:#f0c9a0; /* ASSUMED tints for chips; ink on them 8.95 / 9.36 */
```
Rules: text only in `--ink`, `--rust`, `--brown` (on bg), or cream on brown / avocado-dark. `--accent`, `--avocado` and mustard-on-avocado (3.44) are never text. Stripes always run mustard, orange, rust, brown. Cool colour: one muted teal (#5b7f8c) allowed only inside small illustrations (stools). Validate flagged one warning at 1.19:1 for the kicker pill: a false positive (the tool read the paper PNG, not the brown pill; real cream on brown = 6.59).

## 2. Fonts (all local)

| File | Role | Vietnamese check |
|---|---|---|
| `cambriai.ttf` (italic serif) | display: headline with 3 px stroke + 3-step offset shadow, big numerals, quote | glyphs rendered correctly in snapshots (all tone marks on "Thay đổi", "Ông", "lịch sử"); fontTools was not installed, so the check is visual, not by cmap |
| `SegUIVar.ttf` weight 300-700 | all reading text, chips, captions (700) | rendered correctly (ẫ, ợ, ữ, ế seen in frames) |
| `CascadiaMono.ttf` | kicker labels, source footer | rendered correctly |
| `segoepr.ttf` | NOT used (lacks Vietnamese letters) | - |

The profile asks for Shrikhand, DM Serif Display, Nunito, Be Vietnam Pro: none installed. Substitute: cambriai italic for the fat display serif (it is lighter than Shrikhand, so the stroke + shadow carry the weight), SegUIVar 700 for Nunito/Be Vietnam Pro. Display font has no bold: never set `font-weight` on it.

## 3. Type scale, safe areas, grid (1080 x 1920)

- Side margin 96, content width 888. Top wave strip y 20-240, bottom strip y 1690-1910 (decor, may clip: `data-layout-allow-overflow`).
- Kicker pill y 238, 58 px high. Headline y 310-620. Body zone y 250-1290 (lowest card edge always 1290, so lowest content edge >= 1250 at every hold). Source footer y 1318 (30 px mono, the only footer line). Caption pill top 1400, max 936 wide. y 1500-1690 empty (platform UI).
- Sizes: headline 168-176 px (line 2: 104-128 px), big numeral 196-200 px, sub-head 60-92 px, row text 46-50 px, chip text 42-46 px, caption 44 px, footer 30 px. Nothing under 30 px.
- Radius 36-40 on cards and chips, 999 on pills. Rim 5 px brown, offset shadow `0 8px 0 brown`.

## 4. Layers (back to front)

1. `#root` paper PNG (noise 7, blurred 0.7 px, baked with ffmpeg; heavy noise 14 made the render 84 MB).
2. `#sun`: 18 wedge paths at 10% opacity, rotates 24 deg over the whole video (linear).
3. `#wtop` / `#wbot`: four wavy strokes, drift 360 px per 2.35 s in opposite directions (one wave period, seamless loop, finite repeat 23), plus a 6 px bob.
4. Scene sections (one visible at a time).
5. `#xt`: four stripe bands for the cut.
6. `#footer`, `#cap` (z 50).

## 5. Components

Arch frame (image in an arch with 3 rings: mustard, orange, brown); round badge/disc (numeral + unit); sign panel (avocado-dark, cream double rim); ribbon pill (mustard); owner chips (3 tints); timeline (wavy 3-stroke ribbon drawn by dashoffset with 3 year discs); menu card with 8 rows (dot + text); cream card with offset shadow; quote card with a 300 px stripe band on top (text never sits on the stripe image: see trap 1); caption pill.

## 6. Motion language

- Entrances: `back.out(1.3)` rise 50-80 px; discs roll in from the side with 200-240 deg rotation (`back.out(1.1)`); text slides with skewX -14 and `expo.out`; ribbons draw with dashoffset. Overshoot stays under 1.1.
- Holds: `cam` push 1.00 to 1.03 (linear), headline wobble +-1.3 deg with `sine.inOut` yoyo, period 1.154 s (about 104 BPM), finite repeats sized to the hold; arch image Ken Burns 1.00 to 1.12; sunburst turn; wave drift.
- Spoken-word accents: `bump` (scale 1.07, 0.5 s) at the estimated onset minus 0.1 s; menu rows turn rust while spoken.
- Counters: `ease:"none"`, 0.55-0.6 s, plus a `tl.call` that writes the final text 0.02 s after the end.

## 7. Transitions: stripe-sweep (the signature)

Four bands (mustard, orange, rust, brown, 480 px high, rounded right end) slide in from the left over 0.22 s `power2.in`, staggered 0.04 s, ending at S-0.12; they leave to the right over 0.22 s `power2.out` from S. The incoming scene starts building at S-0.3 so that when the bands open, content is already on screen (trap 2). Cover time under the bands: about 0.12 s full cover. Scene sections swap visibility at S, under the bands.

## 8. Scene recipes (S = scene start; times from `voice/timeline.json`)

| Scene | Content | Notes |
|---|---|---|
| R1 hook (s1, 0-7.7 s) | kicker, 2-line headline, arch with diner illustration, "TỪ NĂM 1926" badge | everything final from frame 0, no counter, badge spins 0.8 s |
| R2 address + people (s2) | sign panel, ribbon, disc "55 năm", owner text, 3 name chips | count 0-55 in 0.6 s |
| R3 timeline (s3) | 3-stroke ribbon, discs 1926 / 1974 / 2021, 3 labels, griddle card | ribbon draws 0.8 s |
| R4 menu (s4) | cream card, 4 + 4 rows, pie illustration in a round 3-ring frame | rows slide in 0.07 s stagger |
| R5 bar + hours (s5) | disc "96 năm", two half tiles (7, 7 sáng đến 3 chiều), counter-with-stools card | count 0-96 in 0.6 s |
| R6 quote (s6) | stripe band top, big quote mark, Vietnamese quote, credit, English original in mono | holds to the last frame (full composition) |

## 9. Captions

Cream pill, 5 px brown border, offset shadow, 44 px SegUIVar 700 ink, current word `--rust`. Chunks of 3-8 spoken words split at punctuation; display text uses digits ("1926", "55 năm"), spoken text uses words; a build check warns if chunk word counts differ from the script (none did). Highlight by `tl.set` at estimated word onsets. Word times are ESTIMATED (proportional to letters), so real onsets drift up to ~0.3 s.

## 10. Sound

No music in this build (no tool). Voice only (VieNeu Hai Dang, 55.5 s, 4 words/s on 220 words). Style intent: funk/soul 96-116 BPM with cowbell and wah stabs; wobble period 1.154 s matches 104 BPM so music can be added later.

## 11. Images (agy)

Three images, about 1 min each, 768x1376: diner interior with stools, pie and coffee, wavy sunburst. Prompt recipe that worked: "1970s groovy riso print illustration of ..., flat ink shapes, mustard rust avocado brown cream palette, soft paper grain, no text". agy added a teal for the stools (outside the earth palette); kept as a small accent, cropped inside the arch. The stripe image is the most useful asset: use it only as a band, never behind text.

## 12. Must not

Cold blues or neon; text over the stripe image; `--accent` or avocado as text; a mask or typing effect on text; dimming tiles; hard cuts without a stripe sweep; segoepr; a call to like or subscribe; any number not on an opened page.

## 13. Traps seen in real builds (this build, measured)

1. **Quote unreadable over the stripe image.** First snapshot of scene 6: 888 x 1028 card filled with the stripe image, ink text crossing orange/brown bands (credit line in rust on rust, effectively 1:1). Fix: stripes only in a 300 px band (y 262-562), text on cream. After the fix ink on cream 12.91:1.
2. **Empty scene after the stripe sweep.** Frames at 20.0 s and 31.2 s: bands opened at S and content began rising at S+0.02, giving 5-6 frames (0.2 s) of paper only. Fix: start all scene tweens at S-0.3 (content hidden by `visibility` until S and covered by bands). Frame check afterwards: 0 BLANK frames in 113 samples; contact sheet at 15 fps shows content at the first open frame.
3. **File size.** Grain noise 14 gave a 84.5 MB silent render; noise 7 + 0.7 px blur gave 46 MB; final mux with CRF 27 preset slow: 10.8 MB (limit 25 MB). The `motion_tools.py mux` default (CRF 20) gave 50.2 MB: re-encode with CRF 27 instead.
4. **Counter caught mid-count.** The sheet frame at 8.0 s showed "20" (the count was still running). Counts take 0.6 s from S+0.3-0.3; the sample at S+0.3 s is inside the window, which is allowed (<= 0.8 s), and every hold frame shows 55 / 96.
5. **Validator contrast false positive** on the kicker pill (1.19:1 reported, real 6.59:1). Do not "fix" by lightening; verify by hand.
6. **No fontTools** on the machine, so the diacritics check is by rendering, not by glyph map.
7. **Wave seam.** A drift of exactly one wave period (360 px = 2 x 180) loops invisibly; a 300 px drift jumped. Keep drift = n x period.
8. **GSAP is inlined from CDN by the renderer** (3.14.2) and works offline in render; no local copy is needed.
9. **Story freshness.** No Fort Worth diner reopening was published in the last 48 h; the newest verifiable story shape in opened pages is from 2022. See manifest notes.
