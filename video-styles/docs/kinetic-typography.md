# Style: kinetic-typography (9:16 Vietnamese word-stack teaser edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in the one demo build (topic shape t109, Jev fit 0.64): announcements and teasers with a short hook, one title and one date: a new series, a launch date, a premiere, an event save-the-date, a manifesto line. Works on any story that can be said as 4-8 big words plus one number. Not for stories with several sourced numbers, tables, UI, or long explanations (profile `avoid`: ui-demo, diagram, terminal). Tier 2 never widens tier 1.

**Status.** Written 2026-11-15 from ONE real build: a 12.0 s silent 1080x1920 sample (`samples/sample-t109.mp4`, 4.5 MB). **Voice-over, word timing, captions and music were NOT exercised** (demo build): every rule below about timing to spoken words, caption bands, beat grid and sound comes from the profile and is untested. The build used a hand-set 0.6 s grid (100 BPM, the profile's low end) with no audio.

**Example videos show the visual recipe, not the niche.** The sample is about a made-up crime series; copy how it is built, not what it is about. All content is generic and labelled "Minh hoạ" on screen.

**Reading order.** Sections 1-11 are the design; section 12 is the traps found in this build (they override earlier sections where they disagree).

One-line identity: giant uppercase words stacked on a left axis, rising out of line masks; the stressed word is orange; beats change by a hard invert (dark <-> light) or by the orange word filling the frame. Energy 4 (profile) but in this build executed as controlled: no shake, no flash.

## 1. Tokens

```css
--bg:#0e0e0e; --ink:#f4f1ea;          /* dark beat: ink on bg 17.1:1 */
--alt:#f4f1ea; --altInk:#0e0e0e;      /* light beat: 17.1:1 (profile alt / altInk) */
--accent:#ff4d00;                      /* 5.8:1 on bg (any size); 2.95:1 on alt (LARGE text only, >= 300 px here) */
--muteD:#b3b0a8;  /* ASSUMED solid mute for small text on dark: 8.9:1 */
--muteL:#55524a;  /* ASSUMED solid mute for small text on light: 6.9:1 */
```
Ratios are hand-computed with the WCAG formula (+-0.1); `hyperframes validate` independently reported "25 text elements pass WCAG AA".
The profile's `mute: rgba(244,241,234,0.35)` is about 2.6:1 on bg: it fails for text. Use the solid `--muteD` / `--muteL` instead and never lower text opacity (rule: nothing under 90% opacity on a held frame).
Accent rules: one accent word per line, maximum one accent line per beat (LỜI GIẢI in beat 1, TÊN in beat 2, the date in beat 3). Accent on the light beat is allowed only at 300 px or larger (2.95:1 is under 3:1 for small text; the 44 px kicker uses ink instead). White ink on an accent fill is 2.95:1: never put text on the accent fill.
Material: flat type only. Outline echo = 2 px accent stroke (`-webkit-text-stroke`), profile says 1.5 px; 2 px stays visible at 1080 wide. No gradients, no grain (profile optional; skipped).

## 2. Fonts (3 local files; the profile's Anton, Inter Tight, Instrument Serif, Be Vietnam Pro are NOT installed)

| Role | Profile asks | Used here |
|---|---|---|
| Impact and connecting words | Anton uppercase / Inter Tight 800 | `SegUIVar.ttf`, weight 700 (axis max), uppercase, `letter-spacing:-0.02em`, `line-height:0.86`. It is wider than Anton: "KHÔNG" needs 240 px, not 300, to stay inside 936 px |
| Kicker and footer | none | `CascadiaMono.ttf` 700 (kicker 44 px, tracking 0.14em) and 600 (footer 32 px) |
| One emotional italic line per beat | Instrument Serif Italic | `cambriai.ttf` (Cambria Italic, 400 only), 84-92 px, lower-case, no tracking |
| Never | | `segoepr.ttf` (no Vietnamese letters) |

Vietnamese diacritics check: the owner docs measured all 36 stacked-diacritic letters present in these three files. In this build the check was done by eye on 1080x1920 renders of every word used: MỘT, VỤ ÁN, KHÔNG, LỜI GIẢI, ĐÊM, TÊN, SẮP RA MẮT, "sự thật chưa từng được kể", "nhớ đặt lịch nhắc", "Minh hoạ", "Series truyền hình mới" all draw every mark (see trap 1 for the one that was cut by a mask, not by the font). The scripted fontTools check could not be run in this sandbox (python scripts needing approval).
Max three typefaces (profile): met (3).

## 3. Type scale, safe areas and grid (1080 x 1920)

| Role | Size | Notes |
|---|---|---|
| Hero word (beat 1 VỤ ÁN) | 270 px | width about 850 px |
| Hero word (beat 1 KHÔNG / LỜI GIẢI) | 240 / 200 px | widths about 880 / 760 px |
| Title words (beat 2 ĐÊM / KHÔNG / TÊN) | 300 / 240 / 300 px | |
| Date (beat 3, "12.12") | 395 px | about 930 px wide, nearly full width; with the 1.04 zoom it touches the margin: 430 px crossed the frame edge |
| Date label "SẮP RA MẮT" | 165 px | |
| Connecting words | 112-120 px | |
| Serif italic | 84-92 px | |
| Kicker | 44 px mono | |
| Footer "Minh hoạ" | 32 px mono | the only line under 90 px except the kicker; above the 30 px floor |

Grid: left axis x = 72, text column 936 px (x 72-1008). Stacks are positioned by their top: beat 1 y 300, beat 2 y 170, beat 3 y 260. Everything real ends by y about 1400; footer at y 1520 (the platform's bottom UI starts about 1480, so the footer is a deliberate, small exception; moving it into the type area collided with the serif line, trap 3). Top 170 px empty. The profile's "big type above y 820" rule is for a caption band; no captions here, so the type uses y 170-1400. When captions are added, the stack must shrink or move up (untested).

## 4. Layers, back to front

`.sc` beat sections (one full-frame section per beat, own background, visibility toggled with `autoAlpha` on the cut frame) -> `.stack` (one scaled group per beat, the slow zoom target) -> `.ln` mask wrappers -> `.w` words -> `.echo` outline duplicate -> `.foot` -> `#fill` (accent block for the type-fill cut, above everything). No flash layer, no shake layer, no grain layer.

## 5. Components

- **Line mask** `.ln`: `overflow:hidden` with `padding-top:150px; margin-top:-150px; padding-bottom:70px; margin-bottom:-70px` (px, not em; see trap 1). Carries `data-layout-allow-overflow`. Any extra spacing between lines is added to the negative margin (`margin-top:-120px` means 30 px of space).
- **Word** `.w`: uppercase, display block, `will-change:transform`. Start state `yPercent:115, rotation:3-4, transformOrigin:"0 100%"`.
- **Outline echo** `.echo`: duplicate of the stressed word, transparent fill, 2 px accent stroke, scales 1 -> 1.18 and fades 0.9 -> 0 in 0.45 s.
- **Accent fill** `#fill`: positioned over the stressed word's box (left 72, top 1090, 760 x 170), then grows to the full frame.
- **Mask bar**: an ink block `scaleX 0 -> 1` (from the left) over the italic line, then `scaleX 1 -> 0` (origin switched to the right) while the line is revealed underneath.
- **Digits** `.digit`: each character of the date is its own inline-block that rises from below the mask, staggered 0.09 s. It is a slam, not a count, so no frame can show a partial number.
- **Footer label**: always the exact string "Minh hoạ", mono 32 px, solid mute colour per beat.

## 6. Motion language

Energy 4 in the profile; used as: line-mask rise (expo.out 0.45-0.55 s, rotation 3-4 deg resolving to 0), stressed-word nudge (scale 1 -> 1.03 -> 1, 0.2 s each way, power2.out), outline echo on the stress, slow push-in on each stack (beat 1: 1.00 -> 1.05 over 3.0 s; beat 2: 1.00 -> 1.03 over 3.8 s; beat 3: 1.00 -> 1.04 over 4.8 s, all `ease:"none"`; the profile asks 1.12 per line, but 1.10 made KHÔNG run off the right edge). No shake, no elastic, no blur.
Transitions used:
1. **Type-fill cut** (beat 1 -> 2, 2.95-3.30 s): the accent block grows from the word's box to the frame in 0.35 s `expo.in` while the three white lines are pushed left (`x:-1200`, 0.25 s `power3.in`); the orange word is hidden at 3.30 s, when the frame is already fully orange.
2. **Mask-slide reveal out of the fill** (3.40-3.68 s): `clip-path:inset(0 0 100% 0)` shrinks the orange block upward in 0.28 s `power3.out`; the light beat's kicker and first word are already rising from 3.45 s, so no empty panel is longer than 0.2 s.
3. **Invert-cut** (beat 2 -> 3 at 7.2 s): a hard cut, no tween, on the 12th beat of the hand-set 0.6 s grid; beat 3's kicker and connecting word start the same frame.
Stagger: lines enter 0.35-0.45 s apart (beat 1: 0.12, 0.50, 0.95 s; beat 2: 3.45, 3.55, 3.95, 4.30 s), a little before the previous line has settled.

## 7. Scene recipes (timings from this build; the voice anchor `W()` was not available, the times are hand-set)

**Beat 1, dark hook, 0.0-3.3 s.** Frame 0: MỘT (120 px) already in place; VỤ ÁN rises at 0.12, KHÔNG at 0.50, LỜI GIẢI (accent) at 0.95; echo and nudge on LỜI GIẢI at 1.5; hold with the push-in to 2.95; type-fill cut.
**Beat 2, light title, 3.3-7.2 s.** Kicker "Series truyền hình mới" (mono 44 px, ink), ĐÊM / KHÔNG / TÊN rise at 3.55 / 3.95 / 4.30; TÊN nudges at 4.9; the mask bar passes through the italic line at 5.20-5.67 s and "sự thật chưa từng được kể." is held from 5.42 s to the cut.
**Beat 3, dark date and final composition, 7.2-12.0 s.** Kicker, ĐÊM KHÔNG TÊN (118 px) at 7.20/7.28; date digits at 7.40, 7.49, 7.58, 7.67, 7.76 (complete by 8.26); SẮP RA MẮT at 8.10; "nhớ đặt lịch nhắc." at 8.70 (complete by 9.25). From 9.3 s to 12.0 s nothing but the push-in moves: the last 1.5 s is the full composition.
Rhythm: 3.3 s / 3.9 s / 4.8 s, something visibly new every 0.4-1 s inside beats and a cut every 3-5 s.

## 8. Captions

Not exercised (demo, silent, no voice). Profile rule kept as an untested assumption: minimal 40 px captions, big type never enters the caption band; on a build with a voice-over, check that the stack ends above the caption band (the sample's stacks end near y 1400, so captions would need a re-fit).

## 9. Sound

Not exercised (no music, no SFX). Profile: 100-128 BPM percussive score, whooshes on word entrances, a sub hit on the invert cut. The sample's cut times already sit on a 0.6 s (100 BPM) grid so a track can be dropped in later; this was not verified against audio.

## 10. Images

None. The style needs no assets (profile). No agy image was generated. Profile avoids imagery behind type; if one is ever added, it goes in an inset between lines, never behind a word.

## 11. Must not

- No text on the accent fill; no accent text smaller than 300 px on the light beat.
- No second accent word on a line; no accent line in a beat that already has one.
- No `em`-based mask padding (trap 1); no mask without padding for diacritics.
- No push-in above 1.05 on a stack whose words use more than 85% of the width.
- No fade-based entrances, crossfades, shake or flash.
- No text below 90% opacity on a held frame; no mute colour from the profile's rgba token for text.
- No counter that counts: slam the digits instead.
- No real company, product, price, spec or date; the label "Minh hoạ" stays on every beat.
- No more than three typefaces.

## 12. Traps seen in real builds (this build, 2026-11-15)

Found by reading snapshots at 0-11.6 s and a 2.5 fps contact sheet of the render.

1. **Diacritics cut under the mask.** First render: "VỤ ÁN" showed as "VU ÁN" (the dot under Ụ lost) and "SẮP RA MẮT" as "SĂP RA MĂT" (the acute above Ă lost). Cause: the mask wrapper had padding of `0.3em`, but `em` is the wrapper's own 16 px, not the 270 px word, so the padding was 5 px. Fix: padding in px (150 px top, 70 px bottom) cancelled by equal negative margins. A line-height of 0.86 puts the stacked marks outside the line box, so every mask on Vietnamese caps needs this.
2. **Inline margin overrides the cancelling negative margin.** After fix 1, an inline `margin-top:30px` on a line replaced the CSS `-150px`, so the stacks grew by 150 px each and the content ran into the footer. Rule: put the spacing inside the negative margin (`margin-top:-120px`), never next to it.
3. **Footer collided with the serif line.** At first the footer sat at y 1430 while beat 2's last line ended at about y 1375 x zoom 1.03 and beat 3's at about y 1470: "Minh hoạ" printed over "sự thật chưa từng". Fix: shrink ĐÊM/TÊN from 330 to 300 px, start beat 2 at y 170 (was 300), beat 3 at y 260 (was 330), and move the footer to y 1520. Measured gap now: type ends about y 1400, footer 1520.
4. **Width overflow from the zoom.** KHÔNG at 285-300 px plus a 1.10 zoom was cut by the right edge at 2.8 s (visible at "KHÔN" on the snapshot); the date at 430 px reached x 1077. Fixed with 240 px and zoom 1.05; the date at 395 px with zoom 1.04 stays inside x 1008. Segoe UI Variable Bold is about 15% wider than Anton: the profile's 180-420 px scale cannot be copied.
5. **Frame 0.** With every word below its mask, frame 0 was a dark frame with only the footer. Fix: MỘT is in place at frame 0 (no tween); the first rise starts at 0.12 s.
6. **Layout inspector warnings are mostly mask artefacts.** `hyperframes inspect` listed 10 `content_overlap` warnings at t = 0.67, 3.33 and 7.33 s (words still below their mask, inside the 150/70 px padding) and one real error: `clipped_text #serwrap overflowed bottom 5px` (the italic line's ợ dot). Fixed with `padding-bottom:16px`. After that only the warnings remain; they disappear once the word has risen. Do not add `data-layout-allow-overlap` blindly; check the frame.
7. **Empty lower third.** Beat 1 ends at about y 1250, so the bottom 35% of the frame is dark and empty for 3.3 s. It reads as intentional on a phone (platform UI covers it) but is the weakest frame; a production build should push the stack down or add a typographic inset (the profile's "small UI inset between type lines") there.
8. **Scripted frame check not runnable.** `frame_check.py` needs numpy, which is not installed here; the check was done by hand on a 6 x 5 contact sheet (2.5 fps). Measured on that sheet: longest empty-panel moment = the orange block 3.3-3.4 s then light panel with only a kicker until 3.55 s (about 0.25 s); ghost of outgoing beat after the cut: 0 frames; last 1.5 s: full composition; held frames at full opacity.

## 13. Retention levers to try next (not tested)

Word-locked timing to a real voice-over (`W()`), caption band co-existence, a kick-synced invert-cut, a stat beat with a real number, a second accent-filled word per beat over a longer video, and a rotate-90 reading-direction change at a section turn (profile signature, not built).
