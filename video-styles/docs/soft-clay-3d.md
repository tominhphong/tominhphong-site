# Style: soft-clay-3d (9:16 Vietnamese news edition, first real build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** Warm, friendly stories about a physical thing a child or a beginner makes, builds, saves or collects: toy and hobby kits, kids' science and robot kits, family-friendly apps with a mascot, habit and saving apps, gift-season product launches. The recipes below worked best where the story has an OBJECT that can be built piece by piece (kit, parts, box) and a short list of plain features. Not for bad news, enforcement, accidents, dense numbers (more than 3 numbers fight the cute objects), quote stories, code or terminal stories. Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the design as built. Section 12 is the list of traps found in THIS build with measured numbers; where 12 contradicts 1-11, 12 wins.

**Status.** Written 2026-11-13 from the first real build: video `robot-r2d2-clementoni-lap-rap` (55.5 s, 7.6 MB) plus two 10 s samples (kids circuit kit, habit app with mascot). No other build has tested it. All "measured" numbers come from that build; anything marked ASSUMED was not measured.

**Example videos show the visual recipe, not the niche.** The build story was a licensed-franchise robot kit, 13 months old (no fresher story of the shape was found; see manifest notes). Copy how it is built, not what it is about.

One idea: every scene is a small clay diorama. Pastel objects land with a squash, a headline sits above them, rounded cream cards carry the facts, and a cream pill carries the karaoke caption. Energy 3: bounce lives in the objects, never in the camera.

## 1. Tokens (contrast measured with the WCAG formula, hand-computed; no script could be run in this sandbox)

```css
--bg:#fdf1e7;         /* page warm tint (relative luminance 0.896)          */
--ink:#3a2e39;        /* warm plum, never black: 11.6:1 on bg, 12.4:1 on card */
--mute:#5e4d5b;       /* secondary text: 7.0:1 on bg, 7.5:1 on card          */
--card:#fffaf4;       /* cards and caption pill                              */
--accent:#ff8a5b;     /* MARKS ONLY (2.1:1 on bg): fills, rings, tube glow   */
--accent-ink:#a63a0b; /* accent AS TEXT: 5.9:1 on bg, 6.3:1 on card          */
--peach:#ffc2a1; --mint:#9ee6c7; --lav:#c6b8ff; --butter:#ffe38a; --sky:#9ad0ff;
```
Ink on the pastel fills (text inside pills and bricks): mint 8.9:1, lavender 7.2:1, peach 8.3:1, butter 10.2:1, sky 7.9:1, accent fill 5.6:1. White on accent-ink 6.5:1. `hyperframes validate` reported "55 text elements pass WCAG AA".

Each pastel has a 3-stop vertical gradient (light, base, darker same hue, e.g. mint `#bff3dc / #9ee6c7 / #6fcfa6`): that gradient IS the clay. Rules: one warm background tint; pastel fill plus darker same-hue shade for depth; accent orange only as a mark (selected day, lit tube, ring), never as small text.

## 2. Fonts (3 local files; the profile's Nunito / Fredoka / Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, labels, captions, pills | Nunito 900 / 600, Fredoka 600 | `SegUIVar.ttf`, weight axis, 700 everywhere (600 for sub-lines) | The 36 test letters and all capitals render correctly in the snapshots (ắ ằ ế ề ố ớ ứ ữ ự ỹ ỷ đ, e.g. "Kỹ năng vận động tinh", "Chiến", "Quỹ tiết kiệm"). `fontTools` could not be run here; the owner docs state SegUIVar has all 36 letters (TÀI LIỆU NÓI). |
| Numbers, badges | Fredoka | none needed: the build has no counted numbers | |
| Never | | `segoepr.ttf` (35 of 36 test letters missing per the owner docs) | not used |

DEVIATION: none of the local fonts is rounded, so the "puffy" feel comes from shapes, not letters. Cascadia Mono and Cambria Italic were not used (mono and serif fight a clay look). If a rounded Vietnamese font is ever installed, swap only the `@font-face` line.

Type scale (1080 x 1920, px, measured in the build): kicker 30 / 700 / tracking .06em; headline 92 (84 when 2 lines of 15+ characters, scene 7); row title 42; row sub-line 31 / 600; pill text 36 (30 for "Minh hoạ" and source chips); captions 46 / 700; footer source line 26 (the single allowed small line). Nothing else is below 30.

## 3. Safe areas and grid (1080 x 1920)

- Side margin 72, content width 936.
- y 0-100 platform zone empty. Kicker pill y 112-172 (600 wide, centred).
- Headline y 190-400 (one or two lines, centred, max 936).
- Stage y 430-1340. Hero object cluster centred on a soft floor ellipse. Lowest content edge at every hold, measured from the layout: s1 1272, s2 1340 (label under the track), s3 1258, s4 1288, s5 1296, s6 1260, s7 1322. All >= 1250 and < 1340-1400.
- Caption pill: top 1400, centred, max 936, up to 2 lines. Footer source line y 1666. y 1700-1920 empty.
- Radius: cards 40-56, pills 999, bricks 60, photo cards 56. Nothing below 16.

## 4. Layers, back to front

1. `#bg` radial cream wash (CSS gradient, one element).
2. `#confetti`: 12 solid pastel dots, 26-66 px, in the left/right margins (x < 80 or x > 960), seeded, finite sine drift. Slowest-looking but fastest-moving layer. Must sit BEHIND `#world` (see trap 3).
3. `#world` camera wrapper: scale 1.00 -> 1.035 over the whole video (`ease:"none"`). Scene sections `.sc` inside it, one visible at a time.
4. Kicker pill and footer line (z 30).
5. `#ball` / `#blob1` transition shapes (z 42).
6. `#caps` (z 50).
No fade layer: the video opens on a finished composition and ends on one.

## 5. Components

- **Card** `.card`: `--card` fill, radius 40-56, shadow `0 14px 28px rgba(150,95,65,.24)` plus `inset 0 -8px 0 #f1d9c6` (clay thickness) and `inset 0 6px 0 rgba(255,255,255,.95)` (top highlight).
- **Pill** `.pill`: radius 999, height 76 (56 for tiny chips), pastel fill, ink text, `0 10px 20px` shadow plus inset bottom shade 6 px. Used for labels, chips and buttons.
- **Photo card** `.photo`: agy clay photo cropped by `overflow:hidden`, radius 56, 10 px cream ring. Ken Burns 1.00 -> 1.07 over the scene. Mark `data-layout-allow-overflow`.
- **Row** (list item): 936 x 140 card, 100 px circular clay icon cropped from an agy photo (circle window onto `parts.jpg`: width = 768 x k, k = 100 / span), title 42, sub-line 31.
- **Brick**: 800 x 140 card radius 60 with a pastel gradient, one text line 42. Three bricks stack like a tower.
- **Clay mascot** (inline SVG, 400 x 520 viewBox): groups `.r-wheels .r-arms .r-body .r-head .r-eyes .r-mouth`, gradients from shared `<defs>`. Built by `robotSVG(w,h)`; each part is a separate group so the same SVG can be assembled (scene 2), tilted (scene 5) or just sit (scene 4, 6).
- **Progress track**: 4 pebbles r 34 (last r 42) on a 16 px tube; a second accent tube grows over it with `stroke-dashoffset` (`pathLength=1`); a check mark is drawn with the same trick.
- **Tube + travelling dot** for a connection (Bluetooth): 18 px sky tube drawn once, an accent dot loops along it with a finite repeat.
- **Caption pill**: see section 8.
- Icons and mascots are inline SVG made of circles and rounded rects. agy photos are used for hero objects and parts only.

## 6. Motion language

- **Landing = squash-pop** (profile signature, used for every hero object): fall 0.20 s `power2.in` from y -150 (scaleY 1.14), squash 0.07 s to scaleX 1.2 / scaleY 0.8 (volume ~ kept: 1.2 x 0.8 = 0.96), settle 0.55 s `elastic.out(1,0.5)`. Transform origin 50% 100% so it squashes from the feet.
- **Pill / chip entrance**: scale 0.5 -> 1, `back.out(2)` 0.5 s. **List row plop**: y 50 -> 0, scale .9 -> 1, `back.out(2)` 0.5 s.
- **Headline**: each word scales 0.4-0.7 -> 1 with `back.out(2.2)` 0.5 s, stagger 0.07. Scene 1 headline is already opaque at frame 0 (scale only).
- **Press** (button on the spoken word): scale 0.92 in 0.09 s, back with `elastic.out(1,0.45)` 0.5 s.
- **Jump** (mascot happy): crouch 0.12 s (y +14, scaleY .9), rise 0.26 s to y -60..-70, fall 0.22 s `power2.in`, landing squash, `elastic.out(1,0.45)` 0.6 s.
- **Idle**: floating pills `bob` (y -5..-8, 0.9-1.2 s sine yoyo), mascot `sway` +-1.2..1.5 deg, photo Ken Burns, confetti drift. Every repeat is FINITE and sized to the hold (trap 2).
- **Camera**: only the slow push 1.00 -> 1.035 plus photo Ken Burns. No shake, no flash, no pulse (profile).
- Reveals are anchored on spoken words with `W(sid, word, nth, lead)`. Word times are ESTIMATED (drift up to ~0.3 s), so reveal 0.1-0.25 s EARLY and clamp to the scene start. For lists use a bigger lead for later rows so the scene never sits half empty (trap 8).

### Transitions (every boundary is covered by a squash or a shape, never a bare cut)
| From -> to | Kind | Timing |
|---|---|---|
| s1 -> s2, s4 -> s5 | press-in: outgoing scene scales to 0.9 | 0.12 s `power2.in`, hidden at the boundary; incoming objects drop in with squash-pop |
| s2 -> s3, s6 -> s7 | squash-pop: outgoing presses down (y 40, scaleY .94) | 0.12 s, hidden at the boundary |
| s3 -> s4 | roll-through: a 2600 px peach clay ball rolls left to right | starts 0.62 s before the cut, 0.9 s `power1.inOut`, scene swaps while the ball covers the frame (~0.3 s of full cover) |
| s5 -> s6 | blob-merge: a 1900 px mint blob swells from the centre | 0.30 s in `power2.in`, swap at full cover, 0.24 s out |
Outgoing ghost is <= 0.12 s because the section is hidden exactly at the boundary.

## 7. Scene recipes (6-7 scenes; S = scene start from `voice/timeline.json`)

Every scene = headline (y 196) + ONE object cluster (y 470-1290) + labels. The object is visible within 0.3 s of S (headline-only frames fail rule 1).

- **R1 Hook, photo hero (0-9.5 s).** Headline "Trẻ tự tay / lắp robot" (opaque at frame 0). Agy robot photo card 936 x 790 at y 480 pops with `elastic.out`; three pills overlap the card edge and pop on their spoken words: "Star Wars" (on "Chiến"), "Clementoni", "Từ 8 tuổi" (on "tám"). Ken Burns on the photo.
- **R2 Assemble (9.5-16.5 s).** SVG mascot (460 x 598) builds from parts: wheels at S+0.2, body on "hộp", arms on "Trẻ", head on "cuối", face on "robot"; a 4-pebble track fills in step (accent tube grows, pebble turns accent), last pebble gets a drawn check and a "Hoàn chỉnh" pill on "hoàn chỉnh"; the finished mascot jumps on "dựng nên".
- **R3 List of parts (16.5-25.1 s).** Five rows (circuit board, two motors, servo, speaker, two-colour LED), each with an agy-crop icon. Rows plop at S+0.28, S+1.0, then 0.9 / 0.5 / 0.45 s before their word. Icons breathe (scale 1.08, finite).
- **R4 Phone and mascot (25.1-33.3 s).** Clay phone (410 x 700, lavender body, cream screen, two buttons, three clay blocks) squash-drops at S+0.12, mascot at S+0.22. Sky tube draws on "Bluetooth" with a "Bluetooth" pill and a looping dot; buttons press on "điều khiển" and "lập trình"; "Điện thoại, máy tính bảng" label on "điện". An illustration chip "Minh hoạ" because the screen is invented, not the app's real UI.
- **R5 Reaction tiles (33.3-41.1 s).** Two cream tiles with generic clay faces (friend, foe), mascot below. Ripple on "Chạm"; on "bạn" the friend tile gets an accent ring, mascot jumps, "Hào hứng" pill; on "kẻ thù" the foe tile rings, mascot tilts -7 deg with eyes scaleY .45, "Cảnh giác" pill. "Minh hoạ" chip (faces are generic, not the app's art).
- **R6 Brick tower (41.1-47.9 s).** Mascot standing on three bricks (logic, creativity, fine motor skills) visible from S+0.2; each brick squashes (scaleX 1.04 / scaleY .94 then elastic) on its word; a clay gift box drops on "mùa" with a "Mùa quà cuối năm" pill.
- **R7 Soft ending (47.9-55.5 s).** Headline "Một chiếc hộp, / một chú robot"; agy box photo card (680 high, crop shows the box and bricks) pops; a cream note card states what the sources did NOT give ("Giá bán, số mảnh ghép: chưa được nêu"); two source chips with dates. Nothing fades; the last 1.5 s are a full composition with finite bobs.

## 8. Captions (Vietnamese karaoke)

- Cream pill `--card`, radius 56, padding 18 x 40, shadow `0 12px 24px rgba(150,95,65,.26)` + inset bottom shade, centred at top 1400, width 936, SegUIVar 700 46 px `--ink`.
- Current word `--accent-ink` (#a63a0b, 6.3:1 on the pill) and scale 1.05; spoken words go back to ink. Highlight with `tl.set` at the estimated word onset (no tween, so a late estimate cannot leave a half-coloured word). `.cw` words carry `margin:0 2px` so the scale does not glue neighbours together.
- Chunks 3-7 spoken words, split at `, . :`; each chunk is a list of word counts per scene (build code consumes words in order, so counts must add up per scene). Chunk visible from its first word minus 0.05 s to the next chunk (max 0.9 s after its last word).
- On-screen words equal the voice-over. Numbers on screen: "8 tuổi" (voice: "tám tuổi"), "Hai động cơ" (words both sides), dates 14.10.2025 / 18.10.2025 only in source chips and the footer.

## 9. Sound

The test pipeline had no music or SFX. Design intent (ASSUMED, untested): marimba or lo-fi 96-116 BPM at low level, soft boings on landings, squish on press, pop on pills, one soft chime on the ending. Voice only in this build: -15.5 LUFS, peak -4.2 dBFS (probe).

## 10. Images (agy, 3 used, ~1 min each)

Prompt skeleton that worked: "Soft clay 3D render, claymorphism, <object> made of puffy pastel plasticine, <colours>, soft contact shadow, plain warm cream background #fdf1e7, centered with margin, <view>". Results: all three came out as convincing plasticine (visible fingerprint texture) with no text.
- **The background is NOT exactly #fdf1e7** (box.jpg ~#f7e5d0, robot.jpg has a lavender floor): do not try to blend it into the page. Use the image as a framed photo card (radius 56, cream ring) or crop parts into circles.
- A flat-lay of loose parts on one image (`parts.jpg`) is the most useful asset: one generation gives 5 icons.
- Never ask agy for a licensed character (the build used a generic round clay robot for a Star Wars story; no logo, no real person).
- Mascot, phone, tubes, gift box, faces: build them in SVG. agy does not draw geometry or icons reliably.

## 11. Must not

- Pure black or neon; ink is warm plum.
- Sharp corners (< 16 px radius), hard-edged display type, grain or glitch.
- Accent orange as small text (2.1:1).
- Live WebGL; shake; flash; screen pulse.
- A landing without squash, a hard stop on a pill or card.
- More than 3 numbers in one scene; counters (this style has no counted numbers).
- Invented UI shown as real: any invented screen or character carries a "Minh hoạ" chip.
- An agy image used with a blended edge (trap 4).

## 12. Traps seen in real builds (written from THIS build; numbers measured)

1. **`immediateRender:false` leaks the finished state before the intro.** The first draft passed `immediateRender:false` to every `fromTo`. In the first render the scene-2 mascot was already complete at 10.0 s (body, wheels, head visible before their drops) and the "Cảnh giác" bubble sat on screen from 34.0 s to 40.0 s. Fix: remove `immediateRender:false` from every `fromTo` on a unique element (keep it only for shared layers). `grep -c immediateRender index.html` = 0 in the final build.
2. **An unbounded `repeat` inflates the timeline.** `repeat:40` on 12 confetti dots (2.1-3.5 s, yoyo) made `snapshot` report the end of the timeline at 136.2 s for a 55.49 s video. Fix: `repeat: Math.floor(DUR/d) - 1`. After this the end frame is at 55.49 s.
3. **Decoration above content.** Confetti with `z-index:1` painted over `#world` (positioned, z auto) and cut the last letters of the "Điện thoại, máy tính bảng" pill ("bả g" in the 28-32 s frames). Fix: no z-index on the dots; they come first in the DOM, so content is above them.
4. **agy background is not the page colour.** Measured by eye on the three images: backgrounds are cream gradients, one has a lavender floor. A multiply blend would show a halo. Fix: framed photo cards and circle crops (section 10).
5. **Headline orphan.** "Robot trẻ em tự tay lắp" wrapped as 4 words + "lắp" alone at 92 px. Fix: explicit line breaks with `|` in the headline source ("Trẻ tự tay|lắp robot"); words stay wrapped in `.w` spans per line.
6. **Voice length.** First draft (about 260 words) = 65.7 s; second 60.7 s; final 55.5 s (224 words, 53.0 s of speech + 6 x 0.35 s gaps + 0.35 s tail). Rule of thumb measured here: ~4.2 words per second of speech. Trim before building, because chunk counts and anchors depend on the final text.
7. **A transition shape that stays too long.** The first mint blob took 0.34 s to shrink, so the new scene's first 0.5 s was mostly covered and read as "empty". Fix: 0.24 s out. Ball roll still covers ~0.3 s; keep the incoming scene's first object <= 0.15 s after the cut.
8. **A list scene that is half empty for 2.5 s.** With rows tied only to their words, rows 2-5 arrived at 18.8 / 20.9 / 22.3 / 24.1 s and the lower half was blank for seconds. Fix: second row at S+1.0 and later rows 0.9 / 0.5 / 0.45 s early (a visible preview is fine, a blank half is not).
9. **GSAP does not animate `left/top` reliably** (sample t108): `tl.set("#mascot",{left,top})` left the mascot at the page corner (top-right after its x tweens). Fix: put the start position in CSS and tween only `x/y`.
10. **SVG viewport clips glow** (sample t170): a glow circle bigger than the bulb svg was cut into a square. Fix: `overflow:visible` on the svg plus `data-layout-allow-overflow`.
11. **Inspect noise.** `hyperframes inspect` reported 13 warnings: container overflow for Ken Burns images, a pebble 2 px above its svg, circular icon crops (all intentional; marked `data-layout-allow-overflow`) and `span.w` overlaps during headline pops (transient). `lint` keeps 3 harmless `overlapping_gsap_tweens` warnings and `composition_file_too_large` (466 lines).
12. **Sandbox limits.** Custom Python could not be run, so contrast was computed by hand and fonts checked by eye in snapshots. Treat the section 1 ratios as hand calculations (not machine-measured); they are consistent with the `validate` AA pass but not proven by it.
13. **Estimated word times.** `voice/timeline.json` splits each scene by character count; anchors can drift by a third of a second. Lead 0.1-0.25 s; never anchor a reveal on the LAST word of a scene.
14. **Frame check passes, eyes still needed.** `frame_check.py` reported 0 BLANK frames in both the first (broken, trap 1) and the final render. It cannot see early reveals or half-empty lists; the contact sheet found all of traps 1, 3, 5, 8.
15. **Facts gate.** The only fresh-looking stories found (WhalesBot, 10-11 Nov 2026) were a companion robot (not a kit) or behind HTTP 403; the story used is 13 months old. Say the age in the manifest and keep a source footer on screen.
