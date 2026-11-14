# Style: mission-control (detail, written from the demo build of 2026-11-14)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** one-event "it is happening now" stories with a build-up and a release: a launch, a release of a big image or dataset, a milestone reveal, a staged roadmap, deep-tech news with 3 plain figures. Worked well for the shape "space telescope releases a new deep-field image" (Jev fit 0.76). Not for warm human stories, testimonials, code, or stories with many equal numbers. Tier 2 never widens tier 1.

**Status.** Demo-only build: ONE silent 12.0 s sample (1080 x 1920, 30 fps, 2.0 MB), topic shape t072. Voice, VieNeu, word timing, captions, music and SFX were NOT exercised: every caption, sync and sound rule in the profile is untested here. Sections below that touch them say "profile only". All on-screen content is generic and labelled "Minh hoạ".

Profile: `skill/references/styles/profiles/mission-control.yaml` (energy 4, dark). Marks: **SUBST** = a named font is not installed and a local one replaces it. **ASSUMED** = profile gives no value. **DEVIATION** = knowingly differs from the profile.

- SUBST: Space Grotesk -> `SegUIVar.ttf`; IBM Plex Mono -> `CascadiaMono.ttf`; Be Vietnam Pro (captions) not used in this build.
- DEVIATION 1: profile title 64 px is for 16:9; in 9:16 the titles are 58 px with 0.14em tracking (0.18em made "ẢNH TRƯỜNG SÂU MỚI" 930 px wide, over the 936 px column).
- DEVIATION 2: profile hairline "1 px"; at 1080 px wide it vanishes on a phone, so hairlines are 2 px and corner ticks 4 px.
- DEVIATION 3: profile says "monochrome"; the hero image (a baked canvas deep field) carries warm orange and pale blue galaxies. Colour lives only inside the hero image; all UI stays white / amber / blue.
- DEVIATION 4: profile "telemetry as side rails at mid-height"; 9:16 has no side room, so telemetry is a row of three boxes under the hero.

## 1. Tokens (contrast measured with the WCAG formula, on #000)

```css
:root{
  --bg:#000;                       /* 1.0 */
  --ink:#fff;                      /* 21.0:1 */
  --mute:rgba(255,255,255,.6);     /* 7.4:1. ASSUMED: the profile's .45 is only 4.4:1 and FAILS */
  --hair:rgba(255,255,255,.3);     /* boxes and rules, decorative */
  --amber:#ffb000;                 /* 11.5:1, live / HOLD states only */
  --signal:#2a5aa8;                /* 3.1:1: LINES ONLY (orbit ring), never text */
  --signal-lt:#6c9be0;             /* ASSUMED, 7.4:1: the trajectory arc line */
}
```
Rules: text colours only `--ink --mute --amber`. `--signal` fails 4.5:1, so it is a stroke colour (non-text 3:1 passes at 3.1). Never lighten a text token to look softer. `hyperframes validate` reported "15 text elements pass WCAG AA".

## 2. Fonts

| File | Role | Vietnamese check |
|---|---|---|
| `SegUIVar.ttf` | titles (600, uppercase, 0.14em), body | all diacritics rendered in snapshots (Ả Ờ Â Ẩ Ê Ồ Ư Ơ Đ); fontTools check NOT re-run in this build (python was not approved); owner docs record 0 missing |
| `CascadiaMono.ttf` | clock, telemetry, labels, checklist | same: rendered Ế, Ệ, Ở, Ữ correctly in snapshots |
| `cambriai.ttf` | not used | - |
| `segoepr.ttf` | NEVER (92 Vietnamese glyphs missing per owner docs) | - |

Uppercase mono with stacked marks (Ẩ, Ế) needs line-height >= 1.1 so marks are not clipped by the line box; all mono lines here use line-height 1 to 1.3 with no overflow clip.

## 3. Type scale (1080 x 1920)

| Role | Font | px | Note |
|---|---|---|---|
| T-minus clock | mono 500 | 160 | tabular numerals, "T-00:03" is 7 chars, about 620 px wide |
| Section title | Seg 600 upper | 58 | 0.14em tracking, one line max 18 characters |
| Sub line | mono 500 | 40 | |
| Telemetry value | mono 500 | 60 | max 7 characters in a 296 px box |
| Checklist, state | mono 500/600 | 34 | |
| Tags, labels, progress labels | mono 500 | 30-32 | the minimum on screen: nothing below 30 px, no footer line used |

## 4. Grid and safe areas

- Side margin 72, content width 936. Three-box row: 296 + 24 gap.
- y 0-200 empty (platform UI). Progress timeline y 210 (2 px line, 22 px event ticks), tick labels y 234.
- Stage row (live dot + stage name) y 310-390. Title y 420-480 (scene A: y 520). Hero y 520-1220 (936 x 700). Telemetry row y 1262-1452. Checklist y 1190-1482.
- y 1480-1920 is EMPTY by design: this is the caption band (profile: captions own it alone). In the sample it is black, which makes the frame look top-heavy; with captions it fills.

## 5. Layers (back to front)

1. `#root` black. 2. `#stars` canvas, baked once: 170 seeded points 2-3 px at 15-60% alpha (not 5%: a 5% star disappears on a phone). 3. `#hud` persistent progress timeline and "MINH HOẠ" tag. 4. Scene sections `#scA #scB #scC` (one visible at a time via autoAlpha set at the cut). 5. `#bars` signal-loss bars. 6. `#flash` white. 7. `#fade` black, 1 to 0 in 0.4 s at the start; NO fade out (the last 1.5 s must be a full composition).

## 6. Components

- **Telemetry block** `.tel` (296 x 190): 2 px hairline box, 4 corner ticks 20 px, mute label (30 px) top, value (60 px mono) below. The box fades in first (0.3 s, 20 px rise), then the value types in over 0.45 s.
- **Checklist row** (936 x 84): name left, state cell right 150 px wide. HOLD amber on black, then GO white on a 14% white fill with a 1.08 -> 1 settle (0.25 s).
- **Hero frame**: hairline box with corner ticks, content reveals by a top-to-bottom scan (clip-path inset, 1.3 s power2.inOut) with a 4 px white scan line riding the edge; 5% scanline texture over the image.
- **Annotation**: ring drawn by dashoffset (0.5 s), leader line (0.5 s), 32 px mono label ABOVE the leader (not on it).
- **Dotted globe**: canvas, 620 Fibonacci-sphere points (3 px squares), front hemisphere only, alpha by depth, slow rotation 1.6 rad over 3.9 s (redrawn in onUpdate, deterministic). Orbit ellipse 4 px `--signal`, arc 4 px `--signal-lt`, travelling dot r 11 via `getPointAtLength`.
- **Progress timeline**: 2 px line, white fill scaleX 0 -> 1 over 11.4 s linear, three event ticks labelled "GĐ 1/2/3" (generic stage names), each lights from 45% to 100% at its scene start.

## 7. Motion language

- Entrances: 30 px rise with `power3.out`, 0.45-0.55 s. Lines draw with `power1.inOut` 1.2-1.4 s (arc, orbit) or `power2.out` 0.45 s (crosshair, ring). Nothing bounces.
- Countdown: the clock changes at 1.2, 1.8, 2.4 s (about 0.6 s steps, near 100 bpm quarter notes; NOT beat-locked, no music), each tick a 1.04 -> 1 settle in 0.2 s. It lands on T-00:00 at 2.4 s and HOLDS 0.6 s in white (amber while counting) before the cut, so no frame holds mid-count.
- Micro-motion in holds: hero slow scale 1.00 -> 1.05 over 4.4 s (`sine.inOut`), globe rotation, travelling orbit dot, progress fill.
- Typing: `typeIn` via a proxy object; a `set` writes the full text 0.01 s after the tween so a seek never leaves a half word.

## 8. Scene recipes (this build, 12.0 s)

| Beat | Time | Content |
|---|---|---|
| A countdown | 0.0-3.0 | stage label, title "KÍNH THIÊN VĂN / VŨ TRỤ", crosshair stubs draw, clock T-00:03 -> T-00:00, sub line, note "Nội dung minh hoạ" |
| cut | 2.967-3.033 | countdown cut: 2 white frames; scene swap at 3.0 is hidden under them |
| B reveal | 3.0-8.03 | title "ẢNH TRƯỜNG SÂU MỚI", hero frame draws, deep-field scan reveal 3.25-4.55, telemetry 120 GIỜ / 1 000+ / 13 TỶ typed at 4.5-5.9, annotation "THIÊN HÀ XA NHẤT" 5.6-6.7, hold to 8.0 |
| feed switch | 7.9-8.06 | 9 seeded white bars at 90% for 0.16 s, scene swap at 8.03 |
| C downlink | 8.03-12.0 | title "ẢNH ĐÃ SẴN SÀNG", globe + orbit + arc from a white square "KÍNH THIÊN VĂN", checklist HOLD -> GO at 9.1, 9.6, 10.1; from 10.5 s every row is GO and the frame is complete to 12.0 |

## 9. Transitions used

Countdown cut (white 2 frames) and feed switch (signal-loss bars 0.16 s). Not built: stage separation and trajectory wipe (profile). Hard cuts under a cover frame leave no ghost of the outgoing beat.

## 10. Captions, sound

Profile only, not exercised: 42 px Be Vietnam Pro, bottom band alone, no telemetry beside it. The layout here keeps y 1480-1920 free for that. Sound (tension pulse, countdown beeps, liftoff rumble) not built.

## 11. Images

One baked layer is enough. The deep field is drawn in a canvas from a seeded rng: 260 soft elliptical galaxies (tints orange / blue / cream, 8% large), 90 white pixel stars, one featured bright galaxy at the annotated spot. The optional agy image was NOT generated (the python runner was not approved in this session); the canvas stand-in reads as a deep field at phone size, but a real generated image would add texture. Radial gradients are used only inside the canvas (baked), never as live CSS.

## 12. Must not

- No colour in the UI beyond white, mute white, amber (live and HOLD only) and blue (lines only). No blue text.
- No rounded friendly UI, no fills on boxes (the only fill is the 14% GO cell), no mascot, no emoji.
- No invented telemetry presented as fact: here every number is labelled "Minh hoạ" in the persistent HUD tag; real use must take figures from the script.
- No second countdown or second white-flash drop in one video.
- Nothing in y 1480-1920 unless it is a caption.
- No text below 30 px.

## 13. Traps seen in real builds (this build, measured)

1. **Profile mute fails.** `rgba(255,255,255,.45)` on black is 4.4:1; use .6 (7.4:1).
2. **Blue signal is not a text colour.** `#2a5aa8` is 3.1:1 on black; fine for a 4 px orbit line, wrong for any label.
3. **Letter-spacing eats the column.** 58 px uppercase at 0.18em made an 18-character Vietnamese title about 930 px; use 0.14em or break the line.
4. **Typing leaves half words.** Text typed by a tween needs a closing `set` to the full string, and its end must come well before the beat ends; mono value "13 TỶ" showed as "13" in a sheet frame 0.2 s before completion.
5. **A blinking live dot is a sub-90% frame.** Dimming to 50% on a 0.3 s cycle put a held frame at 50% opacity; the blink was removed. Use a colour that does not dim, or a discrete on/off shorter than 0.2 s.
6. **Crosshair stubs run into text.** A vertical tick at y 1060 crossed the sub line; keep crosshair stubs beside the clock only, not below it.
7. **Annotation label on its own leader.** Label at the end of a leader line was struck through by the line; place the label above the leader.
8. **Empty hero box.** The frame drew at 3.1 s but the reveal began at 3.5 s: 0.4 s of an empty panel, borderline against the 0.5 s limit; the reveal now starts at 3.25 s. With a power2.inOut ease the first 0.15 s of the scan still shows almost nothing, so the empty time is about 0.35 s.
9. **Top-heavy frame without captions.** Reserving the caption band leaves 440 px of black in a silent sample; judge the layout with that band in mind or show a placeholder caption.
10. **Tooling.** `hyperframes lint / validate / inspect` were clean (0 errors, 0 layout issues, 15 text elements pass AA) but did not catch traps 5-8; only looking at frames did. The render output size was identical (2,035,997 bytes) before and after the reveal-time edit, which looks odd; the frame at 3.3 s confirms the file is current in time, but the byte match was not explained.
