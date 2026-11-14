# Style: editorial-intelligence (9:16 Vietnamese essay edition, demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** Nuanced "what the evidence actually says" explainers with 2 to 4 plain claims and no hero number: research summaries, health and habits, AI research and safety, policy and thought-leadership, correlation-versus-cause stories. Topic shape t079 (sleep and screens, Jev 0.76) fits. Not for breaking one-number stories, dense dashboards (4+ numbers), hype or loud news. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE 12 s silent demo build (`samples/sample-t079.mp4`). Voice-over, karaoke captions, music and SFX were NOT exercised: the voice and caption rules below come only from the profile and are marked **PROFILE**. Everything measured is marked with its number; **ASSUMED** = the profile gives no value and this document invented one. Profile: `styles/profiles/editorial-intelligence.yaml` (energy 2, light mode, family brand-inspired). No brand logo, name or mark of any AI lab is ever used.

Character: a well-edited essay on warm paper. A hand-drawn illustration draws itself, the serif headline arrives after it, claims sit on quiet cards, one clay highlighter sweep marks the single idea that matters, a hairline rule separates sections. Nothing bounces, flashes or glows.

## 1. Tokens

```css
--bg:#f5f0e8;      /* paper (profile)                                  */
--ink:#191919;     /* text, strokes             15.5:1 on bg           */
--slate:#5f5c55;   /* kicker, footer line        5.88:1 on bg, 6.5 on card */
--clay:#d0804e;    /* MARKS ONLY: ring dots, rays, arrow, highlighter (3.2:1: never text) */
--clayink:#8f4a22; /* ASSUMED text-safe clay     5.84:1 on bg, 6.49 on card */
--oat:#e8dfd0;     /* card border */
--card:#fffdf8;    /* card fill (profile) */
/* highlighter = clay at 25% over card = #f3ddce; ink on it 13.5:1 */
```
Contrast was computed with the WCAG formula by hand arithmetic (no interpreter was available to run it); the `hyperframes validate` WCAG check passed on all 5 text elements it sampled. Profile `clay #b8683c` is 3.64:1 on bg, so it fails as small text: use `--clayink` for clay-coloured text (the "?" mark, 110 px, is large). Profile `mute #8a8680` was not used (about 3.2:1). Dark variant (bg #23221e) not built.

## 2. Fonts (profile fonts Fraunces, Manrope, JetBrains Mono, Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, pull line, numbers in circles, the "?" | Fraunces 500 | `cambriai.ttf` (Cambria Italic, 400 only) | glyph coverage of the 36 tone-mark letters + đ was taken from the owner docs (fontTools test, 0 missing); this build's own check could not run an interpreter. Confirmed visually: "Ngủ và màn hình", "nghiên cứu thực sự", "nguyên nhân", "chưa chắc" rendered with every mark intact in the snapshots |
| Body, kicker, card text, node labels, footer | Manrope 400 | `SegUIVar.ttf`, weight axis 300-700 (600 body, 700 labels) | same |
| Code / model output | JetBrains Mono | `CascadiaMono.ttf` declared, not used (no code in this topic) | same |
| Never | | `segoepr.ttf` | 35 of 36 test letters missing (owner docs). Never use |

DEVIATION: the profile headline is an upright soft serif; the only local serif is italic, so the headline is italic. It reads as essay-like and is kept. Declare faces with `font-display: block`; the italic face has no bold: never put `font-weight:700` on it.

## 3. Type scale, safe areas and grid (1080 x 1920, px)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| kicker | Seg 700 uppercase +0.12em | 30 / 1.2 | slate, 16 px clay dot, always the word "Minh hoạ" in this demo |
| h1 (hook) | Cambria italic | 92 / 1.12, -0.015em | 3 lines at 900 px width, longest line "nghiên cứu thực sự" |
| section title | Seg 700 | 58 / 1.15 | one line |
| card text | Seg 600 | 44 / 1.3 | 2 lines, 900 x 230 card |
| circle number | Cambria italic | 58 | in a 100 px hand-drawn ring |
| node label | Seg 700 | 46 | inside a 300 px wobbly circle |
| pull line | Cambria italic | 72 / 1.2 | 2 lines, highlighter behind line 2 |
| sub / footer | Seg 500 | 36 / 30 | footer is the one 30 px line; nothing under 30 |

```
y 0   -170  platform UI: empty
y 190       kicker          y 262  hairline rule (900 x 2)
y 300 -1000 illustration (540 x 700, centred) | section title y 320 | diagram y 300-940
y 1040-1330 h1 (3 lines)    | cards y 520 / 790 / 1060, 230 tall, 40 gap | pull line y 1010, sub y 1290
y 1396      footer line (30 px)
y 1480-1920 platform UI: empty
x 90 - 990  essay column (900 px); illustration is centred, not right third (profile asks right third for 16:9)
```
Measured: lowest content edge 1426 px (footer), lowest body edge about 1330 px, so the body fills 69% of the frame height; the lower 25% is the platform zone by design.

## 4. Layers, back to front

`#root` paper PNG (baked noise, 540 x 960 tile scaled 2x, about 3% fibre; 777 KB) -> scene group (`#s1`, `#s2`, `#s3`, one visible at a time) -> `#kick`, `#rule`, `#foot` (persistent chrome, never fade). No flash, no shake, no fade-to-black, no end fade: the last 1.5 s hold the full composition.

## 5. Components

- **Hand-drawn drawing**: SVG paths with slightly wobbly coordinates, stroke 5 px ink (clay 6-7 px for rays and the arrow), round caps. Every path has `pathLength="1"` so a draw-on is one `strokeDashoffset` 1 -> 0 tween. A circle is generated by JS: 64 points, radius wobble 2.2% + 1.2%, overshoot of the start by 4% so the ends cross like a pen stroke (seeded, deterministic).
- **Card**: `#fffdf8`, radius 12, 1 px oat border, no shadow.
- **Number ring**: a 100 px hand-drawn circle around a Cambria italic digit.
- **Highlighter**: an absolutely positioned `u` behind the key phrase, clay at 25% opacity, `scaleX` 0 -> 1 from the left, 0.4-0.45 s `power2.out`. One per scene, only on the key phrase of that scene (two in the whole sample: scene 2 and scene 3, one each).
- **Hairline rule**: persistent 900 x 2 ink line under the kicker; it is also the section transition.
- **Illustration**: moon over a phone, built as SVG (not an image): 7 strokes plus one clay dot.
- **Label**: "Minh hoạ" kicker on the whole sample and a footer line "Minh hoạ: nội dung chung, không nêu nguồn hay số liệu". Content here is generic, so no source line exists.

## 6. Motion language

Energy 2. Eases used: `power1.inOut` (draw-on), `power2.out` (rise, highlighter), `power2.in` (rule out), `sine.inOut` (micro drift), `none` (fades). No `back`, `elastic`, `slam`, shake or flash.

| Verb | Recipe (measured values) |
|---|---|
| Draw-on | strokes drawn 0.3-0.9 s each, overlapping by 40-60%; the illustration takes 1.4 s in total (moon 0-0.7, phone 0.15-1.05, screen 0.7-1.2, rays 1.5-2.0) |
| Text after drawing | headline rises 20 px with fade, 0.6 s, starting 0.6 s: the drawing is still finishing, text lands about 0.6 s after the first stroke |
| Card rise | y 24 -> 0 + fade, 0.5 s, stagger 0.3 s; the number ring draws 0.5 s starting 0.15 s later |
| Highlighter | scaleX 0.4-0.45 s, lands about 1.5 s after the cards, so the eye reads the card first |
| Section rule | out: scaleX 1 -> 0 to the right, 0.2 s `power2.in`; in: 0 -> 1 from the left, 0.4 s `power2.out`, starting 0.05 s before the next scene fades in |
| Scene hand-off | outgoing scene fades 0.15 s ending exactly when the next one is visible: ghost <= 0.15 s |
| Micro-motion | illustration drifts y -6 px (1.4 s yoyo), one card drifts -4 px, diagram -5 px; nothing is fully still while held |
| Camera | locked off. The profile's slow vertical essay scroll was not used (12 s is too short) |

## 7. Scene recipes (as built, 12.0 s, 30 fps)

1. **Hook, 0-4.2 s (line draw-on + headline).** Kicker, rule, footer; moon and phone draw themselves; clay dot pops 1.9 s; headline in 3 lines at 0.6 s. Hold with illustration drift. Exit: rule retracts 3.75-3.95, scene fades 4.05-4.2.
2. **Claims, 4.1-8.4 s (essay cards).** Rule redraws, section title "Các nghiên cứu thường ghi nhận" at 4.15, three cards at 4.4 / 4.7 / 5.0, number rings drawn, highlighter on "dễ làm khó ngủ hơn" at 6.0. Hold 2.4 s. Exit as above.
3. **Diagram + pull line, 8.45-12.0 s.** Two hand-drawn circles "Màn hình" and "Giấc ngủ" draw 8.35-9.5; labels 9.2 / 9.45; clay arrow 9.6-10.25; "?" at 10.0; pull line "Tương quan / chưa chắc là nguyên nhân" at 10.0, highlighter 10.25-10.65, sub line 10.2. Everything is on screen by 10.7, so the last 1.3 s are a full composition (acceptance asks 1.5 s; the 10.5 mark is full except the final 0.15 s of highlighter growth).

Pacing: something changes every 1-3 s; calm holds of about 1.5 s. Real videos at 75-95 BPM-equivalent reading pace will need holds sized to the words (PROFILE).

## 8. Captions and voice (NOT EXERCISED)

Demo build: silent, no captions, no word timing. **PROFILE only**, untested: no pill; 42 px Be Vietnam Pro 500 ink in a bottom band on paper; current word clay, unread mute. Both clay and mute fail 4.5:1 on paper (3.2 to 3.6), so a real build must use `--clayink` for the current word and `--slate` for unread. Safe band y 1370-1480 should stay empty in the body.

## 9. Sound

Not exercised. Profile: warm acoustic or chamber strings, soft piano; SFX nearly none, a faint pencil scratch on draw-ons.

## 10. Images (agy)

One test image was made ("hand-drawn dark ink line illustration on ivory paper, crescent moon above a phone outline, one clay dot", 768 x 1376 JPG, 77 s). It looked right (loose strokes, ivory ground, one orange dot) but a raster cannot "draw itself", which is this style's signature, so it was NOT used. Rule: draw illustrations as SVG paths with `pathLength=1`; use agy only for a static picture that is placed, not drawn. Never ask agy for text, robots or brains.

## 11. Must not

- No emoji, glow, neon, shake, flash, fast cutting, dark cyber look; no robots or brains; no logo or product name of any AI lab.
- One clay highlight per scene; clay is marks only, clay text uses `--clayink`.
- No generic stock claims presented as findings: the demo's three claims are labelled "Minh hoạ" and say nothing numeric. A real build states only sourced claims.
- No hero number, no 4+ number dashboards (the profile avoids `stats` and `montage`).
- No `segoepr.ttf`; no bold on the Cambria italic.
- No text under 30 px (one footer line only).

## 12. Traps seen in real builds (THIS build, 2026-11-14)

First snapshots (9 times) and the first render showed:
1. **Frame 0 was empty.** Kicker and rule only: at 0.1 s nothing else, because the first stroke started at 0.05 s and the headline waited until 1.5 s. Fix: strokes start at 0 and the headline rises at 0.6 s. Remaining: at t=0.0 and t=8.5 s the 0.5 s-step sheet still shows kicker + rule + footer only (both under 0.2 s, below the 0.5 s limit).
2. **Late text showed before its cue.** At 8.6 s "Đây là nội dung minh hoạ..." was already visible: `fromTo(..., {opacity:0})` with `immediateRender:false` leaves the element visible until the tween starts. Fix: also set `opacity:0` in CSS for every late element (h1, t2, cards, note, sub) and set `#sub` to one short line. The `immediateRender:false` stays only on the shared `#rule`.
3. **Polygon circles.** 26 points with high frequency wobble drew visible straight facets and a jagged edge (seen at 9.8 s). Fix: 64 points and low wobble frequency (0.35 and 0.8 rad per point); circles now read as pen loops.
4. **Sub line wrapped to 2 lines and crowded the footer** (y 1290 text ended at 1352, footer 1396). Shortened to "Nội dung minh hoạ, không phải số liệu." (one line, 36 px).
5. **"?" collided with the arrow** at y 520 over the 7 px arrow; moved up to y 440 (about 70 px clear).
6. **Frame check tool.** `frame_check.py` needs numpy and PIL, which the system `python3` lacked; python could not be run for the contrast check either. Fix in this build: a 2 fps, 8 x 3 ffmpeg tile sheet read by eye (see `selfcheck.md`) and hand-computed contrast. Next build should install numpy and Pillow first.
7. **Body fills 69%.** The 900 px column leaves the lower quarter empty by safe-area design. A taller illustration or a 4th card would use it; not needed for a 12 s demo.

Tool facts (hyperframes 0.7.26): lint 0 errors / 0 warnings; validate no console errors, 5 text elements pass WCAG AA; inspect 0 layout issues on 9 samples; snapshot works at `--at t1,t2,...` (describe skipped, no GEMINI_API_KEY). Render 14.1 s for 12 s, `-q standard --crf 20`, 1.3 MB silent (flat paper compresses very well). Shell notes: `sed -i`, `cp -R` and inline `python3 -c` were refused for approval in this sandbox; the Edit tool and plain `cp` worked.
