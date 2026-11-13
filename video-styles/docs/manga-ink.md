# Style: manga-ink (9:16 Vietnamese news edition, aesthetic family)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** Youth-culture and fandom stories where the subject is a drawn world meeting a product: anime or manga collaborations with footwear and streetwear brands, teen artists winning contests, creators crowdfunding a printed comic volume. It works because the subject itself is ink-on-paper. It carries 4 to 8 short facts well (names, 3 prices, 3 dates) and holds a dramatic opening. Not for sad, enforcement or legal stories (the impact frame reads as violence), not for dense numeric dashboards, not for calm service stories. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built. Section 12 is the list of traps seen in the real build (the later rule wins over any earlier line).

**Status.** Written 2026-11-13 from one full build (video `crocs-chainsaw-man-guoc-hop-tac`, 58.85 s) and two 10 s samples (t123, t163). Source profile: `skill/references/styles/profiles/manga-ink.yaml` (energy 5). Everything the profile does not give is marked **ASSUMED**. Not yet merged into the skill folder.

**One-line look.** A printed black-and-white manga page: diagonal ink-bordered panels on warm paper, radial speed lines behind everything, one red spot colour, an inverted black impact frame with a short shake on the key word, and an ink-bar slash between scenes. Voice only (no music, no SFX in this build).

## 1. Tokens

```css
--bg:#f7f4ec;        /* paper (profile)                                  */
--ink:#0a0a0a;       /* line, text, borders (profile)   18.0:1 on bg, 19.8:1 on white */
--red:#e8132b;       /* spot colour, BIG text/fills only: 4.19:1 on bg, 4.60:1 on white, 4.3:1 on ink */
--red-ink:#c40f24;   /* red used as SMALL text (caption current word, label name): 5.55:1 on bg, 6.10:1 on white  (ASSUMED token) */
--ink2:#4a4a4a;      /* secondary text, unread caption words: 8.06:1 on bg, 8.86:1 on white (ASSUMED token) */
--tone:#9a9a9a;      /* NEVER text: 2.56:1 on bg. Screentone is made of ink dots instead */
--paper2:#e9e4d6;    /* second paper for one panel background */
```
Contrast was measured with the WCAG formula by hand; `hyperframes validate` reported "40 text elements pass WCAG AA". Rule as built: `--red` only for text of 100 px or more (large text, 3:1) and always with a 7 px ink outline (`-webkit-text-stroke:7px; paint-order:stroke fill`); every red text under 60 px uses `--red-ink`. The profile rule "red at most once per scene" was built as "one red element on screen at a time": in a multi-item scene (S3) the red moves from label to label on the spoken word and the previous one returns to ink.

## 2. Fonts (local files only)

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Impact headlines, numbers, labels, captions | Dela Gothic One | `SegUIVar.ttf` weight 700, `letter-spacing:-0.02em`, plus a 7 px ink text-stroke to fake the heavy brush weight | letters used in the video were checked by eye on rendered frames: Ầ Ê Ạ Ả Ỹ Ỹ Ố Ớ Ô Ậ Ữ Ỳ ắ ế ợ ề ễ ỡ ộ (e.g. "LẦN ĐẦU TIÊN", "ĐOẠT GIẢI", "CÁC NHÂN VẬT", "GÂY QUỸ", "Nhật Bản", "nhiều màu") all drew correctly. A fontTools coverage check was NOT run (the sandbox of this build refused ad-hoc python), so the 36-letter table of the other owner docs is cited, not repeated |
| Labels, bubbles | M PLUS 1p 800 | `SegUIVar.ttf` 700 | same |
| Hand-lettered SFX | pre-drawn SVG/PNG | NOT used (no SFX words in this topic) | n/a |
| Never | | `segoepr.ttf` (lacks Vietnamese letters) | not used |

`CascadiaMono.ttf` and `cambriai.ttf` were not needed. Declare the face with `font-display:block`, weight range `300 700`. Line-height 1.12 is the minimum that kept the tone marks of 108 px uppercase lines (Ầ, Ạ, Ả) unclipped.

### Type scale (1080 x 1920, px, measured in this build)

| Token | Size | Use |
|---|---|---|
| hook slab line | 108-128 (uppercase) | `CROCS ×` / `CHAINSAW MAN` |
| numeral | 170-430 | "4" 430, "27" 190, "11" 250, "8–11" 170, prices 150-176 |
| title line | 96-112 | sample slabs |
| label | 46-52 | panel names, box lines |
| sub-label | 34-40 | detail line, "Theo Sole Retriever" |
| caption | 44 / 1.25 | one line, max width 1000 |
| footer | 24 | the single allowed small line (source) |
Nothing else is under 30 px.

## 3. Safe areas and grid (1080 x 1920)

```
y 0    - 170   empty (platform UI)
y 190  - 1290  PAGE: panels (gutter 12 px, 6-8 px ink border)
y 1336 - 1366  footer source line (24 px, paper background)
y 1389 - 1480  caption pill (bottom edge 1480, one line = 91 px tall)
y 1480 - 1920  empty except speed lines
x 24   - 1056  panel column (1032 px)
```
Lowest content edge on every scene hold: y 1290 (acceptance asks >= 1250). Speed lines run to the bottom edge behind everything; they are background, not content. The camera push scales about (540, 740), so a panel edge at 1290 reaches about 1317 at the end of a scene: keep the footer at 1336 or lower.

## 4. Layers, back to front

`#root` paper -> per scene `.cam` (the only thing pushed) holding: speed-line SVG (ink, seeded), panels (`.pn` = clip-path polygon `.in` with art + a separate SVG polygon border `.bd`), label boxes, numerals, bubbles -> `#spd` speed-line burst overlay (transition) -> `#bar` ink slash -> `#imp` inverted impact frame (ink fill, paper speed lines) -> `#foot` -> `#caps`.

## 5. Components

- **Panel**: diagonal polygon, one or two slanted edges (offset 6-10% of the side), border drawn as an SVG polygon stroke 8 px (the visible 4 px inside + 4 px outside; the clip-path would cut a CSS border). Flat, no shadow (profile). Background paper, white, `--paper2`, a screentone, or ink.
- **Label box**: white, 6 px ink border, sits on the panel's bottom edge with `-6px` offsets so the borders merge. Panels that carry a label box have a STRAIGHT bottom edge (a diagonal bottom corner cut the label text in the build).
- **Slab** (title): white box, 6 px border, rotated -1.5 deg (the S7 slab is black, +1.2 deg, paper text).
- **Numeral**: 170-430 px, 7 px ink outline, red only for the one hero number of the scene.
- **Speech bubble**: SVG ellipse (stroke 6) plus a mitred tail polygon, 46 px text, pops with `back.out(1.7)` after the word it follows.
- **Screentone**: SVG data-URI dot lattice at three densities (pitch 12 / 18 / 22 px, radius 1.8 / 4 / 7.4), used as `background-image` on 1-2 panels per scene or with `mix-blend-mode:multiply`.
- **Inverted art**: `filter:invert(1)` on a wrapper turns the white-ground ink drawing into a black panel with white lines; used on at most 2 panels per scene (filters are on the renderer's heavy list).
- **Caption pill**: white, 4 px ink border, `6px 6px 0 ink` hard shadow, 44 px 700, `width:max-content; max-width:1000px`, words `--ink2` until spoken, current word `--red-ink`, spoken words `--ink`. Chunks <= 6 words, split after a comma/full stop at >= 3 words.
- **Footer**: one line, 24 px `--ink2`, paper background with 10 px padding, so speed lines never cut through it.

## 6. Motion language

Energy 5 in the profile; built at "tense hold, one hit per section".

| Verb | Recipe as built |
|---|---|
| slam | `scale 1.5 -> 1`, `opacity 0 -> 1`, `rotation -4..-6 -> 0..-1.5`, 0.2-0.22 s `power4.out`; panels use `scale 1.1 -> 1`, 0.2 s |
| impact frame | `#imp` (ink fill + 190 paper speed lines) visible for 0.07 s (2 frames at 30 fps), then `shake`: 6 steps, amplitude 10 px decaying 1 -> 0.15, 1/30 s apart, on `#stage`/`#root` |
| scene transition | ink bar (1900 x 2080 px, skewX -18 deg) sweeps x -2600 -> 2600 in 0.38 s `power2.inOut`, starting 0.2 s before the next scene start; the scene swap (`visibility`) happens at +0.19 s under the bar; a speed-line burst overlay shows 0.1 s |
| camera | slow push `scale 1.00 -> 1.05` linear over each scene, alternating x drift +-10 px; the hook also does `1.00 -> 1.04` then a snap back `power2.in` / `expo.out 0.12 s` on the key word |
| hold micro-motion | image drift 8-14 px over the whole hold (`sine.inOut`) so nothing is frozen |
| pop | bubble / chips `scale .6 -> 1`, `back.out(1.6)`, 0.26 s |
| slide-in | label lines `x -80 -> 0`, 0.3 s `power4.out`, stagger 0.12 |
Never used: counters (numbers are static slams, so no frame can hold a mid-count), line masks, typing effects, opacity dims. Transition vocabulary in one video: ink-bar slash plus speed-line burst only (the resolver warns above two languages).

## 7. Scene recipes (S = scene start, W() = estimated spoken-word onset)

- **R1 Hook (0-5.07 s).** Frame 0 is finished: speed lines, a tilted (-3 deg) hero panel holding the product drawing, a bubble (appears on "truyện"), and the slab with the two names. On the key word ("Chainsaw", est. 2.95 s) the panel snaps 1.04 -> 1.00, the impact frame flashes 0.07 s and the screen shakes. Red: the franchise name.
- **R2 Count (5.07-11.9 s).** A title panel on screentone + two image panels (product, atmosphere). The hero digit "4" (430 px, red, rotated -4 deg) slams on "bốn" with an impact; "+1" (paper-filled, outlined) slams on "một". All three panels are on screen from S+0.3 s.
- **R3 Four designs (11.9-23.61 s).** 2 x 2 panels with different diagonals, each a crop of the same drawing (flipped, screentone, inverted) so the page is never empty. Names are on screen from the start; the detail line slides in and the name turns `--red-ink` on its spoken word. Four anchors, 3-4 s apart.
- **R4 Prices (23.61-33.48 s).** Three stacked panels: white box with the price (176/176/150 px) + 442 px image strip. The middle price is the red one. Each price scale-slams (1.35 -> 1, 0.2 s) on its spoken number; one impact + 8 px shake on the second.
- **R5 Dates (33.48-42.95 s).** Two panels, image on top, white box lower-left/lower-right with the date numeral; "8–11" slams on "tám", "27" (red) on "hai".
- **R6 Where (42.95-53.14 s).** Panel A: "11" red numeral slams on "mười", plus the outlet name; panel B (black, inverted drawing): label lines slide in on "riêng" and "chỉ".
- **R7 Close (53.14-58.85 s).** Full-width illustration panel, a black slab slides in on "bốn" and stays; no fade, so the last 1.5 s are a full composition.

## 8. Captions

As section 5. Times are ESTIMATED from the voice step (character share inside each scene), so a late phrase can be up to about 0.4 s off; anchors for visuals were placed on words that open a clause, never on the last word of a long sentence. First chunk of a scene starts at S; chunks never overlap (end = min(last word end + 0.15, next start - 0.04)). The caption text is the spoken text (numbers in words); on-screen numerals are digits that say the same thing.

## 9. Sound

Voice only in this build (VieNeu "Hải Đăng", loudnorm -14 LUFS target; measured -15.5 LUFS, peak -4.1 dBFS on the final). The profile asks for J-rock/anime-opening music at 128-150 BPM and whoosh-slash, impact boom and ink-splat SFX: none are available in this toolset, so the impact frame is silent. If music exists, put the impact frames on `TIMING.drops` and the slash on kicks (profile).

## 10. Images (agy)

Five prompts worked at the first attempt (768 x 1376 JPG, ground #f6f4ef, a thin black frame line about 30 px inside the border):
- "Black-and-white Japanese manga illustration, bold brush ink linework with grey screentone dots for shading: ONE <object>, three-quarter view, centered, large, dramatic radial speed lines behind it, pure white paper background, high contrast, no colour, no text, no logo".
- Scenes with people: "no faces, ground-level view of feet" (the street image) gave a usable atmosphere panel with no identifiable person.
Rules learned: crop the frame lines away with the panel window (scale the image 1.1-1.5 and position so the window sits inside the frame); do not ask for several different products in one picture (the "shelf of four clogs" came back as four platform clogs that do not look like the product: it is atmosphere, so the footer says "Tranh: minh hoạ do AI vẽ"); invert instead of generating a second dark picture; the product shape is generic (no logo drawn), but a real product silhouette can still look like the brand: keep the AI-illustration line in the footer.

## 11. Must not

- No emoji; no full-colour gradients; no glass or soft shadows on panels; no second spot colour; no red under 4.5:1 as small text.
- No franchise character, logo or copied panel drawn (the drawings are generic; names appear only as text).
- No counter held mid-count (build digits as slams); no text under 30 px except the one footer line.
- No line masks or typing effects on text (the frame check cannot see a half-revealed word).
- No impact frame within 0.5 s after a scene transition (two flashes in a row read as a glitch).
- No sad, enforcement or accident story (tier 2).
- No number a source does not state; a derived number says how (none were derived in this build).

## 12. Traps seen in real builds (this build, 2026-11-13; measured)

1. **The frame-check tool passed everything.** `frame_check.py` reported BLANK 0 / TOPHEAVY 0 on the first silent render, but the first contact sheet showed a footer line drawn through panel bottoms, a caption pill squeezed to about 180 px wide, clipped label detail lines and a black impact frame with invisible lines. Fix: read the snapshots and a 15 fps sheet around a transition; treat the script as a floor.
2. **Impact frame invisible.** The black `#imp` frame at 3.0 s showed only black: the speed lines I reused were ink on ink. Fix: a separate paper-coloured line set inside `#imp` (190 lines, r_in 200), visible 0.07 s.
3. **Caption pill half-width.** `left:50%` plus `translateX(-50%)` made the pill shrink-to-fit inside a 540 px containing block, so every caption wrapped to 2 lines (about 110 px tall, top at y 1334, touching the footer). Fix: `width:max-content; max-width:1000px`; one line = 91 px, top at 1389.
4. **Footer collision after the camera push.** Panels end at y 1290; at scale 1.05 about (540,740) the edge reaches about 1317, so a footer at 1298 sat on the borders. Fix: footer at 1336, paper background, `width:max-content`.
5. **Label text cut by a diagonal corner.** A 122 px label with `bottom:-6px` inside a panel whose bottom-left corner was cut ([0,.94]) lost its second line. Fix: straight bottoms on panels that hold labels, label height 134 px, name at top 2 px, detail at top 60 px.
6. **inspect: `clipped_text` on labels that start hidden.** Labels slid in from below the panel were reported as clipped text at t = 16.35 s (2 errors). Fix: names visible from the start; only the detail line fades in (`opacity`), then 0 errors.
7. **inspect: 689 `container_overflow` warnings** from the 70-170 speed-line polygons that run beyond the page. Fix: `data-layout-allow-overflow` on every `.abs` wrapper and on `#spd #imp #bar`; `data-layout-allow-occlusion` and `-overlap` on the two numerals that sit over art. Result: "0 layout issues across 9 samples".
8. **lint error `gsap_css_transform_conflict`** on `#bar` (CSS `skewX` + GSAP `x`). Fix: no CSS transform; `skewX` set in GSAP (`fromTo` with `skewX:-18` both ends). Final lint: 0 errors, 1 warning (`composition_file_too_large`, 309 lines, expected).
9. **File size.** Silent render 109.4 MB; the provided `mux` (crf 20) gave 83.4 MB because speed lines and screentone are high-frequency detail. Fix: ffmpeg `-crf 31 -preset slow -maxrate 3500k` plus loudnorm: 13.8 MB, 58.9 s. Samples at crf 28: 2.7 MB and 2.0 MB.
10. **Price too wide.** "$79.99" at 200 px with the 7 px stroke touched the image strip (610 px box). Fix: 176 px (and "$69.99" the same, so the two prices match); "$19.99" 150 px.
11. **Impact right after a transition.** An impact at the first anchor of S3 (0.2 s after the slash) looked like a glitch. Removed; impacts only on S1 ("Chainsaw"), S2 ("bốn"), S4 (second price), with shakes of 7-10 px.
12. **Textures could not be baked to PNG** (the sandbox refused ad-hoc python and node scripts). Substitute: seeded SVG built in the page at load (data-URI tone lattices, inline speed lines), which the renderer handled with 0 console errors and a 39-41 s render for 1766 frames. Baked PNGs remain the profile's rule if scripts are allowed.
13. **Red on paper is 4.19:1**, under 4.5. Used only for >= 100 px text with an outline; small red text uses `#c40f24` (5.55:1).
14. **Voice length.** 7 scenes, 255 whitespace tokens, `--gap 0.35`: 58.85 s total (target was 45-58 s for the voice, video limit 60 s). Numbers spoken in words ("sáu mươi chín đô la chín mươi chín") cost about 12 words per price; with three prices the line count is higher than the 190-225 word guide. Scene lengths 5.07-11.71 s; S3 (11.71 s) needed four internal anchors to avoid a 8 s hold.
15. **Freshness.** 12 search queries found no anime x sneaker/streetwear announcement from the last 48 h (the newest results were Tamagotchi x PUMA, 13 Nov, which is not anime, and Pokemon x adidas, September). The chosen story was announced 29 Sep 2026; its newest opened page is dated 27 Oct 2026 (17 days) and its US release date, 11 Nov 2026, is 2 days old. Stated in the manifest.
16. **Sandbox.** Compound shell commands (`&&`, `;`) and ad-hoc scripts needed approval and were refused; one command per call, files written with the editor tool, `cp` per file.

## Samples (ranks 2 and 3)

`samples/sample-t123.mp4` and `sample-t163.mp4`: 10.0 s, 1080 x 1920, silent. Same recipe, generic copy, "Minh hoạ" tag on the art, no real company, price or number: hero panel + red-outlined slab (slams at 0.5 s), impact frame with shake at 1.3 s, bubble at 1.9 s, two bottom panels slice in from opposite sides at 3.2 s and 3.4 s, then an 8 s hold with drift and a 1.00 -> 1.05 push. Lowest content edge y 1290; frame check: BLANK 0.
