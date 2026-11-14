# Style: playful-game-system (9:16 Vietnamese demo edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build on topic shape t130 (family board game night, new releases for the holidays, Jev fit 0.74): short, friendly "pick one of N" lists with 3 items, each carrying 2-3 small plain facts (players, minutes, a star rating), and a joyful call to action. Good for family products, seasonal picks, kids and youth content, simple step or ladder lists. Not good for dense numbers, charts, specs, bad news, loss, enforcement or any dark story: the toy-like motion makes them feel wrong. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12 s sample (`samples/sample-t130.mp4`), 1080x1920, 30 fps. **Voice, caption, word-timing, music and SFX rules were NOT exercised** (no voice-over, no captions, no sound). Sections 8 and 9 only restate the profile and are marked ASSUMED. The build used only generic "Minh hoạ" content, no images (agy not used), no real brand, product or number.

**Example videos show the visual recipe, not the niche.** The sample is about a generic board-game night; copy how it is built, not what it says.

Look in one sentence: a white stage, chunky ink-outlined rounded shapes with a hard bottom edge (toy buttons), red as the hero colour, blue / yellow / green as one-per-element pops, and everything pops in, hops, squashes and springs back. Energy 4 (profile), but no flash, no shake, no gradient.

## 1. Tokens

```css
--bg:#ffffff;  --ink:#1a1a1a;  --paper:#f3f3f3;
--red:#e8402a;       /* hero fills, big shapes     */
--red-ink:#c42a14;   /* red as TEXT or a chip fill with white text */
--blue:#00a7e1; --yellow:#ffd400; --green:#3ec13e;   /* fills only, one per element */
--mute-ink:#5c5c5c;  /* footer line (replaces profile mute #8a8a8a) */
/* bottom edges (toy-button depth, 8-10 px offset, no blur) */
--red-edge:#b8301e; --blue-edge:#0084b3; --yellow-edge:#d6b000; --green-edge:#2f9a2f;
```

Contrast (WCAG formula, calculated by hand in this build; the helper script was blocked by the sandbox, so numbers are 2-decimal approximations):

| Pair | Ratio | Use |
|---|---|---|
| ink on white | 17.4 | all body text |
| ink on paper #f3f3f3 | about 15.7 | card text |
| white on red #e8402a | 4.04 | ONLY text >= 56 px bold (the end-card word); fails 4.5 for small text |
| white on red-ink #c42a14 | 5.69 | the "Chọn tối nay" chip (32 px bold) |
| red #e8402a as text on white | 4.04 | fails for small text: use red-ink for coloured words (headline "cả nhà" at 112 px) |
| mute #8a8a8a on white | 3.45 | FAILS: profile token, never as text; use #5c5c5c (6.69) |
| ink on yellow | 12.2 | "Minh hoạ" chip |
| ink on blue | 6.3 | ok |
| ink on green | 7.4 | ok |
| white on blue / white on green | 2.76 / 2.36 | never text; white only as an icon glyph with a 4 px ink outline |

Rules: white stage, no gradients, no shadows with blur. Red is the hero; blue, yellow, green appear as one colour per element (one per character, one per card icon). Every shape carries a 4-6 px ink outline (profile says outline for highlights; in this build the outline on every shape read as one family and kept the white stage from looking empty).

## 2. Fonts (local only)

| Role | Profile asks | Used | Vietnamese check |
|---|---|---|---|
| Headlines, card titles, chips | Rubik 800 | `SegUIVar.ttf` weight 700 (the file's maximum; 800 does not exist) | all 36 test letters present (checked by rendering: "Đêm", "cả nhà", "Chơi thôi!", "Xây tháp khối", "Đua ô vuông", "Cả nhà cùng chọn một trò" showed every tone mark in snapshots) |
| Body, meta | Rubik 500 | `SegUIVar.ttf` 500-600 | same |
| Captions | Be Vietnam Pro 700 | not used (no captions in this demo) | n/a |
| Never | | `segoepr.ttf` (lacks Vietnamese letters) | do not use |

Neither Rubik nor Be Vietnam Pro is installed, so the chunky rounded Rubik feel is approximated by Segoe UI Variable 700 with `letter-spacing:-0.02em`. It reads clean but less rounded than the profile intends; the roundness is carried by the shapes instead. Declare `font-display: block`, `font-weight: 300 700`. Line-height >= 1.1 so tone marks (Ệ, ố, ẫ) are not clipped.

### Type scale (1080 x 1920, px; as built)

| Token | Size / line | Notes |
|---|---|---|
| hero headline (scene A) | 112 / 1.1 | 2 lines max; line 1 "Đêm board game" is 14 characters and fits 1000 px at 112 (at 128 it wrapped and overlapped the next block) |
| end-card word | 156 / 1.1 | white on the red star, 2 lines |
| section header | 76 / 1.15 | 2 lines |
| card title | 56 / 1.15 | one line, <= 620 px wide |
| sub line, end sub | 56 / 1.2 | ink |
| card meta | 36 / 1.2 | "2–4 người · 25 phút" |
| chip "Minh hoạ" | 36 / 1.2 | top, persistent |
| pick chip | 32 / 48 | white on red-ink |
| footer | 30 / 1.2 | the only line at 30 px; ink-grey #5c5c5c |

Nothing below 30 px.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170   top platform UI: empty
y 196  -260   "Minh hoạ" chip (persistent, centred)
y 270  -440   section header (scene B)   | y 330 -575 hero headline (scene A)
y 470  -1340  scene B: 3 cards, 270 px high, 30 px gap (470 / 770 / 1070)
y 280  -1060  scene C: 780 px star burst, y 1085 sub line, y 1205 -1397 character row
y 1440 -1476  footer line (label)
y 1480 -1920  bottom platform UI: empty
x 96   -984   card column, 888 px
```

Centred compositions, one idea per scene. Cards are absolute children of one layer, so the numbers are frame coordinates. Keep the footer clear of the character shadows (shadow bottoms reach y 1424).

## 4. Layers, back to front

`#root` white stage -> confetti dots (14, seeded, margins only: x < 64 or x > 950, never behind text) -> scene sections `#sA`, `#sB`, `#sC` (one visible at a time, toggled with `visibility`) -> finger and ripple (scene B only) -> persistent chip and footer on top. No flash, shake, grain or gradient layer.

## 5. Components

- **Toy card**: paper #f3f3f3, radius 28, 4 px ink outline, `box-shadow: 0 8px 0 ink` (hard bottom edge). Inside: icon tile 184 px (radius 28, 4 px outline, 8 px colour edge), title, meta, 5 stars.
- **Icon tile glyphs** drawn in CSS only: "?" 120 px white; three stacked white bars; 2x2 squares (two white, two yellow). No logos, no existing game imagery.
- **Star**: SVG 60 px, 1.6/24 ink stroke; filled yellow, empty white. Row of 5 at 70 px pitch.
- **Character**: 190 px body, circle or rounded square (radius 40), 6 px ink outline, 10 px colour edge, two 26 px dot eyes, a smile arc; floor shadow in paper grey. One colour each: red, blue, yellow, green.
- **Chip**: pill, 4 px ink outline, 6 px ink bottom edge ("Minh hoạ" in yellow); pick chip in red-ink with white text.
- **Finger**: 84 px solid ink disc with a 6 px white ring and a 4 px ink halo; **ripple** 120 px blue ring.
- **Star burst** (end card): 12-point polygon, radius 96 / 74 in a 200 unit viewbox, red, 2.4 ink stroke.

## 6. Motion language

Energy 4 with the profile's constraints: no flash, no shake. Beat 130 BPM = 0.4615 s.

| Verb | Recipe (as built) |
|---|---|
| pop-in | scale 0 -> 1, `back.out(2)`, 0.40-0.42 s; words of the headline stagger 0.09 s eased (`power1.in`) |
| pop-swap out | scale -> 0, `back.in(1.8)`, 0.30 s, stagger 0.01-0.04 s; the incoming scene starts on the frame the last element is at 0 |
| hop | per beat: body y 0 -> -24 `sine.out` (0.23 s), back `sine.in` (0.23 s), then squash scaleX 1.15 / scaleY 0.85 for 0.07 s and `elastic.out(1,0.5)` 0.2 s; transform-origin 50% 100%; each character offset 0.04 s |
| tap | finger travels 0.75 s with x `power2.out` and y `power2.inOut` (an arc); shrinks to 0.85 for 0.1 s; target card moves y +8 and its shadow goes to 0 (press) in 0.1 s, then springs back `elastic.out(1,0.5)` 0.5 s; ripple scale 0.5 -> 1.6 over 0.4 s |
| star fill | each star scale 1 -> 1.35 (0.14 s `power2.out`) -> 1 (0.2 s `back.out(2)`), 0.09 s apart, 0.2 s between cards; empty stars sit at scale 1 once the row is in |
| selection | the tapped card scales to 1.04 (`back.out(2)`, 0.4 s) and a chip pops in its corner |
| micro-motion | confetti drift (sine yoyo, 2.8 s, 3 repeats), star burst turn -> +8 degrees (1.4 s, one yoyo), end word bob -6 px (0.5 s, 4 repeats), chosen card -4 px breathe; all finite and ending before 12 s |

Never `ease` strings without quotes (`"none"`). Camera locked-off (no bouncy zoom was needed in a 12 s demo).

## 7. Scene recipes (S = scene start; every tween start clamped to >= 0)

Timeline of the built sample: 12.0 s, 3 beats.

### R1 Cover / hook (S 0.0 - 3.55)
Chip pops 0.05; headline words pop 0.0-0.8 (white stage never empty: first word is visible at 0.1 s); sub line 0.65; four characters pop 0.45 / 0.55 / 0.65 / 0.75 and hop on beats from 1.15 (five hops each, last landing before 3.3). Pop-swap out 3.2-3.55.

### R2 Pick-one list (S 3.55 - 8.45)
Header pops 3.55. Three cards pop 3.75 / 3.86 / 3.97 (0.40 s each, so all are in by 4.4). Stars fill 4.35 - 5.7 (card k starts 4.35 + 0.2k, 0.09 s per star). Finger enters 5.5, taps card 2 at 6.25, chip "Chọn tối nay" pops 6.4, finger leaves 7.1-7.55. Hold with micro-motion to 8.1. Pop-swap out 8.1-8.45. This is the style's signature scene: every selection has a visible press and spring.

### R3 End card (S 8.45 - 12.0)
Red star burst pops with a -40 degree spin 8.45 (0.55 s), "Chơi thôi!" 8.75, sub line 9.05, four characters pop 9.2-9.5 and hop from 9.95. The last 1.5 s (10.5 - 12.0) shows the full composition (star, word, sub line, characters, chip, footer).

Transitions used: pop-swap (A to B, B to C). Star iris and colour wipe from the profile were not used; the end star burst plays the star role as a pop, not a clip-path iris (no clip-path was needed, which kept the renderer budget at zero).

## 8. Captions

NOT exercised in this build (no voice, no captions). ASSUMED from the profile: white pill, 4 px ink outline, radius 24, 42 px Be Vietnam Pro 700 (not installed: use SegUIVar 700), current word in red-ink #c42a14 (5.69 on white), bottom band only, in y 1370-1480 (the footer line must then move or be dropped).

## 9. Sound

NOT exercised. ASSUMED from the profile: chiptune-flavoured pop at 125-135 BPM and original click, boing and chime SFX; hops, taps and star fills in this build were laid on a 130 BPM grid so music can be added later. No existing game sounds.

## 10. Images

None used (agy not called). The style needs none: icons, characters and the star are CSS and SVG. If an image is ever added it must be flat colour, thick outline, no text, no logo, no real person, no existing game character.

## 11. Must not

- No gradients, blur shadows, texture, photo realism or dark palettes.
- No existing game characters, sounds, logos, fonts or the brand look-alikes the aliases name.
- No white text on blue or green; white on red #e8402a only at >= 56 px bold.
- No #8a8a8a text.
- No dense text, charts, specs or more than 3 cards per scene.
- No tap or selection without a press and spring.
- No real product, price or spec in a demo: label "Minh hoạ" on screen (chip plus footer line).
- No story about death, lawsuit, loss, enforcement or a dark mood.

## 12. Traps seen in real builds (this build, measured)

1. **Headline wrap.** At 128 px "Đêm board game" (14 characters) wrapped in a 960 px box and the second line collided with the sub line; `inspect` reported content_overlap. Fix: 112 px in a 1000 px box. Rule: budget about 0.56 em per Vietnamese character in Segoe 700 and size for the longest line.
2. **Header over the first card.** A 2-line 84 px header (193 px) ran into the card at y 440. Fix: 76 px header at y 270 (ends about 445) and cards from y 470; card height cut from 300 to 270 so three cards end at 1340, above the 1440 footer.
3. **Chip over a title.** The "Chọn tối nay" chip sat top right and covered "khối" in "Xây tháp khối" (seen in the snapshot at 7.2 s, `inspect` did not flag it because the chip is a child). Fix: chip at card bottom right (top 188); the finger taps at x 830, y 830, clear of the title.
4. **Text under a character.** The end sub line (y 1182) sat under the character row (y 1236): `inspect` text_occluded error. Fix: star 780 px, sub line y 1085, characters y 1205, footer moved 1410 -> 1440 so shadows do not touch it.
5. **Palette tokens fail for text.** Profile red #e8402a is 4.04:1 on white and profile mute #8a8a8a is 3.45:1; white on blue 2.76, on green 2.36. Added red-ink #c42a14 (5.69) and #5c5c5c (6.69); coloured words use red-ink.
6. **Pop-in frames look empty.** At 3.5 s only the chip and confetti were on screen for about 0.2 s between pop-swap out and the B header; at 8.5 s the star showed with no word for about 0.3 s. Both are under 0.5 s, but a longer gap would break the "no empty panel" rule: start the incoming header on the same frame the last outgoing element reaches 0 and delay only the body.
7. **Transient spacing glitch.** At 0.5 s the headline words were scaling in as inline-blocks, so the spaces collapsed ("Đêmboardgame" in one frame of the contact sheet). It lasts under 0.1 s per word; it would be clean if the words are given `margin: 0 0.12em` instead of text spaces.
8. **Timeline longer than the video.** Yoyo tweens with repeats (confetti 3.0 s x 4 = 12.6 s) pushed the timeline past 12 s. Size repeats to the remaining time (2.8 s x 4 from 0.6 s ends at 11.8 s).
9. **Inspect false positive.** `inspect` warns content_overlap on the pop-swap out frame (3.33 s) where scaled words overlap; this is the transition, not a defect.
10. **Tooling.** `frame_check.py` needs numpy, which was missing, so frame check was done with an ffmpeg contact sheet (2 fps, 24 frames) read by eye; before a real build install numpy or accept that the BLANK listing is not available. Inline interpreters and `sed -i` were blocked by the sandbox in this session; use the Edit tool for source changes.
11. **File size.** 12 s, 1080x1920 rendered at `standard`: 3.6 MB. Flat colour compresses very well; no size risk for a full 60 s video.
