# Style: precision-hardware (9:16 Vietnamese hardware-news edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Hardware stories whose subject is a physical object made of parts: a phone camera module, a lens, a chip or accelerator, a drone, a camera body, a wearable. It is strongest when the story names components and a few specs (megapixels, focal lengths, memory, launch date) that can each be pinned to one part. Observed in this build: a spec-confirmation story with 4 equal numbers (4 cameras x 50 MP) and one date carried a 57 s video without a single counter. Weak fit: earnings, policy, people, quote stories, anything without an object to take apart. Use tier 2 for other channels, clients or purposes so the search does not start from zero. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built and measured on the first real build (2026-11-12). Section 12 lists what is still ASSUMED. Section 13 "Traps seen in real builds" is the most important section for the next builder; where it disagrees with sections 1 to 11, section 13 wins. Later builds append sections 14+, the newest last wins.

**Clips and screenshots are optional.** This build had none (the maker published no exploded view and no usable clip). If a real maker render or clip exists, the media-first rules of the other owner documents apply (media >= 900 px wide and the largest element). Never fake, invent or pad media.

**Example videos show the visual recipe, not the niche.** Copy how it is built, not what it is about.

**Status.** Written 2026-11-12 from one full build (`final.mp4`, story: Oppo confirms the Reno 17 camera set, 56.9 s) and two 10 s silent samples (cinema lens, accelerator chip). Kept by the owner. Not merged into the skill folder.

Precision hardware is engineered and calm: graphite and silver carry the product, one blue marks the part being talked about, parts separate along an axis into an exploded view and hairline leader lines draw only after the parts come to rest. The camera moves like a drone (combined scale, x and rotation), never shakes, never flashes. Energy 3 (profile). Narration-led: a new focal part every 1.1-3 s inside a scene.

Source of values: `skill/references/styles/profiles/precision-hardware.yaml`. **ASSUMED** = the profile gives no value and this build chose one. **SUBST** = a named font is not installed. **DEVIATION** = knowingly differs from the profile (reasons in `compare.md`).

## 1. Tokens

```css
/* from the profile */
--bg:#0d0f12;        /* page */
--ink:#f2f4f7;       /* headline, values, caption text        17.42:1 on bg, 13.80 on graphite, ~16.0 on tile */
--accent:#3aa0ff;    /* callout dots, active ring, kicker dot  7.00:1 on bg, 5.54 on graphite, ~6.4 on tile (marks only by rule) */
--graphite:#22262c;  /* plates, puck bodies */
--silver:#c7ccd3;    /* hairlines, leaders, sub text           11.89:1 on bg, 9.41 on graphite, ~10.8 on tile */
--mute:#7d848d;      /* inactive dots ONLY                      5.08:1 on bg but 4.02 on graphite: never text on graphite */
--sky:#8fd3ff;       /* active spec value, current caption word 11.81:1 on bg, 9.35 on graphite, ~10.7 on tile */
/* ASSUMED, added in this build */
--tile:#171a1f;      /* spec tile fill (graphite is too light behind mute text) */
--mute2:#a3aab3;     /* labels, kickers, inactive callouts      8.19:1 on bg, 7.44 on tile, 6.48 on graphite */
--hair:rgba(199,204,211,.22); /* 1 px tile and card borders (profile: silver at 20%) */
```

Contrast: WCAG 2 formula, computed by hand from the hex values in this build (the build sandbox blocked ad-hoc measuring scripts, see trap 1); `hyperframes validate` independently reported "35 text elements pass WCAG AA" on the main video and 40 on each sample. Colour rule (profile): graphite and silver carry the product; blue only for callout dots, the active ring and the active spec value (sky); outdoor or product imagery stays natural. Inactive callouts are `--mute2`, never dimmed by opacity.

## 2. Fonts (4 local files; the profile's Manrope / IBM Plex Mono / Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, body, callouts, tile text, captions | Manrope 700/400, Be Vietnam Pro 600 | `SegUIVar.ttf` (SUBST), weight axis 300-700; headline 700, callouts and captions 600 | 0 of 67 test letters missing (owner documents' fontTools run on the same file); every diacritic in this build rendered intact in the 15 snapshots read by eye (ắ ằ ẳ ẵ ặ ấ ầ ẩ ẫ ậ ế ề ể ễ ệ ố ồ ổ ỗ ộ ớ ờ ở ỡ ợ ứ ừ ử ữ ự ơ ư đ seen in "Tách cụm camera", "Lớp thứ", "tự sướng", "Xác nhận chính thức") |
| Spec values, units, kickers, tags, tile labels | IBM Plex Mono 500 | `CascadiaMono.ttf` (SUBST), 600 | 0 missing (same sources); "LỚP 01 · CAMERA CHÍNH", "ẢNH ĐỘNG", "TIÊU CỰ" rendered intact |
| Not used | | `cambriai.ttf` | no quote in this story |
| Never | | `segoepr.ttf` | lacks Vietnamese letters (92 missing in the owner check): never used |

Declare with `font-display:block`, `font-weight: 300 700` / `200 700`. My own glyph script (`tools/measure.mjs`, cmap parser) was written but could not be run (permission block), so the font row rests on the earlier measured run plus the visual check.

### Type scale (1080 x 1920, px)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.kicker` | Mono 600 uppercase +0.06em | 30 / 1.2 | `--mute2`, 12 px accent dot before it, y 176 |
| `.h1` | Seg 700, -0.02em | 70 / 1.14 | profile 68; 2 lines max with explicit `<br>`, <= 24 characters per line ("Tách ống kính anamorphic" = 24 fits 960 px) |
| callout `.co` | Seg 600 | 40 (vertical exploded) / 32-36 (samples) | number prefix `01` in Mono 34 |
| tile label `.lb` | Mono 600 uppercase | 30 | `--mute2` |
| tile value `.val` | Mono 600 | 64 default; 76 hook; 100-120 readout | readout value in `--sky` when it is the active spec |
| tile text `.txt` | Seg 600 | 34-52 | for words, not numbers |
| `.tag` (on images) | Mono 600 | 30 | ink on rgba(13,15,18,.92) |
| `.chip` | Seg 700 | 30 | 2 px accent border |
| diagram label `.lbl` | Seg 600 | 32 | silver |
| `.src` footer | Seg 500 | 26 | the ONE text below 30 px (acceptance 8); one line, <= ~80 characters |
| caption | Seg 600 | 44 / 1.3 | see section 8 |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  platform UI: empty
y 176  -212  kicker
y 226  -386  h1 (2 x 70 px x 1.14)
y 420/430 -1100  BODY: product card / exploded stage / diagram card
y 1050/1110 -1282  readout tile or tile row (lowest content edge 1280-1282 in every scene)
y 1298 -1332  footer source line (26 px)
y 1372 -~1440  caption pill (1 line; 2 lines would end ~1500)
y 1500 -1920  bottom platform UI: empty
x 60 - 1020  content column 960 px; two half tiles 470 + 20 gap + 470
```

Exploded stage (scene coordinates, stage at (60,420), 960 x 680): island plate centred (250,520) half-width 200 half-height 112; seats (180,508) (320,493) (250,563); exploded column x 250 at y 330 / 200 / 70 (130 px apart); leaders from x 312 to x 470; callout text at x 490. Samples: horizontal axis at y 110 with elements at x 120 / 340 / 560 / 780 (lens), vertical column at y 100 / 190 / 262 / 334 (chip).

## 4. Layers, back to front

`#bg` (one radial graphite gradient "studio floor", scales 1.00 -> 1.06 over the video) -> `#floor` hairline -> `#world` (scene sections, one visible) -> inside a scene: product card or SVG stage (midground, with its own camera wrapper) -> readout tiles -> `#fg` (two silver registration corners at y 410 that drift -24 px over the video: the fastest layer, parallax 1.6x) -> `#caps`. No flash layer, no shake, no fade layer (frame 0 and the last frame are full compositions).

## 5. Components

- **Product card** `.card`: 960 wide, radius 12, 1 px `--hair`, `overflow:hidden` + `data-layout-allow-overflow`; holds a still inside a camera wrapper (`#s1cam`) that is oversized so a drone move never shows an edge. Always carries a 30 px tag "Ảnh minh hoạ, không phải máy thật" when the image is generated.
- **Exploded stage**: one inline SVG. Island plate = two polygons (top face rhombus + darker side band, 24 px thick). A **puck** (one lens/camera) = side path `M-62,0 L-62,30 A62,34 0 0 0 62,30 L62,0 Z` filled with a 3-stop graphite gradient + top ellipse rx 62 ry 34 silver 3 px stroke + 2 inner ellipses + a 9 x 4 violet glint at 55%. A periscope puck uses a diamond window instead of an ellipse. Chip layers = isometric rhombi (lid 180 x 90, die 80 x 40, 4 memory stacks 30 x 15, substrate 200 x 100). Lens groups (sample) = vertical ellipses / one rounded rect (cylindrical anamorphic block).
- **Leader + callout**: 1.5 px silver line, blue terminal dot r 8 at the part end, label to the right; active label `--ink` with its number in `--sky`, inactive `--mute2`.
- **Readout tile** (signature of this build): ONE tile under the stage that always shows the active part's spec: label `LỚP 01 · CAMERA CHÍNH`, value `50 MP` in sky. It swaps (hide old, flip new in) on the spoken word, so the same number is never on screen 3-4 times (no-repetition rule).
- **Viewfinder overlay**: thirds grid (two 1 px lines each way at 28% silver), four 56 px corner brackets 3 px silver, a blue AF box that locks (scale 1.6 -> 1, 0.45 s) and an "AF" tag whose dot turns blue on lock; for a field-of-view story a dashed silver frame that widens (0.7 s power3.inOut) and a chip with the zoom value.
- **Periscope diagram**: phone body as a rounded bar 880 x 140, prism triangle, three lens ellipses, sensor bar, light path `M150,30 L150,302 L798,302` drawn with `pathLength=1` dashoffset, a blue marker r 10 travelling the fold (0.45 s down `power2.in`, 0.75 s across `power2.out`, 3 finite passes), lens group slides x 0 -> 70 -> 30 on "zoom".
- **Spec tile grid**: 2 x 2 half tiles 470 x 200-212; active tile = 3 px accent ring + blue dot; inactive tiles stay at full opacity.
- **Footer source line** `.src`: per scene, names the outlets and dates; says "Minh hoạ" when the picture is an illustration.

## 6. Motion language

Energy 3. Eases used: `power2.inOut` (drone move), `power3.out` (explode, flips, entrances), `power2.out` (leaders, rings), `sine.inOut` (bob, orbit, holds), `power2.in` (exits), `back.out(1.4)` (one zoom chip only). No elastic, no shake, no flash, no glow.

| Verb | Recipe as built |
|---|---|
| Drone fly-through | camera wrapper `scale 1.3 -> 1, x 200 -> 0, rotation 3 -> 0`, 2.4 s `power2.inOut` (profile) on product cards; 1.4 s on the exploded stage (DEVIATION: 2.4 s kept text-adjacent parts moving too long) |
| Gimbal orbit | `rotationY -6 -> 6` (perspective 1400) over the rest of the hook (profile asks -20 -> 20: too much for a flat photo, DEVIATION) |
| Exploded view | parts translate to their axis slots with 0.05 s stagger, x `power3.out` 0.9 s, y `power2.inOut` 0.9 s (an arc, not a rail); the island drops 14 px |
| Leader draw | starts at `explode start + 0.1 + 0.9` (parts at rest): line `scaleX 0 -> 1` 0.35 s `power2.out`, stagger 0.08; dot appears with the line; label slides x -16 -> 0, 0.35 s, 0.2 s later |
| Active part | label colour 0.2 s + dot ping (scale 1 -> 1.4 -> 1, 0.12 + 0.35 s) on the spoken ordinal word (`W("nhất")-0.1`) |
| Spec flip | `rotationX 60 -> 0` (perspective 900, origin bottom) 0.5 s `power3.out`, opacity 0 -> 1 in the first 0.12 s; readout swaps 0.35 s |
| Bob | the exploded group y 0 -> -6 px `sine.inOut`, finite yoyo sized to the hold |
| Settle | `scale 1 -> 1.025-1.04` linear over the hold on the stage or card |
| Counters | none: every value is final when it appears (DEVIATION: profile says values `odo()` in; with 4 equal "50 MP" values a counter adds nothing and risks a mid-count frame) |

Pacing: scenes 7.7 / 7.9 / 9.0 / 7.7 / 13.1 / 11.3 s; something changes every 1-3 s; the 13.1 s scene has an internal cut on the word "Máy" (headline swap, card shrinks 600 -> 390 px, four tiles flip in).

### Transitions (profile vocabulary, 3 used)

Every cut: outgoing scene fades 0.15 s `power2.in` ending exactly on the boundary, then `visibility:hidden`; the incoming scene is visible from S-0.08. Measured on a 30 fps strip: 2-3 frames show both scenes, under the 0.15 s ghost limit.
1. **Horizon tilt** (s1 -> s2): outgoing rotates 0 -> 8 deg while fading; incoming starts at -8 deg and settles to 0 in 0.7 s `power2.out`.
2. **Fly-through** (s2 -> s3, s5 -> s6): outgoing scales 1 -> 1.3/1.35 while fading (push past the foreground); incoming runs the drone move.
3. **Exploded split** (s3 -> s4): the two upper pucks fly up 160 px and the island drops 200 px in the last 0.15 s; the next diagram assembles from parts (prism from x -160, lenses from y -140, sensor from x +160, 0.6 s `power3.out`, 0.05 s stagger).
4. **Clean cut** (s4 -> s5): 0.1 s fade and a 24 px rise of the incoming card.

## 7. Scene recipes (S = scene start; W() = estimated word onset; every start clamped with `Math.max(0, ...)`)

### R1 Hook: product hero (0-7.95 s)
Kicker "OPPO RENO 17 · CAMERA"; h1 "4 camera, cả 4 đều / 50 triệu điểm ảnh" (static from frame 0); product card 960 x 650 at y 430 with the drone move from 0 s and orbit after 2.4 s; AF box 360 x 380 lands at 1.2 s and pings on "cụm"; chip "Xác nhận chính thức" drops on "chính"; config tile 960 x 182 at y 1100: "4 × 50 MP" Mono 76 + "3 mặt lưng / 1 mặt trước". Frame 0 already shows everything except the AF box and chip.

### R2 Source: viewfinder (S 7.95)
h1 "Oppo công bố qua / hình ảnh quảng bá"; viewfinder card 960 x 600 (lens macro, slow scale 1.12 -> 1.0); AF locks on "quảng"; two half tiles "Hình thức: Ảnh quảng bá của Oppo" and "Áp dụng cho: Reno 17 tiêu chuẩn" flip in at S+0.05 / S+0.13; ring moves A -> B on "áp".

### R3 Exploded view (signature, S 15.82)
Assembled module on screen from S-0.08 (no empty stage), readout "MẶT LƯNG / 3 camera"; explode on "tách"; leaders after rest; callout 01 active on "nhất" and readout -> "LỚP 01 · CAMERA CHÍNH / 50 MP" on "chính"; 02 on "hai", readout swap on "rộng". Footer "Minh hoạ cấu trúc, không phải bản vẽ của Oppo".

### R4 Principle diagram (S 24.81)
Periscope card 960 x 580; readout tile 960 x 232 "LỚP 03 · TELE TIỀM VỌNG / 50 MP" (110 px sky) from S; light path draws at "kiểu", marker passes, lens group slides on "zoom". Tag "Minh hoạ nguyên lý".

### R5 Viewfinder + spec grid (S 32.52, internal cut)
Part A: front-camera viewfinder, readout "CAMERA TRƯỚC · GÓC SIÊU RỘNG / 50 MP"; FOV frame widens and chip "0,6 lần" pops on "không". Part B (on "Máy"): kicker and h1 swap ("Live Photo ở / nhiều tiêu cự"), card shrinks to 390 px, readout flips away, tiles "Live Photo / 6 giây / 4K / Nhiều, kể cả tự sướng góc rộng" flip in 0.08 s apart; the ring walks on "live", "sáu"(2nd), "bốn", "nhiều".

### R6 Launch card, soft end (S 45.59, holds to 56.9)
h1 "Reno 17 ra mắt / tại Trung Quốc"; product card 960 x 480 with drone move then slow -40 px rise; tiles "Ngày: 16 tháng 11", "Giờ địa phương: 7 giờ tối", wide "Còn chờ sự kiện: Camera bản Pro chưa xác nhận · giá, thông số còn lại"; ring walks on the date, the hour, "Hãng". No fade out: the last 1.5 s (and 1.04 s of silent tail) hold the full composition.

### Sample recipes (no voice, 10 s)
t111 lens: card 340 px + horizontal exploded barrel (4 groups) with leaders down to staggered labels + 2 trait tiles. t032 chip: card 200 px + vertical isometric stack (lid, die, memory, substrate) + 2 tiles with empty values ("— GB", "$ —") so no spec or price is invented. Explode at 0.9 s, leaders at ~1.95 s, active walk at 3.4 / 4.5-4.6 / 5.6-5.8 / 6.7-7.0 s, tiles light at 4.6-5.6 and 7.0-7.6 s, bob from 3.0 s.

## 8. Captions (Vietnamese karaoke)

Dark pill (profile): rgba(13,15,18,.86), radius 16, 1 px silver at 20%, padding 14 x 28, Seg 600 44 px (profile 42), max width 960, top 1372. Current word `--sky`, other words `--ink` (two states only). Chunks: split at `, . : ; ! ?` after >= 3 words or at 6 words; chunks under 3 words merge into the previous. Visibility and highlight by `tl.set` only (no fades, so no caption ghost). Display text maps spoken numbers to digits with a small pattern table (năm mươi -> 50, mười bảy -> 17, không phẩy sáu -> 0,6, bốn K -> 4K, sáu giây -> 6 giây, bảy giờ -> 7 giờ, cả bốn -> cả 4, bốn camera -> 4 camera, mười sáu -> 16, mười một -> 11); a mapped token highlights at its first spoken word. Word times are the same character-share ESTIMATE as `voice/timeline.json`.

## 9. Sound

Voice only (VieNeu "Hải Đăng"): no music or SFX tools were available. Profile: uplifting electronic / cinematic pop 110-120 BPM, air whoosh on fly-throughs, mechanical clicks on exploded parts; beat response (callout pings on kicks) was moved to spoken words. Mux: -15.4 LUFS integrated, peak -4.2 dBFS.

## 10. Images (agy)

agy makes atmosphere and the object, never the diagram. Prompt suffix that worked for all four images: "Precision hardware product photography: machined graphite and brushed silver metal, soft studio rim light from the upper left, deep graphite background #0d0f12, crisp, clean, no glow, no neon, photoreal render." Outputs 768 x 1376 JPG, re-encoded to 1080 wide `-q:v 4` (hero 51 KB, lens 237 KB). Results: phone back with a 3-lens island (usable, but see trap 4), macro lens rings (excellent as a viewfinder backdrop), cinema lens on a dark floor, chip package with gold traces. Exploded views, leader lines, light paths and isometric plates are SVG, never generated.

## 11. Must not

- No shake, flash, glitch, glow, neon, cartoon texture (profile `avoid`).
- No leader line before its part is at rest (profile constraint).
- No blue on anything but callout dots, the active ring/spec and the kicker dot.
- No exploded view, cutaway or "inside" picture presented as the maker's own drawing: label it "Minh hoạ" on screen and in the footer.
- No spec or price on a generic sample: leave the value empty ("— GB").
- No number shown more than twice at once (captions excluded): use the readout tile.
- No counters held mid-count (none were used).
- Nothing below 90% opacity on a held frame; inactive states use colour, not opacity.
- Nothing below y 1340 except the caption pill; nothing below ~1500.
- No mention of a US organisation by acronym in the voice (none in this story).

## 12. Still ASSUMED after this build

`--tile`, `--mute2`, caption pill alpha .86, the readout-tile pattern, 0.08 s scene overlap, orbit amplitude 6 deg, 1.4 s stage fly-through, two-state caption highlight; VieNeu reading of "Oppo", "Reno", "Live Photo", "Pro" is unheard (listed in `ear-check.txt`); word times are estimates.

## 13. Traps seen in real builds (this build, 2026-11-12, measured)

1. **Measuring scripts blocked.** The sandbox only allowed `motion_tools.py`, `frame_check.py`, `npx hyperframes` and ffmpeg; `python3 measure.py` and `node measure.mjs` both needed approval. Contrast was computed by hand and cross-checked by `hyperframes validate` (35/40/40 text elements pass AA). Next time: put measurements in a step the allowlist covers, or ask for the allowlist in the interview.
2. **Fresh-story pages blocked.** gizmochina, 91mobiles, mezha and deccanherald returned 403; gsmarena redirected to a `tollbit` gate (not followed). The story was carried by Sportskeeda, My Mobile India, TechGenyz and Unbox PH (all 200). Six searches before a fitting 48 h story was found; "exploded view" searches return stock art: search for "camera specs officially confirmed" + the week instead.
3. **The shape outran the story.** The rank-1 shape is "maker shows an exploded view", but the real story only confirmed specs; no maker drawing existed. Fix used: the exploded view is an honest illustration with "Minh hoạ cấu trúc, không phải bản vẽ của Oppo" in the footer and no lens-to-part mapping on the photo. Never label which lens on a generated photo is which camera.
4. **agy drew a famous silhouette.** Asked for a "generic unbranded smartphone ... square camera island", agy returned a triangle triple-lens layout that reads like another maker's flagship and not like the square Reno module (Unbox PH: "square camera module"). Accepted only with the tag "Ảnh minh hoạ, không phải máy thật" on both product cards; next time add "lenses in a straight vertical row" or similar to steer away from known layouts, and look at the image before use.
5. **Four equal numbers.** Callouts carrying "50 MP" each would put the same number on screen 3-4 times. Fix: callouts carry names only; one readout tile carries the value of the active part and swaps on the spoken word. Measured: "50" never appears more than twice at once (h1 + tile in s1; once in s3-s5).
6. **Sample overlap.** First t032 snapshot: the exploded lid (top y 610) sat 70 px over the image card (bottom 680). Fixed by card 250 -> 200 px and stage top 700 -> 640 and column y 100/190/262/334; lowest edge then 1088 (stage) and 1282 (tiles).
7. **Flip entrance looks dim.** A tile at rotationX 60 is foreshortened for ~0.3 s; the strip frames show it pale. It is an entrance (< 0.5 s), not a held frame, so accepted; keep opacity reaching 1 in 0.12 s.
8. **Caption chunk breaks.** The 6-word cap split "zoom quang | học" and "Kiểu ống kính tiềm" mid-phrase. Accepted; next time cap at 7 words or split only at punctuation and spaces before a content word.
9. **Lint noise.** `overlapping_gsap_tweens` (8, static analysis of tweens on shared classes at time 0), `duplicate_media_discovery_risk` (hero.jpg used in s1 and s6) and `composition_file_too_large` (398 lines): 0 errors; accepted.
10. **Script size.** 222 spoken words, 6 scenes, gap 0.35 s = 55.86 s (3.97 words/s incl. gaps); video = voice + 1.04 s = 56.9 s. For this voice aim at 200-220 words.
11. **Numbers.** Render 29 s for 56.9 s (silent 13.4 MB, standard quality), final 9.1 MB; samples rendered in ~10 s each (2.8 and 1.7 MB). `frame_check.py`: silent and final 114 frames, 0 BLANK, 0 TOPHEAVY; samples 20 frames each, 0 BLANK, 0 TOPHEAVY. Lowest content edge at every hold 1280-1282 (tiles) plus footer to 1332.
