# Style: retro-crt-broadcast (9:16 Vietnamese news edition, written from the first real build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** Anniversary and "looking back" stories where the thing itself is broadcast, media or nostalgia: a network or channel anniversary with a special programme, a retro console or product returning, a reopened retro venue (diner, cinema, arcade), a countdown to a dated live event. It carries a story that has 3-6 short facts, dates and one or two numbers, each of which can sit on a teletext row or a counter. Not for: bad news, deaths, enforcement, finance dashboards with many numbers, dense policy text, or anything where scanlines, static and a "power off" would read as mocking the subject. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 12 are the design as built and measured. Section 13 lists the traps of THIS build with numbers; where two sections disagree, section 13 wins.

**Status.** Written 2026-11-12 by the build that made `final.mp4` (57.3 s, story: NBC 100th-anniversary special) and the two samples (t057 mini console, t120 seventies diner). Not yet reviewed by the owner. Everything not given by `styles/profiles/retro-crt-broadcast.yaml` is marked **ASSUMED**; a substituted font is marked **SUBST**; a knowing departure from the profile is **DEVIATION**.

Profile: energy 3, dark. A signal coming in off an old tube set. Scenes are "channels": the HUD channel number changes on every cut (CH 01 ... CH 06), a cut is a static burst, a section opens with SMPTE bars, and the ending can collapse to a line and a dot. Format 1080 x 1920, 30 fps, Vietnamese voice-over (VieNeu, no music), estimated-word karaoke captions.

DEVIATION 1: the profile's "outro powers off on the last downbeat" collides with acceptance rule 5 (the last 1.5 s must show a full composition). The power-off is used BETWEEN scenes (s5 off, s6 on), never at the very end. In a silent sample clip it may close the clip.
DEVIATION 2: caption box alpha .94, not the profile's .85 (acceptance rule 7: nothing below 90 % opacity for more than 0.2 s).
DEVIATION 3: no music, so `beat_response` is replaced by a slow rolling sync bar and the 1 Hz REC dot.

## 1. Tokens (contrast = WCAG 2.x relative luminance, computed by hand with the formula; no script runtime was available in this build)

```css
--bg:#0b0d0a;    /* page, L = 0.0038 */
--ink:#e8f5d0;   /* text, 17.1:1 on bg, 18.4:1 on #000 (caption box) */
--acc:#ffb000;   /* amber: hero numerals, lower-third bar, chips; 10.65:1 on bg; dark text on it 10.65:1 */
--pho:#39ff88;   /* phosphor green: derivation lines, teletext header bar, grid cells; 14.7:1 on bg; dark text on it 14.7:1 */
--sig:#ff3b3b;   /* signal red: REC dot, LIVE bug; 5.52:1 on bg; dark text on it 5.52:1; WHITE text on it only 3.53 (fails: never white on red) */
--blue:#2f6bff;  /* 4.34:1 on bg: FILL ONLY (chromatic fringe, SMPTE blue), never text */
--mute:#858d77;  /* profile rgba(232,245,208,.55) flattened onto bg: 5.62:1; source footer only */
SMPTE bars (bumper only): #bfbfbf #bfbf00 #00bfbf #00bf00 #bf00bf #bf0000 #0000bf (75 % bars)
```
Rules: every text colour is one of ink, acc, pho, mute, or bg-dark on acc/pho/sig. Blue is never text. Amber glow `text-shadow 0 0 14px rgba(255,176,0,.6)` plus a 3 px red / blue fringe is used on hero numerals only (3 per video). Nothing semi-transparent that holds: mute is a flat colour, panels are `#050604`, caption box `rgba(0,0,0,.94)`.

## 2. Fonts (SUBST: the profile's VT323 / Archivo Black / IBM Plex Mono / Be Vietnam Pro are not installed)

| Role | Profile asks | Used | Vietnamese check |
|---|---|---|---|
| Hero numerals, teletext rows, chips, HUD, timecode | VT323 / IBM Plex Mono | `CascadiaMono.ttf` weight axis 200-700, 600-700 used | Rendered check on screen: Ơ Ư Ă Â Ê Ô Đ and every tone mark in "TRƯƠNG", "TRỰC TIẾP", "KỶ NIỆM", "THỜI LƯỢNG", "GIỜ", "ĐỊA ĐIỂM", "NHÀ HÁT", "TẠP KỸ" all drew correctly in 1080 px frames; no tofu. (fontTools was not runnable here, so the check is visual on the real strings, not a full glyph table.) |
| Lower-third titles, captions, footer | Archivo Black / Be Vietnam Pro 600 | `SegUIVar.ttf` weight axis 300-700: titles 700 uppercase, captions 600, footer 500 | "TRÒN MỘT TRĂM TUỔI", "THẬP NIÊN", "ĐẾM NGƯỢC" and the whole caption text drew correctly |
| Quote | none | `cambriai.ttf` not used (no quote in this story) | - |
| `segoepr.ttf` | - | NEVER (92 Vietnamese letters missing per the owner docs) | - |

Cascadia Mono is a wider, more modern face than VT323: the hero numerals look clean, not pixel-chunky. The look stays retro because of glow, fringe and scanlines. Cascadia draws the "-" hyphen fine; `-` replaces "−" and arrows (not verified in the font): write derivations with a plain hyphen.

## 3. Type scale, safe areas and grid (1080 x 1920)

- Tube bezel: baked `tubemask.png`, black outside a rounded rect inset 28 px, radius 56 px. Everything important stays inside x 96-984 (888 px, margin 96 = profile inset).
- HUD y 112-158: REC dot (26 px, x 100) + `REC 00:SS:FF` timecode (Cascadia 34 px, x 140) on the left; channel `CH 0n` (34 px amber, right edge x 980) on the right.
- Body zone y 200-1320. Caption box top 1400, width 888, 44 px / 56 px line, 1-2 lines. Footer source line y 1646, Seg 500 30 px (the only footer line). y 1700-1920 empty (platform UI).
- Type scale: hero numeral 360 px (s1 "100"), 440 px (s5 "28"), 288 px (s4 date), 230 px (s3 "75"), 200 px (s6 "4 GIỜ"/"3 GIỜ"); label next to a hero 96-120 px; teletext row 38 px / 50 px; chip 30-32 px; lower-third bar 40-46 px Seg 700 uppercase; derivation line 32-40 px; HUD 34 px; footer 30 px. Smallest authored text = 30 px. (Profile asks hero 72-120 px: scaled up 3-4x for a phone.)
- Layout blocks (y): media monitor inset 200-760 (560 high; 500 when a teletext page follows); hero 740-1150; teletext header bar 64 px; rows 96 px pitch (one line) or 122 px (two lines); lower third 4 px ink rule + accent bar 92-100 px high at y 1150-1196; chip row under it 44 px. Lowest content edge at every hold: 1270-1320 (measured by layout: s1 chip row 1320, s2 waveform 1290, s3 chips 1312, s4 bar 1274, s5 bar 1272, s6 bar 1270).

## 4. Layers, back to front (z-index)

1. `#root` bg. 2. `#world` (z2) holds the scene sections `.sc`; each has an inner `.in` wrapper that does the slow 1.00 -> 1.025 hold zoom. 3. `#hud` (z30). 4. `#bars` (z28, SMPTE bumper, below the HUD so the timecode shows over it). 5. `#caps` (z50). 6. `#stat` noise sprites (z55). 7. `#dot` power-off dot (z56). 8. `#roll` rolling sync band (z57, 260 px tall, 7 % ink gradient, crosses every 5.2 s in 2.6 s). 9. `#scan` baked scanlines PNG (z60, 1 px dark / 1 px clear, alpha 46/255 = 18 %). 10. `#vig` baked vignette PNG (z61). 11. `#tube` bezel PNG (z62).
All textures are baked PNGs made with ffmpeg `geq`/`noise` (scanlines 12.8 KB, vignette 207 KB, tube mask 14.8 KB, 4 noise frames 270 x 480 scaled up with `image-rendering: pixelated`). No live blur, no SVG filter.

## 5. Components

- **Monitor inset** `.mon`: 888 wide, radius 36, 4 px solid `#a5b392`, baked glass reflection (CSS linear-gradient top 28 %), image inside at 120 % width with a 1.00 -> 1.07 Ken Burns, bottom-left tag "MINH HOẠ" (amber, 30 px mono) when the picture is an AI illustration.
- **Hero numeral** `.hero`: Cascadia 600, amber, glow + fringe. Static (s1) or counted 0 -> n over 0.6 s (s3 "75", s5 "28") from the scene start + 0.02-0.12 s.
- **Lower third** `.lt`: flat opaque amber bar, 4 px ink top rule, dark Seg 700 uppercase text, wipes in with `clip-path inset(0 100% 0 0) -> 0` in 0.3 s `power3.out`, clip-path set to `none` after. Static on scene 1 (frame 0 must be complete).
- **Chip row** `.chipr`: mono 32 px phosphor; carries every derived number with its derivation ("CÒN 3 NGÀY: 15.11 - 12.11 = 3", "10.12 - 12.11 = 28 NGÀY").
- **Teletext page**: phosphor header bar (dark text, 38 px mono) + rows; each row = amber chip (190 x 56, label) + text typed at 0.03 s per character with a phosphor block cursor; row border 2 px at 20 % ink. The chip flips amber -> phosphor 0.1 s on the spoken keyword and back 1.5 s later (voice-following highlight).
- **Block-graphics grid** (diagram): 32 px phosphor cells, pitch 36 px, drawn row by row (0.22 s per row, 0.018 s stagger); one floor = 2 rows x 10 cells; the top floor amber.
- **Waveform / oscilloscope**: SVG path, 5 px phosphor stroke, drawn with `stroke-dashoffset` 1.2-1.4 s `power2.inOut`; s5 variant is a flat line with blips ("standby").
- **SMPTE strip**: 888 x 100, 4 px ink border; the "TRỰC TIẾP" (LIVE) bug sits on it, red, dark 30 px text.
- **Comparison card** (s6): 888 x 440 panel `#050604`, 4 px ink border, tag chip, 200 px hero, 34 px label, 40 px bar track; bars proportional to the numbers (4 h = 100 %, 3 h = 75 %).

## 6. Motion language

- Locked-off camera. Only motion on holds: Ken Burns on the monitor (1.00 -> 1.07, 7-12 s), `.in` zoom 1.00 -> 1.025, rolling sync band, REC dot (1 s cycle: bright 0.8 s, dim 0.2 s), timecode counting frames, block cursor, waveform.
- Entrances: wipe (lower thirds), rise 12 px + fade 0.14 s (teletext rows), typeIn, cell fills, counters (`ease none`), bar growth 0.6 s `power3.out`. No bounce, no elastic, no shake, no flash (energy 3 with the profile's "no screen pulse").
- Exits: every exit is a transition (below). Nothing fades out alone.
- Anchors: reveals use `W(sid, word)` = estimated word start, always clamped with `mx(floor, W(...) - lead)` so a drifted estimate never leaves a row late. Estimated times drift up to 0.3 s: chips flip on `W() - 0.1`.
- Initial hidden states are written with `tl.set(..., 0)`; every entrance tween is `fromTo(..., immediateRender:false)`. See trap 1.

## 7. Transitions (as built; times measured on the render)

| Cut | Kind | Build |
|---|---|---|
| s1 > s2, s2 > s3 | channel-change | 4 noise sprites stepped every 0.05 s from T-0.1 to T+0.1 (0.2 s total, inside the 0.25 s cap), scene swap hard at T, incoming gets a 14 px / 4 deg horizontal tear `steps(3)` over 0.12 s |
| s3 > s4 | SMPTE bars bumper | full-frame bars at T (hold 0.2 s), collapse into the 888 x 100 strip by `fromTo left/top/width/height` in 0.18 s `power2.in`, strip becomes visible at T+0.4; content already building under it from T+0.4 |
| s4 > s5 | v-roll | outgoing `y 0 -> -1920`, incoming `1920 -> 0`, both `steps(4)` in 0.12 s |
| s5 > s6 | power-off / power-on | outgoing `scaleY 1 -> .004` in 0.08 s, `scaleX 1 -> 0` in 0.04 s, white dot 40 px with glow at T-0.04 shrinking over 0.1 s; incoming `scaleX 0 -> 1` in 0.06 s then `scaleY .004 -> 1` in 0.1 s. Total 0.2-0.28 s |
Three transition languages (static, bars, roll) plus power in one video is at the limit of "more than two reads as noise"; they are used once or twice each, and the HUD channel number is the constant that ties them together.

## 8. Scene recipes (S = scene start from `voice/timeline.json`; six scenes, 56.3 s of voice + 1.0 s silent tail = 57.3 s)

- **s1 Hook (0-7.82).** Monitor (TV with static, illustration) 200-760; hero "100" 360 px + "NĂM" 96 px; lower third "NBC TRÒN MỘT TRĂM TUỔI"; chip row with the 3-day derivation. Static from frame 0 (no entrance), Ken Burns 1.00 -> 1.08. The hero number is on screen before it is spoken (hook rule).
- **s2 History (7.82-16.6).** Monitor (radio, illustration) 200-700; teletext page "P.101 NBC - 1926" with 3 rows typed at S+0.12, S+1.6 (floor, or `W("bốn")-0.3`), S+3.4 (floor, or `W("quảng")-0.45`); oscilloscope wave drawn S+0.25 over 1.4 s.
- **s3 Exhibit (16.6-28.58).** Monitor (empty studio, illustration); 3-floor block graphic (6 rows of 10 cells, 0.22 s per row from S+0.12); counter "75" 0 -> 75 in 0.6 s from S+0.12; "3 TẦNG"; lower third wipes at S+0.1; date chips "MỞ 18.09" (S+0.2) and "ĐẾN 20.11" (S+0.3); cut-in: "ĐẾN 20.11" flips to phosphor and pulses 1.0 -> 1.06 on `W("đến")-0.1`.
- **s4 Special (28.58-42.1).** Bars bumper (0.4 s) into the strip; "TRỰC TIẾP" bug; hero date "10.12" 288 px; "8:00 PM ET/PT" 56 px; four teletext rows (venue, length, form, content) typed at T+0.1, T+1.1, T+2.1, T+3.1; chips flip to phosphor on "nhà", "kéo", "theo", "nhìn"; lower third "NBC 100: The Live Celebration" (the title as the source gives it).
- **s5 Countdown (42.1-49.12).** Hero "28" 440 px counted 0 -> 28 in 0.6 s from S+0.02 plus "NGÀY"; derivation chip "10.12 - 12.11 = 28 NGÀY" (S+0.2); two teletext rows ("KHÁCH MỜI / CHƯA CÔNG BỐ", "CHI TIẾT / SẼ ĐẾN TRONG VÀI TUẦN TỚI"); standby waveform; lower third "ĐẾM NGƯỢC ĐẾN 10.12".
- **s6 Comparison (49.12-57.3).** Two cards: "1926 / 4 GIỜ / PHÁT SÓNG ĐẦU TIÊN TỪ NEW YORK" and "2026 / 3 GIỜ / TRỰC TIẾP TỪ NHÀ HÁT DOLBY, 10.12"; bars grow 0.6 s; lower third "NBC100 - một thế kỷ phát sóng". Holds to the end (last 1.5 s = full composition).
- **Signature recipe for short clips (samples).** SMPTE bumper -> monitor + teletext page typed row by row -> lower third wipe -> chips flip -> power-off collapse to a dot in the last 0.4 s; or channel change between two pages (t057).

## 9. Captions (Vietnamese karaoke)

Black teletext box `rgba(0,0,0,.94)` (DEVIATION), no radius, 6 px amber left rule, left 96, width 888, top 1400, Seg 600 44 px / 56 px, padding 14 x 24. Chunks are built in the page from the word list: split after a word ending in `, .` once the chunk has 3 words, or at 7 words; a 1-2 word tail merges into the previous chunk when the total stays <= 9. Chunk visibility and the current-word colour are `tl.set` only (no fades, no ghosts): current word amber `#ffb000` with `0 0 8px rgba(255,176,0,.6)`, others ink, glow only on the current word (profile constraint). Chunk ends at the next chunk's first word, or speech end + 0.1 s. Captions show the spoken words as written (numbers in words); the visual numerals on screen are digits with the same value. The captions stay on screen during bars and static (z50 over `#bars` at z28; under the noise at z55).

## 10. Sound

No music (the pipeline has none). The voice is the only sound: VieNeu via `motion_tools.py voice`, `--gap 0.3` between scenes. Measured on `final.mp4`: -15.5 LUFS, peak -4.2 dBFS (mux does loudnorm I=-14, TP=-1.5; two-pass not used). Profile sound (dial click + static on cuts, tube whine on power-off) is NOT available here; if a SFX set exists, put it on the 0.2 s static bursts and on the 0.12 s power-off. Words that went to Phong's ear (listed in `ear-check.txt`): "New York", "Dolby", "Los Angeles" (not in the trusted dictionary).

## 11. Images (agy)

- 3 illustrations in the video + 2 in the samples (about 700 KB each, jpg, 768 x 1376): old CRT TV with static (s1), tabletop radio and microphone (s2), empty TV studio with a camera (s3); sample images: generic console with two pads, empty 1970s diner. Prompt shape that worked first time: "<subject>, dark near-black background, phosphor green and amber glow, analog film grain, scanlines, centred, no text, no letters, no people". 1 try each, 50-70 s, no retries needed. No logo, no text, no real person appeared.
- Placement: `.mon img` is 120 % wide (so Ken Burns never shows an edge); its `top` is computed so the subject centre lands in the box: `top = boxHeight/2 - subjectCentre x 1909` (height of a 120 % wide 9:16 image is 1909 px). Values used: TV 0.50 -> -675 (560 box), radio 0.57 -> -838 (500 box), studio 0.62 -> -934, console 0.52 -> -733 (520 box), diner -700 (470 box). The first attempt used guessed offsets and cropped the TV to its top edge (trap 5).
- Illustrations always carry the "MINH HOẠ" tag. The generic console picture shows a maze game on its screen: it is generic but resembles a famous arcade game; do not reuse it for a story about a real product.

## 12. Must not

- Live noise filters, SVG filters, backdrop blur, or more than one baked texture of each kind on screen.
- A static burst longer than 0.25 s, or anywhere but a cut. Glow on caption text except the current word. Glossy glass cards. Smooth parallax camera. Dense modern UI screens.
- Power-off in the last 1.5 s of a full video. White text on `--sig`. Blue as text. `segoepr` for any Vietnamese word.
- Any number on screen that the voice does not say, except a derived number whose derivation is printed beside it.
- A logo, mark, peacock or other brand device: the story name is written as plain mono text ("NBC", "NBC100").

## 13. Traps seen in real builds (this build, 2026-11-12; measured)

1. **Entrance tweens with `immediateRender:false` leave the element visible before its entrance.** First render: floors (6 rows of cells), date chips, teletext rows and wipes showed their final state for 0.1-3 s, then jumped to the from-state and played. Seen on the 16.7 s and 13.0 s snapshots (empty chips with cursors visible 1.5-3 s before their text). Fix: write the hidden state with `tl.set(el,{autoAlpha:0},0)` (or `opacity`, `clipPath`, `width`) at time 0 for every element whose entrance is later than the scene start; counters use plain `fromTo` (immediateRender on) so they start at 0, not at the final number. Hold-time colour flips (`backgroundColor` fromTo pairs) must keep `immediateRender:false`, otherwise the second tween writes its from-colour at time 0.
2. **A full-frame bumper hides everything.** SMPTE bars at full frame for 0.30 s + 0.22 s morph = 0.52 s with nothing else readable (limit 0.5 s). Fixed to 0.20 s hold + 0.18 s morph (0.38 s), content starts building at T+0.4 under the shrinking bars. In `inspect` the bars still report `text_occluded` for the 8 scene texts at t = 28.65 s: intentional, attribute `data-layout-allow-occlusion` must be on each bar `<i>`, not on the parent. The 8 remaining errors are expected, accepted.
3. **`tl.to` with unset start values drifts when the timeline is seeked directly.** The first bars morph used `tl.to` and a snapshot at 29.0 s showed full-frame bars still there with the footer text over them. Use `fromTo` with explicit start values for any shared overlay (bars, dot, roll).
4. **Semi-transparent "CRT" pieces break the 90 % rule.** Profile values rgba .85 caption box, rgba .55 mute, rgba .5 monitor border, rgba .55 card fill, and a LIVE bug blinking to 35 % for 0.45 s every second are all below 90 % for more than 0.2 s. Replaced by `.94` caption alpha, flat `#858d77`, flat `#a5b392`, flat `#050604`, and a LIVE bug that does not blink (only the 26 px REC dot dims, for 0.2 s of each second).
5. **Image placement by guess.** Offsets typed by eye cropped the subject (TV top edge only, studio camera cut off). Compute `top` from the subject's vertical centre as in section 11; check the snapshot before the render.
6. **Mono font width is the layout.** Cascadia Mono advances 0.586 em: 38 px = 22.3 px per character, so a 670 px text column holds 30 characters; 288 px "10.12" = 843 px wide (fits 888), 360 px "100" = 633 px; "THỜI LƯỢNG" (10 characters) needs a 30 px chip font to fit a 190 px chip. "NĂM" beside a 360 px "100" collided at x 700 and had to move to x 775. Count characters before choosing a size.
7. **Word count vs voice time.** 263 spoken words (6 scenes) = 56.3 s with `--gap 0.3` (4.7 words/s). The brief's 190-225 words would have given about 45 s. Use the voice duration, not the word count, as the gate.
8. **Overlay z-order vs the HUD and captions.** The bars at z54 covered the timecode and the caption; z28 keeps both visible. Static noise (z55) still covers the caption for 0.2 s on cuts: accepted.
9. **File size.** The silent render at "standard" is 25.3-25.5 MB (static noise and scanline PNG are hard to compress); the mux re-encode with crf 20 brings the final to 18.4 MB. Do not judge size on the silent file.
10. **Lint / validate noise.** `overlapping_gsap_tweens` on a chip's `backgroundColor` pair (0.00-0.10 s) is a false warning from `immediateRender:false` pairs; `composition_file_too_large` (333 lines) expected. `validate` reports 10 contrast warnings at 1.01-1.02:1 for elements of hidden scenes (sampled while `display:none`): false positives.
11. **Tools.** In this build `python3`/`node`/`awk`/`sed` were not allowed outside `motion_tools.py` and `frame_check.py`; contrast was computed by hand, edits were done with the editor tool, and the pixel checks used `ffmpeg` `select`/`tile` sheets. Frame check: `final.mp4` 0 BLANK frames, 0 long blank runs, 1 TOPHEAVY info frame (likely the 0.2 s power-off collapse near 49.1 s; not investigated); samples 0 BLANK.

## 14. What to do next time

- Build one real teletext "page" per scene with a header bar so the recipe is recognisable; scenes 2, 4 and 5 did, scenes 1, 3 and 6 are closer to a generic card layout.
- Add a proper SFX set for static and power-off when the pipeline has it.
- Pick a pixel face if one is installed (VT323) and re-measure the character widths in trap 6.
