# Style: cinematic-streaming (9:16 Vietnamese teaser edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in the t109 build: a SHAPE with one title, one date and a teaser mood - a streaming platform announcing a new series with a premiere or teaser date; also film trailers, game or event reveals, a "coming soon" catalogue row, a documentary teaser. Not for numbers, step-by-step explanations, enforcement or bad-news stories, or anything that needs more than about three text lines per beat. Tier 2 never widens tier 1.

**Reading order.** Sections 1-12 are the recipe from the build. Section 13 is the traps from that build, with measured numbers. Where they disagree, 13 wins.

**Status.** Written 2026-11-14 from ONE demo build: `samples/sample-t109.mp4` (1080x1920, 30 fps, 12.0 s, silent, 3.7 MB, topic t109, Jev fit 0.73). No owner document existed before. **Voice-over, captions, sound and music were NOT exercised** (demo build): sections 8 and 9 are the profile's rules carried over, marked ASSUMED. The content is generic and labelled "Minh hoạ" (series name, date, tile art are all invented).

## 1. Tokens (contrast measured on the real backgrounds, WCAG relative luminance)

| Token | Value | Use | Contrast on #0b0b0b |
|---|---|---|---|
| bg | #0b0b0b | every frame | - |
| ink | #f4f4f4 | headlines, date | 17.9:1 |
| mute | rgba(244,244,244,.6) = about #979797 | kickers, metadata, footer, tag | 6.7:1 |
| accent | #dc3a22 | ONE word of the title, progress bars, light sweep | 4.38:1 (3.0 passes only for large text; 4.67:1 on pure #000) |
| ember | #9e2a17 | impact flash (opacity .25), radial glow, sweep edges | decoration only |
| bar | #000 | letterbox bars | - |

Rule that held: red on at most one element per frame. In the final frame it is the word "TỐI" plus the thin progress line (two, a small violation; the line is a bar, not text). `hyperframes validate` reported "15 text elements pass WCAG AA".

## 2. Fonts (Vietnamese diacritics check)

- Installed: SegUIVar.ttf (Segoe UI Variable), CascadiaMono.ttf, cambriai.ttf. The profile's Bebas Neue, Inter and Be Vietnam Pro are NOT installed. Substitute: **SegUIVar weight 900, uppercase, +0.02em** for titles; weight 500-600 for kickers and meta. Say so in any brief.
- Diacritics check: done by LOOKING at rendered snapshots of the real strings (SỰ THẬT, KHÔNG NGỦ, BÓNG TỐI, THÀNH PHỐ, PHIM HÌNH SỰ, TEASER CHÍNH THỨC, "Minh hoạ", "Nội dung giả định, không phải phim thật"): every stacked mark (Ố, Ậ, Ủ, Ự, Ớ) rendered, no tofu. The scripted fontTools glyph test could not be run in this session (python was blocked), so a full lowercase-plus-capitals glyph test is still open.
- segoepr.ttf lacks Vietnamese letters: never used.

## 3. Type scale (1080 x 1920, px; all measured from the build)

| Role | Size | Notes |
|---|---|---|
| Hook headline (2 lines) | 150, line-height 1.15 | 9 chars "KHÔNG NGỦ" is about 890 px wide |
| Final title line 1 "BÓNG TỐI" | 170, line-height 1.15 | about 870 px wide |
| Final title line 2 "THÀNH PHỐ" | 150 | about 840 px |
| Date | 240, line-height 1.1 | "20.12" |
| Metadata title | 64 | |
| Kicker | 36, tracking .3em, mute | the style's "small caps" voice |
| Metadata sub | 36 | |
| "Minh hoạ" tag | 32 | top bar |
| Footer line | 30 | the one allowed small line |

Nothing is below 30 px. Max uppercase title width for a 1080 frame is about 940 px: at 7.0 em-per-char average a 9-letter word is the ceiling at 150 px.

## 4. Safe areas and grid

- Letterbox bars: open from 960 px each (full black) to **300 px each**, leaving a 1320 px window (y 300-1620). They close to 960 px for 0.4 s on act changes and reopen over 0.9 s.
- Top bar holds the "Minh hoạ" tag (left 60, top 150). Bottom bar holds the footer (bottom 150).
- Content margins 70-90 px left/right. Hero text sits in the lower-left third of the window over a bottom scrim; the final act centres.
- Poster tiles 290 x 420, radius 6, gap 16, pitch 306. Two rows at top 470 and 906; metadata card at top 1385 (ends about 1610, just inside the bar).

## 5. Layers, back to front

1 bg and scene backdrop (gradient, ember glow) - 2 rain / lamp / poster rows (camera group, slow scale) - 3 bottom scrim - 4 text - 5 letterbox bars (z 50) - 6 ember flash (55) - 7 red sweep (60) - 8 grain PNG at 10% (70) - 9 tag and footer (80).

## 6. Components

- **Kicker**: mute, 36 px, tracking .3em, masked rise 0.6 s `power3.out`.
- **Headline mask**: `overflow:hidden` box, line-height 1.15, `yPercent 110 -> 0`; carries `data-layout-allow-overflow`. line-height must be at least 1.1 or the diacritics clip.
- **Poster tile**: gradient (dark hue to bg), a dark silhouette block, a bottom gradient; no text. Pure CSS, no image needed.
- **Focus tile**: same size, ember-tinted, red bottom stripe, shadow `0 30 60`; scale 1.14 on `power3.out` 0.6 s; marked `data-layout-allow-overlap`.
- **Metadata card**: 64 px title, 36 px sub, grey track plus red fill bar (`scaleX 0 -> 1`, 1.4 s).
- **Date block**: kicker "Ra mắt ngày" over a 240 px date and a red progress line.

## 7. Scene recipes (12.0 s, three beats; every tween start is clamped at or above 0)

**A Hook (0-3.7 s).** Bars open 0.1-1.5 s `power3.inOut`; ember glow and a lamp line fade in; 26 seeded rain streaks fall (3 finite repeats); camera scale 1.00 -> 1.07 `sine.inOut` over 3.7 s; kicker at 1.0 s, "SỰ THẬT" at 1.35 s, "KHÔNG NGỦ" at 1.55 s (masked rise). Exit: **red light sweep**, skewed 30 deg, crosses 3.5-3.95 s; scene swaps at 3.72 s under the band.

**B Catalogue (3.7-7.2 s).** Two poster rows glide in opposite directions (`power1.inOut`, 400-500 px over 3.4 s), tiles fade up with 0.06 s stagger; kicker "Sắp lên sóng" at 4.1 s; focus tile appears 4.5 s and grows 1.14 at 5.0 s; metadata card rises 5.3-5.5 s; red bar fills 5.6-7.0 s. Exit: **letterbox close** 6.85-7.25 s (bars meet), swap at 7.25 s.

**C Title and date (7.25-12.0 s).** Bars reopen 7.45-8.35 s; kicker "Teaser chính thức" at 7.6 s; a 0.7 s hold with only the kicker and ember glow; **title slam at 8.3 s** (line 1), 8.38 s (line 2): scale 1.08 -> 1 `expo.out` 0.5 s, ember flash .25 for 0.05 s, 7-step decaying x shake of 9 px; kicker "Ra mắt ngày" 8.9 s; date 9.1 s (rise 50 px); red line fills 9.3-10.2 s; footer 9.3 s. 10.2-12.0 s is a full static-composition hold with slow push (bg 1.08, title 1.03).

## 8. Captions (ASSUMED, not exercised)

Profile rule: no pill, 44 px Be Vietnam Pro 600 ink, shadow `0 2 12 black`, bottom band, current word ink and unread mute. In the 9:16 edition the bottom band is the lower letterbox bar (y 1620-1920): captions would live there, and the footer line must then move. Untested.

## 9. Sound (ASSUMED, not exercised)

Profile: low drone, one riser into the title, one sub boom on the slam (8.3 s in this timing), whoosh on the red sweep (3.5 s), no multi-note signature. The 0.7 s hold before the slam is where silence would sit.

## 10. Images

None used (agy image generation could not be run in this session). The style works without them: gradients, glow and silhouettes carry the mood. If used: dark noir street or abstract silhouette, 9:16, no text, no faces, large dark negative space in the lower half, one faint red source.

## 11. Must not

- No real studio, series, price, spec or logo; the sample's text is invented and labelled "Minh hoạ".
- No bright backgrounds, no bouncy easing, no `back` ease (use `expo.out` / `power3.out`).
- Red on more than one text element; red text under 24 px (4.38:1 fails AA for small text).
- A hard cut that is not on a slam or sweep.
- Three-plus text lines per beat; dense explanation.
- A title wider than 940 px.

## 12. Transitions used

red sweep (A to B, 0.45 s), letterbox close and reopen (B to C, 0.4 s plus 0.9 s), slam on silence. Dip to black from the profile was not needed.

## 13. Traps seen in real builds (this build, 2026-11-14, t109)

1. **Title wider than the 9:16 frame.** "KHÔNG NGỦ" at the profile's 200 px measured about 1190 px and was cut at the right edge; "BÓNG TỐI" at 210 px touched both edges. Fix: 150 px and 170 px (about 890 and 870 px). The profile's 180-240 px assumes 16:9.
2. **Diacritics clipped by tight line-height.** Display lines at line-height .95 clip stacked marks inside a `overflow:hidden` mask and raise `content_overlap` warnings between lines. Use 1.1-1.15.
3. **Dead air before the slam.** The first draft kept the window empty 7.45-8.7 s (1.25 s, over the 0.5 s limit). Fix: kicker at 7.6 s and slam at 8.3 s, so the empty stretch is 0.35 s (bars reopening) and the kicker-only hold 0.7 s.
4. **Letterbox 2.39:1 does not exist in 9:16.** A true 2.39:1 window would be 452 px tall. Used bars of 300 px (window 1320 px) instead, closing to 960 px on act changes.
5. **Accent fails AA as small text.** #dc3a22 on #0b0b0b is 4.38:1; fine for 170 px or bars only.
6. **Focus tile in a moving row.** The focus tile is a child of the sliding row, so its slot must be computed from the row's end offset (row x -829 puts the tile at x 395, centred). Placing it at left 0 pushed it off-screen.
7. **Row and meta card collision.** Three rows of 420 px plus a metadata card did not fit; two rows (top 470 and 906) leave the card at 1385-1610.
8. **`inspect` false warnings.** `content_overlap` on opacity-0 elements (7.3-8.7 s, "RA MẮT NGÀY" box) stayed after fixes; the held frames are clean. Treat as a false positive only after looking at the snapshot.
9. **Grain without python.** Baked with `ffmpeg -f lavfi -i "color=c=black:s=512x512,noise=alls=70:allf=t+u" -frames:v 1 grain.png` (600 KB), shown at 10% opacity; it lifts black slightly, so keep it at or below 10%.
10. **Tooling limits seen.** `motion_tools.py image` and `frame_check.py` need python and were blocked in this session; the frame check was done with an ffmpeg contact sheet (`fps=2,scale=216:384,tile=8x3`) and `hyperframes snapshot`.
