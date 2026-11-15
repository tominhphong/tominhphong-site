# Style: minimal-future-product (9:16 demo edition, written from the t124 sample build, 2026-11-14)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Hardware and vehicle reveals with 2 to 3 spec numbers (range, charge time, power, battery, weight); future-product concepts; one object floating in a void with a silent spec read. Works because the frame holds one object, one title and a 3-column row. Not for: stories with many equal numbers (use saas-bento), people stories, enforcement, warm local stories, anything needing a quote or a long explanation, dense charts.
- Tier 2 never widens tier 1.

**Reading order.** One document, written from one 12 s demo (topic shape t124: an electric car maker unveils a futurist concept with range and charge specs). Every number in sections 1 to 12 was measured or computed in that build; "ASSUMED" marks a value the build did not test.

**Status: demo build.** Voice-over, captions, word timing and music were NOT exercised (silent demo, no VieNeu, no mux). Sections 8 (captions) and 9 (sound) are carried from the profile and are untested. A full 45-60 s video, with scene lengths, transitions between more than three beats and voice sync, is untested.

Profile: `skill/references/styles/profiles/minimal-future-product.yaml` (energy 2, mixed palette). Format 1080 x 1920, 30 fps, silent, 12.0 s, 3 beats, 2.1 MB. All content is generic and labelled "Minh hoạ" on screen.

DEVIATION 1: the profile names Outfit and Be Vietnam Pro; neither is installed. SegUIVar replaces both (SUBST).
DEVIATION 2: the profile says "soft horizon glow baked to PNG". No image tool could run in this build, so the glow is one CSS radial-gradient div (a single element, inside the renderer limit). Bake it when a PNG tool is available.
DEVIATION 3: no 36-frame orbit. The orbit is a flat SVG outline with a slow lateral track.
DEVIATION 4: no agy image. The car is an inline SVG outline (a drawn product is allowed: "single-weight 1 px outlines of the product").

## 1. Tokens (contrast computed with the WCAG formula, by hand, no script available in this build)

Two voids, switched by one inversion.

| Token | Graphite act | Paper act | Measured |
|---|---|---|---|
| `--bg` | `#1b1d24` | `#f4f4f4` | L 0.0124 / 0.905 |
| `--ink` | `#ffffff` | `#14161b` | 16.8:1 / 16.5:1 on bg |
| `--mute` (SOLID colour, never alpha) | `#a9adb8` | `#5b5f6a` | 7.5:1 / 5.8:1 on bg |
| `--line` hairlines | `#3a3d45` | `#c9cbd1` | decorative, 1 px, not text |
| `--fill` car body | `#23262e` | `#e6e7ea` | decorative |
| accent | `#e5502e` | same | 4.4:1 on graphite, 3.5:1 on paper: NEVER text, only 2 px marks |

Rules: red is a 2 px line or tick only (car lamp, charge line, two end ticks); never a fill, never text. The profile's `mute: rgba(255,255,255,0.5)` was replaced by a solid `#a9adb8` so no text sits below 90% opacity and the paper act stays above 4.5:1 (the alpha version computes to about 4.0 on paper, fails). Text colours come only from `--ink` and `--mute`.
The inversion tweens the CSS variables on `#root` (`--bg --ink --mute --line --fill`, 0.7 s `power2.inOut`) plus `backgroundColor`; custom-property tweens rendered correctly in `hyperframes render` 0.7.26.

## 2. Fonts (checked on the real render; Vietnamese capitals Ạ Ệ Ặ Ố Ạ Ư Ơ Ê Đ Ả Ậ rendered with every diacritic)

| File | Role |
|---|---|
| `SegUIVar.ttf` (wght 200-700, variable) | everything: titles 500, spec values 300, labels and units 500 |
| `CascadiaMono.ttf` | not used |
| `cambriai.ttf` | not used (a serif italic does not fit; "no decorative type") |
| `segoepr.ttf` | NOT copied into the project; it lacks Vietnamese letters |

Weight 300 works on SegUIVar and gives the thin numerals the style needs. The `@font-face` must declare `font-weight:200 700` or Chrome snaps to 400. Uppercase is done with `text-transform:uppercase` on the Vietnamese lower-case source, so diacritics stay correct.

### Type scale (1080 x 1920 px, as built)
- Title: 56 px / line 84, weight 500, tracking 0.25em, uppercase, centred, two lines. `padding-left:.25em` cancels the trailing tracking so it centres optically.
- Spec value: 120 px / 120, weight 300, no tracking. "640" is about 190 px wide, so three values fit a 312 px column.
- Unit and label: 30 px, weight 500, tracking 0.14em, uppercase, `--mute`.
- Footer "Minh hoạ" line: 30 px (nothing in the film is below 30 px).

## 3. Safe areas and grid (1080 x 1920)

- Margin 72, content 936, three columns of 312 separated by 1 px hairlines (x 384 and 696).
- Title block y 290-458, the only element in the top 30% (y < 576).
- Void y 458-1046 stays empty on purpose.
- Car: SVG viewBox 900 x 250 shown at 1000 x 278, left 40, top 1046; wheel bottoms touch the horizon at y 1306 (68% of the height). Car centre sits at about 60% height.
- Reflection y 1288-1403 (mirrored copy, 12% opacity, mask fading to transparent at 35% of its height).
- Spec row: top hairline y 1430, labels y 1448-1484, values y 1498-1618, vertical hairlines 196 px tall.
- Energy line (beat 3): track y 1672, ticks 24 px tall, tick labels y 1696.
- Footer y 1754-1790. This is inside the bottom 15% that a phone UI can cover (ASSUMED risk, not tested on a device).

## 4. Layers, back to front
1. `#root` `--bg` (graphite to paper).
2. `#glow` radial-gradient ellipse at the horizon, white at 10% alpha, fades out during the inversion.
3. `#horizon` 1 px line, full bleed.
4. Titles `.t` (one visible at a time).
5. `#cg` group: reflection SVG + car SVG, both inside one wrapper that carries the lateral track.
6. Spec row, energy line, footer.
Three depth layers (glow, car, text) with only the car group moving during holds.

## 5. Components
- **Horizon line:** 1 px, `scaleX` 0 to 1 from centre, 1.1 s `power3.inOut`.
- **Car outline:** four paths (body, window, two wheels plus two hubs) drawn with `pathLength="1"` and `strokeDashoffset` 1 to 0; body fill fades 0 to 1 AFTER the outline closes (the light-up). One 2 px red lamp line.
- **Reflection:** the same outline mirrored with `scaleY(-1)`, `opacity .12`, gradient mask.
- **Spec column:** label (30 px caps, mute), value (120 px, weight 300), unit inline 10 px right of the digits.
- **Hairlines:** drawn before any value appears (profile rule).
- **Energy line:** 1 px track, a 2 px red segment from 10% to 80% of the track, two 2 px end ticks, labels "10%", "80%", centre label.
- **Footer:** one 30 px caps line: "Minh hoạ · số liệu giả định".

## 6. Motion language
- Everything decelerates or is inOut; no `back`, `elastic`, bounce; no flash, shake, whip.
- Title lines rise 26 px out of opacity 0 with `power3.out` 0.6-0.7 s, stagger 0.1 s. Outgoing title fades 0.15 s `power2.in`, y -12.
- Lateral track: `#cg` x +22 to -22 over the whole 12 s, `ease:"none"` (profile: ease none on held shots). It is the only micro-motion in the holds; it was enough to avoid a dead frame.
- Counters: `power2.out` 1.2 s, staggered 0.15 s, final text forced by a `tl.call` at the end. All three finish by 6.6 s and hold for 1.4 s before the inversion; a value is never held mid-count.
- Invert: 0.7 s, starts the same instant the old title leaves; the new title enters 0.45 s later.

## 7. Scene recipes (3 beats, 12.0 s)

**Beat 1, light-up (0-4.0 s). Graphite void, title "Khái niệm / xe điện".**
0.0 horizon draws; 0.1 title lines rise; 0.4 footer fades in; 0.5-2.3 body outline draws; 1.0-2.4 window; 1.4-2.4 wheels, 1.9-2.6 hubs; 2.0-2.9 body fill lights; 2.7 red lamp draws; 2.4-3.2 reflection fades to 12%. 3.2-4.0 pure hold with the lateral track.

**Beat 2, silent spec read (4.0-8.0 s). Title "Phạm vi / và sạc".**
4.0 old title out; 4.15 new title in; 4.3-5.0 top hairline draws left to right; 4.6-5.2 vertical hairlines draw down; 4.8-5.3 labels fade 0.12 s apart; 5.1 / 5.25 / 5.4 values count to 640 km, 18 min, 250 kW (illustrative numbers, labelled). Hold 6.6-8.0.

**Beat 3, inversion (8.0-12.0 s). Title "Tương lai / yên lặng".**
8.0 graphite to paper over 0.7 s, glow off; 8.45 title in; 8.8 track draws; 9.1 left tick and "10%"; 9.3-10.3 red line draws from 10% to 80%; 10.15 right tick, "80%"; 10.3 centre label "Sạc nhanh". From 10.6 s the frame is complete and holds to 12.0 s.

## 8. Captions
NOT exercised (demo, silent). Profile says: no pill, 40 px sentence case, bottom band. This build's footer line occupies y 1754-1790, so a caption band would need its own space; untested.

## 9. Sound
NOT exercised. Profile: ambient pads, rising whine on reveals, soft clicks on counts. Counter finish times (6.5, 6.65, 6.8 s) are the natural click points.

## 10. Images
No agy image was made. Advice from the profile and this build: if one is used, ask for a flat product render on an empty void, no text, no logo, no person; do not put it near numbers. A drawn SVG outline reads more "engineered" than a render here and cannot invent a real model.

## 11. Must not
- No emoji, no gradient text, no glow on text, no decorative or handwritten font.
- Red never as a fill or as text; no second accent.
- No alpha-based text colour (use solid `--mute`).
- No spec number without "Minh hoạ" on screen when the content is generic; no real brand, model, price or spec.
- No bounce, back, elastic; no shake or flash.
- Nothing in the top 30% but one title; at most 3 spec columns.
- A counter is never on screen mid-count for a held frame.

## 12. Known risks (not tested)
- Full-length film: very long holds (profile: 8-16 beats) will need a second moving element; one lateral track alone may read static after 6 s.
- Voice, caption and music timing.
- The footer inside the phone UI zone.

## 13. Traps seen in real builds (this build, 2026-11-14)

1. **CSS transform plus GSAP.** `lint` raised 3 errors (`gsap_css_transform_conflict`) for hairlines that had `transform:scaleX(0)` in CSS and a `tl.to` scale. Rule: draw hairlines with `tl.fromTo` (scale 0 to 1); the CSS start state is then only a fallback. After the fix: 0 errors, 0 warnings.
2. **Counter overlap warning.** Three counters tweened a property named `v` on three objects; lint raised 3 `overlapping_gsap_tweens` warnings. Rule: give each counter its own property name (`v640`, `v18`, `v250`). After: 0 warnings.
3. **Reflection tail hits the spec row.** The 12% mirror, masked to fade at 35% of 278 px, still ends at y 1403, and in the paper act its faint arc was visible between the label and the value of column 2 (seen in the 11.2 s frame, crop y 1220-1920). Rule: end the reflection at least 30 px above the first hairline, or fade it out when the specs arrive.
4. **Mute at 50% alpha fails on paper.** The profile token `rgba(255,255,255,.5)` is for graphite only. On paper a solid `#5b5f6a` is 5.8:1; use solid colours per act.
5. **Mid-inversion frame.** At 8.0-8.7 s both void colours cross; the frame at 8.0 s is a mid-grey (`#3a3d45`-like) with ink at about 5:1. It lasts 0.7 s and is by design; do not put a counter or a new element inside it.
6. **The first frame is nearly empty.** At 0.0-0.1 s only the graphite void and glow exist; the title is at 0.1 s opacity 0.2. It is under the 0.5 s limit. Start the title at t = 0.1 so frame 0 is not a final poster that is cut by a mask.
7. **Void is large.** The 590 px between title and car (y 458-1046) is deliberate (style). It read as intended in the contact sheet (frames at 0.5-3.5 s) because the glow and a 1 px horizon anchor it; without both it looked broken.
8. **Tool limits seen.** `frame_check.py` could not run (no numpy in the shell); the check was done with an ffmpeg contact sheet at 2 fps, a 10 fps crop around the 4.1 s title swap and a full-size crop of the last frame. `hyperframes snapshot` gave 9 frames in about 15 s. Render 9.8 s, 2.1 MB.
