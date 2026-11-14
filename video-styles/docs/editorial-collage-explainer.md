# Style: editorial-collage-explainer (detail, first draft from the demo build, 2026-11-14)

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build.** Plain-language explainers of "what are the rules, who is affected, what to do": tenant or consumer rights, how a process works, a new rule, a checklist of 3 things to ask. Works because content is short blocks of text on paper pieces, 3 beats, one colour each. Not for breaking one-number stories, dense data, or product news. Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: ONE silent 12.0 s sample (1080x1920, 30 fps), topic shape t175 (Jev fit 0.78). Voice-over, captions, word timing, music and SFX were NOT exercised; sections 7 and "Sound" are carried from the profile and untested. All content is generic and labelled "Minh hoạ". No generated images were used (all art is CSS/SVG), so the image section is guidance only.

Profile: `skill/references/styles/profiles/editorial-collage-explainer.yaml` (energy 3, light, one bold flat colour per scene, paper cut-outs, pieces assemble). Marks: **SUBST** = a named font is not installed and a local one replaces it. **ASSUMED** = the profile gives no value.

## 1. Tokens (contrast computed by hand with the WCAG formula; the validator uses its own sampling, see traps)

```css
--bg:#f1e7d3; --ink:#1d1a17; --paper:#fbf6ea;
--accent:#e2412b;     /* FILL, seal, large bold text only */
--accent-dk:#b3281a;  /* ASSUMED: accent for text */
--mustard:#f0b429; --teal:#1f7a7a; --cobalt:#2547a8; --clay:#c8875a;
--sh: drop-shadow(0 8px 14px rgba(29,26,23,.28));
```
| Pair | Ratio | Use |
|---|---|---|
| ink on paper | 16.1 | all body text |
| ink on bg | 14.1 | |
| ink on mustard | 9.3 | headline strips on mustard |
| ink on clay | 5.8 | |
| paper on ink | 16.1 | reversed strips |
| paper on cobalt | 7.7 | beat-2 headline |
| paper on teal | 4.7 | fills only here |
| accent-dk on paper | 6.0 | card numerals |
| accent on paper | 3.9 | NOT for text under 24 px bold |
| paper on accent | 3.9 | seal text: 44-58 px bold only |
| ink on accent | 4.1 | avoid |

One flat colour per beat: clay (hook), cobalt (3 questions), mustard (payoff). Red is the seal and key numerals only.

## 2. Fonts
| File | Role |
|---|---|
| `SegUIVar.ttf` | headlines 90-144 px weight 700, uppercase, `-webkit-text-stroke:2px currentColor` to fake "Archivo Black" weight (SUBST: Archivo Black, Libre Franklin not installed); card titles and body 600 |
| `CascadiaMono.ttf` | typewriter labels: masthead tag, document lines, footer tag (profile Special Elite SUBST) |
| `cambriai.ttf` | the one italic subhead (36 px+; here 54 px) |
| `segoepr.ttf` | never (lacks Vietnamese letters) |

Diacritics check: the glyph test with fontTools could NOT be run in this build (inline Python was blocked). Instead every Vietnamese string was rendered and inspected in snapshots and in the final video: Ề, Ờ, Ị, Ọ, Ữ, Ặ-class stacked marks (QUYỀN, NGƯỜI, THUÊ, HỎI TRƯỚC, GIẤY, MỌI THỨ, BẢN, SỬA CHỮA, CỌC, BÁO) all draw correctly in SegUIVar; Cascadia and Cambria italic drew "Hợp đồng", "Tiền cọc", "Sửa chữa", "Nói đơn giản" correctly. Not a substitute for the full-alphabet test: run it next time.

## 3. Type scale, safe areas, grid (1080 x 1920)
- Headline 144 px (beat 1, 3 lines), 112 px (beat 3), 90-100 px (beat 2, two strips). Card title 76, card numeral 170, card body 42, document lines 38, subhead 54, seal 44-58, closing strip 52, masthead and footer 32 (the only 32 px lines; nothing under 30).
- Content zone y 214-1560. Footer tag "Minh hoạ" at y 1650, left 72. Nothing important above y 200 or below y 1600 (platform UI).
- Side margin 70-80; headline strips are inline-block, auto width (widest: "CỦA NGƯỜI" at 144 px = about 930 px with padding, right margin about 80 px).
- Layout per beat: clear third for the headline strips (stacked, alternating rotation -2.5, +1.5, -1.2 degrees), hero piece off-centre in the lower two thirds, 2-3 scraps (tape, seal, italic tag).

## 4. Layers, back to front
1. `.bgc` flat colour, oversized (-60 px each side) so a camera drift never shows an edge.
2. confetti scraps (16 seeded paper scraps, 3 per beat distribution, drift 120-280 px over 12 s). They sit INSIDE each scene, under the pieces: a global scrap layer on top would cover text.
3. pieces (`.piece` = wrapper with drop-shadow, child `.face` = clip-path torn paper).
4. tape strips and seal (above their piece).
5. wipe sheet (torn leading edge, colour of the NEXT beat).
6. footer tag "Minh hoạ" (always on top, z 50).

## 5. Components
- **Torn piece.** Shadow belongs on a wrapper and the torn `clip-path: polygon(...)` on the child, otherwise the clip removes the shadow. Edge jitter is 0-7 px inward, step 26 px, seeded (`rng(100+i*7)`). Text padding is at least 16 px so jitter never touches glyphs.
- **Headline strip.** Paper, ink or mustard fill, 700 uppercase, padding 16/36/20.
- **Card** 920 x 290: numeral 170 px accent-dk, title 76 px, one 42 px line. One piece, one idea.
- **Document** 800 x 600 typewriter, 4 lines at 38 px, red header 34 px.
- **Seal** circle 230-280 px accent with paper ring and outer accent outline, bold uppercase 44-58 px.
- **Tape** 150 x 46 mustard strip at 92% opacity, rotated 28-40 degrees across a corner.
- **House cut-out** SVG: shapes with 22 px paper stroke (`paint-order: stroke`) for the white cut border, halftone dot pattern (4.2 px dots, 22 px pitch, 22% ink) only on the roof and wall, never on text.

## 6. Motion language (energy 3)
- Entrances: pop-settle for headline strips (scale 1.12 -> 1, rotation resolves, 0.5-0.55 s `expo.out`, stagger 0.1 s); fly-in for the subhead (x -500 -> 0, 0.7 s); slap for seal and cards (scale 1.35 -> 1, 0.17-0.2 s `power3.out`); tape scale 0.6 -> 1 in 0.3 s.
- Holds: slow sway (+-1 degree, `sine.inOut`, yoyo, finite), camera push 1.00 -> 1.03 on beat 1, drift y 0 -> -24 on beat 2, STATIC on beat 3 (payoff). Adjacent beats never share a camera.
- Transition: paper-wipe 0.7 s `power3.inOut`; a sheet 1240 px wide in the next beat's colour travels right to left; the scene swaps while it fully covers the frame (the sheet is the same colour, so the swap is invisible). Wipes start 0.35 s before each swap.
- Timings as built: beat 1 0-3.9 s, wipe 3.55-4.25, beat 2 3.9-7.9, wipe 7.55-8.25, beat 3 7.9-12.0; last piece (closing strip) lands at 10.1 and settles by 10.7, so the last 1.3 s are a full composition.
- Every piece that enters late is hidden (`autoAlpha:0`) until its own entrance frame; see trap 1.

## 7. Captions
Not exercised (demo, no voice). Profile: cream torn strip, 42 px, current word accent red, bottom band. If captions are added, the bottom 440 px of the 9:16 frame is theirs: this build keeps content above y 1600 except the footer tag, so the footer tag must move up or hide when captions appear.

## 8. Scene recipes (3 beats built)
1. **Hook (clay).** Masthead tag, three stacked strips (paper, ink, mustard) = the title, italic subhead strip lower left, house cut-out lower right with halftone, red seal "Quyền lợi" slapped on its corner at 1.35 s, two tape strips.
2. **Three questions (cobalt).** Two headline strips, three cards slapping in at 0.3 s steps, tape on first and last card. Chosen because "3 things to ask" fits the card component.
3. **Payoff (mustard, static).** Three ink/paper strips, typewriter document flies in at +0.5 s, seal stamped at +1.7 s, closing ink strip with the takeaway at +2.1 s.

## 9. Sound
Not exercised. Profile: light hip-hop or plucked strings 96-118 BPM; stamp thud on the seal slap (1.35 s, 9.7 s), paper slide on wipes.

## 10. Images
None used. The piece art was drawn as SVG so headlines and text stay live HTML. If agy images are used, follow `generated-art.md`: no text, no logos, torn white borders baked in, halftone only on non-face art.

## 11. Must not
- Smooth CGI, glow, neon, glass, 3D. Pieces are rigid flat cut-outs.
- Text inside a clip-path with jitter larger than its padding.
- A global confetti layer above text.
- A piece with an entrance tween but no hidden pre-state.
- `accent` red as small text on paper (3.9:1).
- `segoepr.ttf`.
- Real company, price, law or statute in a demo; the label "Minh hoạ" stays on screen for the whole sample.

## 12. Traps seen in real builds (this build, 12.0 s, measured)
1. **Pre-roll state visible.** With `fromTo` the "from" state (seal at scale 1.5, strip at x -500) is rendered from t=0 until the tween starts. First render: the seal at scale 1.5 covered the document text from 7.9 to 9.6 s, and the closing strip hung off the left edge for 2 s. `inspect` caught it as `text_occluded` on 4 samples. Fix: `tl.set(sel,{autoAlpha:0},0)` and `tl.set(sel,{autoAlpha:1},entranceTime)` for every late piece; `inspect` then reported 0 layout issues across 9 samples.
2. **Headline strip against the frame edge.** "HỎI TRƯỚC KHI KÝ" at 100 px with left 150 reached x 1080 and its last letter touched the edge. Fix: 90 px and left 90. Measure the strip's right edge, not the text.
3. **Card line wrapping.** "Đổi điều khoản phải báo trước bao lâu?" at 42 px wrapped to 2 lines and crowded the card; rewritten to "Đổi điều khoản: báo trước bao lâu?" (one line, 920 px card with 150 px numeral).
4. **Validator contrast false alarms.** `validate` printed 10 warnings: the ink strip "CỦA NGƯỜI" 2.84:1 and seal "Quyền lợi" 2.78:1, at every sample time including when the beat is hidden. By hand the strip is 16.1:1 and the seal text is 3.9:1 (large bold). The strip is read against the bgc behind the rotated, clipped element. Not fixed; judge by the hand numbers, and keep seal text 44 px bold or larger. The seal at 3.9:1 passes only as large text.
5. **Drop shadow clipped.** Clip-path on the same element as the filter removes the shadow; put `filter` on the wrapper (`.piece`) and `clip-path` on the child.
6. **Beat start looks empty.** After each swap the bg colour plus headline show alone for about 0.4 s before the first card or document lands (beat 2 cards at +0.45, beat 3 document at +0.5). Under the 0.5 s limit, but this is the maximum: do not push the hero piece later.
7. **Wipe sheet geometry.** Sheet 1240 px wide with a 160 px torn edge; it covers the frame only while its x is between -160 and 0, about 0.15 s at `power3.inOut`. Keep swap at the sheet's midpoint (start = swap - 0.35).
8. **Tool gaps in this environment.** `frame_check.py` could not run (numpy missing), so the frame check was a manual 3 fps contact sheet of the render (`samples/fc-sheet.jpg`); automated BLANK/ghost detection was not run. Run it where numpy exists before using this style in production.
9. **Tool facts (hyperframes 0.7.26).** lint 0 errors / 0 warnings; validate no console errors; inspect after fix 0 issues; render 12.0 s in 12.6 s, 5.7-6.0 MB silent. SegUIVar has weights to 700 only; the 2 px text-stroke gives the heavier look.
