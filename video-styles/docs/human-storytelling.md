# Style: human-storytelling (9:16 Vietnamese warm-story edition)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build.** Warm, person-and-place stories where trust and belonging matter more than numbers: a family business spotlight, a community or neighbourhood story, a testimonial, a host or maker profile. The topic shape t040 (family taqueria in San Antonio, Jev 0.77) worked well: three beats, no number needed. Not for specs, dense data, enforcement, bad news or hype. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample `samples/sample-t040.mp4`. There was no owner document before. **Voice-over, word timing, captions and music were NOT exercised** (demo build): nothing in this file about them is tested; section 8 and 9 are profile values only, marked ASSUMED. Values come from `styles/profiles/human-storytelling.yaml`; anything the profile does not give is marked ASSUMED.

**What it is.** Energy 2. Rounded white-bordered cards float over off-white paper; a coral accent marks one thing per scene; motion breathes (slow push, light parallax); beats change by a card shuffle, never a cut.

## 1. Tokens

```css
--bg:#fffaf6;          /* paper (flat, no grain)             ink on it 15.35:1 */
--ink:#222222;         /* headlines, chips, labels           15.35 on bg, 14.7 on white (hand-computed WCAG) */
--accent:#ef6f58;      /* MARKS ONLY: underline, route dots, heart. 2.86:1 on bg: never text */
--accent-ink:#c8402a;  /* ASSUMED text-safe coral: 4.80 on bg, 4.97 on white, white on it 4.97. Not used as text in this build */
--blush:#ffe3dd;       /* chip fill, blob; ink on blush 13.09. accent-ink on blush only 4.09: FAILS, never put it there */
--sand:#f2e7dc;        /* blob, map ground, chip border */
--mute:#717171;        /* host line, footer: 4.71 on bg, 4.89 on white */
--card:#ffffff;
```
Method: WCAG formula worked by hand (the sandbox blocked python and node), cross-checked by `hyperframes validate`: "30 text elements pass WCAG AA". Teal #1a9e7e appears only inside illustrations (leaf, bunting), never as text.

Colour rule: coral on ONE focal element per beat: B1 underline, B2 underline, B3 route dots + heart pin together. Everything else is ink, sand, blush, mute.
Material: card radius 24, 10 px white border, shadow `0 20px 40px rgba(34,34,34,.12)`. Chips are pills (radius 28-30). No gradient, glow, glass, grain.

## 2. Fonts (2 local files used; profile fonts Nunito, Fraunces, Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Check |
|---|---|---|---|
| Headline, chips, labels, footer | Nunito 800 | `SegUIVar.ttf`, weight 700 max, -0.01em | Vietnamese rendered correctly in frames: Một quán của cả gia đình Công thức bà Bữa sáng khu phố Bếp Mở từ sáng sớm |
| Quote and host line | Fraunces italic 500 | `cambriai.ttf` (Cambria Italic, 400 only) | rendered correctly: “Bột ngô nhào bằng tay, nướng mỗi sáng.” Ba thế hệ cùng đứng bếp |
| Never | | `segoepr.ttf` | lacks Vietnamese letters |

The fontTools 36-letter glyph test could not run in this build (python blocked); the check was visual on every string actually used (selfcheck.md). Re-run the glyph test before using a new string with ặ ẫ ỷ. Declare faces with `font-display: block`; Segoe `font-weight: 300 700`. Segoe is a plain grotesque, not rounded like Nunito: warmth comes from colour, cards and the italic serif.

### Type scale (1080 x 1920 px, measured in this build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.h1` | Segoe 700 | 88 / 1.12 | 2 lines max, sentence case, <= 17 chars per line (840 px box) |
| `.q` quote | Cambria italic | 56 / 1.25 | 2 lines, curly quotes |
| `.host` | Cambria italic | 38 / 1.2 | `--mute` |
| `.sc` sub chip | Segoe 600 | 32 in a 60 px pill | ink on blush |
| header chip, map label | Segoe 700 | 30 in a 56 / 52 px pill | |
| footer | Segoe 500 | 26 / 1.2 | the ONE line under 30 px; "Minh hoạ: ..." |

Line mask wrappers: `padding .1em 0 .14em; margin -.1em 0 -.14em` so tone marks (Ộ, ữ, ố) are not clipped by `overflow:hidden`; carry `data-layout-allow-overflow`.

## 3. Safe areas and grid (1080 x 1920)

Margins 120 px left and right (content box 840). Vertical bands, all measured from this build:
- y 92-148 header: kicker chip left (place, with ink pin), "Minh hoạ" chip right.
- y 210-~450 headline (2 lines of 88 px).
- y 560-1460 card stack (840 x 900), asymmetric left-aligned text over a centred card.
- y 1510-1770 sub area: chips (B1, B3) or quote + host (B2).
- y 1826 footer line.
No caption band is reserved (no voice in this build); if captions are added, they belong in y 1560-1780 and the sub area must be dropped (ASSUMED).

## 4. Layers, back to front
1. Paper `#fffaf6` + two flat blobs (blush 620 px bottom-left, sand 520 px top-right), drift -20 px over 12 s.
2. Card stack (map C, tortillas B, storefront A; z 1-3), drift -14 px.
3. Text (header chips, headline, sub area, footer).
4. Foreground dots (4 sand circles 16-24 px at the far edges), drift -30..-34 px: the fastest layer, kept off all text.

## 5. Components
- **Photo card**: 840 x 900, radius 24, 10 px white border, soft shadow; inside an 820 x 880 picture. This build had no photos (see 10): flat SVG illustrations (storefront with awning and bunting, comal with tortillas, map).
- **Place chip** (kicker): white pill, 2 px sand border, ink pin dot.
- **Label chip** "Minh hoạ": blush pill, always on screen.
- **Underline**: coral hand-drawn path under one key word, drawn with `strokeDashoffset`.
- **Route**: 26 coral dots (r 8) placed along a bezier with `getPointAtLength` at build time, popped one by one; start pin ink ring, end pin coral heart.
- **Map label**: white pill with shadow, ink 30 px 700.

## 6. Motion language (energy 2: no shake, flash, bounce larger than back.out 1.4)
- Entrances: headline lines rise out of a mask (`expo.out`, 0.65 s, stagger 0.1); chips and sub text rise 30 px + fade (`power3.out` 0.6 s); underline draws 0.6-0.7 s `power2.inOut`.
- Exits: lines go up out of the mask 0.32 s `power2.in`, sub area fades up 0.28 s.
- **Card shuffle** (signature, used twice): top card x 0 -> 1120 (or -1120), rotation 6 deg (or -6), 0.75 s `power2.inOut`; the card behind goes rotation 3.5 -> 0, scale .96 -> 1 over the same 0.75 s. Cards are stacked from frame 0 so a corner of the next card peeks out.
- Holds: slow push inside the card (`scale 1 -> 1.05`, `sine.inOut`, 4 s), steam drift 18 px, paper and card parallax. Nothing is frozen.
- Heart pop: scale 0 -> 1.22 -> 1 (0.3 s + 0.3 s), then one 1.1 pulse with finite repeat.
- Depth parallax ratio actually used: background 20 px : cards 14 px : foreground 30-34 px over 12 s (the profile's 20 / 60 px was too strong with a 900 px card; ASSUMED lower is safer).

## 7. Scene recipes (this build: 12.0 s, 3 beats, no voice)

| Beat | Time | Content | Moves |
|---|---|---|---|
| B1 hook | 0 - 4.1 | place chip, "Một quán taqueria / của cả gia đình", storefront card, chips "Bếp gia đình" "Mở từ sáng sớm" | finished at frame 0; chips rise at 0.15 / 0.3; underline draws 0.5-1.2; card push |
| T1 shuffle | 3.85 - 4.7 | storefront card exits right with tilt; tortilla card settles | text out 3.85, card 3.95-4.7 |
| B2 quote | 4.3 - 8.0 | "Công thức / của bà", tortilla card, italic quote, host line | lines in 4.3; quote 4.75; host 5.2; underline 5.1; steam drift |
| T2 shuffle | 7.85 - 8.7 | tortilla card exits left (-6 deg), map rises | |
| B3 place | 8.3 - 12.0 | "Bữa sáng của / cả khu phố", map card, route, heart, chips "Từ bếp nhỏ" "đến cả khu phố" | pin 8.85, dots 9.1-10.2, heart 10.2, label 10.35, chips 9.65; full composition from 10.7 |

Rules: a beat is 3.5-4 s; one person/place/hand-made detail per beat; one coral focal group per beat; the last beat settles by 10.7 s so the final 1.3 s is a complete frame.

## 8. Captions
NOT exercised (no voice). Profile: white pill rgba(255,255,255,.92), radius 22, 42 px Be Vietnam Pro 600 ink, current word coral. Not installed font and coral-on-white fails 4.5:1 (2.86 / 3.1): if built, current word should use `--accent-ink` (4.97 on white) or a bold ink underline (ASSUMED).

## 9. Sound
NOT exercised (silent demo). Profile: acoustic guitar, light percussion, warm piano, very few SFX (page flick on shuffle, pin tick).

## 10. Images
Intended: warm documentary photos in cards, no text, no real faces. In this build the image tool (`motion_tools.py image`, a python script) was blocked by the sandbox, so NO photo was generated; cards hold flat SVG illustrations. This is a known imperfection: the style's soul is real photography ("photos carry the colour"). Illustration cards read friendly but flatter. Prompt to use when available: "Warm documentary photograph, golden morning light, off-white and coral tones, shallow depth of field, no people, no text".

## 11. Must not
- No emoji, no hard cut, flash, shake, glitch, neon, glass, gradient text, dark background.
- No coral text; no `--accent-ink` on blush (4.09).
- No more than one coral focal group per beat.
- No real business name, price or spec in a demo: label "Minh hoạ" in the header AND in the footer.
- No `segoepr.ttf`.
- No mask or typing reveal on a held frame; frame 0 shows a finished headline.

## 12. Traps seen in real builds (this build, 2026-11-14)

1. **Dotted underline broke into pieces.** `vector-effect: non-scaling-stroke` with `pathLength=1` and `strokeDasharray=1` made the line a row of dashes (frame 2.0 s). Fix: remove the vector-effect and give each underline its own viewBox sized like the word (460 x 22 for "cả gia đình", 135 x 22 for "bà"); the stroke then drew cleanly.
2. **Underline path drawn in a 100 x 20 viewBox, stretched to a 460 px word**: horizontal strokes got ~4x thicker than vertical. Size the viewBox in px.
3. **Heart and its label collided.** The "Khu phố" chip sat directly under the heart pin, touching the last route dots. Moved to left of the heart (x 420, y 226 inside the card) after the first snapshot.
4. **Headline gap during a shuffle.** Outgoing lines leave at 3.85-4.17 and incoming start at 4.3: the headline zone is empty for about 0.4 s (frame sheet, 4.0 s). Under the 0.5 s limit; do not lengthen it.
5. **The map card is empty until 8.85 s** (route and pin start after the headline). It shows the map ground itself, so it is not an empty panel, but it is the weakest 0.5 s; start the pin at 8.6 if the clip is cut shorter.
6. **Tools blocked.** `python3` and `node` (even `-e`) were refused, so no fontTools glyph test, no `frame_check.py`, no agy images. Frame check was done with an ffmpeg tile sheet (2 fps, 6 x 4) and `hyperframes inspect` (0 layout issues in 9 samples). Check what the sandbox allows before planning on python.
7. **Hand-computed contrast.** Coral #ef6f58 is 2.86:1 on paper: pretty but unreadable as text; the text-safe twin #c8402a is 4.80 and still fails on blush (4.09).
8. **Chip row looks light under a big card.** At 32 px chips under a 900 px card feel small; the beat is held by the card, not the chips. Prefer one 40-48 px line.
9. **Mask clipping in transition frames.** At 4.4 s "Công thức" is cut by its own line mask while rising; accepted because it is a 0.65 s move, not a held frame.

## 13. Measured numbers from this build
File 2.08 MB, 1080 x 1920, 30 fps, 360 frames, 12.00 s, h264, silent. `hyperframes lint`: 0 errors 0 warnings. `validate`: no console errors, 30 text elements pass WCAG AA. `inspect`: 0 layout issues across 9 samples. Render 11.6 s with `-q standard`.
