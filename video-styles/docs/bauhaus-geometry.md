# Style: bauhaus-geometry (9:16 Vietnamese explainer edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in the t169 build:** explaining STRUCTURE: "parts snap together into a whole" stories (low-code and no-code builders, modular products, plugin or block systems, how a process is assembled, 3 to 4 named parts). It carries 3 short labels well. Not for stories with many numbers, quotes, bad news, enforcement, or anything needing photos (the profile forbids photography). Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a 12.4 s silent sample (`samples/sample-t169.mp4`, 1080x1920, 30 fps, 8.8 MB), topic shape t169 "low-code platform lets teams snap together apps from reusable blocks" (Jev fit 0.71), content generic and labelled "Minh hoạ". **Voice-over, word timing, captions, music and SFX were NOT exercised** (demo build): sections 8 and 9 are the profile's values, marked ASSUMED. No agy image was used (the profile excludes photography).

Source of values: `styles/profiles/bauhaus-geometry.yaml`. Anything the profile does not give is marked ASSUMED.

Look: cream paper, three flat primaries, only circle, square, triangle and 8 px ink bars. Shapes roll, pivot and lock together like machine parts. Energy 3, mechanical and calm: no glow, no shake, no flash.

## 1. Tokens (contrast measured with the WCAG relative-luminance formula, computed by hand from the hex values)

```css
--bg:   #efe8d8;  /* cream paper; L 0.810 */
--ink:  #1a1a1a;  /* text, bars, panel frame      14.27:1 on bg, 9.58:1 on yellow */
--red:  #d62828;  /* shape family 1 (circle), cover circle   4.10:1 on bg: NOT small text, marks only (large text >= 48 px only) */
--blue: #1d4e9e;  /* shape family 2 (square), scene-3 background   6.53:1 against bg: cream text on blue passes */
--yel:  #f2b705;  /* shape family 3 (triangle), chip fill   1.49:1 on bg: marks only; ink on yellow 9.58 */
--mute: #b9b09c;  /* 1.76:1 on bg: marks only, never text (not used in the build) */
```

Other pairs: cream on red 4.10 (large text only); ink on red 3.48 (never text); yellow on blue 4.38 (large text only, avoided). `hyperframes validate` reported "5 text elements pass WCAG AA".
Rule kept in the build: circle = red/yellow anchor, square = blue, triangle = yellow; every text is ink on cream, cream on ink, cream on blue, or ink on yellow.
Grain: a baked 1080x1920 PNG (ffmpeg `noise=alls=90:allf=t` on grey) at 6% opacity over everything. It is visible only as faint texture; the renderer showed no black frames with it.

## 2. Fonts

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headlines, labels, body, chip | Josefin Sans 700 / 400 (not installed) | `SegUIVar.ttf`, weight axis 300-700, headline 700 uppercase, `letter-spacing:0.04em` | tone marks verified in rendered frames (Ế, Ộ, Ứ, Ụ, Ầ, Ệ in "GHÉP ỨNG DỤNG", "MỘT ỨNG DỤNG", "CÙNG BỘ KHỐI", "NHIỀU"): none clipped at line-height 1.12. The fontTools glyph test was not run (no permission to run a script); the check is the rendered frames. |
| Numerals, mono | none | not used | |
| Never | | `segoepr.ttf` (no Vietnamese letters) | |

Josefin is not installed, so Segoe UI replaces it; the geometric feel comes from the shapes, not the face. Profile mentions Be Vietnam Pro for captions: also not installed; use Segoe UI 700.

### Type scale (1080 x 1920 px, all measured from the build)

| Token | Size / line | Notes |
|---|---|---|
| `.h` headline | 100-104 / 1.12, uppercase, +0.04em, `white-space:nowrap` | longest line "NHIỀU ỨNG DỤNG" = about 790 px at 100 px, "MỘT ỨNG DỤNG" about 770 at 104. Max 2 lines, max about 14 characters per line (limit 960 px) |
| `.lab` shape label | 44 / 1.2, 700, centred in 260 px | "Giao diện" fits |
| `.sub` | 40 / 1.2, 600 | one line, <= 36 characters (790 px) |
| panel header | 46, 700, no uppercase | |
| panel footer, tile names | 34-36 | smallest text in the video is the 34 px chip "Minh hoạ" and the 34 px tile names; nothing under 30 px |

## 3. Safe areas and grid (1080 x 1920; ASSUMED because no caption band was built)

```
y 0    -170   platform top UI: empty (chip "Minh hoạ" sits at y 176-232, just under it)
y 250  -950   anchor circle zone, 700 px circle at x 190-890 (title scenes)
y 240  -480   2-line headline (scene 2), x 60
y 1000 -1270  ink headline bar 960 x 270 at x 60 (scene 1)
y 560  -1130  diagram rows (scene 2)
y 1050 -1610  app panel 920 x 560 at x 80
y 1290 -1660  tiles and names (scene 3)
y 1700 -1920  empty (kept clear for the platform UI and a future caption band)
x 60 / 80     left margin (bars 60, panel 80), right margin 60
```

If captions are added, the band y 1370-1480 used by the other styles collides with the panel and tiles: untested; move the panel/tiles up or drop the footer line.

## 4. Layers, back to front

`scene` sections (cream or blue background, each hidden with `visibility` when not active) -> `#cover` (2600 px solid circle, z 40) -> `#grain` (z 50) -> `#chip` "Minh hoạ" (z 60, persistent from 0 to the end). No flash layer, no vignette.

## 5. Components

- **Anchor circle**: 700 px, one per title scene, with a 150 px contrasting square inside so the roll is visible (a plain circle shows no rotation).
- **Headline bar**: solid ink rectangle 960 x 270, cream text on it (14.27:1).
- **Shape palette row**: circle, square, triangle at 260 px, centres 210 / 540 / 870, labels 44 px below, joined by 8 px ink bars 70 px long.
- **App panel**: ink rectangle 920 x 560 with a cream inset (12 px) as a flat shape, header 46 px, the three shapes copied in at scale 0.85 and joined by 8 px ink bars.
- **Mini app tile**: cream square 280 x 300 holding two shapes of the kit in a different arrangement; name 34 px below.
- **Chip**: yellow rectangle 56 px high, ink 34 px 700 text "Minh hoạ".

## 6. Motion language

Eases used: `power2.out` (roll, rise, bars), `power3.out` (bars, text), `power3.inOut` 0.45-0.5 s (pivots), `power2.in` / `power2.out` 0.4 / 0.45 s (cover), `sine.inOut` (45 degree hold rotation). No elastic, no overshoot, no shake.
- **Roll**: wrapper `x` from -950 (or +950) plus `rotation` -155 (or +155) degrees to 0 in 0.8-0.9 s: 950 px over a 700 px circle is 155 degrees, so rotation matches distance.
- **Pivot**: `rotation` 90 or -90 to 0 around a bottom corner (`transform-origin: 0 100%`), 0.45 s, with opacity 0 to 1 at the same time. Used for triangle, square, panel, tiles (stagger 0.2 s).
- **Shape-cover**: a 2600 px solid circle centred on the frame scales 0 to 1 in 0.4 s (`power2.in`), the scene is swapped under it, then it scales 1 to 0 in 0.45 s (red, scene 1 to 2) or is simply hidden (blue, scene 2 to 3, because scene 3 background is the same blue).
- **Clone and snap**: the palette shapes stay; a copy leaves the same spot and flies 680 px down into the panel in 0.5 s (stagger 0.15 s), then an 8 px bar grows between copies in 0.25 s.
- **Hold motion**: the anchor circle rotates 45 degrees over 1.5-1.8 s with `sine.inOut`.

## 7. Scene recipes (S = scene start, measured in this build; total 12.4 s)

### R1 Title (0 - 3.5 s)
0.0-0.9 red circle rolls in; 0.2-0.5 headline fades up on the ink bar (bar grows from 50% to 100% width, 0.45-0.95); 1.0 triangle and 1.2 square pivot in (0.45 s); 1.3 sub line; 1.7-3.2 circle turns 45 degrees; 3.1-3.5 red cover closes.
### R2 Structure diagram (3.5 - 7.9 s)
3.9 headline; 4.0 / 4.2 / 4.4 circle rolls, square pivots, triangle scales in; 4.7-4.9 labels; 4.95 and 5.1 bars; 5.2-5.7 panel pivots in; 5.6 header; 5.8 / 5.95 / 6.1 copies snap in; 6.5 / 6.65 bars; 6.7 footer line; 7.5 blue cover. Full composition holds 7.0-7.5.
### R3 Outcome (7.9 - 12.4 s)
7.95-8.75 yellow circle rolls in from the right; 8.5 headline; 9.0 / 9.2 / 9.4 tiles pivot in; 9.5-9.95 names; 9.0-10.8 circle turns 45 degrees. From 10.1 s every element is at full opacity (2.3 s of a complete composition; the last 1.5 s is identical except the slow circle turn).

## 8. Captions, 9. Sound

Not exercised (demo build, silent). Profile values, ASSUMED: caption = cream bar with 4 px ink top rule, 42 px 700 ink, current word in red (red on cream is 4.10: fails for small text, so use ink with a red underline bar instead). Sound: 96-116 BPM percussive electronic, wooden clacks on lock.

## 10. Images (agy)

None used. Photography is excluded by the profile; if one is ever needed, it must be a flat geometric illustration in the three primaries.

## 11. Must not

- Gradients, glow, shadows, borders, blobs, photos, emoji.
- Red or yellow as text colour on cream; yellow text on blue.
- A plain circle rolling with no marker inside (the roll is invisible).
- Text smaller than 30 px (one footer line excepted).
- A cover circle positioned off the frame centre.
- Fake data: shapes and names are generic and the "Minh hoạ" chip stays on screen for the whole video.

## 12. Traps seen in real builds (from the t169 build, 2026-11-14)

1. **Cover circle off-centre.** A 2600 px circle placed at `top:200px` has its centre at y 1500, so mid-cover the frame showed a red arch with a cream gap (frame at about 3.4 s). Centre it on the frame: `left:-760px; top:-340px` (frame centre 540, 960). Fixed.
2. **`text_occluded` from inspect at t 3.44 s** for the headline and sub line under the cover circle. Marking the cover with `data-layout-allow-occlusion` did NOT clear it; the attribute has to be on each occluded text element (`#t1`, `#sub1`). Also `canvas_overflow` (info) for the circle rolling in from x -950: put `data-layout-allow-overflow` on the section.
3. **Empty ink bar at frame 0.** The bar was visible from 0.0 s and its text only faded in at 0.7 s: an empty panel of 0.7 s (limit 0.5 s). Moved the text to 0.2 s (0.3 s fade): empty panel now 0.2 s. Frame 0 still shows only the chip and part of the circle: a roll-in start costs an almost empty first frame.
4. **Plain circle roll is invisible.** A solid circle rotating shows nothing; the 150 px inner square (yellow on red, blue on yellow) is what reads as a roll.
5. **Hold rotation hides in the last 1.5 s.** The circle still turns 45 degrees until 10.8 s. The marker square moves, but all text and tiles are static from 10.1 s, which satisfies "full composition" (nothing under 90% opacity).
6. **Bottom 260 px empty in scene 3 and scene 1** (content ends at y 1660 and 1670). With no captions the frame feels top-heavy; a caption band or a taller tile row would use it.
7. **Pivot with opacity looks like an outline.** At 5.3 s the panel (ink, rotating from 90 degrees) shows as a thin rotated frame with a half-transparent fill; it lasts about 0.2 s and is acceptable, but do not pivot a large dark panel while another element is still entering beside it.
8. **Red text fails.** red on cream is 4.10: caught by arithmetic before use; the profile's "current word in accent red" caption rule needs an ink word with a red bar instead.
9. **Tooling.** `frame_check.py` and `motion_tools.py probe` need a Python call that this build's sandbox did not approve; the check was done with ffprobe and an ffmpeg contact sheet (3 fps, plus a dense 8 fps sheet around each cut). Rerun `frame_check.py` where Python is allowed.
