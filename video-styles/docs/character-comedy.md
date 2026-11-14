# Style: character-comedy (9:16 mascot-comedy demo edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build.** Gamified or habit-forming consumer products told with a joke: streaks, savings, learning, fitness and reminder apps; product-feature promos where one character can react to a UI change; short social cuts. Jev fit for the shape "habit-tracking app adds streaks and a mascot to help people save money" was 0.83. Not for serious, sad, enforcement, legal or dense-number stories; not for dark palettes. Tier 2 never widens tier 1.

**Status.** Written 2026-11-13 from ONE demo build: a single 12.0 s silent sample on topic shape t108 (`samples/sample-t108.mp4`). Voice-over, word timing, karaoke captions, music and SFX were NOT exercised (demo build): sections 8 and 9 are the profile's values, marked UNTESTED. Everything marked MEASURED comes from this build; ASSUMED = invented here; SUBST = a named font is not installed.

**Reading order.** Sections 1-7 are the design as built. Section 13 lists the traps found in this build and overrides anything above it contradicts.

Profile: `skill/references/styles/profiles/character-comedy.yaml` (energy 5, light mode). Format 1080 x 1920, 30 fps, silent, 3 beats in 12 s, text plus motion only. On-screen label "Minh hoạ" on every frame (generic illustrative content, no real brand, price or spec).

## 1. Tokens

```css
:root{
  --bg:#ffffff;        /* profile bg */
  --ink:#3a3a40;       /* profile ink       11.3:1 on white, 4.8:1 on --accent (text on green buttons) */
  --mute:#6b6a66;      /* ASSUMED: profile mute #b2b0ab is 2.2:1 and fails text; this one is 5.4:1 on white */
  --accent:#45c21f;    /* hero green: FILLS only; white text on it is 2.3:1 and FAILS */
  --accent-edge:#2f9a12; /* ASSUMED: 0 8px 0 bottom edge of chunky buttons */
  --accent-dk:#2f7d12; /* ASSUMED: green TEXT on white 5.2:1, on --soft 4.6:1 */
  --leaf:#a6dd2a;      /* belly, transition panel 2, leaf */
  --sky:#3a8ff0;       /* confetti only */
  --flame:#ff7f24;     /* fill only: 2.5:1 on white, ink on it 4.47 (fails 4.5) */
  --flame-dk:#c2410c;  /* ASSUMED: orange TEXT (streak number, punchline) 5.2:1 on white */
  --gold:#f4b93a;      /* rewards; ink text on it 6.4:1 */
  --red:#f0506a;       /* cheeks only (3.4:1 as text: never text) */
  --line:#e6e4df; --soft:#e8f7de; --skysoft:#e4f0fd;  /* borders, pill fills, background blobs */
}
```
Ratios computed by hand with the WCAG formula (python was not allowed to run in this session, so the numbers are hand-calculated and rounded to 0.1). Rules: text colours only from `--ink --mute --accent-dk --flame-dk`; `--accent --flame --gold --red --sky` are fills. Never put white text on the green button: use ink (4.8:1). Flat fills, no gradients, no outlines on the mascot.

## 2. Fonts (checked on the real script: all Vietnamese capitals, lower case, Đ đ, Ơ ơ Ư ư, tone marks)

| File | Role |
|---|---|
| `SegUIVar.ttf` | EVERYTHING read. SUBST for Nunito 900 and Be Vietnam Pro 800 (neither installed). Weight axis tops out at 700, so "chunky" headlines use weight 700 plus `-webkit-text-stroke: 2-5px currentColor` to thicken the rounded look |
| `CascadiaMono.ttf`, `cambriai.ttf` | not used |
| `segoepr.ttf` | NOT used: lacks Vietnamese letters (92 missing in the sibling docs) |

Diacritics check (selfcheck.md lists every string): rendered snapshots were read by eye; every tone mark and horn (ư, ơ, ữ, ỗ, ề, ạ, ệ) showed correctly. The font-glyph script (`fontTools`) could not be run in this session (no python permission), so the check was visual only.

### Type scale (1080 x 1920, MEASURED = values in the build)
| Use | px / weight |
|---|---|
| Punchline number-line ("Lần thứ 12.") | 170 / 700 + 4 px stroke, `--flame-dk` |
| Closing headline | 140 / 700 + 2 px stroke, 2 lines |
| Setup line | 96 / 700 |
| Streak numeral | 270 / 700 + 5 px stroke |
| Button label | 52 / 700 uppercase +0.04em |
| Card title, heo label, % | 44 / 40 / 40 |
| "+10 xu" reward chip | 56 |
| Sub line | 46 / 600 |
| Day labels (T2..CN) | 32 (smallest in the build, above the 30 px floor) |
| "Minh hoạ" tag | 34 |

## 3. Safe areas and grid
- Side margin 72 (tag) and 90 (card, button: width 900). y 0-200: only the "Minh hoạ" tag (top 110, height 60). Nothing at y > 1780.
- Beat 1: text y 250-580; mascot 640 x 704 at left 220, top 860 (about 37% of the frame height, 59% of the width).
- Beat 2: card y 250-1020 (900 x 770, radius 48), button y 1070-1220, mascot scaled 0.69 bottom-right (center x about 780, y about 1530), reward chip bottom-left y 1420.
- Beat 3: headline y 230-540, sub y 610, mascot scale 1.1 (about 704 px wide) y about 760-1540, streak chip y 1640-1760.

## 4. Layers, back to front
1. `#bg`: three flat pastel blobs (`--soft`, `--skysoft`), slow drift 30-60 px over the beat (ratio 0.3).
2. `#fg` confetti: 16 flat dots 14-27 px (`--accent --gold --sky --leaf --flame`), seeded, bursting in at 9.3 s and drifting. Kept BEHIND text (see traps).
3. Beat UI (`#b1`, `#b2`, `#b3`): text and card.
4. `#mas` mascot (above UI so it can overlap), one persistent element moved between beats.
5. `#panel` (green) and `#panel2` (leaf) transition slams, `#tag` "Minh hoạ" on top.

## 5. Components
- **Mascot (original, egg-shaped blob, no beak, no wings, no owl):** body `--accent`, belly `--leaf` ellipse, two white eyes r 62, orange feet, leaf sprout on top. Three expression groups toggled with `autoAlpha` on a beat: `ex-dead` (heavy lids = the body colour half-circles with a 8 px ink lid line, flat mouth), `ex-happy` (open mouth, raised brows, cheeks), `ex-plead` (big pupils r 44 with two highlights, tilted brows, wobbly mouth). Squash group `.m-squash` with origin at the feet.
- **Chunky button:** radius 38, fill `--accent`, `0 8px 0 --accent-edge`; press = y +5 and shadow 3 px in 0.07 s, then `back.out(3)` spring back in 0.3 s.
- **Streak card:** white, 4 px `--line` border, `0 10px 0 --line` bottom edge. Flame icon (flame + gold core), numeral mask with two stacked numerals (6 and 7) for the roll, 7 day dots (88 px) with 32 px labels, "Heo đất" progress bar 44 px high.
- **Reward chip:** gold pill `+10 xu`, ink text.
- **Streak pill (closing):** `--soft` pill with 4 px `--line` border, flame icon and "7 ngày liền" at 54 px.

## 6. Motion language (energy 5)
- Entrances: pop with `back.out(1.6-2.4)`; text slams (scale 1.6 to 1 in 0.22 s `expo.out`, rotation -2 to -3 degrees resolving with `elastic.out(1,0.4)`); squash and stretch 1.18/0.82 on landing.
- **Snap zoom:** `#mas` scale 1 to 1.5 in 0.2 s `power4.out` (transform-origin 50% 43%, the face), creep to 1.56 over 0.9 s so the hold is never frozen, back to 1 in 0.3 s.
- **Beat of silence before the punchline:** beat 1 from 1.7 to 2.6 s has no new element; only the creep and one blink (2 frames, scaleY 0.1). Beat 3 from 7.95 to 9.1 s: only the pleading pupil wobble.
- Counter: numeral 6 rolls up out (0.12 s) while 7 rolls in `back.out(1.8)` (0.28 s); flame scale 1 to 1.3 (0.14 s) to 1 `elastic.out(1,0.4)`; bar 62% to 84% `back.out(1.6)` 0.55 s; the % text swaps at 5.8 s.
- Coins: 14 gold dots burst from the button, seeded angle (spread 2.6 rad) and distance 260-580 px, x `expo.out`, y `power2.inOut` plus gravity, fade 6.35 s.
- Held-frame micro motion: flame scale 1.04 yoyo, reward chip bob 8 px, mascot rotation 1.5 degrees, pupil wobble, confetti drift, background blob drift.
- Transitions (ONE language, a colour panel slam, direction changes): beat 1 to 2 green panel from the left (enter 0.2 s `expo.out`, swap at 3.72 s, exit 0.3 s `expo.out` to the right); beat 2 to 3 leaf panel from the bottom (7.5 s enter, swap 7.72 s, exit upward). The mascot jumps to its next slot while the panel covers the frame. Measured full-cover time per transition: about 0.3 s.
- Timings: the whole sample is 12.0 s: beat 1 (0-3.72), beat 2 (3.72-7.72), beat 3 (7.72-12). All reveals finish by 10.5 s; the last 1.5 s show a full composition.

## 7. Scene recipes
- **R1 Hook, deadpan gag (0-3.72 s):** setup line rises at 0.3 s; mascot pops in with deadpan face; snap zoom at 1.5 s; silence; punchline slams at 2.6 s ("Lần thứ 12.", flame-dark) while the mascot zooms back and its pupils glance up toward the text (x -8, y -10); panel slam at 3.5 s.
- **R2 UI demo, reward (3.72-7.72 s):** card pops at 3.85 s; flame, numeral 6, label, 6 green dots (stagger 0.07 s), heo bar, button; mascot rises from below with a pleading face; the button hint-pulses (scale 1.04) at 5.1 s, is pressed at 5.55 s; at 5.6 s: counter 6 to 7, flame flare, 7th dot turns gold, bar fills, coins burst, "+10 xu" pops, mascot swaps to the happy face and jumps (y -110, `bounce.out` back). Everything settles by 6.4 s and holds 1.1 s.
- **R3 Plea and payoff (7.72-12 s):** mascot pops oversize (1.35 to 1.1) with the pleading face; one full beat of silence; headline slams in two lines at 9.1 and 9.3 s with a mascot hop; sub line at 9.75 s; streak pill at 10.0 s; confetti burst; micro motion to the end.

## 8. Captions (UNTESTED: not exercised in this demo build)
Profile value only: white pill with 3 px `#e6e4df` border and 0 4 0 bottom edge, 44 px, ink text, current word green. Remember the contrast trap: green text on white must be `--accent-dk`, not `--accent`. Not measured here.

## 9. Sound (UNTESTED: not exercised in this demo build)
Profile value only: bouncy marimba 125-135 BPM, game dings, record-scratch before punchlines. This build is silent; the beats of silence (R1, R3) are timed for a record-scratch or ding to land on the punchline frame.

## 10. Images (agy)
No generated image was used: the mascot, card, flame and coins are inline SVG and CSS, which kept every edge crisp and every expression switchable. Generated art is not needed for this style.

## 11. Must not
- No owl, bird or any look-alike character; the mascot stays an egg-shaped blob.
- No white text on `--accent`, `--flame` or `--gold` fills below large size (2.3:1, 2.5:1 and 1.8:1).
- No gradients, outlines or dark mode; red never as text.
- No `segoepr.ttf` (no Vietnamese letters).
- No real company, price or spec; keep "Minh hoạ" on screen for demo content.
- No long hold without the character on screen; no scene without a reaction face.

## 13. Traps seen in real builds (this build, 2026-11-13)
1. **Profile mute and accent fail as text.** `#b2b0ab` on white is 2.2:1 and white on `#45c21f` is 2.3:1. Fix: `--mute #6b6a66` (5.4:1), ink on the green button (4.8:1), `--accent-dk #2f7d12` (5.2:1) for green text.
2. **Flame orange fails twice.** `#ff7f24` on white is 2.5:1 (fails even large text) and ink on it is 4.47:1 (just under 4.5). Fix: `--flame-dk #c2410c` (5.2:1) for the streak numeral and the punchline.
3. **Nunito 900 is not installed.** SegUIVar caps at 700; 2-5 px `-webkit-text-stroke: currentColor` gives the chunky feel without a layout shift (text width grows about 2 px per stroke px; leave 40 px slack).
4. **Panel slam ate a full second.** First version: enter 0.28 s then exit `expo.in` 0.32 s left the screen solid green for about 0.6 s per transition (a blank-frame risk, over the 0.5 s limit). Fix: enter 0.2 s `expo.out`, swap at the middle, exit `expo.out` 0.3 s: measured about 0.3 s full cover (4-5 frames at 15 fps).
5. **Mascot jump on swap.** Setting the mascot slot at the swap and then a `fromTo` that starts later from a different value shows a visible jump after the panel clears. Fix: `set` the slot with the SAME start values the first reveal tween uses (y 560 offscreen-low, scale 0.69; scale 1.35).
6. **Confetti over text.** `#fg` dots layered above the headline hid "7 ngày liền" (inspect `text_occluded` at 11.33 s). Fix: put `#fg` directly after the background, behind UI and mascot.
7. **Numeral roll reads as occlusion.** The hidden numeral 7 waiting below its mask counted as text under a dot (inspect error). Fix: keep it at `autoAlpha 0` until it rolls in, and mark the mask `data-layout-allow-overflow data-layout-allow-overlap`.
8. **Blink squashes the mouth.** Scaling the whole `.m-eyes` group (which also holds the brows and mouth) to 0.1 for the blink flattens the mouth for 2 frames; it reads as a comic gulp, so it was kept, but a pure eye blink needs its own group.
9. **Snap zoom headroom.** At scale 1.5 to 1.56 the 640 px mascot reaches 960-1000 px wide, which still fits 1080. Text sits above it (bottom of the punchline y 580 versus mascot top about 700 at the zoom), so no overlap. A larger mascot or a 2.2 zoom (the profile value) would hit the frame edge: 2.2 was NOT used.
10. **The shipped frame checker needs numpy.** `frame_check.py` stopped at `import numpy` on this Mac; the check was done with ffmpeg 2 fps and 12-15 fps contact sheets read by eye (see selfcheck.md). Install numpy to run the original.
11. **Layout checker noise.** `inspect` flagged the transform-slam text (scale 1.6) as canvas overflow at one sample; mark the beat wrapper `data-layout-allow-overflow`. Lint, validate and inspect report 0 issues after the fixes.
