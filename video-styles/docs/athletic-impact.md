# Style: athletic-impact (9:16 Vietnamese hype edition) - DEMO build

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** loud, physical, high-momentum story shapes: sports and festival promos, event announcements ("comes to <city>"), launches, motivational finales. Not for explainers, numbers-heavy stories, sad or enforcement stories, or dense UI. Tier 2 never widens tier 1.

**Status.** Written 2026-11-15 from ONE silent 12.0 s demo sample (topic shape t153, Jev fit 0.6: extreme sports festival in Austin). **Voice-over, captions, word timing, sound and music rules were NOT exercised**; sections 8 and 9 are the profile's values, unverified. Everything marked MEASURED comes from this build; ASSUMED = invented here; SUBST = a named font is not installed.
Profile: `skill/references/styles/profiles/athletic-impact.yaml` (energy 5, dark, brand-inspired). Format 1080 x 1920, 30 fps. Content is generic and labelled "MINH HOẠ" in every beat.

## 1. Tokens

```css
:root{ --bg:#000; --ink:#fff; --accent:#d4ff00; --red:#ff3b1f; --mute:rgba(255,255,255,.4); }
```
MEASURED contrast (WCAG formula): white on black 21.0; lime #d4ff00 on black 18.1; black on lime 18.1; black on white 21.0; red on black 5.9; red on white 3.4 (fill only); `--mute` on black 3.7 (FAILS for text: use only for decoration). `hyperframes validate` reported 15 text elements pass WCAG AA.
Rules as built: one accent per beat (lime on one word, one bar, or the whole finale background); red appears once, as a 0.12 s flash at the finale (opacity 0.85 to 0). One inverse white beat (BMX) used as a punch. Never put lime text on white (1.2:1).

## 2. Fonts (glyph test with fontTools, all Vietnamese capitals and lower case incl. Ơ Ư and dotted/hooked vowels)

| File | Missing glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 | EVERYTHING: giant words (weight 800 requested), sub-lines (700). SUBST for Anton and Archivo Black (not installed) |
| `CascadiaMono.ttf` | 0 | the "MINH HOẠ" tag, 34 px, +0.06em |
| `segoepr.ttf` | many | not used |

SUBST consequence: Segoe is wide, not condensed. Condense by `transform:scaleX(.78)` on the word (width ratio about 0.78 keeps strokes heavy and reads as condensed). The profile's 220-420 px range does not apply; sizes below were fitted.

### Type scale (1080 x 1920, MEASURED from the build)
| Use | px | Notes |
|---|---|---|
| Two-line slam word (TRƯỢT, LƯỚT, VÁN) | 370 | scaleX .78; visual width about 1000 for TRƯỢT |
| Single hero word (BMX) | 560 | visual width about 1010 |
| Place word (AUSTIN) on photo beat | 300 | |
| Finale stack (RA / SÂN / AUSTIN) | 340 / 340 / 315 | AUSTIN at 340 touched the edges, 315 clears by 36 px |
| Giant number "3" | 980 | left 10, lime |
| Discipline list | 104 | scaleX .8, left aligned at x 640 |
| Sub-line / footer | 46-52 | weight 700, no scale |
| Tag "MINH HOẠ" | 34 mono | only text near 30 px; nothing below 30 |

## 3. Safe areas and grid
Side margin 36-48 (type may reach 36 px from the edge; bleeding off-frame was NOT used). Status zone y 0-140 empty except the tag at y 150. Slam stacks use 400 px steps (line top 560 and 960 for 370 px words; 380 / 790 / 1200 for the finale). Lowest content edge at hold: y 1750 (finale sub-line); title beat y 1470.

## 4. Layers, back to front
beat background (inset -60 px so shake never shows an edge) / photo or type / bars / grain PNG (opacity .18, overlay, 540x960 noise baked with ffmpeg `noise`) / white flash / red flash. Stage shake moves `#stage` only.

## 5. Components
Slam word (wrapper scales, inner span carries the static scaleX), accent bar (18-20 px, scaleX from left), mono tag, photo block (1080 x 1180, grayscale + contrast 1.25 in CSS), giant number, list row. No cards, no chrome.

## 6. Motion language (MEASURED values)
- Slam: scale 1.6 (1.5 on single words, 1.7 on finale) to 1 over 0.18 s `power4.in`, autoAlpha 0 to 1 in the same tween, plus stage shake 6 frames decaying (amplitude 10-18 px, set per frame with `tl.set`).
- Invert flash: white layer 0.9 to 0 over 2 frames at the cut.
- Hard cuts by `tl.set autoAlpha` on the same frame: no ghost of the outgoing beat (0 ms).
- Speed ramp: photo scale 1.00 to 1.22 in 0.45 s `power4.in`, then 1.22 to 1.28 over 2.55 s `sine.out`.
- Stutter: "3" settles then 4 `tl.set` x offsets (-30, -10, -30, 0), one frame each.
- List rows enter x +260 to 0 in 0.2 s `expo.out` on half-beat steps (0.5 s).
- Micro-drift on every held word: scale 1 to 1.03 linear over the hold (no dead frame).
- BPM 120 assumed (beat 0.5 s): cuts at 0, 1, 2, 3, 6, 9 s.

## 7. Scene recipes (12.0 s, 4 beats; times absolute)
- **R1 Montage cut (0-3.0):** three one-second type cuts: TRƯỢT / VÁN (lime), BMX (white inverse), LƯỚT / VÁN (lime). Words slam on 0, 0.25 / 1.0 / 2.0, 2.25; each holds fully drawn 0.55 s or more.
- **R2 Place + photo (3.0-6.0):** photo block with speed ramp, lime bar 0.25 s, AUSTIN slam at 3.5, sub-line rises at 4.0 (held from about 4.3).
- **R3 One number (6.0-9.0):** "3" slams with stutter at 6.0, three disciplines at 6.5 / 7.0 / 7.5, bar 7.75, sub-line 7.85; complete frame from 8.05 and held to 9.0 as the "silence" before the finale.
- **R4 Finale (9.0-12.0):** hard cut to full lime, red flash 0.12 s, RA 9.0, SÂN 9.25, AUSTIN 9.5, bar 10.0, sub-line 10.2; full composition held 10.5 s to 12.0 s (1.5 s) with 2.5 percent drift; no fade out.

## 8. Captions
NOT EXERCISED (no voice). Profile value only: black block, 4 px accent bar, 44 px uppercase, current word accent. Check against section 2 before use: Be Vietnam Pro is not installed.

## 9. Sound
NOT EXERCISED. Profile: trap/drill/DnB 120-150 BPM, impacts on slams, a hard stop before the finale. The 6-frame shake and the 1.0 s freeze (8.05-9.0) are built to sit on those hits.

## 10. Images (agy)
One image, 71 s: "grainy black and white skateboarder silhouette mid-air above a concrete bowl at night, floodlights". The result looked like a real photograph (no text, face dark). Use only with the "MINH HOẠ" tag; do not present it as a real event. CSS grayscale and contrast make it match the black/white rule. One image carried the whole style: more is not needed.

## 11. Must not
Pastel or soft palettes; fades or cross-fades between beats; two accents in one beat; lime text on white; red more than once; flashes closer than 2 beats (here: flashes at 1.0, 2.0, 3.0, 6.0 are one beat apart in the montage: accepted for the build-up, but see trap 6); any text under 30 px; a real brand, real person or real price.

## 12. Traps seen in real builds (this build, 2026-11-15)
1. **Scaled text is not centred.** First render: `display:inline-block; transform:scaleX(.8)` inside a 1080 px block. The layout box stays unscaled (about 1250 px for TRƯỢT at 420 px), so it started at the left edge and overflowed right (TRƯỢT cut at x 1080, BMX cut). Fix: `.w{display:flex;justify-content:center;width:1080px}` so the box overflows equally on both sides, then `scaleX` about the centre.
2. **Size fits are by eye.** At 420 px TRƯỢT and 700 px BMX still touched both edges after centring; final 370 and 560. AUSTIN 340 touched at 11.0 s, final 315. Check every word on a snapshot at the widest letter.
3. **`inspect` is blind to scaleX.** It listed 11 warnings and 4 canvas_overflow notes (overflow right 178-270 px) from the unscaled boxes while the visual was fine, and overlap warnings between the "3" and the list because the 980 px number's box is wider than its glyph. Judge by snapshots, not by those numbers.
4. **Stacked uppercase Vietnamese needs line pitch 1.0 em or more.** The profile's 0.85 would put the hooks and dots (Ỡ, Ợ, Ớ, Ả) into the line above. Slam lines were set 400 px apart at 370 px (pitch 1.08).
5. **Fonts are not condensed.** Anton and Archivo Black are missing; scaleX .78 on SegUIVar 800 gave an acceptable stand-in, but the strokes are thinner than real Anton.
6. **Flash density.** The profile says max 1 flash per 2 beats; the montage cuts every 2 beats (1.0 s) with a 2-frame invert flash, within the rule, but the 3.0 s flash lands one beat after the 2.0 s one: avoid a new one there next time.
7. **Held "silence" must not be empty.** The profile's 4-beat silence would be a blank panel over 0.5 s; here the number list is fully drawn and drifting (8.05-9.0) and the drop is the cut itself.
8. **No numpy, no `frame_check.py`.** In this environment `python3` has no numpy, so the script could not run; the check was done with an ffmpeg 2 fps contact sheet (24 frames) read by eye. Install numpy for the real script.
9. **A "3" in a giant size leaves a hole** if the list is not placed to its right: first build put the list at x 560 and it overlapped the "3" (visual width 668 at 1180 px). Final: 980 px number, list at x 640.

## 13. Measured build facts
Render 11.4 s (hyperframes 0.7.26), 3.8 MB, 1080x1920, 12.0 s, h264. Lint 0 errors; validate 0 console errors; inspect 0 errors.
