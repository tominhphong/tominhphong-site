# Style: Precision dark product (9:16 Vietnamese dark-UI edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), as observed in the demo build.** A fast, exact story about a command-line or keyboard-driven tool, where the product itself is the picture: a command is typed, steps run in order, a result appears. Shapes that fit: dev tools, CLIs, CI/deploy flows, changelog items, "one command does X" explainers (the tested shape was t029: a command line tool that turns a README into a deployment, Jev fit 0.78). Not for warm human stories, enforcement stories, single big-number news, or anything that needs a photo, a face or a map. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE 12 s silent demo (`samples/sample-t029.mp4`, 1080x1920, 30 fps). **Voice, captions, music and SFX rules were NOT exercised** (demo build): sections 8 and 9 repeat the profile and are ASSUMED. Numbers below were measured on that build unless marked ASSUMED. Content in the demo is generic and labelled "Minh hoạ" (no real product).

Energy 3 (profile): fast, exact, quiet. Near-black stage, one desaturated indigo accent, hairline borders, snappy 0.1-0.3 s UI moves, no bounce, no flash, no shake.

## 1. Tokens

```css
--bg: #0a0a0d;        /* stage */
--surface: #111216;   /* window, pills */
--row: #14151a;       /* rows, nodes, cards inside the window (ASSUMED: one step above surface) */
--ink: #f5f5f3;       /* 18.1:1 on bg, 17.1:1 on surface */
--mute: #8e9099;      /* 6.2:1 on bg, 5.9:1 on surface (headline gradient end, labels, status words) */
--hair: rgba(255,255,255,0.08);   /* every border, 1 px */
--accent: #6d5fd0;    /* MARKS ONLY: progress fill, 12 px tag dot. 3.74:1 on surface: FAILS as text */
--accent-ink: #a99ff0;/* ASSUMED text-safe variant: 7.9:1 on surface; caret, URL */
--green: #3fb39c;     /* 20-24 px status dots only (7.3:1) */
--amber: #eeaf4a;     /* 20 px "running" dot only (9.7:1) */
--keycap: #1b1c22;    /* keycap fill; ink on it about 15:1 */
```

Contrast figures were computed by hand with the WCAG formula (no script could run in this build); `hyperframes validate` independently reported "20 text elements pass WCAG AA". Status colours are dots only; status text stays ink/mute (profile: status colours on small dots and badges).
Baked layers: `assets/glow.png` (1080 x 900, accent at 30% peak alpha, ellipse centred at the top, rendered with ffmpeg `geq`; max 2 glows allowed, this build used 1) and `assets/noise.png` (256 px tile, 2% white noise, repeated over the frame).

## 2. Fonts (3 local files; the profile's Inter / JetBrains Mono are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, row labels, captions, card text | Inter 500 | `SegUIVar.ttf`, weight axis 300-700; headline 600, `letter-spacing:-0.035em` | all tone-mark letters present (checked earlier on this exact file in the owner docs; this build confirmed by eye: "Từ README đến bản triển khai", "Tự sắp xếp thứ tự các bước", "Đã triển khai", "hoàn tác" all render with intact marks) |
| Terminal text, URL, keycaps, status words | JetBrains Mono | `CascadiaMono.ttf` 400-500; advance width 0.586 em (used to place the typing caret) | "cổng", "Biến", "Tìm thấy 4 bước" render correctly in mono |
| Never | | `segoepr.ttf` (no Vietnamese letters); `cambriai.ttf` not needed | |

Declare faces with `font-display: block`. Gradient headline text works with `background-clip:text` in the HyperFrames renderer (rendered clean, no black frames).

### Type scale (1080 x 1920, px; no text under 30 px anywhere in the demo)

| Token | Font | Size | Notes |
|---|---|---|---|
| `#tag` "Minh hoạ" | SegUI 600 | 30 | pill 56 px high, hairline border, 12 px accent dot |
| `.hl` headline | SegUI 600, -0.035em, line 1.1 | 84 | 2 lines, gradient ink 0-35% then to mute at 100%; max about 20 characters per line in 936 px |
| terminal line | Cascadia 400 | 34 | README lines (mute, heading in ink); prompt line 36 / 500 |
| row label | SegUI 500 | 42 | row 130 px high |
| row status | Cascadia 400 | 32 | mute, then ink when "xong" |
| node label | SegUI 500 | 36 | node 240 x 124 |
| card title | SegUI 600 | 68 | -0.03em |
| URL chip | Cascadia 400 | 34 | accent-ink, in a hairline chip |
| card lines | SegUI 400 | 36 | mute, key figure in ink 600 |
| keycap | Cascadia 500 | 32 | 72 px high, label beside it SegUI 34 mute |
| window title | Cascadia 400 | 30 | mute, centred |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -150  platform UI: empty
y 150  -206  "Minh hoạ" tag (always on screen)
y 252  -430  headline, 2 lines of 84 px
y 520  -1400 window (x 72-1008, 936 x 880, radius 20); title bar 80 px; body 796 px
y 1440 -1524 keycap row, centred
y 1524 -1920 empty (platform UI; the demo leaves it dark on purpose)
x 72  -1008  content column, 936 px
inside the window body: 44 px side padding, content 846 px wide
```

Rows: 130 px high, 150 px pitch (20 px gap), first row at body y 30, 4 rows end at y 630; progress track at y 640 (8 px). Result card: y 224-744 under a node row at y 44-168.

## 4. Layers, back to front

`#glow` (baked PNG, breathes scale 1 -> 1.04 over 6 s, yoyo, whole piece) -> `#noise` (2%) -> `#tag` -> headlines `#h1 #h2 #h3` (one per beat, stacked in the same box) -> `#persp` (perspective 1800 px) holding `#win` (title bar + three beat bodies `#b1 #b2 #b3`) -> `#keys` (keycap groups). No flash layer, no fade-to-black layer (the piece starts on a finished headline and ends on a held composition).

## 5. Components

- **Window**: surface fill, 1 px hair border, radius 20, inner top highlight `inset 0 1px 0 rgba(255,255,255,0.04)`. Three 14 px grey dots (12% white) in the title bar.
- **Terminal block**: README excerpt in mute with the heading in ink, hairline rule, prompt line "$ command", accent-ink block caret (18 x 40 px), result line with an arrow.
- **Status row**: 20 px dot (grey -> amber while running -> green when done), label left, mono status word right; the three words ("chờ", "đang chạy", "xong") are stacked and crossfaded 0.1 s.
- **Progress track**: 8 px, radius 4, 8% white track, accent fill growing with `scaleX` from the left, linear, ends with the last row.
- **Node + connector**: 240 x 124 hairline nodes, 63 px 1 px connectors (22% white) drawn with `scaleX` from the left (`transform-origin: 0 50%`).
- **Result card**: row-fill, hairline, 24 px green dot + 68 px title, URL chip, hairline rule, two lines of facts.
- **Keycap**: 1 px hair border, radius 12, plus a `0 4px 0 rgba(255,255,255,0.10)` lower edge as the "key thickness" (the only non-hairline edge; keep it under 4 px). Press = y +4 and lower edge to 0 in 0.08 s, release 0.15 s; the Enter press also tints the fill to `#2a2742`.

## 6. Motion language

Allowed eases: `power3.out` (entrances, tilt), `power2.out` / `power2.in` (presses, exits), `power2.inOut` (connector draw), `sine.inOut` (glow breathing), `none` (progress). No `back`, no `elastic`, no bounce.
Durations as built: tilt-in rotateX 18 -> 0 in 1.2 s (perspective 1800, origin bottom centre); headline rise 24 px in 0.35-0.45 s; README lines 0.2 s with 0.12 s stagger; typing 0.045 s per character (23 characters = 1.04 s); keycap press 0.08 s + release 0.15 s; row dot colour 0.12 s; FLIP swap 0.25 s `power3.out` (two rows move +/-150 px at once); node pop 0.25 s with 0.15 s stagger; connectors 0.3 s; card rise 0.3 s.

### Transition rules between beats

The window stays; only its content and the headline change. Out: content, headline and keycap group fade to 0 in 0.12 s (`power2.in`) ending exactly where the next beat starts; in: next headline rises 24 px over 0.35 s while its body fades in over 0.15-0.2 s. The old beat is `visibility:hidden` 0.12 s after its fade starts, so no ghost survives more than 0.12 s. Cut points as built: 3.4 / 3.52 s and 7.95 / 8.07 s.

## 7. Scene recipes (S = beat start; times are absolute in the 12 s demo)

### R1 Command typed (0 - 3.5 s)
Headline at full opacity from frame 0 (no empty start). Window tilts in under the glow (0 - 1.2 s). README lines appear from 0.35 s. Caret appears 1.0 s; the command types 1.1 - 2.14 s, caret moving one character per tick. Keycap "Enter" fades in 2.2 s, presses 2.55 s; the caret hides at 2.6 s and "→ Tìm thấy 4 bước triển khai" rises in at 2.75 s. Hold to 3.4 s.

### R2 Steps run, rows reorder (3.52 - 8.0 s)
Four rows rise in with a 0.07 s stagger. Row 1 runs 4.1 - 4.7 s. At 4.8 s the FLIP swap moves "Dò cấu hình" above "Dựng container" (the order changes by itself: this is the "tool sorts the steps" message). Rows 3, 2, 4 run 5.15-5.85, 5.85-6.65, 6.65-7.35 s. The progress fill runs 4.1 - 7.35 s linear and is full before the hold. Hold 7.35 - 7.95 s with four green dots.

### R3 Result (8.07 - 12 s)
Three nodes pop (README -> Container -> Bản chạy) at 8.12 s with 0.15 s stagger, connectors draw 8.37 and 8.67 s, the result card rises at 9.02 s, keycaps "Ctrl" "Z" + "hoàn tác" appear at 9.57 s and press at 10.47 s. Everything is on screen from 9.6 s and held to 12.0 s (2.4 s of full composition). Only the glow breathes during the hold.

## 8. Captions (Vietnamese)

NOT exercised in the demo (silent, no captions). Profile (ASSUMED here): surface pill with hair border, radius 10, 40-44 px Be Vietnam Pro 500 ink (use SegUIVar 600 instead; Be Vietnam Pro is not installed); unread words mute. In 9:16 the bottom caption band would sit at y 1420-1524, which this build uses for keycaps: when captions are added, move keycaps up into the window or drop them for caption beats.

## 9. Sound

NOT exercised. Profile (ASSUMED): minimal ambient electronic 110-128 BPM, key taps on keycap presses (2.55 s and 10.47 s are the press frames), nothing else.

## 10. Images (agy)

No image was generated: the style is carried by its own UI. If one is ever needed, use a soft top-light texture only, no UI, no text, no logos, no people. Never use an image where the demo shows a window; a generated "dashboard" would fake data.

## 11. Must not

- No bright or light theme; no chunky or coloured shadows; no mascot; no emoji.
- No bounce, spring, shake, flash or glitch; no tween longer than 0.45 s except the tilt-in (1.2 s) and holds.
- No accent colour as text under 4.5:1: `#6d5fd0` is a mark; text uses `#a99ff0`.
- Status colours only on 20-24 px dots (never as a text colour).
- 1 px hairlines only (the keycap lower edge is the single exception).
- No real product, company, price, spec or URL: use `.example` hosts, generic names, and keep "Minh hoạ" on screen for the whole piece.
- No empty window body: the panel must hold content within 0.5 s of its first frame.
- No text under 30 px (one footer line may be smaller).
- No more than 2 baked glows; no CSS animation or `requestAnimationFrame`.

## 12. Traps seen in real builds (this build, 2026-11-14, 12 s demo, hyperframes 0.7.26)

1. **CSS transform + GSAP scaleX.** `#fill` had `transform:scaleX(0)` in CSS; `lint` gave an error (`gsap_css_transform_conflict`). Fix: no CSS transform, `gsap.set(el,{scaleX:0})` in JS. Lint then 0 errors.
2. **Typing caret flagged as occluding text.** `inspect` reported `text_occluded span.ch inside #caret` at t = 2 s (the caret overlapped the last typed character). `data-layout-allow-occlusion` on the caret did NOT clear it; moving the caret 6 px right of the character edge did (inspect: 0 layout issues across 9 samples).
3. **Accent fails as text.** `#6d5fd0` on the 111216 surface is 3.74:1; a caret and URL in it would fail. Added `#a99ff0` (7.9:1) for the two places accent colour is read as text.
4. **Empty window on frame 0-0.35 s.** The tilted window shows only its title bar and the first README line until the lines stagger in at 0.35 s (a 0.35 s near-empty panel, inside the 0.5 s limit). Do not start the README stagger later than 0.35 s.
5. **Status crossfade overlap.** "đang chạy" fades out and "xong" fades in both over 0.1 s, so for about 0.1 s two words overprint ("đang xong" visible at about 4.7 s in the 2 fps sheet). Under the 0.15 s ghost limit, but start "xong" 0.05 s after "đang chạy" ends to remove it.
6. **Lint false positives.** `overlapping_gsap_tweens` on `.dot` and `.s1` (4 rows share class names; the tweens target different elements). 0 errors, 2 warnings, accepted.
7. **Bottom fifth of the frame is empty.** Window ends at y 1400 and keycaps at 1524, so y 1524-1920 is dark (platform UI zone). It reads as intentional; do not stretch the window into it.
8. **Tool environment.** `frame_check.py` could not run (no `numpy` in the Studio's python3), and ad-hoc python scripts needed approval. The glow and noise PNGs were baked with `ffmpeg geq` instead of PIL, and the check used `ffmpeg fps=2,tile` sheets plus two `hyperframes snapshot` sets read by eye. Install numpy before relying on the scripted check.
9. **Tilt-in on a fresh frame.** At 0.1 s the window is a trapezoid (rotateX about 17 degrees); the headline above it is already finished, which keeps frame 0 readable. Keep the headline un-faded at frame 0.
10. **Numbers from the build.** Render 11.1 s for 12.0 s, 1.5 MB (file 1.6 MB by probe), 1080 x 1920 h264, silent; lint 0 errors / 2 warnings; validate no console errors, 20 text elements pass WCAG AA; inspect 0 issues.

## 13. Not tested (do before the first full video)

Voice-over timing, karaoke captions, music/beat response (glow pulse on kicks, keycap press on beats), sound design, the command-palette scene change (profile signature; the demo uses a typed command plus Enter press as the "command-cut" instead), a clip or screenshot scene, and a 45-60 s pacing run.
