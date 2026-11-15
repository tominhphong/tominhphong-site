# Style: Neo brutalist web (9:16 Vietnamese demo edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Loud, cheeky, low-budget and community-flavoured shapes: underground events, zine and music fairs, indie launches, ticket and sign-up pushes, "3 things" lists, changelogs, social cuts. Topic shape t133 (underground zine fair: bands, printers, tickets; Jev fit 0.73) worked well: three parallel items, one ticket card and one button map directly onto the style's cards and button press. Not for solemn, premium, legal or finance stories, and not for dense numbers. Tier 2 never widens tier 1.

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample (`samples/sample-t133.mp4`, 1080x1920, 30 fps, 3.1 MB). No owner document existed before this one. **Voice-over, word timing, captions, sound and music were NOT exercised** (demo build): sections 7 and 8 are taken from the profile and marked ASSUMED. Content is generic and labelled "Minh hoạ" on screen; no real company, price or spec.

**Reading order.** Sections 1-6 and 9-11 are measured on the build. Section 12 lists the traps found in it.

Character (profile, energy 4): saturated flat blocks, 4 px black outlines, hard offset shadows that never blur; elements stamp in with overshoot like buttons being pressed. Source of values: `styles/profiles/neo-brutalist-web.yaml`; anything the profile does not give is **ASSUMED**.

## 1. Tokens

```css
--bg: #fffdf5;      /* page, warm paper                                   ink on it 20.6:1 */
--ink: #000000;     /* text, every border, every hard shadow               */
--accent: #ff5c00;  /* orange block                                        ink on it 6.78:1 ; white on it 3.10 (FAILS) */
--yellow: #ffe600;  /* highlighter block, ticket                           ink on it 16.6:1 */
--blue: #3d7bff;    /* block                                               ink on it 5.47:1 ; white on it 3.84 (FAILS) */
--white: #ffffff;   /* cards                                               ink on it 21:1 */
```

Rules: text is ink on every fill (never white on orange or blue: both fail 4.5:1). Max 3 fills on screen plus bg and ink (measured: S1 yellow/orange/blue, S2 yellow/orange/blue/white rows, accepted because the white is a card, not a fill; keep to 3 coloured). Flat only, no gradients, no glow. Contrast ratios computed with the WCAG formula by hand; `hyperframes validate` reported "10 text elements pass WCAG AA".

Material: `border: 4px solid #000; box-shadow: 10px 10px 0 #000; radius 0`. Stickers: border 4 px, shadow 6px 6px 0, mono 36 px uppercase. Pressed state: shadow 2px 2px 0 plus translate 8,8 (measured: 0.08 s down, 0.2 s `back.out(3)` up).

## 2. Fonts (local files only)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headlines, card titles, body | Archivo Black / Space Grotesk | `SegUIVar.ttf`, weight 700 uppercase, `letter-spacing:-0.02em`; body 600 | Rendered correctly in all frames for the letters used (Ạ, Ầ, Ở, Ế, Ự, Ớ, Ọ, Ờ...). The full 36-letter fontTools test was NOT run (the shell refused the call); run it before using other words. |
| Labels, stickers, numerals | Space Mono 700 | `CascadiaMono.ttf` weight 700 | Same: rendered correctly (Ạ in "MINH HOẠ", Ầ). |
| Never | | `segoepr.ttf` (no Vietnamese letters), `cambriai.ttf` (not this style) | |

Segoe at 700 is thinner than Archivo Black: the 4 px outline and the block carry the weight, not the font. The profile's "Be Vietnam Pro 800" caption font is not installed (captions not built).

## 3. Type scale (measured in the build)

| Use | px | Notes |
|---|---|---|
| Hook headline blocks | 150 | uppercase, one block per line, rotated -2 / +1.5 / -1 deg; "ZINE NGẦM" is the widest, 9 characters, about 840 px of the 1080 frame |
| Ticket headline | 150 | two lines inside the ticket card |
| Row titles | 88 | |
| Section header chip | 70 | |
| Chip labels | 56 | |
| Button | 84 | |
| Body line | 52 / 46 / 42 | weight 600 |
| Kicker, mono labels | 40 / 38 | |
| Stickers | 36 (44 for the long one) | |
| Footer line | 28 | the ONLY text under 30 px; one line |

## 4. Safe areas and grid (1080 x 1920)

```
y 0    -190  platform UI: empty
y 210  -1480 content (stickers last at y 1450-1510)
y 1560       footer line (28 px mono, centred, one line)
x 80   -1000 content column (cards 880 wide at x 100)
```

Loose 8-column feel, in practice a 880 px card column with 1-3 deg tilts (rotation never above 3 deg) and 20-120 px of deliberate offset between blocks. One dominant block per beat. S4 sits in a section shifted down 150 px so the final composition is centred (content ended at y 1250 before the shift, leaving the lower third empty).

## 5. Layers, back to front

1. `#root` background `#fffdf5` (no texture in this build; the profile allows a baked dot grid at 8%).
2. `#cam` wrapper (reserved for punch-in; not animated in the final build, see traps).
3. Scene sections (`visibility` toggled at the wipe midpoint).
4. Cursor (z 30).
5. `#foot` line (z 20).
6. `#slab` block-wipe (z 50, solid colour, 8 px ink edge).

## 6. Components

- **Headline block**: text on a flat colour rectangle with 4 px border and 10 px shadow, rotated 1-2 deg. One per line, never two words on one line if it exceeds 900 px.
- **Row card** (880 x 290): coloured number tile 150 px wide (mono 84 px "01"), title 88 px, one 42 px line. Three rows stacked with 50 px gaps, alternating tilt -1.5 / +1.2 / -0.8 deg.
- **Ticket card** (880 x 700, yellow): mono tag, 150 px two-line title, dashed 6 px perforation at 470 px, one body line, one mono "GIÁ: MINH HOẠ" line.
- **Button**: orange 600 x 170 block, 84 px label; presses on the cursor click and flips to yellow.
- **Cursor**: chunky black arrow with hard shadow copy; tip lands on the button's right edge, never on its label.
- **Sticker**: mono uppercase tag; every beat has "Minh hoạ" as one.
- **Chip stack** (closing): three rotated chips (-3, +2.5, -1.5 deg) at different x offsets.

## 7. Motion language

Energy 4, but no shake or flash was needed. Verbs used (all measured in the timeline):

| Verb | Recipe |
|---|---|
| Stamp | `scale 1.25 -> 1` with opacity 0 -> 1 and shadow 0 -> 10 px, 0.32 s, `back.out(2.2)`. Hook headline blocks use 1.12; closing headline 1.3 |
| Sticker | scale 1.4 -> 1, 0.28 s, then a 3 deg wobble 0.16 s x2, 0.5 s later |
| Kicker | slide from x -60, `power4.out` 0.3 s |
| Block-wipe | slab `x -1100 -> 0` 0.2 s `power4.in`, scene swap at the midpoint, `0 -> 1100` 0.2 s `power4.out`; slab colour = the next accent (yellow, blue, orange). Total 0.4 s, wipes at 3.0, 6.2, 9.4 s |
| Button press | translate 8,8 plus shadow 10 -> 2 px, 0.08 s; release 0.2 s `back.out(3)` |
| Hold micro-motion | headline blocks float y -8 over 0.8 s yoyo; row cards y -6; chips rotate +2 deg yoyo |
| Stagger | 0.25-0.35 s between stamps in a list (not uniform 0.05 s: rows are big) |

## 8. Scene recipes (demo timing; 12.0 s, 4 beats)

| Beat | Time | Content | Choreography |
|---|---|---|---|
| S1 hook | 0-3.0 | "HỘI CHỢ / ZINE NGẦM / Ở AUSTIN" on yellow / orange / blue blocks, white body card, "xem 3 thứ" sticker | frame 0 already shows the first block; blocks stamp at 0.35 and 0.7 s, body card 1.2 s, sticker 1.7 s; hold from 2.0 s |
| S2 list | 3.0-6.2 | "BA THỨ CHÍNH" header and rows 01 Ban nhạc, 02 Nhà in, 03 Vé vào | wipe in yellow; header 3.45, rows 3.7 / 4.05 / 4.4, sticker 4.9 |
| S3 ticket | 6.2-9.4 | ticket card, button "ĐẶT VÉ", cursor | wipe in blue; ticket 6.65, button 7.1, cursor arc 7.35-7.95, press 8.2, yellow flip 8.3 |
| S4 close | 9.4-12.0 | "ZINE HẾT LÀ HẾT" plus three chips and a sticker | wipe in orange; stamps 9.62, 9.9, chips 10.2 / 10.35 / 10.5, sticker 10.7; full composition held for the last 1.3 s |

Captions, voice and word anchors: not exercised. ASSUMED for a full build: anchor stamps on spoken words (`W(sid, word)`), button presses on the word "đặt" or "vé", and keep the 1.5-2 s reading holds.

## 9. Captions and sound (NOT exercised: demo build)

From the profile, ASSUMED: yellow caption block, 3 px ink border, 6px 6px 0 ink shadow, 42 px ink text, current word on orange. In 9:16 the caption pill must sit at y 1370-1480; this build's stickers stop at y 1510 and the footer is at 1560, so a full build must move the stickers above y 1370 or drop the footer. Sound: upbeat electro 120-140 BPM with clicks on stamps and presses; none built.

## 10. Images

None used (optional, skipped to stay lean). For a full build: one flat sticker-style shape or halftone-free illustration from agy, on bg colour, no text; never a photoreal render (profile avoid). Draw all UI in CSS.

## 11. Must not

- No emoji, no gradients, no blur, no glow, no soft shadow (every shadow `Npx Npx 0 #000`).
- Every filled shape has the 4 px ink border; text on a fill is ink, never white on orange or blue.
- No tilt above 3 deg on text blocks; tilted headline blocks need 20 px margin from the frame edge.
- No more than 3 coloured fills in a beat.
- No cursor covering a label on a held frame.
- No Vietnamese letters from `segoepr.ttf`.
- No real company, price or spec in a demo; label "Minh hoạ" on every beat.

## 12. Traps seen in real builds (this build, 2026-11-14, topic t133, 12.0 s)

1. **Cursor hid the button label.** First snapshot at 8.0 s and 8.3 s showed the arrow sitting on "ĐẶT VÉ" (tip at about x 434 of a label centred at 540), reading as "ẠT VÉ". Rule: aim the tip at the button's lower-right corner (final offset x +56, y -220 from the cursor's start); verify with a snapshot at the press frame. Fixed; later frames show the label clear.
2. **Empty beat after a wipe.** At 9.5 s the first S4 element only stamped at 9.85, so about 0.45 s of bare background followed the slab (under the 0.5 s limit, but visible in the 2 fps sheet). Rule: first stamp of a beat at wipe end plus 0.02 s (S4 moved to 9.62 s).
3. **Bottom third empty.** Before the fix, S4's content ended at y 1250 of 1920 and the sticker (y 1330) overlapped the footer line at y 1560. Fix: shift the section down 150 px and put the sticker at y 1305 + 150 = 1455; the final frame is now centred and clear of the footer.
4. **Fonts 404 in validate.** `hyperframes validate` failed with 4 errors ("404 loading assets/fonts/SegUIVar.ttf") because the font folder had not been copied into the project (the copy was blocked by the shell). Rule: check `ls assets/fonts` in the project before the first validate; after copying: "No console errors, 10 text elements pass WCAG AA".
5. **Lint warning is harmless.** `overlapping_gsap_tweens` on `#slab` (0.00-0.20 s): the shared slab is reused by `fromTo` with explicit values, as the composition contract asks. `inspect` also reports a nested `div.txt` overlap in the ticket (150 px lines with line-height 1 touching); both are intentional, the render is clean.
6. **Frame-check tool needs numpy.** `frame_check.py` stopped with `ModuleNotFoundError: numpy`; the substitute was a 2 fps ffmpeg contact sheet read by eye (see `selfcheck.md`). Install numpy where the tool runs, or this check is only visual.
7. **Weight.** Segoe 700 is lighter than the profile's Archivo Black; headlines still read as loud at 150 px with the 4 px border. Do not go below 120 px for headline blocks.
8. **Tilted blocks and the frame edge.** Rotations of up to 2 deg on 880-900 px blocks moved corners by about 16 px; blocks sat at x 80-150, so nothing touched the edge. Keep that margin.
