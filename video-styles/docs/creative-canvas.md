# Style: creative-canvas (9:16 shared-board edition, first draft from a demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in the t142 build (Jev fit 0.82).** Stories where several people look at, mark up and change ONE shared object: architects and clients on a floor plan, design review, a team editing a plan or process board, a product-design workflow. The camera can go "plan close-up -> whole board", so it suits a story with an object plus comments. Not for: single big numbers, enforcement, bad news, data dashboards, terminal/code stories (profile `avoid: terminal, spec`). Tier 2 never widens tier 1.

**Status and what was NOT exercised.** Written 2026-11-14 from ONE 12 s silent demo (`samples/sample-t142.mp4`, 1080x1920, 30 fps, text plus motion only). There was no voice-over, no word timing, no music and no captions in this build. So section 8 (captions) and section 9 (sound) are copied from the profile and are UNTESTED; any number there is ASSUMED. Everything else carries measured numbers from this build. Marks: **ASSUMED** = not measured. **SUBST** = a named font is not installed, a local one replaces it. **DEVIATION** = knowingly differs from the profile.

Profile: `skill/references/styles/profiles/creative-canvas.yaml` (energy 3, light mode, brand-inspired). Character: the story happens on a shared canvas; named cursors, selection handles, frames that zoom and snap.

DEVIATION 1: profile cursor colour c1 `#d6457a` fails text contrast (white on it 4.21:1, ink 3.96:1). Cursor and tag use `--c1-dk #b0356a` (white 5.89:1); raw c1 is kept for fills (guide line, sticky tint).
DEVIATION 2: profile says Inter and Be Vietnam Pro; neither is installed (SUBST, section 2).
DEVIATION 3: profile 11-14 px frame labels (24 px at 2x) are too small for a phone; labels are 32 px on screen (section 3).

## 1. Tokens (contrast computed by hand with the WCAG formula, because script execution was blocked in this session; `hyperframes validate` also reported "25 text elements pass WCAG AA")

```css
:root{
  --bg:#f5f5f5;          /* canvas; ink on it 15.3:1 */
  --ink:#1e1e1e;         /* 16.7:1 on white */
  --mute:#5c5c5c;        /* DEVIATION from profile #8c8c8c (3.36:1 on white FAILS); 6.69:1 on white, 6.13 on bg */
  --frame:#ffffff; --line:#e6e6e6;
  --accent:#2f7df6;      /* FILL/outline only: 3.90:1 on white fails for text; white on it 3.90 */
  --accent-dk:#1b5fd1;   /* accent TEXT: 5.83:1 on white; white on it 5.83 */
  --accent-soft:#e3eefe; /* chip fill; accent-dk on it about 5.0 */
  --c1:#d6457a;  --c1-dk:#b0356a;  /* c1 fill only; c1-dk tag/arrow, white 5.89:1 */
  --c2:#e39b2d;          /* ink on it 7.13:1 (tag with INK text, sticky) */
  --c3:#2a9d8f;          /* ink on it 5.02:1; white on it 3.32 FAILS, so never white text on c3 */
  --c4:#5b5fc7;          /* white on it 5.38:1 */
}
```
Rules: text only from `--ink --mute --accent-dk` (and white on c1-dk / c4 / accent-dk, ink on c2 / c3). Never put white text on c2 or c3. Sticky tints (`#cfd1f3`, `#f6cfdf`) carry ink text, above 11:1 (ASSUMED from lightness, all clearly above 7). Room fills in the plan are pastel (`#e9f1fe #fdf1dc #e3f3f0 #f1edfa #f6efe6`) with `--mute` labels: 6:1 or better. One accent; no dark mode, no neon, no gradients.

## 2. Fonts (Vietnamese diacritics check)
| File | Missing Vietnamese glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 (all lines rendered with correct diacritics in the frames: "Phòng khách", "Sửa ngay trên bảng", "Cửa sổ phía nam lớn hơn?") | everything read: headline 700, labels/tags/stickies 600. SUBST for Inter |
| `CascadiaMono.ttf` | 0 (kicker "MINH HOẠ · BẢNG CHUNG" renders) | the 30 px kicker only, +0.06em |
| `cambriai.ttf` | not used | - |
| `segoepr.ttf` | lacks Ơ ơ Ư ư and hooked vowels | NEVER used |

The check was visual on rendered frames (glyph-level fontTools test was not run: script execution blocked). SegUIVar has no weight above 700.

## 3. Type scale, safe areas and grid (1080 x 1920, measured)
| Role | Size on screen | Notes |
|---|---|---|
| Headline | 88 px / 94 line, 700, two lines, second line in `--accent-dk` | box x 72, y 190-380, 936 wide |
| Kicker | 30 px mono | y 132; always contains "MINH HOẠ" |
| Cursor tag, frame label, dock text, chips | 30-32 px | counter-scaled, see below |
| Room labels / sticky text | 56 world px; 31 px on screen at the zoom-out (scale 0.55) | the smallest text in the video, on purpose |
| Reply bubble | 38 world px, 47 px at zoom 1.25 | |

Rule that matters: **everything in screen space must be at least 30 px at EVERY camera scale.** World text is sized so that at the smallest scale (0.55) it is still >= 30 px (56 x 0.55 = 30.8). Cursors, tags, frame labels, selection borders and handles are counter-scaled with a CSS variable `--inv` on `#world` (inv = 1/scale: 1.0, 0.8, 1.818), tweened together with the camera. `--inv` is a tween, not an `onUpdate` callback (callbacks can be suppressed by a paused seek).

Layout (y): 0-130 platform zone empty; kicker 132; headline 190-380; board zone 470-1420; dock 1500-1584 (presence pill: 3 dots, "Lan, Minh, Hoa đang xem", chip "Minh hoạ"); 1584-1920 empty. Lowest content edge in the hold frames: y 1584 (dock), board ends 1415.

World layout (px): frame A (60,300) 800x800, frame B (1060,300) 800x800, notes frame N (60,1264) 1800x700; plan SVG 720x720 inset 40; sticky 500x420, x = 110 / 710 / 1310, y 1404 (3 x 500 + 2 x 100 gap = 1700 fits inside N's 1800). Camera states `{x,y,scale}`: C1 {80,220,1.0} frame A fills 800 of 1080; C2 {-35,105,1.25} plan fills the width; C3 {20,335,0.55} whole board. An extra slow push `#push` 1.00 -> 1.035 over the whole 12 s is the micro-motion for every hold.

## 4. Layers, back to front
`#bg` flat `--bg` -> `#dots` (one 3600x3600 element, CSS radial-gradient dot grid, 48 world px pitch, `#c9c9c9`, inside the world so it scales; 1 element so far below the ~40-gradient renderer limit) -> frames (A, B, N) -> plan SVGs, connectors (`#conn`), guide line, marquee, selection outline + handles -> sticky notes + reply bubble -> cursors (top of world) -> screen-space HUD: `#kick`, `#head`, `#dock` -> `#fade` (bg-coloured, 0.3 s in at the start only; no end fade, the last frame is a full composition).

## 5. Components
- **Frame**: white, 2 px `--line`, no radius, no shadow. Label above top-left, 32 px, `--mute`.
- **Floor plan (SVG, drawn in code, never an image)**: 10 px ink walls (`stroke-linecap: square`), 5 pastel rooms, grey 6 px furniture outlines (1 circle, 2 rectangles), room labels 56 px. Built by one `plan(k, wallX)` function used for A and B, so a wall edit is a set of `attr` tweens (x1/x2/width/x of lines, rects and labels).
- **Cursor**: 30x42 arrow in the collaborator colour with a 3 px white stroke, plus a tag pill (46 high, radius 23, 30 px 600) at (+26,+34). Lan = c1-dk with white text, Minh = c4 with white, Hoa = c2 with INK text. Names are fictional first names.
- **Selection**: 3 px accent outline (screen px via `--inv`), four 28 px white handles with 4 px accent border. Marquee: accent at 12% fill plus 3 px accent border.
- **Sticky**: flat, 500x420, 56 px 600 ink, `box-shadow 0 8px 0 rgba(0,0,0,.08)`, rotation -1.5 to +2.5 deg. Hoa (client) = c2 solid, Minh = c4 tint, Lan = c1 tint: the colour tells who wrote it.
- **Reply bubble**: white pill, 3 px c1 border, "Lan:" in c1-dk bold.
- **Connector**: 6 world px accent line with an arrowhead, drawn with `strokeDashoffset` (pathLength 1) in 0.5 s.
- **Dock**: presence pill with dots (c1-dk, c4, c2) and a "Minh hoạ" chip (accent-dk on accent-soft).
Not replicated: any real app toolbar or icon (profile constraint).

## 6. Motion language
Energy 3. Eases used: `power3.out`, `power3.inOut` (camera, 0.8-0.95 s), `power2.inOut` (cursor y, wall drag), `expo.out` (cursor x, headline rise), `back.out(1.4-1.6)` (handles, sticky pop), `back.out(2)` (wall snap), `sine.inOut` (idle nudges), `none` (fade, push-in). No elastic, no shake, no flash, no rotation of the camera (profile constraint).
- **Cursor travel**: `x: expo.out` and `y: power2.inOut` with the same duration (1.1 s) gives an arc; three cursors arrive 0.25 s apart.
- **Camera**: only pan/zoom of `#world` between C1, C2, C3; zoom range 0.55-1.25 (profile 0.4-2.0).
- **Marquee -> select -> drag -> snap**: marquee grows 0.5 s `power2.out`; wall turns accent and 2 handles pop (0.3 s, stagger 0.06); drag 0.55 s to 504, snap 0.2 s `back.out(2)` to 500; guide line (c1 dashed) flashes 0.08 s in, fades 0.35 s.
- **Headline swap**: out 0.15 s `power2.in` (y -22), in 0.5 s `expo.out` (y 28 -> 0) 0.1-0.15 s later: the outgoing text is gone within 0.15 s.
- **Match-move**: the comment sticky is created on the plan at scale 0.55 and, during the zoom-out, tweens to its slot in the notes frame (scale 1, 0.85 s `power3.inOut`): the same element, no rebuild.
- **Holds**: continuous 1.00 -> 1.035 push on `#push`; sticky rotation yoyo +-2.5 deg; cursors nudge 12 px with sine yoyo (even repeat count so they end on their mark).

## 7. Scene recipes (the 12 s sample; times in seconds)
**R1 Board arrives (0-3.5, camera C1).** 0 fade-in 0.3 s; headline 1 rises 0.1; kicker and dock at 0.1-0.2 (dock rises 24 px); frame A is already full (plan, labels) from frame 0. Cursors Lan 0.2, Minh 0.45, Hoa 0.7 arrive; avatar dots pop (back.out(1.6)) as each arrives; Hoa clicks (8 px dip) 2.1; Lan selects frame A at 2.7 (outline, then handles 2.75 stagger 0.05).
**T1 zoom into the frame (3.5-4.3).** Camera C1 -> C2 0.8 s `power3.inOut`; selection and label fade 0.2 s first; headline swap 3.5/3.65.
**R2 Edit on the board (3.7-7.9, camera C2).** Lan to the wall 3.7; marquee 4.45-4.95; wall selected 5.0; drag 5.5-6.05 (wall, 3 room fills and 3 labels move together); snap + guide flash 6.0-6.6; deselect 6.5; Hoa's sticky pops 6.5 (back.out(1.4)); Lan's reply bubble 7.0.
**T2 zoom out reveal (7.95-8.9).** Camera C2 -> C3 0.95 s; headline swap 7.9/8.05; bubble out 0.15 s; frames B and N fade in (0.3 s, stagger 0.1) from 8.1, i.e. while the camera is still moving, so no empty board is ever shown; labels return 8.4.
**R3 Whole board (8.0-12, camera C3).** Sticky flies to its slot 8.0-8.85; connectors A->B 8.7, A->N and B->N 9.0 (stagger 0.15); stickies 2 and 3 drop (y 1250 -> 1404, back.out(1.3)) 9.0 and 9.35; cursors settle under their notes 8.2-9.7. Last 1.5 s: full static-ish composition (only push-in and nudges).

## 8. Captions: NOT EXERCISED (no voice in this demo)
Profile only (ASSUMED): white pill with 1 px border, radius 8, 40 px Be Vietnam Pro 600 ink, current word accent. Here Be Vietnam Pro is not installed, so SUBST SegUIVar 600; the accent word must use `--accent-dk`. The caption band of a voiced edition must be planned: the dock (y 1500-1584) would have to move or the caption sit at y 1590-1700.

## 9. Sound: NOT EXERCISED
Profile only (ASSUMED): indie-electronic 100-120 BPM, soft clicks, snaps and plops. Natural SFX anchors seen in the build: cursor arrival, click dip, marquee release, wall snap (6.05), sticky pop/drop (6.5, 9.0, 9.35).

## 10. Images
No generated image was used. agy cannot draw exact geometry, so the floor plan MUST be SVG. If one image is ever wanted, use it only for a hero outside the board (never as a plan, never with text or people).

## 11. Must not
- No camera rotation; pan and zoom only. No real app toolbar or icons. Cursor names are fictional first names.
- No text under 30 px on screen at any scale: counter-scale screen-space things, size world text for the smallest zoom.
- No white text on c2 or c3; no raw `--mute #8c8c8c` or raw accent as text; c1 text only as c1-dk.
- No label inside a layout-checked box that it leaves on purpose without `data-layout-allow-overflow` (frame labels sit above the frame).
- No invented spec, price, area or dimension on the plan; illustrative content carries "Minh hoạ" on screen from the first frame to the last.
- No dark neon, heavy texture, hard beat cuts, emoji.

## 12. Traps seen in real builds (this build, 2026-11-14, measured)
1. **A world-positioned element with both `left/top` and a GSAP `y`.** Stickies 2 and 3 had `top:1404px` and `y:1404`: `hyperframes validate` reported them 85-91 px below the canvas. Rule: elements moved by GSAP get `left:0;top:0` and all placement in `x/y`.
2. **Arithmetic of the zoom-out frame.** Three stickies of 540 px plus gaps (1980) did not fit a 1800 px notes frame; the third was cut at the right edge in the t=11.5 snapshot. Fix: 500 px stickies at x 110/710/1310. Rule: compute the whole-board layout in world px first, then pick the scale.
3. **Counter-scaled UI can still hit the edge.** The Lan tag touched x = 535 of 540 (half-size view) at the end; moved the cursor from world x 1800 to 1580. Rule: cursors parked near the board edge need tag width + 26 px of room.
4. **Handles too small.** 16 px handles (inv-scaled) were invisible in the 0.5x contact sheet; 28 px with a 4 px border read. Rule: selection handles >= 28 px on screen.
5. **A connector crossing a label.** The A -> N arrow at world x 460 ran through the "Ghi chú của nhóm" label; moved to x 700. Rule: connectors leave a frame away from its label corner.
6. **Label overflow flagged as errors.** `validate` marked 7 `text_box_overflow` errors for labels placed above frames; `data-layout-allow-overflow` on label and frame clears them. The 11 `canvas_overflow` infos came from cursors that wait off-screen before arriving; they are intentional.
7. **Profile `mute` fails.** `#8c8c8c` on white is 3.36:1; use `#5c5c5c` (6.69:1).
8. **frame_check.py could not run** on this Mac (no numpy/PIL for the default python); an ffmpeg `fps=2, tile=6x4` contact sheet was reviewed by eye instead (selfcheck). Install numpy and Pillow before the next build.
9. **Plan edit is subtle at the finale.** A (wall 500) and B (wall 440) differ by 16 px at scale 0.55; they read as nearly equal. Rule: when the finale must show a before/after, change more than 60 world px or add a label ("trước/sau").

## 13. Known risks (not exercised)
Voice-led timing (word anchors for cursor actions, captions vs the dock) and music beat sync were not tested; the camera/inv tween pair drifts slightly mid-zoom (cursor size not exactly constant during the 0.8 s move; invisible in the sheet but not measured).
