# Style: sensory-tech (9:16 Vietnamese consumer-tech showcase edition)

Written 2026-11-14 from ONE real demo build: `samples/sample-t118.mp4` (12.0 s, 1080x1920, 30 fps, silent, project `samples/t118/`). Topic shape t118: a phone OS update personalises colours and widgets. Generic "Minh hoạ" content only. Marks: **MEASURED** = a tool showed it in this build. **HAND** = computed by hand with the WCAG formula (python/node scripts were blocked in this session). **ASSUMED** = the profile gives no value and this document chose one.

## 0. Read this first: niche, status

- **Tier 1 niche: not yet chosen.** No channel is assigned to this style yet.
- **Tier 2 (general fit, reference only), observed in this build:** product and feature showcases where a device or screen is the hero and the message is "it adapts to you": OS and app updates, new phone features, display, camera and personalisation stories, consumer promos. It carries 2-4 short claims, never numbers tables. Not for news with figures, dense text, sad or serious stories, government or finance (the bright gradient and bouncy chips fight the subject).
- **Not exercised in this build (demo only):** voice-over, captions, word timing, sound and music, counters, source line, the full 45-60 s arc. Every rule about those below is carried from the profile and marked ASSUMED; the first full build must test them.
- Profile: `skill/references/styles/profiles/sensory-tech.yaml` (energy 3, dark mode with gradient). Fonts named by the profile (Sora, Be Vietnam Pro) are not installed; local substitutes below.

## 1. Tokens (measured contrast on `--bg`)

```css
--bg:#0a0a14;        /* profile. page and frame edge */
--ink:#ffffff;       /* 19.7:1 on bg (HAND) */
--violet:#7b61ff;    /* 4.7:1 on bg (HAND): fills, glow, dock icon; text only >= 40 px */
--violet-ink:#b8acff;/* ASSUMED text-safe violet, 9.8:1 on bg (HAND) */
--coral:#ff7a8a;     /* 7.9:1 on bg (HAND): text ok */
--mint:#5ef2c2;      /* 14.1:1 on bg (HAND): text ok */
--accent:#3a2fb5;    /* profile deep blue for chips/CTAs; white on it 9.6:1 (HAND); not used in this sample */
--mute:rgba(255,255,255,.6); /* resolves to ~#9a9aa0, 7.0:1 on bg (HAND) */
--glass:rgba(10,10,20,.62);  /* DEVIATION: chip fill. Profile says white 14%; see trap 3 */
```
`hyperframes validate` reported "80 text elements pass WCAG AA" on the final composition (MEASURED). Rules: one liquid gradient per beat built from two of violet/coral/mint (beat 1 violet+coral, beats 2-3 violet+mint). The key word of each headline takes the beat's hue (coral, mint, violet-ink). Never raw `--violet` for small text.

## 2. Fonts (glyph check on the real strings; every Vietnamese letter used in this video rendered, MEASURED by snapshot, tone marks intact)

| File | Role | Notes |
|---|---|---|
| `SegUIVar.ttf` (weights 300-700) | everything read: headlines 700, chips 700, labels 500-600 | SUBST for Sora / Be Vietnam Pro. No 800 weight |
| `CascadiaMono.ttf` | numerals inside the device (clock, temperature, percent) at 600, tabular | gives the screen a UI feel; includes the ° sign |
| `cambriai.ttf` | unused in this build | keep for one pull quote only |
| `segoepr.ttf` | NEVER: lacks Ơ ơ Ư ư and dotted vowels | |

The Segoe-based headline is rounder than Sora; acceptable. Declare faces with `font-display: block`.

## 3. Type scale (1080x1920 px, all MEASURED from the build)

| Token | Size / line | Use |
|---|---|---|
| headline | 88 / 1.12, 700, -0.015em, 2 lines, max 16 characters per line (936 px wide) | one claim per beat |
| kicker pill | 32, 700, +0.02em, pill 64 px high | "Minh hoạ · Cập nhật hệ điều hành" |
| device clock | 132 Cascadia 600 | |
| device widget label / chip text | 30-36, 600-700 | nothing in the video is under 30 px except none; the footer is exactly 30 |
| widget numerals | 112 (temperature), 56 ("3 việc"), 34 inside ring | |
| footer | 30, 500, `--mute` | the single small line |

A 72 px "3 việc" wrapped to two lines in a 226 px widget (trap 4): size every in-device string for the Vietnamese length and set `white-space: nowrap`.

## 4. Safe areas and grid (1080 x 1920)

```
y 0-168     platform top: empty
y 168-232   kicker pill (x 72)
y 262-460   headline (2 x 99 px), x 72, width 936
y 590-1690  phone: 540 x 1100, radius 92, centred (x 270); screen 512 x 1072
y 523-1777  phone at its hero scale 1.14 (beat 3), still clear of headline (ends ~460) and footer
y 1800-1830 footer line, x 72
x 20-250 / 830-1060  orbit chips (112 px high, 205-250 wide), overlapping the phone edge by <= 25 px
```
Open conflict (ASSUMED, not exercised): a full build needs a caption pill. The hero device occupies y 590-1690, so captions would have to sit at y 1690-1790 and the footer move into the source line, or the device shrinks to about 0.85. Decide in the first full build, with the interview.

Inside the screen (absolute from the screen's top-left): notch y 20; banner y 76-176; clock y 196; date y 338; widget 1 y 400 (464 x 190, becomes 150 in beat 3); widgets 2 and 3 y 610 (226 x 226, move to y 590); widget 4 y 828 (464 x 100, appears in beat 3); dock y 948 (4 icons 96 px).

## 5. Layers, back to front

`#bgA` baked mesh (violet + coral) -> `#bgB` baked mesh (violet + mint), clip-path circle, flooded in -> `#scrim` (bg to transparent over y 0-780, keeps headline contrast) -> glow discs (radial-gradient, fastest drift, foreground accent) -> kicker, headline -> `#cam > #phone` (3D rotateY float) -> orbit chips -> footer. No flash, no shake, no beat pulse (no music).

Gradient meshes were baked with ffmpeg (`gradients` source, `gblur=sigma=30`, 540x960 scaled to 1080x1920, JPG) in a few seconds; no agy image was needed. Each is a single `background-image`; the bright band sits behind the phone and the top stays dark for text.

## 6. Components

- **Device**: dark body, 7 px border white 28%, radius 92, big soft shadow plus a violet glow; screen wallpaper = the same baked mesh, dimmed by a 38-50% navy overlay so the white clock reads (trap 2).
- **Widget**: dark glass `rgba(10,10,20,.72)`, radius 34, 3 px coloured border and a coloured accent element (dot, ring, number). Colour = the beat hue; it is the thing that recolours.
- **Banner** (update arrives): 464 x 100 glass, one line of 32 px text and a 10 px progress bar that fills to 100% before the flood.
- **Highlight outline**: 5 px mint ring plus 44 px glow around widget 1, "AI region" cue.
- **Orbit chip**: pill 112 px high, 2 lines of 32 px, 22 px colour dot, fill `--glass`, border white 30%.
- **Light sweep**: skewed white gradient bar, opacity <= 0.3, 0.7 s, inside the screen.
- **Equaliser** (widget 4): five 12 px bars, `scaleY` yoyo with finite repeats, micro-motion in the hold.

## 7. Motion language (energy 3)

Eases: `power3.out` (entrances), `power3.inOut` (reflow, push), `power2.inOut` (flood, recolour), `back.out(1.4)` (chips only), `sine.inOut` (float, glow drift), `none` (backdrop drift). No elastic, no shake, no flash. Overlap: widgets stagger 0.07 s with `power1.in` distribution.

Measured timeline of the 12 s sample:

| Time | Event |
|---|---|
| 0.00 | frame 0 is finished: kicker, headline, device with all widgets, footer. Only widgets slide up 70 px over 0.55 s |
| 1.00-1.55 | banner drops in; 1.7-2.9 progress bar fills |
| 0.9-1.6 | light sweep across the screen |
| 3.45-3.61 | headline 1 out (0.16 s) |
| 3.50-4.15 | colour flood: circle clip-path from the device centre, 0.65 s `power2.inOut`, on the page (r 1900 px) and inside the screen (r 900 px) |
| 3.70-4.20 | headline 2 in (y 44 to 0) |
| 3.80-4.40 | widgets, ring, dock icon recolour coral to mint, staggered |
| 4.70-5.15 | highlight outline; chips c1 (4.5) and c2 (5.0) pop |
| 7.55-7.70 | headline 2, chips and outline out (0.15-0.16 s) |
| 7.6-8.6 | push 1.05 to 1.14, widget 1 shrinks, widgets 2-3 move, widget 4 enters, ring turns violet |
| 8.5, 8.9, 9.3 | chips c3, c4, c5 pop (hold to 12.0, breathing 8 px) |
| 0-6 / 6-12 | device rotateY -14 to 12 to -9 (profile asks +-25; +-14 keeps text legible) |

## 8. Scene recipes (3 beats: set-up, change, hero hold)

- **R1 Arrival (0-3.5):** device already on screen, headline states the news, widgets slide up, banner proves "update ready", progress bar completes. Tint: coral.
- **R2 Personalise (3.5-7.6):** flood from the device switches the whole world to the second gradient; widgets recolour in a stagger; highlight outline; two chips explain.
- **R3 Hero hold (7.6-12):** push in, layout reflow, a new widget enters, three feature chips orbit. The last 1.5 s (10.5-12.0) are a full composition in constant light motion (device float, chip breathing, equaliser, glow drift).

## 9. Captions, voice, sound

Not exercised (demo build). Carried from the profile and ASSUMED: caption pill rgba(255,255,255,.14), radius 24, 44 px, current word `#5ef2c2`; bright electronic pop 115-122 BPM; liquid-swoosh SFX on the flood. See the caption-zone conflict in section 4.

## 10. Images

None generated. Baked ffmpeg gradient meshes replaced the agy image (the agy call needed approval that was not available). Rule: meshes are baked JPGs, never live blur stacks; the device itself is HTML/CSS, which kept the screen text sharp and editable.

## 11. Must not

- Live `filter: blur` stacks or more than ~40 gradient/clip-path elements; bake meshes.
- More than two gradient hues per beat; monochrome austerity; dense text (3 words per chip line max).
- A beat without the device in frame.
- `segoepr.ttf`; raw `--violet` as small text; chips with the profile's white 14% fill over a bright mesh.
- Real brands, specs, prices; every illustrative scene carries "Minh hoạ" in the kicker and the footer.
- Text under 30 px except one footer line.

## 12. Traps seen in real builds (this build, measured)

1. **Banner overlapped the clock.** Frame at 1.8 s: the 100 px update banner (y 76-176) sat on the 132 px clock (y 132-264); `inspect` flagged `content_overlap`. Fix: clock y 196, date 338, widgets pushed down 48 px.
2. **White on a bright wallpaper.** The wallpaper mesh behind the clock is coral/violet (white on #ff7a8a is about 2.5:1). Fix: a 38-50% navy overlay on the screen; `validate` then passed all 80 text elements.
3. **Chips over a bright mesh.** Profile glass (white 14%) would leave 32 px text near 3:1 over the mint band. Fix: dark glass `rgba(10,10,20,.62)` with a white 30% border; DEVIATION from the profile.
4. **"3 việc" wrapped.** At 72 px it wrapped in a 226 px widget and overlapped its label (`inspect`: content_overlap). Fix: 56 px, `white-space: nowrap`.
5. **Off-screen banner left a pink line.** The hidden banner (y -140) still showed its 10 px progress bar at the top of the screen, and `inspect` listed container_overflow at 6 of 8 samples. Fix: `visibility: hidden` outside 1.0-3.85 s.
6. **Lint false positives.** `overlapping_gsap_tweens` (4 warnings: #phone scale, #h2, #arc stroke, #ring2) persisted after converting the `to` tweens to explicit `fromTo` with `immediateRender:false`; the renders and frames are correct. Treat as known; do not chase.
7. **Headline ghost.** The outgoing headline takes 0.16 s to fade; frame 3.6 s (n=108) shows it at about 40% over the incoming flood. That is within the 0.15 s ghost rule only because the incoming one starts at 3.70; do not lengthen the out tween.
8. **Phone push vs headline.** At scale 1.14 the device top is y 523; with 88 px headline ending near 460 the gap is 63 px. A larger push or a third headline line would collide; cap the scale at 1.14.
9. **Tooling.** `frame_check.py` needs numpy and python scripts needed approval, so the frame check was done with ffmpeg contact sheets (see selfcheck.md). Contrast figures are HAND-computed plus the `validate` pass.
10. **Hinge fold and iris lens-zoom, device morph** from the profile were not built; only the colour flood and macro push were exercised.
