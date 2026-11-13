# Style: Accelerated Compute (9:16 Vietnamese chip-news edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build:** a story where a chip or platform maker claims a measured multiple over its own previous model (2x, 2.7x, +80%) and the claim comes with 3 to 6 sourced numbers: accelerator, GPU or TPU launches, AI-infrastructure announcements, public benchmark leaderboards, spec-and-price reveals. Bars with a baseline carry the story. Not for quote stories, human-interest stories, finance results, enforcement or anything slow. Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the recipe as built. Section 12 lists the traps seen in THIS build (2026-11-12) with measured numbers; where 12 and an earlier section disagree, 12 wins. Everything the profile (`styles/profiles/accelerated-compute.yaml`) does not give is marked **ASSUMED**.

**Status.** Written 2026-11-12 from one real build: `final.mp4`, 55.8 s, 1080x1920, 30 fps, 13.8 MB, story "Google TPU 8i Max and TPU 8tx" (blog.google, 2026-11-09), plus two 10 s samples (`samples/sample-t032.mp4`, `samples/sample-t027.mp4`). No owner has reviewed it. Not merged into the skill folder.

Energy 4 (profile): black stage, acid-green light, bars that surge past a baseline, one slam per big number. No music in this build (sound is voice only).

## 1. Tokens

```css
--bg:#050505;      /* stage */
--ink:#ffffff;     /* headline, numerals     20.4:1 on bg, 17.4:1 on steel */
--acc:#4cc41c;     /* bars, ring, bar fills; text only >= 30 px   8.95:1 on bg, 7.64:1 on steel */
--lime:#a4e22b;    /* current caption word, kicker, big numbers  13.1:1 on bg, 11.2:1 on steel */
--steel:#1a1a1a;   /* panels, cards */
--rival:#333333;   /* baseline / rival bar fill (ink on it 12.6:1) */
--mute:#8c8c8c;    /* 6.06:1 on bg, 5.17:1 on steel: ok but the build used --mute-ink instead */
--mute-ink:#b8b8b8;/* ASSUMED: labels, notes, footer (about 9.5:1 on steel) */
--cyan:#00c2ff;    /* secondary series only (the partner CPU node): 8.4:1 on steel */
/* dark text on green: #050505 on #4cc41c = 8.95:1 (bar names and values inside a green bar) */
```

Contrast figures are hand-computed with the WCAG formula (relative luminance: bg 0.0015, steel 0.0103, acc 0.411, lime 0.624); `hyperframes validate` confirmed "20 text elements pass WCAG AA" on the full video and 15 on each sample. Rule kept from the profile: green is the energy colour, cyan only for a secondary series, no other hue. Material: radius 20, 1 px green border at 40%, inset glow `0 0 40px rgba(76,196,28,.08)`, outer glow `0 0 30px rgba(76,196,28,.10)`. Glows are box-shadows, never `filter`.

## 2. Fonts (3 local files; the profile's Sora / JetBrains Mono / Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, captions, card sub-lines | Sora 700 / 800, Be Vietnam Pro 600 | `SegUIVar.ttf`, weight axis 300-700: headline 700 -0.02em, captions 600 | Rendered frames show ắ ằ ế ề ổ ợ ứ ữ ự ơ ư đ correctly (checked in the snapshots and in the final frame sheet). Owner docs record 36 of 36 test letters present for this file. The fontTools script could not run in this session (python was not permitted for a new script), so the letter test is by rendered pixels, not by glyph table |
| Labels, units, model names, numerals | JetBrains Mono 500 | `CascadiaMono.ttf`, weight axis 200-700: labels 600, big numbers 700 | same; model names (TPU 8i Max) and numerals (2,7×) are Latin and digits |
| Never | | `segoepr.ttf` | owner docs: 35 of 36 Vietnamese test letters missing |

`cambriai.ttf` is unused. Faces declared with `font-display: block`. The profile's 800 weight does not exist: 700 is used (ASSUMED).

### Type scale (1080 x 1920, px; all measured from the build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.kick` | Cascadia 600, +0.1em | 30 / 1 | lime; max about 22 characters when a badge sits at x 760 (about 20 px per character) |
| `.h1` | Segoe 700, -0.02em | 76 / 1.1, mask 84 px per line | max 2 lines, one claim; key word in lime |
| `.big` | Cascadia 700, -0.04em | 240 hero, 200 date, 170 two-number panel, 150 counter, 130 tile | lime with a 40 px green text-shadow |
| `.val` | Cascadia 700 | 34-84 | model names 84, bar-end values 34-40 |
| `.lbl` | Cascadia 600 | 30 | `--mute-ink`, uppercase, max about 36 characters in a 792 px track |
| bar name | Segoe 600 | 30 | ink on `--rival`, `#050505` on green |
| `.sub` / `.note` | Segoe 600 / 500 | 32-44 / 30 | notes never below 30 |
| footer `#src` | Cascadia 500 | 26 | the one allowed line under 30 px; always "Nguồn: ..." |
| caption | Segoe 600 | 44 / 1.25 | pill, see section 8 |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -140  top platform UI: empty (badge "Minh hoạ" in samples sits at y 140-188)
y 150  -180  kicker (30 px)
y 196  -364  headline (2 lines x 84), green bar x 80, y 204-372, 6 x 168
y 450  -1290 BODY: one steel panel x 96, 888 wide, up to 840 tall (or die image full frame in scene 1)
y 1316 -1342 source footer (26 px, one line)
y 1366 -1496 caption pill (bottom edge 1480-1490)
y 1496 -1920 bottom platform UI: empty
x 96   -984  content column, 888 px; panel padding 48 -> track 792 px
```

Rule from the acceptance list: at every hold the lowest content edge is >= y 1250. In this build every body panel ends at y 1288-1290 and scene 1's die ends at about 1325. Nothing but the footer and caption sits below 1290.

## 4. Layers, back to front

`#root` (flat `#050505`) -> per-scene `section.sec` (each carries its own opaque background: `linear-gradient(rgba(5,5,5,.9)...)` over the baked circuit PNG, so the 10% circuit texture is part of every scene and no scene shows through another) -> `.cam` (one per scene, `settleCam` scale 1.00 -> 1.03 linear over the scene) -> `#ptl` (48 seeded dots, 6 px, opacity .25-.6, rising 220-640 px over the whole video, linear, one tween each) -> `#sweep` (12 px lime bar with a green glow) -> `#src` footer -> `#caps` -> `#flash` (pale green, 0.22-0.5 peak) -> `#fade` (0.3 s fade-in only; there is NO fade-out, the last frame is a full composition).

## 5. Components

- **Panel** `.panel`: steel, radius 20, green border 40%, 888 wide.
- **Bar** `.bar` (56 px; 90-110 px in a 2-bar chart): fixed width = value x unit (396 px = 1x, 792 px = 2x in a "2x" chart; 792/2.7 = 293 px for 1x in a "2.7x" chart). Rival = `--rival`, ours = `--acc` with `0 0 26px rgba(76,196,28,.55)`. Name inside at the left, value at the bar end (inside right for ours, outside right for the baseline). Revealed with `clip-path: inset(0 100% 0 0)` -> `inset(0)`, never by animating width (section 12, trap 2).
- **Die icon** `.die`: 130 px square, 3 px green border, four 26 px squares and a lime centre dot; two of them merge for a "two chips in one package" beat.
- **Node** `.node` (diagram): 688 x 190, green border; the secondary partner (host CPU) uses `.node.cy` with cyan.
- **Packet** `.pk`: 18 px lime (or cyan) dot travelling along an edge with `power1.inOut`, finite `repeat: 2`.
- **Cell grid** `.cell`: 140 x 118, 5 x 4, gap 12, inside a dashed footprint box; lit cells `#4cc41c`.
- **Tile** `.tile`: 280 x 290 recap tile (130 px "2×" + 32 px label).
- **Badge "Minh hoạ"** (samples only): lime pill 224 x 48 at x 760, y 140.
- **Unit and baseline rule** (profile): every chart panel states its baseline in a 30 px note ("Mốc: TPU 8i = 1×") and any derived number says how (`1,8× = 1 + 80%`; bar length is "minh hoạ tỷ lệ 2×").

## 6. Motion language (measured)

| Move | Values |
|---|---|
| Headline | masked line rise `yPercent 115 -> 0`, rotation 3 -> 0, 0.5 s `expo.out`, stagger 0.08; kick fades from x -30 in 0.35 s; green bar scaleY 0 -> 1 in 0.4 s |
| Panel in | `y 50 -> 0`, opacity 0 -> 1, 0.4-0.5 s `expo.out` |
| Baseline bar | clip reveal 0.6 s `power4.out`, started 0.25-0.4 s after the scene start so the scene has content at once |
| Surge bar | clip reveal 0.9 s `power4.out`, starts 0.05-0.3 s BEFORE the spoken word; ours is always longer than the rival so it "clears" it |
| Slam (hero number) | scale 1.6 -> 1, opacity 0 -> 1, 0.26 s `expo.out`, pale flash 0.5 -> 0 in 0.14 s, six 1-frame seeded shakes of the die (amplitude 18 px decaying) |
| Counter | 0.7 s `power3.out`, then a 1.06 bump in 0.12 s (used for the footprint multiplier 1× -> 2×; finishes inside 0.8 s) |
| Camera | `settleCam` 1.00 -> 1.03 linear per scene; scene 1 pushes the die image 1.25 -> 1.0 in 0.9 s `expo.out`, then 1.0 -> 1.07 |
| Transition: trace-through | 0.15 s: incoming scene revealed by `clip-path: inset(0 0 100% 0)` -> `inset(0)` top to bottom (`power2.in`) while a 12 px lime bar with glow runs y -30 -> 1950; outgoing hidden at +0.15 s, clipPath reset at +0.151 s. A 0.15 s overlap is the limit for "no ghost" |
| Internal cut (scene longer than 7 s) | scene 5 (11.3 s) swaps the diagram for the latency chart on the word "Độ trễ" (instant visibility swap, new panel scales 0.96 -> 1 in 0.3 s) |
| Particles | linear, finite, one tween per dot over the whole video |

No `filter: blur`, no per-element bloom. `clip-path` is used on at most 15 elements at a time (bars) plus the scene wipe.

## 7. Scene recipes (starts from `voice/timeline.json`; word anchors from `T(sid, phrase, nth)` = scene start + speech x (characters before the phrase / all characters))

| Scene | Start-end (s) | Type | Recipe |
|---|---|---|---|
| s1 hook | 0.00-6.35 | hook | Generated die image full frame (low-angle chip, green traces). Headline "Google ra mắt / 2 chip AI mới". On "gấp đôi" (4.8 s): 240 px "2×" slams in the black space above the die with a 36 px label "sức tính toán của TPU 8i Max, so với TPU 8i"; die shakes 6 frames |
| s2 names | 6.35-15.02 | spec | Date tile "9.11" (200 px) present from 0.12 s so the first 3 s are not a bare headline; card 1 "TPU 8i Max" (84 px) on its spoken word with two dies sliding together; card 2 "TPU 8tx" on its word |
| s3 chart | 15.02-25.21 | chart | Merge row (two 96 px dies slide together, "2 chip → 1 gói TPU 8i Max"), three groups (compute, on-chip memory, memory bandwidth) each with a 1x baseline bar (396 px) and a 2x green bar (792 px) that surges on each "gấp đôi"; note "Mốc: TPU 8i = 1×" |
| s4 density | 25.21-29.88 | diagram | Dashed footprint box with 20 cells; half lit at 0.3 s; the other half lights in seeded order on "gấp đôi" while the counter goes 1× -> 2× (0.7 s) |
| s5 8tx | 29.88-41.19 | diagram + chart | Part A: three stacked nodes (TPU 8t, TPU 8tx, host CPU in cyan) with edges drawn and packets travelling. Part B on "Độ trễ": big "2×", baseline bar 792 px, TPU 8tx bar 396 px, note "độ dài thanh minh hoạ tỷ lệ 2×" |
| s6 generation | 41.19-50.74 | chart | Two groups: training 2,7× (baseline 293 px, ours 792 px) and inference price-performance +80% (baseline 293 px, ours 528 px = 1.8x); note "1,8× = 1 + 80%" |
| s7 close | 50.74-55.81 | outro | Three recap tiles "2×", panel "CHƯA CÔNG BỐ: Giá bán / Ngày ra thị trường"; soft ending, full composition for the last 5 s |

## 8. Captions (Vietnamese karaoke)

Pill `#caps`: x 96, y 1366, width 888, `rgba(5,5,5,.94)` fill (profile says .78; the "nothing below 90% opacity" acceptance rule wins), 1 px `--acc` border, radius 30, 44 px Segoe 600, white, current word `#a4e22b`. One chunk per phrase, 3 to 9 words, at most 2 lines. Each chunk carries two strings: the DISPLAY text (digits, "TPU 8i Max") and the SPOKEN text (words); timing of a chunk = scene start + speech x cumulative characters of the spoken text. Word highlight inside a chunk is proportional to display characters. Word times are ESTIMATED (the voice step gives no alignment); measured against silence detection the error was 0.1-0.3 s.

## 9. Sound

No music or SFX in this build (the helper tools do not include them). Profile wants driving electronic 125-130 BPM, electric-surge SFX on bar surges, a sub hit on the slam. Voice: VieNeu "Hải Đăng"; final loudness measured -15.4 LUFS integrated, -4.2 dBFS peak after the helper's `loudnorm`.

## 10. Images (agy)

Two generated stills, no text, no logos: `die.jpg` ("macro close-up of an abstract AI accelerator die, low angle, black stage, acid-green emissive traces, centre composition with empty dark space top and bottom") used full frame in scene 1 and cropped in sample t032; `traces.jpg` ("top-down black circuit board, fine acid-green traces, mostly black") used at 10% (gradient `rgba(5,5,5,.9)` over it) as every scene's background. Generation took about 1 minute each. Both images came out at 768 x 1376 and fill 1080 x 1920 with `object-fit: cover` (aspect error 0.8%). Ask for empty dark space above the die: the 240 px number needs it.

## 11. Must not

Pastel or warm colours; a second energy colour; `filter` bloom on elements; width-animated bars; any benchmark without a unit and a baseline; a number on screen that is not in the voice (or not derived on screen); the company logo, product photo or brand colour of the real maker; a fade-out ending; text under 30 px except the one footer line; captions below y 1496 or other content between y 1296 and 1366 except the footer.

## 12. Traps seen in real builds (this build, 2026-11-12; measured)

1. **A child with `visibility: visible` outlives its hidden parent.** Scene 5's internal swap set `#s5b` to `visible`; when `#s5` was hidden at 41.19 s the child stayed visible on top of scene 6 and `inspect` listed 11 `text_occluded` errors at 46.5 s and 52.7 s. Fix: use `visibility: "inherit"` for the visible state of children of a scene (`hidden` / `inherit` pair).
2. **Bars animated by `width` fail `inspect`.** At 15.5 s the 2× value label (40 px) sat inside a bar 18 px wide: 4 `text_box_overflow` errors. Fix: bars have their final fixed width and are revealed with `clip-path: inset(0 100% 0 0)` -> `inset(0)` (0 errors afterwards, labels appear as the clip passes).
3. **Kicker and badge collide.** A 30 px mono kicker costs about 20 px per character with 0.1em spacing: "BỘ TĂNG TỐC MỚI · THÔNG SỐ + GIÁ" (31 characters, 620 px) ran under the badge at x 760 (visible in the sheet at 0-8 s; one `text_occluded` error in sample t027). Fix: kickers of 22 characters or fewer when a badge or pill sits at the right.
4. **Script length.** The first draft (215 spoken words) rendered to 60.6 s; the target was <= 58 s. Cutting 12 words (the date clause "vốn ra mắt từ tháng tư", "so với TPU tám i" tail, two adjectives) gave 55.81 s. Measured rate: 203 spoken words in 55.5 s = 3.66 words/s including 0.35 s gaps.
5. **A scene that opens on its bare headline.** Scene 2's first named product comes about 3.4 s into the sentence ("Ngày chín tháng mười một, Google giới thiệu ..."), so cards could not appear at the scene start. Fix: a date tile ("9.11", 200 px) present at +0.12 s carries the first 3 s; likewise scene 6 shows the two 1x baseline bars and both big numbers at +0.2-0.8 s before the surge words (about 4.7 s in).
6. **Caption fill 0.78 fails the opacity rule.** Raised to 0.94 (visually unchanged on the dark scenes).
7. **Transparent scene backgrounds ghost.** During the 0.15 s wipe the outgoing scene's text showed through the incoming one; each `section` now has its own opaque gradient background.
8. **Voice start offset.** Silence detection on `voice.wav` put real speech 0.08-0.11 s after each estimated scene start (6.456 vs 6.35, 15.103 vs 15.02, 25.309 vs 25.21, 29.947 vs 29.88, 41.280 vs 41.19, 50.841 vs 50.74). Visuals led the words by about 0.1 s: harmless, but do not tighten anchors below 0.1 s.
9. **Lint noise.** `composition_file_too_large` (334 lines) and three `overlapping_gsap_tweens` warnings on the shared `#flash` layer are expected: each flash tween is `fromTo` with `immediateRender: false`; nothing was changed for them.
10. **Python helpers.** A scratch `fontTools` script and a timeline printer could not be run in this session (permission); timings were read from `voice/timeline.json` with grep and the glyph test was replaced by rendered-pixel inspection (section 2).

Final acceptance numbers (frame check on `final.mp4`, 112 frames at 2 fps): 0 BLANK frames, 0 TOPHEAVY frames, no long blank run; inspect: 0 errors, 0 warnings after fixes; file 13.8 MB.
