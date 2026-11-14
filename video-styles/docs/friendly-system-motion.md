# Style: friendly-system-motion (9:16 Vietnamese everyday-service edition)

## 0. Read this first: niche, status, how this document was made

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build.** Useful, positive everyday services told in plain words with one habit or one benefit per beat: a habit or savings app, a sign-up, a free programme, a new store, a utility or transit change. It carried a topic with a mascot, a streak and a small bar chart without strain. Not for bad news, enforcement, accidents or dense multi-number financial data (the card layout fits 1 counter, 2 chips, 5 bars at most). Tier 2 never widens tier 1.

**Status: DEMO-ONLY build, 2026-11-14.** One silent 12.0 s sample (`samples/sample-t108.mp4`, 1080x1920, 30 fps, 1.0 MB) on topic shape t108 (a habit-tracking app adds streaks and a mascot to help people save money, Jev fit 0.85). **Voice-over, word timing, music and karaoke captions were NOT exercised**; nothing in this document about them is tested. Sections 7 and 8 therefore only give assumed rules, marked ASSUMED. Everything on screen is generic and labelled "Minh hoạ" (no real company, product, price or spec).

Profile: `skill/references/styles/profiles/friendly-system-motion.yaml` (family brand-inspired, energy 3, light mode). Marks: **MEASURED** = seen or computed in this build. **ASSUMED** = invented here, not tested. **SUBST** = a named font is not installed, a local one replaces it. **DEVIATION** = knowingly differs from the profile.

DEVIATION 1: profile type is Outfit / Roboto Mono / Be Vietnam Pro (none installed); SUBST below.
DEVIATION 2: profile layout is "headline top, illustration centre" for 16:9; in 1080x1920 it stacks: headline y 230, one card or illustration below, nothing under y 1600.
DEVIATION 3: profile sizes (72 headline, 32 body, 22 mono) are too small for a phone; this build uses 88-96 / 40 / 30.

## 1. Tokens

```css
:root{
 --bg:#ffffff; --ink:#22252b; --mute:#62666e; --surface:#f2f2f5; --line:#d5d8e0;
 --accent:#5566e8;    --accent-dk:#3a49c9;  --accent-soft:#e6e9fc;
 --red:#ef5b6e;       --red-dk:#c23550;     --red-soft:#fde3e7;
 --yel:#f79a2a;       --yel-dk:#9a5200;     --yel-soft:#fdebd3;
 --grn:#1fa88f;       --grn-dk:#127a66;     --grn-soft:#d9f2ed;
 --sh1:0 2px 6px rgba(34,37,43,.15); --sh2:0 8px 24px rgba(34,37,43,.15);
}
```
Contrast (WCAG formula, **computed by hand** because no Python or Node of my own could run in this build; the HyperFrames `validate` step independently reported "15 text elements pass WCAG AA"):

| Text token | on white | on --surface #f2f2f5 | on its own soft chip |
|---|---|---|---|
| --ink #22252b | 15.4 | 13.7 | - |
| --mute #62666e | 5.8 | 5.2 | - |
| --accent #5566e8 | 4.7 | **4.2 (fails)** | - |
| --accent-dk #3a49c9 | 7.1 | 6.3 | 5.9 on --accent-soft |
| --grn-dk #127a66 | 5.3 | - | passes on --grn-soft (validator) |
| --yel-dk #9a5200 | 5.9 | - | passes on --yel-soft (validator) |
| --red-dk #c23550 | 5.4 | - | not used for text in this build |

Rules (MEASURED): `--accent` text only on white and only at headline size (96 px / 88 px); on a grey card or a chip use `--accent-dk`. `--red`, `--yel`, `--grn` are FILLS (dots, bars, rings); their text versions are the `-dk` tokens. Primaries as full backgrounds only in the circle reveal (profile constraint kept). No gradients, no dark mode.

## 2. Fonts

| File | Role | Vietnamese check |
|---|---|---|
| `SegUIVar.ttf` | everything read: headline 600, numbers 700, body 400-500 (SUBST for Outfit / Be Vietnam Pro) | The owner doc style-fluent-productivity records 0 missing glyphs for all Vietnamese capitals and lower case. In this build the glyph test could not be re-run by script; instead the rendered frames were read: every diacritic combination used (ỗ, ế, ệ, ặ, ậ, ờ, ư, ụ, ắ, ố, ồ, ọ) draws correctly, and the currency is written with the letter "đ" (not the sign U+20AB) after `20.000đ` |
| `CascadiaMono.ttf` | the "Minh hoạ" tag and small data labels at 30 px, +0.03em (SUBST for Roboto Mono) | same: "Minh hoạ", "tuần này", "5 ngày" draw correctly |
| `cambriai.ttf` | unused (profile forbids serif display) | - |
| `segoepr.ttf` | NEVER used: lacks Ơ ơ Ư ư and dotted vowels | - |

SegUIVar has no 800 weight; 700 is the heaviest and is enough for the 210 px counter.

### Type scale (1080x1920, MEASURED from this build)
Headline 96 (beat 1) and 88 (later beats), weight 600, -0.01em, line 1.08, ONE key phrase coloured (`--accent` on beat 1, beat 2 and `--grn-dk` on beat 3 text). Hero counter 210/700. Coin glyph "đ" 240/700. Card title 44 (40 in the chart card). Counter unit 52/600. Bubble 46/600. Chip 34/600. Sub line 40/400 `--mute`. Day labels, mono labels, "Minh hoạ" tag, progress caption: 30-32. **Nothing under 30 px, and no footer line was needed.**

## 3. Safe areas and grid (1080x1920)
- Side margin 72, content width 936. y 0-200 platform zone: only the "Minh hoạ" tag (left 72, top 132, 30 px mono, white pill with 2 px `--line` border).
- Headline block y 230-440 (two lines). Card or illustration y 520-1400. Beat 3 mascot row y 560-820, chart card y 940-1580.
- **Lowest content edge at a hold: y 1580 (beat 3), 1400 (beat 2), 1300 (beat 1 coin; the sub line sits at y 1450-1530).** y 1650-1920 stays empty (bottom UI zone). Beat 2's lower third is lighter than beat 3's; it passes the "lower third not empty" rule only because the card runs to y 1400.
- Radius: card 24, chip 999, bar top 16. Card inner padding 48. Streak row: 7 slots on a 120 px pitch, 72 px dots, centres x 180...900, y 790.

## 4. Layers, back to front
1. `#root` white. 2. Beat sections `.sec` (each white, `visibility` toggled by `tl.set`). 3. `#disc` (z 30, the circle-reveal colour disc, 2400 px, scales from 0). 4. `#dots` (z 20, the nine travelling dots, created in JS before the first tween). 5. `#tag` "Minh hoạ" (z 60, always on top, readable on white and on green).
Rule (MEASURED trap): dots that must travel between beats live in ONE layer above the beats, with absolute frame coordinates; they are NOT children of the card, so the card can change shadow without moving the targets.

## 5. Components
- **Dot**: circle, 72 px base, scaled 0.5-1.2 for mixed sizes (36, 40, 44, 48, 56, 64, 72, 80, 88 px in the build), colours cycle accent / red / yellow / green. Landing = squash (scaleY 0.8, scaleX 1.12, 0.1 s) then back (0.15 s).
- **Coin**: 500 px disc `--yel-soft`, 14 px `--yel` border, "đ" in `--ink`; nine dots orbit on its rim at radius 250.
- **Card**: `--surface`, radius 24, `--sh1`, lifts to `--sh2` (shadow only) at focus. Title 44 top-left, 30 px mono tag top-right.
- **Streak slot**: 72 px ring, 4 px `--line`; filled by a landing dot. Day label under it, 30/500 `--mute`.
- **Counter**: seven stacked digit spans, `tl.set` opacity swaps at each landing (a counter that never shows a half-rolled digit). Final 7 reached at 5.07 s.
- **Chip**: 64 px high, soft fill + `-dk` text, 34/600, pop `back.out(1.6)` in rotating primaries.
- **Progress bar**: 24 px, track `--line`, fill `--accent`, `scaleX` 0 to 1 in 0.6 s from origin left (set the start with `gsap.set`, not CSS).
- **Mascot**: a 260 px `--grn` dot with two white eyes, dark pupils, two red cheeks, a smile stroke. It is a plain dot with a face, not a character with limbs. Bubble: `--accent-soft` fill, `--accent-dk` 46/600 text, radius 24, `--sh2`.
- **Bars**: 96 px wide on a 168 px pitch, tops radius 16, one 44 px dot of the same colour rides on each top and squashes when the bar stops.

## 6. Motion language (MEASURED timings from this build)
- Dots idle-bounce (power2.out up 60 px 0.28 s, power2.in down + squash 0.26 s), staggered 0.05 s per dot.
- Gather: power2.inOut 0.75 s, stagger 0.04 s. Coin pop: `back.out(1.6)` 0.45 s.
- Idle hop on the beat: 12 px, 0.15 s up + 0.15 s down, every 0.55 s (about 110 BPM, matching the profile's 100-120).
- Entrances: `power2.out`, y 40 + fade, 0.35 s. Cards and headlines never bounce; only dots, chips, the bubble and the mascot do.
- Camera: locked off. The profile's 1.0 to 1.05 push was left out (not needed at 12 s).
- No flash, no pulse, no gradient, no blur.

### Transitions (both used; every cut is a transition)
- **Dot-morph, beat 1 to 2 (3.7-4.9 s).** The coin collapses (scale to 0, 0.25 s) while headline and sub fade over exactly 0.15 s, then the same nine dots fly 0.5 s to the seven streak slots (two shrink to 0). The next beat's card is already fading in at 3.9 s under them. No frame is empty.
- **Circle reveal, beat 2 to 3 (7.55-8.4 s).** A green disc grows from a point (540, 1000) over 0.55 s (`power2.in`); beat 3 is revealed through `clip-path: circle()` from the same point, starting 0.25 s later. Solid green is on screen for about 0.35 s (measured on a 10 fps strip: 3 to 4 frames); that is the only full-primary frame in the video. Origin of the disc and the clip circle must be the same point (see Traps).

## 7. Scene recipes used (12.0 s, 3 beats; S = beat start)
**B1 Hook, 0-3.9 s: "dots to coin".** Frame 0 already shows the finished headline (no mask, no typing): "Thói quen nhỏ, tiền tiết kiệm lớn" with "tiền tiết kiệm" in `--accent`. Nine mixed dots bounce 0-1.5 s, gather on a ring at 1.5-2.3 s, the coin pops at 2.3 s, the 40 px sub line fades in at 2.7-3.1 s, dots hop on the beat 3.0-4.1 s. Hold from 3.1 s.
**B2 Streak, 3.9-8.4 s: "dots land in a habit row".** Headline "Mỗi ngày bỏ ống, chuỗi ngày dài thêm" (88 px). Card and slots in by 4.3 s; dots land one per 0.13 s from 4.35 s, the big number counts 1 to 7 on the landings (finished 5.07 s); chips pop at 5.5 and 5.7 s; progress bar fills 5.9-6.5 s; hold 6.5-7.5 s.
**B3 Mascot and savings, 8.2-12.0 s: "mascot nudges, dots settle into bars".** Headline "Linh vật nhắc đúng lúc, tiền dành dụm tăng đều". Mascot drops in 8.3 s with a landing squash, bubble "Hôm nay bỏ ống chưa?" pops at 8.9 s, five bars grow 9.35-10.4 s (0.14 s stagger) with a dot riding each top. **From 10.5 s to 12.0 s the full composition is on screen** (mascot, bubble, five bars with their dots, labels); only the mascot's 12 px hop moves.
ASSUMED for a longer video: 4 to 8 beats of the same three recipes (dots-to-icon, dots-land-in-a-UI-row, dots-settle-into-bars), a search-bar typing beat (profile signature, NOT built here), and a closing circle reveal.

## 8. Captions and sound
**Not exercised (demo build; silent, no voice, no karaoke).** ASSUMED from the profile only: white pill radius 24, 40 px 600 `--ink`, current word `--accent-dk`, placed in the empty zone y 1620-1760, never over the card. No SFX or music was made; the profile calls for soft bloops on dot landings and a 100-120 BPM marimba/ukulele bed. The idle hops in this build are already on a 0.55 s grid so a 110 BPM bed would line up.

## 9. Images
No agy image was used (0 of 2 allowed): the mascot, coin and bars are drawn in HTML/SVG and read cleaner than a generated picture. ASSUMED if an image is needed: flat vector, white background, rounded shapes, the four primaries, no text, no logo, no real person.

## 10. Must not
- No product logo, no real brand, price or spec; mark illustrative numbers "Minh hoạ" (the tag stays on screen the whole video).
- No dark mode, no gradient, no serif display, no segoepr.ttf.
- No primary as a full background except the circle-reveal disc.
- No four-dot assistant mark; the dots are of mixed sizes, never a row of four equal ones.
- No bad news, enforcement or accident content (tier 2 says so).
- No text under 30 px; no text under `--ink`/`-dk` tokens on a grey card.

## 11. Traps seen in real builds (from THIS build, measured)
1. **The disc and the reveal had different origins.** First render: the green disc grew at (540, 1540) while the clip circle opened at (540, 1000); the strip showed a green ball low on the card and the next beat appearing somewhere else. Fix: disc `top:-200px` for a 2400 px disc so its centre is (540, 1000), the same point as `clip-path: circle(... at 540px 1000px)`. Compute both from one point.
2. **Accent text on a grey card fails.** `--accent` #5566e8 is 4.7:1 on white but only 4.2:1 on `--surface`. Counter and bubble text use `--accent-dk` (6.3 on surface).
3. **`transform` in CSS plus a GSAP scale lint error.** `#prog` with CSS `transform:scaleX(0)` failed lint (`gsap_css_transform_conflict`). Remove it from CSS and use `gsap.set` before the tween.
4. **Travelling dots inside a transforming card miss their targets.** The streak dots live in a frame-level layer with absolute coordinates, and the card only animates shadow after 5.6 s.
5. **Counter mid-count.** A tweened number would be caught mid-roll; stacked digit spans swapped by `tl.set` at each landing give 1,2,...7 with the last change at 5.07 s and nothing moving after.
6. **Bubble wrapped badly.** "Hôm nay bỏ ống chưa nào?" at 46 px in a 636 px bubble broke as "chưa / nào?"; shortened to "Hôm nay bỏ ống chưa?" (one line).
7. **Frame 0 sparse.** The first 1.5 s shows a finished headline and scattered dots on white only (about 20 % ink coverage). Acceptable as a hook because the dots are moving from frame 0, but a voice-over build should put the first spoken noun there.
8. **Beat 2 holds a lighter lower third** than beats 1 and 3: card ends y 1400, nothing below. The 24 px progress bar was added to pull the content edge down to y 1364.
9. **Tooling.** The delivered `frame_check.py` needs numpy, which was not installed here, so the official frame check could not run; an ffmpeg contact sheet (4 fps, 48 frames) and a 10 fps strip of the transition were read by eye instead. Run `frame_check.py` where numpy exists before reuse.
10. **Short transition tail.** The full-green frame lasts about 0.35 s. Starting the clip at 7.7 s instead of 7.8 s would cut it by 0.1 s; not changed.

## 12. Check before delivery (carried from the other style docs)
Lint 0 errors, validate no console errors and AA pass, inspect 0 layout issues, snapshot read frame by frame, `frame_check.py` where numpy exists, probe 1080x1920 and 10-15 s, file under 15 MB.
