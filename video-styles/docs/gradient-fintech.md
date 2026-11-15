# Style: Gradient fintech (9:16 Vietnamese pricing / product-change edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in the t034 demo build:** a calm, premium "one product changes, here is the new thing" story: a pricing change, a new plan or tier, a new API or feature with a short config or code snippet that drives a live card. Works best with 1 hero number plus 2-3 supporting cards. Not for dense multi-number reports (use saas-bento), enforcement or sad news, quote stories, or anything needing a photo montage. Tier 2 never widens tier 1.

**Status.** Written 2026-11-15 from ONE demo build: a silent 12.0 s, 1080x1920, 30 fps sample on topic shape t034 ("Pricing change: an AI assistant adds a cheaper plan", Jev fit 0.65). **Voice-over, captions, sound and pronunciation rules were NOT exercised**; section 8 and 9 are inherited from the profile and marked UNTESTED. Everything with a number in it below was measured or computed in this build; anything else is ASSUMED. All content on screen is generic and labelled "Minh hoạ".

Source of values: `styles/profiles/gradient-fintech.yaml` (energy 3). Where the build departed from the profile, the departure is stated.

Characteristic look: a slanted baked-mesh gradient band across the top, white 12 px-radius cards with deep soft shadows entering from depth, one card lifted with an accent ring, a navy code panel that types while the lifted card updates (button spinner, then a drawn check).

## 1. Tokens

```css
--bg:#f4f6fa;  --ink:#14213d;  --mute:#4a5468;  --accent:#7050e8;  --card:#ffffff;  --navy:#14213d;
--navy-mute:#c9d2e6;  /* ASSUMED added: secondary text on navy */
--teal:#2bd9d0; --pink:#ff7ab8; --orange:#ffb86b;  /* mesh colours: band, badge gradient, code syntax only */
--accent-deep:#5a3fd0; /* button "done" state fill */
```
Contrast (WCAG formula, computed by hand because the python/node one-liners were blocked in this session; `hyperframes validate` independently reported "15 text elements pass WCAG AA"):

| Pair | Ratio | Use |
|---|---|---|
| ink #14213d on bg #f4f6fa | 14.77 | headline |
| ink on card white | 15.99 | card names, prices |
| mute #4a5468 on white | 7.61 | features, sub-lines |
| mute on bg | 7.03 | footer line |
| accent #7050e8 on bg | 4.85 | headline key words (72 px, large text) |
| white on accent | 5.25 | chip "Rẻ hơn Pro 67%" |
| ink on pink #ff7ab8 | 6.64 | badge gradient, left end |
| ink on orange #ffb86b | 9.38 | badge gradient, right end |
| teal #2bd9d0 on navy | 9.09 | code keys |
| pink on navy | 6.64 | code numbers |
| orange on navy | 9.38 | code strings |
| navy-mute #c9d2e6 on navy | 10.54 | code panel title |
| white on navy | 15.99 | button text |
| mute #4a5468 on navy | 2.10 | FAILS: never put mute on navy |
| violet #9a6cf5 on navy | 4.45 | not used as text |

Rules: mesh colours only in the band and small highlights (badge, code syntax); never as paragraph text. White text on the mesh band fails, so the band carries only the white kicker pill; the headline sits on `--bg` below the band.

## 2. Fonts (3 local files; the profile's Sora / JetBrains Mono / Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headline, card names, chips, kicker, button | Sora 700 / 600 | `SegUIVar.ttf` weight axis 300-700 (700 headline, 600 kicker/units, 500 body) | Rendered "Trợ lý AI thêm gói giá nhẹ hơn", "Dừng gói bất cứ lúc nào", "Rẻ hơn", "MINH HOẠ" in the snapshots: all diacritics visible, none clipped at line-height 1.12. The 36-letter fontTools test could not be run (interpreters blocked), so the check is visual on the strings actually used. |
| Prices, code | JetBrains Mono 400 | `CascadiaMono.ttf` weight axis 200-700, 700 for prices, `font-variant-numeric: tabular-nums` | digits and "đ" render; Vietnamese letters not needed in code lines |
| Never | | `segoepr.ttf` (no Vietnamese) | |
| Not used here | | `cambriai.ttf` | not needed in this recipe |

Declare faces with `font-display: block`.

### Type scale (1080 x 1920, px; all measured from this build's CSS)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| `.hl` headline | Seg 700, -0.02em | 72 / 1.12, 2 lines in 880 px | key phrase in `--accent` |
| kicker | Seg 700, +0.06em | 30 | white pill, 64 px high, radius 32; always contains "MINH HOẠ" |
| `.nm` card name | Seg 700 | 44 / 1.2 | |
| `.pr` price | Cascadia 700 | 56 / 1.2 | unit "đ/tháng" Seg 600 30 px mute |
| badge, chip, feature, button, sub-line | Seg 500-700 | 30 / 48 (chip, badge), 30 / 44 (feature) | profile says 22-24 px: raised to 30 because the acceptance bar forbids text under 30 px |
| code line | Cascadia | 32 / 48 | profile says 22 px: raised to 32 |
| footer | Seg 500 | 26 / 34 | the ONE allowed sub-30 line: "Minh hoạ: nội dung giả định, ..." |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  top platform UI: empty (band art only)
y 190  -254  kicker pill
y 372  -542  headline (2 lines of 81 px)
y 690  -1480 content stack: cards x 100-980 (880 wide)
y 1160 -1450 code panel (beat 3)
y 1458 -1492 footer line
y 1480 -1920 bottom platform UI: empty
```
Cards use one column: left 100, width 880, radius 12. Card slots (beat 2): Free y 690 h 130; Lite y 850 h 450; Pro y 1330 h 130 (ends 1460). Beat 3: Lite y 660 (after -190 move; stack drift -30 puts it at ~630) h 450; code panel y 1160 h 290.

## 4. Layers, back to front
`#band` (baked mesh JPG, skewY -8deg, constant for the whole video) -> `#kick` -> `#head` (h1 and h2, swapped) -> `#stack` (perspective 1800 px; cards) -> `#code` -> `#foot`. No flash, no shake, no beat pulse (no music). Page background is flat `--bg`; no fade layer (the last frame is a full composition).

## 5. Components
- **Band:** one agy-generated vertical mesh image (pink, orange, violet, teal), used as `background` 130% wide on a 1320 x 600 box with `skewY(-8deg)`. Baked image, not blurred divs (profile constraint). Bottom edge reaches y ~190 at the right and ~340 at the left.
- **Card:** white, radius 12, shadow `0 50px 100px -20px rgba(20,33,61,.22), 0 30px 60px -30px rgba(0,0,0,.3)`. Active card adds a 4 px accent ring.
- **Badge** "MỚI": gradient pink to orange, ink text 30 px, radius 24. **Chip:** accent fill, white text.
- **Code panel:** navy, radius 12, title "plan.json" 30 px navy-mute, 3 lines of 32 px mono.
- **Button:** navy 68 px high; states: label, spinner (34 px ring), done (accent-deep fill + white check drawn with `strokeDashoffset`).
- Max 3 cards in the stack here (profile limit 4).

## 6. Motion language
Energy 3: no shake, no flash. Eases: entrances `power4.out` / `expo.out`; layout moves `power3.inOut`; exits `power2.in`. Entrance verbs: slant sweep of the band (0.7 s `power3.inOut`, x -1400 to 0); headline lines rise from a mask (0.6 s `expo.out`, 0.1 s eased stagger); cards from depth (z -300, y 60-80, rotationX 14 to 0, 0.7-0.8 s `power4.out`, 0.15 s apart); badge and chip `back.out(1.4)` 0.4 s; features slide 24 px 0.45 s with 0.22 s eased stagger. Micro-motion: one mesh-drift tween (background-position 0%/25% to 100%/70%, `sine.inOut`) spanning the whole 12 s with no repeat; stack float -18 px then -30 px in two slow tweens.

Transitions between beats: beat 1 to 2 carries motion (Pro steps down 440 px while Lite drops into the gap, 0.7 s, Free shrinks 170 to 130); beat 2 to 3 the outgoing cards and headline leave in 0.2 and 0.18 s (the ghost limit is 0.15 s plus ease; measured on frames: gone by 8.4 s) while Lite glides up 190 px.

## 7. Scene recipes (S = beat start; times from this 12 s build)

### R1 Hook (0 - 4.2)
Band sweeps 0-0.7; kicker 0.3; headline lines 0.5-1.1 ("Trợ lý AI thêm / gói giá nhẹ hơn"); card Cơ bản 1.0, card Pro 1.15, each with a 30 px sub-line. Hold from ~1.9 to 4.1 with the slow float.

### R2 New plan (4.2 - 8.2)
Pro steps down and the sub-lines fade (4.05-4.8); Lite drops in 4.25; price counts 0 to 99.000 from 4.4 and lands at 5.2 (final value held 3 s); badge 4.9; chip 5.3; three features 5.5-6.2; hold to 8.1 with the stack drifting.

### R3 Code drives the live card (8.2 - 12)
Others leave 8.1-8.3; Lite glides up 8.2-8.9; headline swaps to "Chọn gói mới, / trả ít hơn" 8.35; code panel rises 8.5; 3 lines type 8.9-9.3, 9.4-9.8, 9.9-10.3 (0.4 s each); button label hides 10.0, spinner 10.05-10.75, button turns accent-deep 10.75, check drawn 10.8-11.15, pulse 1.03 at 11.1; footer visible from 9.3. Last 1.5 s (10.5-12): full composition, nothing moving except the mesh drift.

## 8. Captions (UNTESTED: demo build is silent)
Inherited profile rule, not exercised: white pill, radius 12, soft shadow, Be Vietnam Pro is not installed so use Segoe UI Variable 600 at 40+ px, current word accent (`--accent` on white 5.25). Keep captions out of y 1458-1492 (footer) in a full build.

## 9. Sound (UNTESTED)
Profile: smooth electronic 100-120 BPM, soft ticks, success chime on the check (here at 10.8 s). Not built or heard.

## 10. Images (agy)
One image only, via `motion_tools.py image mesh "..."`: abstract mesh gradient, pink / orange / violet / teal, no text, no people. Took 89 s and came back portrait (768 x 1376), which suits a band cropped by `background-size`. Prompt that worked: "Abstract smooth flowing mesh gradient, soft blurred blobs of pink, orange, violet and teal, silky light, wide band, no text, no logos, no people, no grain". Prompting for a "wide horizontal band" still returned a portrait image, so crop in CSS.

## 11. Must not
- No live blurred divs for the mesh; baked image only. No grain or retro texture. No brand wordmarks or real prices.
- Slant stays -8deg everywhere. No white or navy-mute text on the band; no mute text on navy (2.10).
- No text under 30 px except one footer line. No `ease:"linear"` except drifts.
- Never write a formatted number with `tl.set(el,{textContent:"99.000"})`: see trap 1.
- Mesh drift never `repeat:-1`.

## 12. Traps seen in real builds (this build, t034, 2026-11-15)
1. **Counter lost its thousands separator.** At 6.5 s the Lite price read "99 đ/tháng" instead of "99.000". Cause: `tl.set("#num",{textContent:"99.000"})`; GSAP parsed the string as the number 99. Fix: remove the set; the counter tween's own `onUpdate` with a formatter already ends on "99.000" (verified at 6.5 s and 9.0 s snapshots). Related: the counter sat at "87.537" at 4.5 s; it finishes at 5.2 s (0.8 s after start), so no held frame is mid-count.
2. **Beat 1 was top-heavy.** First version had cards 130 px tall: at 2.5 s the cards ended at y 850 and 630 px of the safe zone (y 850-1480) was empty. Fix: cards 170 px with a 30 px sub-line (cards end y 1060); they shrink to 130 px in beat 2 when Lite arrives. Remaining empty band y 1060-1480 for 4 s in beat 1 is still large; a full build should add a third element (flow diagram) there.
3. **Feature list touched the button.** Third feature (y 300-344) vs button top 346 = 2 px. Fix: button top 366, height 68; card stays 450.
4. **Mask overflow warnings.** `inspect` reported 3 `container_overflow` warnings (12.46, 40.98, 6.44 px) at 0.67 s and 8.67 s from the rising headline lines. Fix: `data-layout-allow-overflow` on every `.ln` mask; rerun gives none.
5. **Frame 0 is blank.** At 0.0 s only the page colour shows (band starts off-screen); band is on by ~0.4 s. Under the 0.5 s limit, but a full build should start with the band already half-swept.
6. **Frame check script needs numpy.** `frame_check.py` failed (`No module named 'numpy'`) and interpreters were blocked in this session, so the check was done with an ffmpeg 2 fps contact sheet (24 frames) read by eye: no empty panel > 0.5 s, no cut text on held frames, outgoing cards gone by 8.4 s, last 1.5 s full. Not a numeric proof.
7. **Typing lines.** The code lines type by rewriting `innerHTML` from a proxy tween; mid-type frames (8.9-10.3) show partial words ("pla", "pri") which is intended, but each line completes 0.4 s after it starts and the panel is full by 10.3 s.
8. **Perspective stack.** Applying `perspective` on the stack container and animating `z` on cards gives the depth entrance; holding cards at rotateX 0 keeps text crisp and keeps `inspect` quiet. The profile's held tilt (rotateX 12 / rotateY -18) was NOT used: at 30 px text on a 880 px card it blurs and fails the "no text below 30 px effective" intent.
9. **Render.** 12.0 s render took 10.8 s on this Mac; file 1.8 MB.

## 13. Selected numbers for reuse
Canvas 1080 x 1920, 30 fps, 12.0 s, silent, h264, 1.8 MB. Kicker top 190; headline top 372; cards left 100 width 880; code panel top 1160 height 290; band skew -8deg; ring 4 px accent; 3 beats at 0 / 4.2 / 8.2 s.
