# Style: neon cyberpunk (9:16 synthwave release edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY, observed in one demo build, topic shape t136, Jev 0.81):** hype and atmosphere pieces with ONE hero title and ONE date or number: music and album releases (synthwave, darksynth), game and event launches, nightlife, web3 launches. Observed: it carries a "title + 3 list rows + release date + CTA" story well. Not for quotes, charts, testimonials, daylight or warm human stories, dense numbers (profile `avoid`).

**Status.** Written 2026-11-14 from ONE demo build: a 12.0 s silent sample, 1080x1920, 30 fps, 9.9 MB, 3 beats. **Voice-over, caption and sound rules were NOT exercised** (demo build: no VO, no word timing, no music). Sections 7 (captions) and 8 (sound) are copied from the profile and marked UNTESTED. Content in the sample is generic and labelled "Minh hoạ".

Marks: **UNTESTED** = from profile, not built. **SUBST** = a profile font is not installed and a local one replaces it. **ASSUMED** = invented here.

Profile: `skill/references/styles/profiles/neon-cyberpunk.yaml` (energy 5, dark). Loud and nocturnal: magenta and cyan tubes over near-black violet, a striped sun on a grid horizon, title that buzzes on, glitch slice cuts.

## 1. Tokens (contrast = WCAG, computed by hand from the hex values)

```css
:root{--bg:#07040f;--ink:#f2eaff;--mag:#ff2bd6;--cyan:#00f0ff;--yel:#fcee0a;--pur:#3a0ca3;--mute:#7d6b9e;
 --panel:#12062b /*ASSUMED: panel fill, sun slits, slice bars*/}
```

| Token | On `--bg` | On `--panel` | Use |
|---|---|---|---|
| ink #f2eaff | 17.4 | 16.6 | all reading text |
| cyan #00f0ff | 14.4 | 13.7 | kickers, numbers, edges, bars |
| mag #ff2bd6 | 6.4 | 6.0 | big display words (>= 100 px), CTA, glows |
| yellow #fcee0a | 16.8 (bg-dark text ON yellow) | - | ONLY the "MINH HOẠ" tag, dark `--bg` text on it |
| mute #7d6b9e | **4.32 FAILS 4.5** | 4.0 | never text; borders/decor only |
| purple #3a0ca3 | 1.7 | - | fills only (sky, slice bars) |

Panel fill is `rgba(7,4,15,.94)` (>= 90% opacity). Glow is a layered `text-shadow` driven by one CSS variable `--g` on `#root` (px, base 14, kick pump 26 / 32 on bar downbeat), chroma split by `--rgb` (0 to 12 px, stepped).

## 2. Fonts (SUBST)

Profile fonts (Orbitron, Chakra Petch, Share Tech Mono, Be Vietnam Pro) are not installed. Used (glyph coverage 0 missing for all Vietnamese capitals and lower case, from the owner docs' fontTools test of the same files; confirmed visually in snapshots: ĐÊM, MỞ MÀN, ĐẶT NHẮC LỊCH, HOẠ, Ướt, Đường render with all marks; my own fontTools run was blocked in this session):

| File | Role |
|---|---|
| `SegUIVar.ttf` weight 700 | headlines uppercase (230 / 130 / 310 px, +0.04em), row titles 58 px, sub line 76 px. SUBST for Orbitron 800: much softer; the neon glow does the work |
| `CascadiaMono.ttf` weight 700 | kickers 36 px, track numbers 60 px, durations 36 px, tag 34 px, pills 40-54 px. SUBST for Share Tech Mono |
| `cambriai.ttf` | unused |
| `segoepr.ttf` | NEVER (92 Vietnamese glyphs missing) |

The "Tube flicker" is stepped opacity (autoAlpha sets at 0.05 s steps), not a font trick.

## 3. Grid and safe areas (1080 x 1920)

- Side margin 72, content width 936. y 0-196 empty except nothing; tag at y 196. y 1650-1920 empty (grid floor only).
- Horizon at y 1180 (cyan line 6 px). Sun (600 px circle) clipped at the horizon, top at y 790. Skyline y 1010-1180. Floor y 1180-1920.
- Beat 1: kicker y 290, headline y 350 and 545 (230 px, rotate -4 deg), pill y 1410.
- Beat 2: kicker y 290, headline y 350/470 (130 px), rows 160 px high at y 680/860/1040, equaliser y 1250-1450, total pill y 1500.
- Beat 3: panel 936 x 720 at y 430 (rotate -3 deg), CTA pill y 1290-1420.
- Lowest content edge 1596 (beat 2), 1420 (beats 1 and 3). The floor below is decoration only.

## 4. Layers, back to front

1. `#sky` gradient + horizon glow (static). 2. `#sunwrap` sun with 6 slits, `#city` SVG skyline (static, seeded windows), `#horizon`, `#floor` 3D grid (perspective 520 px, rotateX 74 deg, background scrolls 840 px over 12 s, `ease:"none"`), `#floorfade`. 3. Scenes `#s1 #s2 #s3` (z 10, one `display:block` at a time). 4. Tag z 40. 5. `#vig` + `#scan` (z 29-30, static). 6. Slice bars z 35, `#flash` z 36. Everything sits in `#world` (oversized 1.2x so push and shake never show an edge) inside `#stage` (jitter target).

## 5. Components

- **Neon word** `.neon-m/-c/-w`: colour + 4 layers of text-shadow (rgb split +/-, 4 px white core, `--g` and `--g`*2.2 glow).
- **Panel** `.panel`: `rgba(7,4,15,.94)`, 2 px cyan border, radius 10, glow 14 px, inset purple. **Pill**: same with radius 999.
- **Track row**: 936 x 160, number (mono 60 cyan), title (58 ink, top 18), duration (mono 36 cyan, top 100), play glyph right.
- **Equaliser**: 17 tubes 36 px wide, pitch 56, alternate mag/cyan, `scaleY` from the bottom, seeded.
- **Tag** "MINH HOẠ": yellow, skewX -8, mono 34 px, top-left, whole video.
- **Slice bars**: 6 bars 320 px high, purple gradient, 6 px magenta lower edge, alternate left/right origins.

## 6. Motion language (measured on the build)

- Title buzz-on: stepped autoAlpha on/off over 0.28-0.30 s plus an x slide 60 px `expo.out` 0.5 s. First title word at 0.30 s, second at 0.60 s.
- Visual metronome (no audio): 140 BPM, beat 0.4286 s, 28 beats. Each beat: `--g` 14 to 26 (32 on every 4th) in 0.07 s, back `power2.in`; sun scale 1.015 (1.03 on bar downbeat). Without music this is only a pulse; with music re-fit to the grid. UNTESTED against audio.
- Camera: beat 1 push 1.00 to 1.06 over 3.4 s linear; beat 2 zoom-punch 1.3 to 1.0 `expo.out` 0.5 s then drift to 1.04; beat 3 punch 1.2 to 1.0 0.45 s then drift to 1.035. Adjacent beats never share the move.
- Cut (the signature): jitter of `#stage` x +/-14 px in 0.04 s steps for 0.16 s, chroma split `--rgb` stepped 9,0,12,4,10,0 over 0.22 s, 6 slice bars cover in 0.26 s `expo.inOut` (stagger 0.02), scene swap hidden under the bars, bars exit in the opposite direction 0.26 s, `#flash` 0.7 to 0 in 0.12 s. Total 0.55 s; the frame is fully covered for about 1 frame.
- Row glitch-in: x +/-90 px and skewX +/-14 to 0, `expo.out` 0.4 s, border magenta to cyan 0.5 s, stagger 0.3 s. No clip-path, no mask: nothing is cut.
- Scramble: digits cycle seeded pool "0123456789#%/<>" at 24 steps/s and resolve left to right; 0.6-0.8 s; the element shows its final text at frame 0 of its tween and again after.
- Holds: grid scroll, sun pulse, equaliser, panel rotation drift -3 to -2.2 deg, CTA pulse 1.00-1.03 (6 yoyos).

## 7. Captions (UNTESTED)

Not exercised. Profile: dark panel `rgba(7,4,15,.82)` 1 px cyan edge, 42 px 700 ink, current word magenta with glow. Panel opacity .82 is under the 90% rule: use .94 if built.

## 8. Sound (UNTESTED)

Not exercised. Profile: darksynth 128-150 BPM, glitch zaps on cuts, bass hit on drops. The sample's cuts at 3.58 s and 7.88 s are 8.4 and 18.4 beats at 140 BPM: if music is added, move cuts to a bar line (multiples of 1.714 s).

## 9. Scene recipes (the three beats of t136, sample 12.0 s)

**R1 Hook, 0-3.6 s.** Sun rises 140 px (`power3.out` 1.3 s), kicker, two-word title (ink-magenta glow "ĐÊM", cyan "NEON", rotate -4 deg), pill with generic facts "10 BÀI · 42 PHÚT · SẮP RA MẮT" at 1.2 s. Ends with jitter + split + slices (3.15-3.58 s).
**R2 Tracklist, 3.6-7.9 s.** Zoom-punch in, kicker 3.7, headline flicker 3.75/3.95, rows glitch in at 4.2/4.5/4.8, durations scramble (0.6 s each), equaliser grows 5.2, total pill 5.9 with scramble to "42:18" resolved by 6.7, hot-edge pulses on rows at 6.6/6.8/7.0. Cut 7.45-7.88.
**R3 Release, 7.9-12.0 s.** Panel slams in (scale 1.25 to 1, rotate -8 to -3, 0.45 s), date "12.12" scrambles 8.25-9.05 (310 px magenta), "Nghe thử đêm nay" 9.2, CTA "ĐẶT NHẮC LỊCH" pop-settle at 9.3. Full composition from 9.7 s to 12.0 s (2.3 s), no fade-out.

## 10. Transitions

Used: chroma-glitch + slice-wipe + zoom-punch combined (above). Profile also lists neon-flicker (used for titles, not as a cut). Never a plain fade.

## 11. Images (agy)

Not used: `motion_tools.py image` needed approval that was not available in this session, and the sun, skyline and grid are better as exact CSS/SVG. If used: "vertical synthwave night landscape, magenta and cyan neon sun with slit bars over a glowing grid floor, no text, no logos, no people", as a baked backdrop only; agy never draws type.

## 12. Must not

Warm or pastel palette; mute #7d6b9e as text; yellow beyond the tag; real artist, label, album or platform names (use generic and "Minh hoạ"); SVG filters left attached (the build uses none: glitch is text-shadow offsets and bars); `repeat:-1`; text under 30 px (smallest here 34 px); fade-out at the end.

## 13. Traps seen in real builds (this build, 2026-11-14)

1. **Profile `mute` fails text contrast.** #7d6b9e is 4.32:1 on `--bg`. Kept for decoration only; every small text is ink or cyan.
2. **Validator contrast false positive on the skewed tag.** `hyperframes validate` reports "MINH HOẠ 1:1" at 5 times though the real contrast is 16.8:1 (dark on yellow). Ignore after measuring by hand; do not recolour.
3. **`content_overlap` between row title and duration.** Title (58 px) at top 36 overlapped the duration at top 100: fixed by moving the title to top 18. Same warning for `#k3` over `#date` (310 px at line-height .95): date moved from top 130 to 170.
4. **Decorative oversize flagged.** Sun (214 px below its mask), skyline (4 px), grid (1490 px each side) trigger `container_overflow`: mark them `data-layout-allow-overflow`; 34 warnings became 0 real issues.
5. **Overlapping `#world` scale tweens** (punch 7.90-8.35 vs drift from 7.90): lint warning; the drift now starts at 8.4 s. Plan camera as sequential tweens, not parallel.
6. **Scrambled number caught mid-count.** At 8.5 s the date read "38.60". Resolved by 9.05 s and held 2.95 s as "12.12"; this is allowed (in motion), but a snapshot at a random time will show it: frame-check only held frames.
7. **Sun hidden in beat 3.** The 720 px panel covers the sun; only a faint glow remains. Accepted (panel is the hero); if the sun must stay, lower the panel to y 520 or shrink to 600 px.
8. **Grid too sparse at the near plane.** With 140 px cells at rotateX 74 only 2 horizontal lines are visible at once. Use 100 px cells for denser motion.
9. **Tooling.** In this session `python3` scripts (`frame_check.py`, `motion_tools.py`) and `sed -i` / `cp -R` were refused, so probe and frame check ran with ffprobe, ffmpeg (blackdetect, freezedetect, tile sheets) and Read on PNGs. Re-run the official frame check when allowed.

## 14. Numbers of the build

Render 13.6 s for 12.0 s; 9.9 MB; 360 frames; ffprobe 1080x1920, 30 fps, h264, 12.000 s. No black frame (blackdetect 0.05 s) and no freeze (freezedetect 0.3 s) found.
