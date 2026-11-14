# Style: comic-multiverse (family: house; detail, written from the demo build of 2026-11-13)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in the build.** Loud, young, playful announcements with ONE hero idea per beat: youth sneaker / streetwear drops, collaborations, event or product launches, social cuts, giveaways. Topic shape t164 (youth sneaker and streetwear brand announces an anime collaboration, Jev fit 0.79) worked well. Not for sad, enforcement, finance, data-dense or dignified stories; not for dense numbers (4+ numbers per beat). Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: one silent 12.5 s sample (`samples/sample-t164.mp4`), no voice-over, no music, no captions, no word timing. **The voice, caption and sound rules of this style were NOT exercised**; sections 8 and 9 repeat the profile's values and are marked UNTESTED. Everything else below is measured on the real build. Marks: **ASSUMED** = invented here; **SUBST** = a named font is not installed, a local one replaces it.

Profile: `skill/references/styles/profiles/comic-multiverse.yaml` (energy 5, mixed palette). Skill detail: `skill/references/style-comic-spiderverse.md`. Inspired by the look only: no franchise names, logos or characters. All content in the sample is generic and labelled "Minh hoạ" on screen.

Format as built: 1080 x 1920, 30 fps, 12.5 s, 4 beats, silent, h264 4.7 MB (hyperframes render gave 18.1 MB at default quality; re-encoded with ffmpeg `-crf 26 -preset slow`, no visible loss).

## 1. Tokens (contrast = WCAG formula, computed by hand from relative luminance; script runs were not permitted in this sandbox, so numbers are rounded to 0.1)

```css
:root{
  --bg:#1a0b3d; --ink:#0d0a1a; --paper:#fff6e5; --cyan:#19d3ff; --magenta:#ff2e9a;
  --red:#ff2b3a; --yellow:#ffd21f; --purple:#5b1fd1; --orange:#ff7a1a; --green:#2ee59d;
  --rx:0px; /* misregistration offset, kicked 12-14 px on a slam, decays to 3 px in 0.5 s */
}
```
Measured pairs that carry text:
| Text on fill | Ratio | Use |
|---|---|---|
| yellow on bg `#1a0b3d` | 12.5 | headline (with ink stroke) |
| yellow on ink | 13.5 | kicker, panel title on dark box |
| ink on paper | 18.2 | panel text |
| ink on yellow | 13.5 | kicker, HUD, button box |
| paper on bg | 16.9 | sub-line on ink box |
| cyan on bg | 10.2 | second headline line, `×` |
| ink on cyan | 11.0 | (available) |
| ink on magenta | 5.7 | tag chips |
| yellow on purple `#5b1fd1` | 5.7 | (available) |
| ink on orange | 7.5 | (available) |
| magenta on paper | 3.2 | FILL ONLY, fails text |
| paper on red | 3.5 | large text only (>= 3), not used |

Rules: text colours only from the table; magenta and red are fills, shadows and rings, never small text on paper. Universe gradients (vertical): night `#1a0b3d > #3a1394 > #5b1fd1`; cyan `#0b3a73 > #0a7fb8 > #19d3ff`; red-sun `#8f0f2a > #ff2b3a > #ff7a1a`. Text over a bright universe always sits on ink, paper or yellow boxes or carries the 9 px ink stroke; never bare on `#19d3ff` or `#ff7a1a`.

## 2. Fonts (fontTools check was not runnable here; inherited from the saas-bento and fluent docs, where the same four files were glyph-tested on all 36 Vietnamese letters ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ; the sample's own text, every Ă Â Ê Ô Ơ Ư Đ and tone mark shown, rendered correctly in the snapshots)

| File | Role |
|---|---|
| `SegUIVar.ttf` (weight 300-700) | SUBST for Anton / Bangers / Be Vietnam Pro: headlines (700, UPPERCASE, 9 px ink stroke), kickers, labels, chips |
| `CascadiaMono.ttf` | declared, unused in the sample (reserved for code or log panels) |
| `cambriai.ttf` | unused |
| `segoepr.ttf` | NEVER: lacks Vietnamese letters, and is not needed (Permanent Marker signature is replaced by nothing) |

Anton, Bangers and Permanent Marker are not installed. Consequence: the condensed Anton impact is lost; compensate with size (250 px for a one-word line), the thick stroke and the CMY offset. Uppercase Segoe 700 with `paint-order: stroke fill` and `-webkit-text-stroke: 9px` keeps the diacritics readable (stroke painted behind the fill, so tone marks are not eaten). Line-height .94 was enough for the capitals with marks (GIÀY, ĐỒ, MỚI, SẮP, MẮT) at 128-250 px; do not go below .9.

### Type scale (1080 x 1920, measured in the build)
| Token | Size | Notes |
|---|---|---|
| hero word `.hl` (GIÀY, ANIME) | 250 px | 9 px ink stroke, text-shadow -rx cyan / +rx magenta / 10 px ink extrusion |
| hero symbol `×` | 130 px | cyan |
| hero number "20.12" | 230 px | ink on the yellow burst (burst gives the contrast) |
| two-line headline | 128 px | "THẾ GIỚI MỚI / ĐÔI GIÀY MỚI" (width ~870 of 1080) |
| row title | 66 px | uppercase, ink on paper |
| panel strip | 44 px | "PHIÊN BẢN GIỚI HẠN" |
| kicker | 46-50 px | yellow box, 6 px ink border, rotated -3 deg |
| sub-line box | 40-52 px | |
| tag chip / HUD / stamp | 34 px | the smallest text in the video; no text under 30 px |

## 3. Safe areas and grid (1080 x 1920)
- y 0-200: platform zone, empty. HUD box (left 56, top 206, 230 x 62) and "MINH HOẠ" stamp (right 56, top 206) sit just below it.
- Kicker y 326; headline block y 400-960; hero object (panel, burst, rows) y 560-1600; sub-line box ends by y 1580. y 1650-1920 empty. Lowest content edge at the hold: beat 1 y 1600, beat 2 y 1580, beat 3 y 1500, beat 4 y 1520 (measured on the snapshots, ASSUMED row positions +/- 10 px). The lower third reads full because of the panel and box stack.
- Side margin 56 (HUD) to 90-150 (content). Panels are rotated 1.5-3 deg, so their corners reach +/- 14 px beyond the nominal box: keep 60 px clear.

## 4. Layers, back to front
`#u1..#u4` universe gradients (hard swap on each cut) > `#rays` (repeating-conic, 20 deg period, rotates 100 deg over the whole video, opacity .8) > `#tone` (baked `dots-pink.png`, opacity .26, pulses to .34 / scale 1.04 on each beat of 1.04 s) > `#tone2` (baked `dots-ink.png`, opacity .16) > `#shake` (scenes `#s1..#s4`) > `#bars` (4 slice bars) > `#flash` > `#hud` > `#mh` (Minh hoạ stamp). Fixed overlays are outside `#shake` so labels do not wobble.

Textures are baked: the two dot PNGs were generated with ffmpeg `geq` (alpha = distance to the nearest grid centre < radius, radius 1 to 10 px growing diagonally, cell 28 px) because Python and PIL could not be run; 50 KB each. Live radial gradients were avoided (profile: they blacked out frames). `repeating-conic-gradient` for the rays rendered correctly in 0.7.26.

## 5. Components
- **Panel** `.panel`: paper fill, 6 px ink border, shadow `-6px -4px 0 cyan, 6px 4px 0 magenta, 16px 16px 0 ink`, halftone triangle in the top-right corner (300 x 300, pink dots at .55, clip-path), rotation 1.5-3 deg alternating sign. `overflow:hidden` is deliberate and holds nothing near the edge.
- **Kicker** `.kick`: yellow box, 6 px ink border, 8 px hard shadow, -3 deg, slides in from x -500.
- **Headline** `.hl .w`: words as inline-block spans so each can flip.
- **Row** (beat 2): 900 x 230 panel, number disc 130 px yellow with 6 px ink border, title 66 px, magenta tag chip under it.
- **Burst** (beat 3): 48-point polygon, radii 436 / 330, yellow fill, 10 px ink stroke, offset ink copy (+16, +16) as a hard shadow; the number sits on top.
- **Ink box**: ink fill, 6 px yellow border, yellow or paper text, hard magenta or yellow shadow.
- **HUD**: yellow tilted box "SỐ 01 / 04" ... "SỐ 04 / 04", swapped by `tl.set` visibility on each cut (the comic issue counter doubles as a beat counter).
- **Stamp**: "MINH HOẠ" ink box, yellow text and border, +3 deg, on screen for all 12.5 s.
- **Sneaker**: inline SVG of rounded shapes (sole, upper, toe cap, tongue, laces, stripe), 10 px ink strokes. Drawn in code; agy was not used (no image was needed, no image was generated).

## 6. Motion language
- **On twos**: `steps(n)` ease with n = round(duration x 12) gives 12 poses per second. Used for every entrance of text, panels, kickers and boxes (0.30-0.36 s). Camera-like moves (rays rotation, headline scale 1.00 to 1.03, shoe float) stay smooth (`none`, `sine.inOut`).
- **Headline words flip up**: `rotationX -75 to 0, y 50 to 0, opacity 0 to 1`, 0.36 s on twos, stagger 0.10-0.17 s.
- **Slam**: scale 1.30-1.50 to 1 plus opacity, 0.30 s on twos, with a 7-keyframe shake (45 ms steps, amplitude 9-14 px, seeded rng) on the same frame, and an `--rx` kick of 12-14 px.
- **Cut = glitch**: outgoing hidden exactly on the boundary (no ghost), incoming shown, universe swapped, white flash .85 to 0 in 0.22 s, four coloured slice bars sliding 180 px in 0.26 s on `steps(3)`, stage x jitter 16 px in 0.24 s. Total effect 0.28 s. No SVG filter was needed.
- **Holds are never frozen**: rays rotate, tone pulses, shoe floats +/- 14 px and tilts +/- 2 deg, number discs rock, burst rocks +/- 3 deg, headline slowly scales.
- Beat times as built: 0 / 3.4 / 6.9 / 10.0 / end 12.5 (3.4, 3.5, 3.1, 2.5 s). Entrances finish within 0.9-1.4 s of each cut; the rest is hold.
- Not used: dots wipe, flip transition, speed lines (replaced by slice bars + flash). They remain in the profile.

## 7. Scene recipes (as built; all text Vietnamese; content generic)
**R1 Hook (0-3.4)**: night universe. Kicker "HỢP TÁC GIỚI HẠN" slides in at 0.0; words GIÀY / × / ANIME flip up at 0.08 / 0.25 / 0.42; paper panel with the sneaker and strip "PHIÊN BẢN GIỚI HẠN" slams in at 0.8 with shake. Frame 0 is a clean background plus HUD and stamp (kicker is mid-slide, <0.1 s).
**R2 List (3.4-6.9)**: cyan universe, glitch cut. Headline "3 MÓN ĐỒ MỚI" flips up at +0.04; three rows slam at +0.3 / +0.55 / +0.8 (GIÀY CAO CỔ, ÁO KHOÁC HOODIE, BALO MINI with tags); ink box "Thiết kế chung với studio hoạt hình" at +1.2.
**R3 Date burst (6.9-10.0)**: red-sun universe. Kicker "NGÀY RA MẮT"; burst slams at +0.1; "20.12" flips up at +0.45 (static text, no counter); ink box "SỐ LƯỢNG CÓ HẠN / Hãng giày × studio hoạt hình" at +0.9. The date is invented for illustration.
**R4 End card (10.0-12.5)**: night universe. Kicker "SẮP RA MẮT"; two headline lines "THẾ GIỚI MỚI" (yellow) and "ĐÔI GIÀY MỚI" (cyan); sneaker panel "GIÀY × ANIME" at +0.5; yellow box "ĐÓN CHỜ BỘ SƯU TẬP" at +0.85. Fully built by 10.9, so the last 1.6 s is a full composition. No call to action beyond a wait line.

## 8. Captions (UNTESTED: demo build has no voice)
Profile values only: yellow narration box, 5 px ink border, hard ink + cyan shadow, 40 px bold, current word `#a3005a` (contrast with the box not measured here). For 9:16 the box must sit above the 1650 line and the HUD/stamp zone must stay free. Do not rely on this section until a voiced build exists.

## 9. Sound (UNTESTED)
Profile: punchy ~110 BPM breakbeat, dense comic SFX on cuts. Not built. The sample's cut times (3.4, 6.9, 10.0) were not aligned to a beat grid; with music, snap the cuts to bars.

## 10. Images
None generated. Everything is code: CSS, inline SVG, two baked dot PNGs. Advice for a full build: agy may supply a graffiti or skyline texture only as a baked, text-free PNG; it must never draw the product, the characters (an anime collaboration must use a generic or licensed character; no real characters are drawn here) or any text.

## 11. Must not
- Franchise names, logos, real anime characters, real brands, real prices or specs; emoji.
- `segoepr.ttf`; text on a bright universe without a box or stroke; magenta or red small text on paper.
- Live `backdrop-filter`, live radial gradients, SVG filters left attached after the effect.
- More than one hero idea per beat; a fixed identical panel repeated in every beat.
- A frame 0 with half-flipped words; a hold with nothing moving.

## 12. Traps seen in real builds (this build, 2026-11-13)
1. **Default render size.** `hyperframes render` produced 18.1 MB (over the 15 MB limit) because halftone, rays and 12 fps-stepped motion defeat compression. Fix: ffmpeg re-encode `-crf 26 -preset slow -pix_fmt yuv420p` gave 4.7 MB. Start with that, not with `-q`.
2. **The "end frame" snapshot is blank.** `snapshot` adds a frame at 12.61 s, past the 12.5 s duration; it renders only the bare background colour. It is a tool artefact, not a missing last frame (the 11.8 s and the ffmpeg 2 fps sheet both show a full composition at 11.5-12.0).
3. **Inspect overlaps are all mid-animation.** `inspect` reported `content_overlap` for the kicker versus the flipping hero word at 0.69-2.08 s (kicker box 326-400, hero line box starts at 410 but the 250 px glyph box with line-height .94 reaches up into it) and for the burst overflowing its own SVG by 6-19 px (the stroke and ink offset copy). Both are visual non-issues: nothing touches on a held frame. Left as warnings (0 errors); next time move the headline block down 24 px and give the SVG 40 px padding.
4. **Contrast warnings on hidden HUD spans.** `validate` flagged `#h1 "SỐ 01 / 04"` at 1.06:1 at t = 1.25, 3.75, 6.25, 8.75, 11.25. At those times only one of the four HUD spans is visible and the span's text is ink on yellow (13.5:1); the sampler hits the `visibility:hidden` copy. False positive, same family as the fluent doc's "hidden layer" note.
5. **Hard-set universes avoid ghosts.** Universe and scene swaps by `tl.set` at the exact boundary gave no ghost of the outgoing beat (the 2 fps sheet shows a clean cut every time); cross-fading universes was not needed.
6. **Entry frames are by design mid-slam.** At cut + 0.04-0.1 s the incoming beat shows a half-flipped word or a 1.3x panel at partial opacity. They last 0.12-0.36 s, so they pass the "nothing below 90% opacity for more than 0.2 s on a held frame" rule only because flip and slam are 0.30-0.36 s on twos (4 poses, of which at most 2 are partial). Do not lengthen them.
7. **Python helpers were blocked.** `frame_check.py` needs numpy, which is not installed for the default python3, and python and node scripts could not be executed here. The frame check was replaced by hyperframes `snapshot` (7 frames) plus an ffmpeg 2 fps contact sheet (25 frames) read by eye. Run the real `frame_check.py` when numpy is available.
8. **Contrast was hand-computed**, not script-computed, for the same reason (see section 1).
9. **Anton / Bangers missing.** The look loses its condensed impact with Segoe; size and stroke recover most of it. Install Anton and Bangers (OFL) in `assets/fonts` for a faithful edition and re-run the diacritics check on them.
10. **Leftovers in the project.** `samples/t164/small.mp4` (intermediate), `samples/t164/snapshots/` and `/tools/` scripts could not be deleted (no permanent deletion step); ignore them.
