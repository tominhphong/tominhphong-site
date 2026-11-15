# Style: constructivist-poster (first document, written from the demo build of topic shape t139, 2026-11-15)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), as observed in this build.** Declarative, collective, "a group demands / announces / calls" stories: manifestos, coalition statements, campaigns, petitions, call-to-action and sign-up moments, labour and housing advocacy, bans and orders. It carries three short demands well (three slabs) and one big imperative well ("KÝ TÊN VÀO TUYÊN NGÔN"). Not for warm intimate stories, dense numbers (no room for more than one number per beat), product or UI demos, or sad stories. Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build: one silent 12.0 s sample (`samples/sample-t139.mp4`, 1080x1920, 30 fps, 5.7 MB). Voice-over, caption, word-timing, music and SFX rules were NOT exercised and are not written here; the profile's caption and sound lines are unverified. Content on screen is generic and labelled "Minh hoạ". Only 3 beats and 1 generated image were tested. Everything in sections 1-9 is measured on this one build; anything marked ASSUMED was not tested.

**Example video shows the visual recipe, not the niche.** Housing-coalition content was only a vehicle.

## 1. Tokens

```css
:root{--bg:#efe6d2;--ink:#141414;--red:#c8102e;--cream:#f6efdf;--grey:#5e5a55}
```
Contrast (WCAG relative luminance, computed by hand with the formula; the session could not run Python scripts):

| Pair | Ratio | Use |
|---|---|---|
| ink on bg | 14.8 : 1 | headlines, body |
| cream on ink | 16 : 1 | label tag, black strip, black block text |
| cream on red | 5.1 : 1 | slab text, big cream headline on red (>= 46 px only) |
| red on bg | 4.7 : 1 | the ONE key word per beat, only at >= 150 px |
| grey on bg | 5.5 : 1 | not used in this build (ASSUMED ok for a footer) |
| ink on red | 3.5 : 1 | big headline only (128 px used); never below 60 px |

Rules: red, black, cream only. Red is for wedge, slabs and one key word per beat. Rendered red measured about #b0002a to #c8102e because the grain overlay (multiply, 16 %) darkens flats: keep the overlay <= 16 %. The `hyperframes validate` contrast audit reported 15 warnings at 1.19 : 1 (tag, strip, date); they are false positives (it samples under the full-frame grain layer and hidden beats): the snapshots show the real contrast. Ignore, but look at the png.

## 2. Fonts (glyph test)

| File | Result | Role |
|---|---|---|
| `SegUIVar.ttf` | Vietnamese capitals and lower case render with all marks in snapshots (NHÀ Ở, NGƯỜI, TUYÊN, ĐẤT, ỔN ĐỊNH, ĐÌNH). Owner docs measured 0 missing glyphs for the same file | everything: headline (700), slabs (700), small text (600) |
| `CascadiaMono.ttf` | renders "TUYÊN NGÔN", "NỘI DUNG GIẢ ĐỊNH" with marks | dates and footers, 30-34 px |
| `cambriai.ttf` | not used | - |
| `segoepr.ttf` | lacks Vietnamese letters | never used |

The profile asks for Oswald and Russo One, which are not in `assets/fonts`. SUBSTITUTE: SegUIVar 700 with `transform: scaleX(.8)` on an inline-block wrapper to fake a condensed face. Method note: the glyph test script could not be run (Python scripts needed approval, denied); the diacritics check is the visual check of the rendered frames plus the owner-docs result.

**Trap 1 (measured).** `scaleX` does not shrink the layout box: the unscaled width still counts, so a line that looks fitted overflows or clips where the parent is narrower. Size lines by natural width * 0.8 and verify in the snapshot.

## 3. Grid and safe areas (1080 x 1920)

- Side margin 72. y 0-200 is the platform zone: only the "Minh hoạ" tag (y 140, 34 px).
- Headline block y 330-1060 (rotated). Content stays above y 1880. No captions in this demo.
- Main axis: -14 deg for the headline, -8 deg for slabs, -12 deg for the closing headline. Do not mix more than three angles; all rotate counter-clockwise (rising to the right).
- Corners are hard; radius 0 everywhere.

## 4. Layers, back to front

1 background bed (cream or red); 2 baked image or big shape (wedge, black block); 3 headline and slabs; 4 transition wedge (z 70); 5 label tag (z 80); 6 grain (z 90, multiply 16 %).

## 5. Components

- **Wedge**: clip-path triangle 1700 x 900, red, bottom-left to upper-right at about -28 deg (beat 1 lower half).
- **Headline stack**: three lines at 250 px, SegUIVar 700, scaleX .8, uppercase; the middle line red. Natural widths: "CHO MỌI" about 800 px after scaleX at 250 px.
- **Black strip**: ink bar with cream text 52 px, padding 14 x 26, rotated -14 deg, used for the subtitle so it never depends on the background under it.
- **Slab** (beat 2): 1300 x 230 bar, rotated -8 deg, red / black / red; number 130 px and label 76 px, cream.
- **Image panel**: agy picture, 980 x 400 crop, rotated -8 deg, object-position 50 % 70 %. The generated image is already in palette (red, black, cream halftone): no filter needed.
- **Tag**: ink bar, cream 34 px, with "Minh hoạ" in a cream box with red text.
- **Black block** (beat 3): ink slab y 1200-1920 holding the slogan and footer.

## 6. Motion language

- Everything enters on a straight line, no bounce: `power4.out` 0.45-0.5 s for slabs and wedge; `expo.out` 0.55 s for type.
- Offsets: type from x = -1200 to -1600 (left) or +900 (right); the three headline lines stagger 0.15 s.
- Slabs alternate left, right, left (4.3 s, 4.7 s, 5.1 s; 0.4 s step), each hard-stopped.
- Held micro-motion: 2.6-3.0 s `ease:"none"` creep of 12-40 px along the axis (wedge, headline, slabs, closing headline). Nothing is frozen.
- No glow, no pulse, no shadow, no overshoot.

## 7. Captions

Not exercised (demo build, silent). Profile line (black bar, 42 px Be Vietnam Pro 700 cream, current word red) is untested; Be Vietnam Pro is not in the local fonts, so SegUIVar would substitute.

## 8. Scene recipes (12.0 s sample)

| Beat | Time | Recipe |
|---|---|---|
| 1 Cover | 0-3.96 s | Wedge drives in (0-0.45), headline "NHÀ Ở / CHO MỌI / NGƯỜI" slides along -14 deg and locks by 1.0 s, black subtitle strip and mono date at 0.95-1.6 s. Hold 2.4 s with creep |
| Transition | 3.55-4.4 | Full-frame red square rotated 25 deg crosses left to right: in 0.40 s `power4.in`, swap at 3.96, out 0.42 s `power3.out` |
| 2 Demands | 3.96-8.4 | Title "BA CAM KẾT" (190 px, one red word), image panel at 4.05, three slabs 01 02 03 at 4.3 / 4.7 / 5.1 s. Hold 3 s |
| Transition | 8.0-8.85 | same wedge |
| 3 Call to action | 8.4-12.0 | Black block rises, "KÝ TÊN" 310 px cream, "VÀO TUYÊN NGÔN" 128 px ink, slogan 66 px, "MINH HOẠ / NỘI DUNG GIẢ ĐỊNH" 30 px. Full composition from 10.0 s |

Cadence: a visible change every 1.5-4 s. Rhythm was set by hand, not by beats.

## 9. Transitions

Wedge-drive only (two used): the swap happens while the frame is fully red, so no outgoing ghost remains. `diagonal-slide` is inside each beat. Hard cut on downbeat was not tested.

## 10. Image guidance for agy

One image only, brief that worked (78 s, one pass, no text): "1920s Russian Constructivist poster illustration, flat ink halftone cut-out of a tall row of apartment houses and a crane seen from a low angle, black and deep red on cream newsprint paper, letterpress grain, strong diagonal composition, bold red wedge, no text". Result: in palette, no letters, no people. A heroic human figure (profile signature) was not tested because of the "no real people" rule.

## 11. Sound

Not exercised. Profile: march-like 112-132 BPM, press stamp and clank SFX; unverified.

## 12. Must not

- No bounce, no soft shadow, no gradient, no rounded corners, no glass.
- No colour outside red, black, cream (the image is the only other tone: its halftone greys).
- No text under 30 px (the smallest here is the 30 px footer).
- Never `segoepr.ttf`.
- No number or fact presented as real in a demo: label "Minh hoạ".

## 13. Traps seen in real builds (this build, measured)

1. **scaleX does not narrow layout** (section 2): first pass had "CHO MỌI", "VÀO TUYÊN NGÔN" and the slogan clipped at the right edge at 290 / 150 / 84 px. Fixed at 250 / 128 / 66 px.
2. **Red text on a cream-to-red diagonal**: the first subtitle (cream on the wedge) crossed the wedge edge and was unreadable on the cream part. Fix: a black strip behind it.
3. **Accents hit the tag**: the 290 px headline at top 300 put the Ở mark into the tag at y 140-200; moved to top 400.
4. **Late second beat**: first timing left the lower half of beat 2 empty for about 2 s (slabs at 4.55 / 5.15 / 5.75, panel 6.2). Moved to 4.05 / 4.3 / 4.7 / 5.1; the lower half now fills by 4.5 s.
5. **Big empty red field in beat 3**: at 230 px the closing headline left a hole between y 700 and 1200; at 310 px it fills.
6. **Validator contrast warnings at 1.19 : 1** are false positives under a full-frame grain layer (section 1).
7. **Frame-check script could not run** (no numpy in the session); replaced by an ffmpeg tile sheet every 0.5 s plus dense frames around the transitions. Run the real script where numpy exists.
8. The inline-block `.cond` wrapper rotates and scales as one: rotate the parent, scale the child; do both on one element and the origin shifts.
