# Style: premium-ui-demo (detail, written from the demo build of 2026-11-14)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build.** App and feature walkthroughs where ONE interface is the hero and the story is "press this, this happens": wellness and habit apps, onboarding, a new feature, a product-update reveal, sign-up flows. It worked well on topic shape t128 (wellness app launches a guided breathing programme, Jev fit 0.76). Not for: dense numbers (use saas-bento), breaking news, enforcement or sad stories, anything without a screen to show. Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: one silent 12.0 s sample (1080 x 1920, 30 fps, 2.4 MB), text plus motion, no voice-over, no word timing, no captions, no music. **Voice, caption, sound and pronunciation rules were NOT exercised**; sections 7 and 8 below are therefore profile-derived and marked UNTESTED. No images were generated (the style needs none: the interface is built from CSS).

Profile: `skill/references/styles/profiles/premium-ui-demo.yaml` (family brand-inspired, energy 2, light mode, bpm 90-110 not used). Marks: **ASSUMED** = profile gives no value and this document chose one. **DEVIATION** = knowingly differs from the profile. **SUBST** = a local font replaces a named one.
- SUBST: profile says Inter and Be Vietnam Pro; both are absent. `SegUIVar.ttf` replaces them for everything.
- DEVIATION 1: the profile lays out "text left third, UI right two-thirds" for 16:9. In 1080 x 1920 everything stacks: headline on top, device panel below.
- DEVIATION 2: headline 76 px (profile 64) and body 34-38 px (profile 30) because 9:16 is read on a phone.
- DEVIATION 3: zoom-into-control scale 1.55 over 0.9 s (profile 1.6), because 1.6 pushed the panel past the frame on both sides.
- The profile's "no live backdrop-filter" holds: the sheet is a 92% white fill.

## 1. Tokens

```css
:root{
  --bg:#f2f1ee;            /* flat background, never a gradient */
  --ink:#1a1b1f;           /* 15.2:1 on bg, 17.2:1 on white */
  --mute:#6f6e69;          /* 5.11:1 on white, 4.52:1 on bg (tight; text >= 34 px only on white) */
  --surface:#ffffff;
  --accent:#3b74f2;        /* FILL / ripple / dots ONLY: white text on it is 4.23:1, FAILS 4.5 */
  --accent-dk:#2f5fd6;     /* ASSUMED: button fill and accent text; white on it 5.63:1, on accent-soft 4.71:1 */
  --accent-soft:#e3ebfd;
  --green:#34c77f;         /* FILL only: status dot, toggle track (no text on it) */
  --green-dk:#1a7a4a;      /* ASSUMED: green dot that sits on grey, 5.35:1 on white */
  --hair:rgba(0,0,0,.08);
}
```
Contrast was computed by hand with the WCAG formula (python was not usable in this session, see trap 9), and `hyperframes validate` confirmed "20 text elements pass WCAG AA". Rules: text colours only from `--ink --mute --accent-dk` and white on `--accent-dk`. `--accent` and `--green` are never text. Never lighten a text token. Orange from the profile was not needed (one accent plus green was enough).

## 2. Fonts (glyph test on the real strings plus all Vietnamese capitals)

| File | Missing glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 (checked on every on-screen string and the capitals Ơ Ư Ê Ô Â Ă Đ; also rendered and read in frames) | EVERYTHING: headlines 600, UI 500, buttons 600 |
| `CascadiaMono.ttf` | 0 | not used in this build (UI demos do not need it) |
| `cambriai.ttf` | 0 | not used |
| `segoepr.ttf` | many (no Vietnamese hooks) | never used |

Letter-spacing -0.025em on headlines and -0.02em on large UI titles (profile value). No 800 weight exists.

## 3. Type scale, safe areas and grid (1080 x 1920)

| Role | Size | Weight |
|---|---|---|
| Headline (2 lines) | 76 px / 1.1 | 600 |
| Sheet title | 56 px | 600 |
| Screen title in panel | 68 px | 600 |
| Button | 44 px | 600 |
| "done" title | 50 px | 600 |
| Breathing label inside disc | 64 px | 600 |
| Rows | 38 px | 500 |
| Sub, trailing values, "Minh hoạ" chip, reminder chip | 32-36 px | 400-500 |

Smallest authored text: 32 px. Nothing under 30 px.

- Side margin 90 for headline; device panel x 110, width 860, radius 44, 1 px hair border, shadow `0 30px 80px rgba(0,0,0,.12)`.
- y 96-152 "Minh hoạ" chip (always visible, from frame 0 to the end). y 200-370 headline. y 392-496 reminder chip (beat 3 only). Panel y 470-1710. y 1710-1920 empty (the lowest content edge on the held end frame is y 1722; the bottom reads a little bare but safe for platform UI).
- Inside the panel: padding 56, button 748 x 120 radius 60 at panel y 1064; sheet top at panel y 300, height 940, radius 44 44 0 0.

## 4. Layers, back to front

1. `#root` flat `--bg` (nothing else: the panel casts all the depth).
2. Headlines `.hl` (z 5), one visible per beat, line masks.
3. `#drift` (z 10, perspective 2000): camera wrapper. Scales 1.00 to 1.025 linearly over the whole 12 s, origin (540, 1090): the "never frozen" micro-motion.
4. `#dev`: zoom wrapper (own scale, origin on the tapped control, so the zoom and the drift do not fight).
5. `.panel` (clips its content): screens `#sA`, `#sB`, `#scrim`, `#done`, `#sheet`.
6. `#note` reminder chip (z 20, outside the drift, overlaps the panel top edge on purpose).
7. `#chip` "Minh hoạ" (z 30), `#dot` touch dot and `#rip2` ripple (z 40).
Maximum two panels on stage: the device panel plus the small reminder chip.

## 5. Components

- **Device panel**: white, radius 44, hair border, soft shadow. Hero of every beat.
- **Primary button**: `--accent-dk` fill, white 44 px text, 748 x 120, radius 60.
- **Concentric art** (`#art`): four CSS circles (600 / 440 / 280 / 130 px) in `#eef3fe #dbe5fc #bccffa #2f5fd6`. Replaces a generated image; breathes 1.00 to 1.06 in the hold.
- **Progress ring**: SVG r 280, stroke 16, track `#e8e7e3`, arc `--accent-dk` via `stroke-dashoffset` 1759.3 to 0, rotated -90.
- **Breathing disc**: 380 px `--accent-soft` circle scaling 0.6 to 1 to 0.7; its label swaps "Hít vào" to "Thở ra" with `tl.set`.
- **Sheet**: `rgba(255,255,255,.92)`, hair top border, shadow `0 -20px 60px rgba(0,0,0,.10)`, grab handle 80 x 8, rows 112 px high, toggle 112 x 64 (track `#d6d5d0` to `#34c77f`, knob 56 px white with shadow).
- **Scrim**: `rgba(26,27,31,.12)` over the previous screen while the sheet is up.
- **Touch dot**: 40 px `rgba(26,27,31,.2)`, no cursor arrow. Ripple ring: 6 px border (`--accent` on the button, `--green` on the toggle), scale 0 to 1.6 and fade.
- **Reminder chip**: white, radius 30, 540 x 104, green dot, 32 px text, shadow `0 20px 50px rgba(0,0,0,.14)`.
- All icons and art are CSS or SVG. If agy is used at all it makes only a soft mood wash; it cannot draw the interface.

## 6. Motion language (as built)

| Move | Value |
|---|---|
| Panel tilt-in | `y 90 to 0`, `rotationY 8 to 0`, `back.out(1.2)` 0.75 s, opacity 0 to 1 in 0.25 s (separate tween, no overlap warning) |
| Headline | line masks, `yPercent 110 to 0`, `power3.out` 0.6 s, stagger 0.08 |
| Content rise | `y 40 to 0` `power3.out` 0.5 s stagger 0.06; art and button `back.out(1.2)` |
| Tap | press `scale .94` 0.1 s `power2.out`, release `back.out(1.4)` 0.45 s, ripple 0.6 s, dot press 0.8 and fade 0.3 s |
| Zoom into control | `#dev` scale 1 to 1.55 around the button centre, 3.40 to 4.30 s `power3.inOut`; old screen fades 4.00-4.25; new screen fades in 4.00-4.30; pull back 1.55 to 1, 4.30-5.10 `power3.inOut` |
| Sheet | `yPercent 100 to 0`, `power3.out` 0.7 s; scrim 0.5 s; rows `y 30 to 0` 0.45 s stagger 0.05 |
| Toggle | knob `x 0 to 48` `back.out(1.4)` 0.4 s while the track turns green in 0.3 s |
| Beat swap of headlines | outgoing `autoAlpha 0` in 0.12 s, incoming starts 0.05-0.1 s later |
| Drift | linear scale 1.00 to 1.025 over 12 s; concentric art yoyo; reminder chip floats -8 px yoyo |

No elastic, no bounce above `back.out(1.4)`, no shake, no flash, no whip.

## 7. Captions (UNTESTED: demo build, no voice)

Not exercised. Profile intent only: white pill `rgba(255,255,255,.9)`, hair border, radius 18, 40+ px, current word `--accent-dk`. In 9:16 the pill would sit under the panel at y 1760-1860, which this build keeps free. Test before relying on it.

## 8. Sound (UNTESTED)

Not exercised (silent). Profile intent: minimal pop 90-110 BPM, tap ticks and soft swooshes at volume 0.2-0.3. The three tap-like moments in this recipe are at 3.05 s (button), 4.0-4.3 s (zoom swap) and 9.5 s (toggle).

## 9. Scene recipes (12.0 s, three beats)

**R1 Hook / feature intro (0.0-3.4 s).** Headline "Ra mắt chương trình / thở có hướng dẫn" (accent word "thở"). Panel tilts in at 0.1 s; chip "Chương trình mới", title "Thở sâu bảy ngày", sub, concentric art and the "Bắt đầu" button fill in from 0.12 to 0.95 s (so the panel is never empty). Touch dot arrives on an arc 1.9-3.0 s, presses at 3.05 s.

**R2 Zoom and session (3.4-7.4 s).** Camera leans into the pressed button, the next screen emerges, camera pulls back. Headline "Thở theo nhịp, / từng vòng một" at 4.85 s. Ring draws over 2.4 s from 5.0 s, disc inhales 5.0-6.6 s ("Hít vào"), label swaps and the disc exhales 6.6-7.4 s ("Thở ra"). Seven day-dots pop in with staggered `back.out`.

**R3 Sheet and payoff (7.4-12.0 s).** Headline "Bảy ngày, mỗi ngày / chỉ năm phút" at 7.5 s. A sheet rises over the dimmed session screen with a 7-day list (3 rows), a toggle "Nhắc nhở mỗi sáng", button "Bắt đầu ngày 1". The dimmed strip above it carries "Buổi 1 hoàn thành" (fades in at 7.9 s). Dot taps the toggle at 9.5 s; the reminder chip springs in at 9.9 s. Hold from 10.5 s: a full composition with drift and the chip float. The last 1.5 s shows everything, nothing fading.

## 10. Transitions (profile set, as used)

1. R1 to R2: **zoom-into-ui** (above), the signature move.
2. R2 to R3: **sheet** (rises from the bottom, previous screen scrimmed and then faded under it).
3. Not used here: spring-rise as a cut, cross-fade with blur. One interaction on screen at a time was kept.

## 11. Image guidance

None generated. If a mood image is wanted: soft neutral wash, hexes from section 1, no text, no people, no logos, generous empty margins; used only as a flat background layer, never inside the panel.

## 12. Must not

- Live `backdrop-filter`; elastic or overshoot above 1.4; dark neon; cursor arrows; busy backgrounds.
- `--accent` or `--green` as text colour; white text on `--accent` (4.23:1).
- A real company, product, price or spec: label the build "Minh hoạ" on screen from frame 0 to the end.
- Two interactions at once; a third panel; text under 30 px; emoji.
- segoepr for Vietnamese.

## 13. Traps seen in real builds (this build, 2026-11-14, t128)

1. **Empty panel at the start.** First version started the panel content at 0.5 s: the frame at 0.4 s showed a blank white card (exceeds the 0.5 s empty-panel limit once the panel's own rise is counted). Fix: content starts at 0.12 s, panel opacity reaches 1 by 0.35 s.
2. **Sheet over a screen that still has text.** `inspect` reported 3 `text_occluded` errors (the session caption, the day label and the label under the reminder chip hidden beneath the sheet and chip, t 8.67-11.33 s). A 92% sheet also lets the old text ghost through. Fix: fade the session screen to 0 at 7.95-8.20 s and set it hidden.
3. **Hiding the lower screen leaves an empty grey strip.** After trap 2 the dimmed 300 px above the sheet was empty for about 4 s (reads as an empty panel). Fix: a "done" block ("Buổi 1 hoàn thành" 50 px plus a 36 px line) in that strip, ink text (muted text on the scrim is about 3.9:1 and fails).
4. **Off-canvas sheet flagged as overflow.** `inspect` listed `canvas_overflow` on every sheet row while the sheet waits at `yPercent 100`. Fix: `data-layout-allow-overflow` on `#sheet`. Result: 0 layout issues across 9 samples.
5. **Overlapping opacity tweens.** Lint gave 2 `overlapping_gsap_tweens` warnings (`#dev` 0.10-0.35 s and `#note` 9.90-10.10 s) because a rise tween and a fade tween both wrote opacity. Fix: opacity only in the short tween. Lint 0 errors, 0 warnings.
6. **White text on the profile accent fails.** `#3b74f2` with white is 4.23:1. The button uses `#2f5fd6` (5.63:1). Keep `#3b74f2` for ripple, dots, ring track tints.
7. **Zoom collides with chrome.** At scale 1.55 around the button (frame y 1594) the panel top reaches y -45, covering the headline and the "Minh hoạ" chip for about 0.5 s (frame at 3.9 s shows the chip over the kicker). Accepted as transient camera motion; the headline fades out first (3.35 s, 0.12 s). Do not place anything permanent in the top 300 px that must stay legible during the zoom, or give it a lower z-index than the panel.
8. **Reminder chip wraps.** At 540 px wide and 32 px, "Nhắc nhở · 07:30 · Hít thở năm phút" breaks to two lines and leaves "phút" alone on line 2 (visible in the final frame). Not fixed in the demo; use 620 px wide or shorten the text.
9. **Tooling.** `frame_check.py` could not run in this session: `python3` has no numpy and `/usr/bin/python3` was not allowed. Frame check was done by hand: ffmpeg contact sheet at 2 fps (24 frames) plus single frames at 0.1, 0.3 and 11.2 s, read visually. Contrast was computed by hand. Re-run `frame_check.py` where numpy exists.
10. **Mute token is tight on the page background.** `--mute` is 4.52:1 on `--bg`, 5.11:1 on white: only use it on white surfaces, at 32 px or larger.
11. **Mid-motion frames at transitions are real.** At 7.9 s the ring is still visible through the rising sheet (0.3 s) and at 4.0 s the zoomed screen shows both screens cross-fading. Both are shorter than the 0.5 s limits; keep fades at or under 0.3 s.
12. **Timeline length.** The render came out at exactly 12.0 s using `tl.set({}, {}, 12)` and `data-duration="12"`; no timing file was needed because there is no voice.
