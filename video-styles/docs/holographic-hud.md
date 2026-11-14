# Style: holographic-hud (9:16 Vietnamese tech-launch edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** A hardware or AI-product unveil told as a scan: one hero object, 3-5 short specs and one price (shape t032: "chip maker unveils a new accelerator with specs and price", Jev fit 0.77). Also good for security tools, analytics promos, "system analysing" openers. Not for warm human stories, quotes, long explainers, or stories with many equal numbers. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE 12 s silent demo sample (`samples/sample-t032.mp4`), not from a full video. **Voice-over, word timing, captions and sound rules were NOT exercised** (demo build): sections 8 and 9 are the profile's values, ASSUMED. Everything else is measured on the sample. Content on screen is generic and labelled "Minh hoạ".

Source of values: `styles/profiles/holographic-hud.yaml` (energy 3). Anything the profile does not give is marked ASSUMED.

Character: thin cyan linework over deep navy, as if seen through a visor. Rings spin up, amber brackets lock on the subject, readouts populate, a scan line sweeps. Line-based, no solid panels.

## 1. Tokens

```css
--bg: #030b17;      /* flat page */
--ink: #d9f6ff;     /* headline, values        17.5:1 on bg, 16.0 on panel (hand-computed WCAG) */
--accent: #35e0ff;  /* rings, unit text, sub labels  12.5:1 on bg, 11.4 on panel */
--amber: #ff9f1c;   /* ONLY lock brackets, lock label, price, badge   9.6:1 on bg, 8.8 on panel */
--mute-text: #8fd3e6; /* ASSUMED text-safe label colour  11.9:1 on bg, 10.8 on panel */
--line: rgba(53,224,255,0.6); /* ring and panel borders: decoration, not text */
--fill: rgba(53,224,255,0.06); /* panel fill */
```
`hyperframes validate` passed WCAG AA on all 10 text elements. The profile's `--mute` (alpha 0.35) is NOT text-safe: never use it for text; `--mute-text` is the replacement. Contrast values were computed by hand with the WCAG formula (no script could run in this build).

Rule held: cyan family plus amber only. Amber = confirmed / locked / price. Glow is `text-shadow 0 0 8px rgba(53,224,255,0.5)`, never heavier.

## 2. Fonts (local files only)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline | Rajdhani 600 uppercase | `SegUIVar.ttf` 700, uppercase via CSS, `letter-spacing:0.06em` | covers all Vietnamese letters (Ộ, Ă, Ế, Ớ rendered correctly in snapshots) |
| Readouts, labels, units, tags | Share Tech Mono | `CascadiaMono.ttf` 400/600, `font-variant-numeric: tabular-nums` | tone marks on Ỹ, Ợ, Ấ, Ê rendered correctly at 30 px in snapshots |
| Never | | `segoepr.ttf` | lacks most Vietnamese letters |

Rajdhani and Share Tech Mono are not installed: replaced by Segoe UI Variable and Cascadia Mono (same classes: squared grotesk, mono). `font-display: block`. Line-height of the 100 px uppercase headline is 1.15 so the tone marks of Ộ and Ế are not clipped (checked in snapshot).

### Type scale (1080 x 1920, px, measured in this build)

| Token | Font | Size | Notes |
|---|---|---|---|
| `.h1` headline | Segoe 700 uppercase | 100 / 1.15, +0.06em | 2 lines, 96 px left margin, "BỘ TĂNG TỐC" is ~730 px wide |
| `.sub` bracket-code sub label | Cascadia | 32 | accent, prefix `[SYS-0n]`, one per beat |
| `.pl` panel label | Cascadia | 30 | `--mute-text` |
| `.pv` panel value | Cascadia 600 | 68 (spec), 92 (price) | unit 36 / 44 in accent / amber |
| tag, badge, lock label | Cascadia | 30-32 | |
| footer | Cascadia | 24 | the single line under 30 px |

## 3. Safe areas and grid (1080 x 1920)

```
y 64   frame brackets (inset 64, arm 90, stroke 3)
y 98-146  tag [SYS-04] left, "Minh hoạ" badge right (amber outline)
y 168-398 headline, 2 lines
y 424-460 sub label (changes per beat)
y 490-1150 hero: concentric rings radius 330 / 290 / 250, centre (540, 820)
y 1170-1210 lock label (amber, centred)
y 1240-1596 spec panels, 2 x 2, each 436 x 172, gap 16 (x 96 and 548)
y 1622-1792 price panel, 888 x 170
y 1816-1840 footer (24 px) 
```
Everything sits inside x 96-984. Nothing in the top 98 px. No caption band was reserved (no captions in this build); with captions, the price panel must move up or the bottom panels must shrink: ASSUMED.

## 4. Layers, back to front

`#root` flat bg -> `#glow` (one radial gradient, pulses 0.7-1.0) -> `#scanl` (one repeating-linear-gradient scanlines, drifts 40 px over 12 s) -> `#hud` SVG (grid lines 5% alpha, frame brackets, hero group: rings, crosshair ticks, chip wireframe, amber lock brackets; sweep rects) -> text and panels. Heavy effects count: 1 gradient glow, 1 gradient scanlines, 0 blur, 0 clip-path (panel chamfers are SVG polygons, not clip-path). Render was clean, 9.8 MB.

## 5. Components

- **Panel**: div + inline SVG polygon, chamfer 18 px, fill 6% cyan, 1.5 px line 60%. Never solid.
- **Stepped bar**: 10 (or 24) 8 px segments, switched on one by one with `set`, in the same time as the counter.
- **Ring stack**: 3 circles (dashed 6/14, dash 190/42, dotted 2/12), each in an outer "step" group (entrance scale, +-15 deg beat step) and an inner group (continuous rotation: +100, -140, +60 deg over 12 s). Split in two groups so tweens never fight (lint warned when they shared one element).
- **Lock brackets**: 4 amber L-paths, half-size 150 around the 220 px chip.
- **Chip**: wireframe: outer square, inner die, 4 diagonals, 24 pins, solid core square pulsing 0.45-0.85.
- **Badge** "Minh hoạ" always on screen, top right.

## 6. Motion language

Energy 3. Eases: `expo.out` (ring scale-in 0.9 s), `power3.out` (counters 0.8 s, frame draw), `back.out(1.6)` (bracket lock 0.4 s), `power1.inOut` (sweeps), `sine.inOut` (pulses), `none` (ring rotation). No shake, no elastic, no flash layer. Flicker-on = stepped opacity 0, 1, 0.4, 1 over 5 frames (0.167 s) via `set`; flicker-off = 0.4 then 0 in 2 frames. Panels flicker on, then values count: counters start 0.15 s after the panel and finish within 0.8 s.

Micro-motion in every hold: ring rotation, core pulse, glow pulse, scanline drift, hero push 1.0 -> 1.07 over 3.4 s in the lock beat, repeating sweep line (0.9 s) over the hero, amber bracket pulse 1.0 -> 1.05.

## 7. Scene recipes (demo: 3 beats, 12.0 s, S = beat start)

- **B1 Boot + scan (0-3.6).** Frame brackets draw (0.05, 0.7 s). Headline flickers on at 0.1 and 0.3 (visible from frame 3). Rings scale 0.7 -> 1 and flicker on at 0.3 / 0.45 / 0.6. Chip draws 0.7-2.2. Sub label "ĐANG QUÉT CẤU TRÚC" at 1.0. Sweep over hero at 1.0 and 2.1. Scan panel at 1.1, counter 0 -> 100 % in 1.6 s with 24 stepped segments, done at 3.0 and held 0.5 s. Panel flickers off at 3.5.
- **B2 Lock + specs (3.6-7.2).** Amber brackets fly in at 3.6 (scale 1.8 -> 1, back.out(1.6), 0.4 s), middle ring steps 15 deg, hero pushes to 1.07. Sub label and lock label swap. Four spec panels flicker on every 0.28 s from 3.85, values count 0.8 s each (last one ends 5.65), all four held 1.5 s with micro-motion.
- **B3 Price (7.2-12.0).** Full-frame scan-sweep (band + bright line, 0.6 s) at 7.1, sub label swaps, outer ring steps -15 deg, hero eases back to 1.0. Price panel flickers on at 7.6, counter 0 -> 1.999 in 0.8 s (done 8.55), panel bumps 1.00 -> 1.02 -> 1.00. Footer line at 7.9. Held composition 8.6-12.0 (3.4 s) with two more sweeps, bracket pulse, ring rotation.

## 8. Captions (NOT exercised in this demo build)

Profile value, ASSUMED: chamfered panel rgba(3,11,23,0.8), 1 px line border, 40 px ink, current word accent, bottom band. Not tested.

## 9. Sound (NOT exercised)

Profile value, ASSUMED: cinematic electronic synth 100-122 BPM, soft bleeps, scan sweeps, lock-on chirp. No audio in this build; no beat sync.

## 10. Images

No agy image was used (generation could not be run in this build). The hero is pure vector (SVG), which suits the style: a wireframe chip needs no photo. If an agy image is ever used: a dark navy volumetric background with cyan linework, no text, kept under the rings at 100 % ink-safe contrast.

## 11. Must not

- No solid opaque panel, no warm colour except amber for lock / price / badge, no hand-drawn texture.
- No text below 30 px except ONE footer line (24 px).
- No glow heavier than 8 px; bake it if heavier.
- No text under `--mute-text` brightness (the profile `--mute` fails as text).
- No real company, spec or price: label generic content "Minh hoạ" on screen the whole time.
- No clip-path on more than a handful of elements; use SVG polygons for chamfers.
- Never clip text with a typing mask on a held frame; use flicker-on, not typeIn.

## 12. Traps seen in real builds (this build, measured)

1. **Pin ticks drawn in the wrong place.** The first build reused the top-pin coordinate for the side pins, so 12 ticks floated 270 px above the chip (seen in snapshot at 1.4 s). Rule: compute side-pin y from the chip's own y (732 + 33 i), and check the first snapshot at 3x zoom.
2. **Frame 0 half-built.** Pins and the translucent chip fill showed before the chip "drew" and the second headline line was missing. Fixed: chip parts at opacity 0 until 0.7 s, pins until 1.4 s, headline at 0.1 / 0.3 s.
3. **Tweens on one SVG element fight.** Continuous ring rotation plus a +-15 deg beat step plus the scale-in on the same group gave 5 `overlapping_gsap_tweens` warnings. Rule: outer group for entrance and steps, inner group for the endless rotation (0 warnings after the split).
4. **Label box overlapped the value box.** `inspect` flagged `content_overlap` for the price label and the 104 px value (box 40 px vs label bottom 51 px). Fix: 92 px value, line-height 1, top 56 px; 0 issues after.
5. **Text-safe mute.** The profile `--mute` (alpha 0.35) is a line colour, not a text colour. Panel labels use `#8fd3e6` (10.8:1 on the panel).
6. **Bottom of the frame empty while the top is full.** In B1 y 1240-1790 held only one panel and in B2 the price slot (y 1622-1792) stayed empty from 3.85 to 7.6 s (3.75 s). It does not break the acceptance rule (no empty panel is drawn) but reads unbalanced. Rule: either draw the price panel's outline early with a "chờ" state, or place hero lower (centre 900) in B1-B2. Not fixed in the demo.
7. **Counters sampled mid-count.** The 1.5 fps frame sheet caught 47 %, 96 %, 108, 9 GB, 224 W, 1.980 USD: that is the 0.8 s count passing, not a held frame; all values are final 0.8 s after their panel starts (4.8 s at the latest for specs, 8.55 s for price) and the last 3.4 s are complete. Counters must be at most 0.8 s and finish before any hold.
8. **Tools that could not run.** In this build the project-local `frame_check.py` needed numpy (missing), and Python/node scripts and the agy `image` command were blocked by the permission mode. The frame check was done by eye on a 1.5 fps ffmpeg sheet plus 8 HyperFrames snapshots. Rule: check `python3 -c "import numpy"` before the build.
9. **Glow and gradient limits.** Only 2 gradient elements and no blur were used; render took 12.2 s for 12 s of video and the file is 9.8 MB (10.3 MB reported by probe). No black frames.
