# Style: organic-biomorphic (detail, round 1, first real build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Calm, human, product-or-programme stories with a gentle structure (a schedule, a few steps, who can use it, a slogan): wellness apps and breathing or sleep programmes, nature and conservation stories, reforestation, founder stories, brand stories. It held a 57 s news explainer with no data dashboard. Not for urgent, enforcement, financial-number, spec-sheet or sad stories (the style has no hard edge, no flash, no shake). Tier 2 never widens tier 1.

**Reading order.** Sections 1-12 are the design as built. Section 13 is the trap list from this build, with measured numbers; where 13 contradicts an earlier section, 13 wins.

**Deviations from the profile (organic-biomorphic.yaml), all kept on purpose:**
1. Fraunces, Outfit and Be Vietnam Pro are not installed. Headlines use `cambriai.ttf` (Cambria Italic, a soft serif, the only serif file), body and captions use `SegUIVar.ttf`.
2. Profile entrances are 0.8 s. Built: the move is 0.7 s `sine.out`, the fade is 0.3 s, so nothing sits below 90% opacity for long (acceptance rule 7).
3. Profile transitions list four kinds. Built: ONE language, `blob-morph` (a cover blob grows and recedes), because three kinds in one video read as noise.
4. Profile says avoid `hook`; news needs a hook in 3 s. The hook is a big number inside a blob ("5 phút mỗi sáng"), entering with the calmest verb.
5. Profile caption pill is Be Vietnam Pro 42 px; built SegUIVar 700 44 px.
6. A pastel photo-like background from agy is used under blobs (profile asks for baked soft grain and optional leaf shadow); grain is a baked PNG at 5%.

**Status.** Written 2026-11-13 from one 57.3 s build (Peloton Breathwrk programme, `final.mp4` 14.7 MB) and two 10 s samples. Not yet merged into the skill folder.

## 1. Tokens

```css
:root{
  --bg:#f4f1ea;       /* paper                         */
  --ink:#1f2a24;      /* 13.16:1 on bg                 */
  --mute:#4a5a50;     /* 6.49:1 on bg                  */
  --accent-dk:#1f6b4f;/* 5.69:1 on bg, 6.41 white-on   */
  --clay-dk:#8a4f2a;  /* 5.76:1 on bg (text variant)   */
  --accent:#2f8f6b;   /* FILL ONLY: 3.54:1 on bg       */
  --moss:#8fb996; --sky:#a9c8d8; --clay:#d9a47c; --blush:#e8b7b0;  /* FILLS ONLY */
  --deep:#16352b;     /* night variant bg; bg-on-deep 11.80:1 */
}
```
Measured with the WCAG formula (jq): ink on moss 6.75, on sky 8.44, on clay 6.75, on blush 8.36; clay on bg 1.95 (fails, fill only); accent-dk on moss 2.92 (fails: never put accent-dk text on a moss fill). Rules: text colours only from `--ink --mute --accent-dk --clay-dk` on light, `--bg` and `#cfe3d5` on `--deep`. `--accent`, `--moss`, `--sky`, `--clay`, `--blush` are fills. Blobs use 2-stop gradients of neighbouring hues (moss to sky, clay to blush, sky to moss, accent to moss). Never neon or pure black.

## 2. Fonts

| File | Missing glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 (inherited from the saas-bento and fluent-productivity owner docs, same file; this build could not run its own fontTools test because local scripts were denied by the sandbox) | everything read: cards, chips, captions (700), labels (600, uppercase, +0.14em) |
| `cambriai.ttf` | 0 (same note) | all headlines and the hero number, italic only, -0.02em |
| `CascadiaMono.ttf` | not used | not used in this style |
| `segoepr.ttf` | 92 missing (Ơ ơ Ư ư and dotted vowels) | never used |

Diacritics check done by eye on 16 snapshots and the 115-frame sheet: ẩ, ở, ỡ, ợ, ể, ỹ, ặ, ữ, đ, Đ all render in both fonts (headline "Lịch học rất gọn", "Bảy ngày để thức dậy với năng lượng", card "Đăng nhập bằng tài khoản Peloton sẵn có"). Cambria Italic has no bold: weight comes from size (88-136 px), not from weight.

## 3. Safe areas and grid (1080 x 1920)

- Side margin 72, content width 936. Kicker label at y 140 (30 px, uppercase). Headline top y 195-215.
- Body zone y 200-1340. Hero blob centre about y 760 (shape spans 360-1160 before any scale).
- Captions: pill centred, top 1400, max width 936, up to 2 lines. Footer source line: top 1640, one line, 30 px, on a 90% paper pill (otherwise it was unreadable over the clay and pink wave).
- Right rail and y > 1340: empty except captions and the footer.
- Radius: pebble cards `40px 72px 48px 80px` (asymmetric), caption pill `30px 46px 30px 46px`, chips 30-40. No strokes on blobs or cards; the only strokes are the tendril (9 px) and ripple rings (5 px).
- Acceptance 2 (lowest content edge >= 1250 at every hold), measured from layout coordinates of the last-entering element: S1 1325, S2 1310, S3 1365, S4 1327 (day labels), S5 1300 (blob), S6 1298. Frame check (frame_check.py) on final.mp4: BLANK runs >= 1 s none; TOPHEAVY 5 of 115 samples (all inside the first 1-2 s of a scene).

## 4. Layers, back to front

1. `#root` `--bg`.
2. `.bg` x3 (z 0): agy images (`wash.jpg` for s1/s3/s4, `dawn.jpg` for s2/s5, `forest.jpg` for the night scene), 0.8 / 0.6 / 1.0 opacity, drift `y 0 -> -40, scale 1 -> 1.04` over the whole video (0.3x parallax).
3. `#world` (z 5): camera wrapper, `scale 1 -> 1.02 -> 1` sine.inOut over 57 s.
4. Scene sections `.sc`: per scene one SVG (foreground pebbles `fg`, the main blob group `g`), then the HTML cards and text. Max 12 blobs on screen (built: at most 7).
5. `#xt` (z 20): the blob-morph cover path.
6. `#caps` (z 40), `#foot` (z 40), `#grain` (z 30, baked 540x960 PNG, 5%, multiply).

## 5. Components

- **Hero blob**: one of three pre-authored 4-cubic paths A, B, C (equal point counts), gradient fill; breathes `scale 1.00 -> 1.03` per 2.6 s (`sine.inOut`, finite repeats sized to the hold) and morphs A->B->C through the hold (`attr d`, sine.inOut, 3-4 s per leg). Scaled with an `XF()` transform attribute on the path, never on the group that breathes.
- **Pebble card** `.peb`: white 88%, radius asymmetric, shadow `0 18px 40px rgba(22,53,43,.12)`; deep variant (`--deep` bg, `--bg` text); clay and moss variants for emphasis. Text 38-58 px, SegUIVar 600-700.
- **Tendril**: SVG path, `stroke #1f6b4f` 9 px round caps, drawn with `strokeDashoffset` (1.6 s sine.inOut), with seed-pebble nodes that pop and swell to 0.26 on the spoken day.
- **Bars as pods**: pebble-topped columns (radius `50px 50px 34px 34px`), 100 px wide, 50 px per minute, `scaleY` from the base 0.8 s `sine.out`; the 5-minute bars sky-to-moss, the 10-minute bars blush-to-clay; a faint track behind each.
- **Merge**: two labelled blobs slide together on the spoken "mua lại" (x +-190, 1.1 s sine.inOut).
- **Caption pill**: see section 8.
- Icons: none; initials in a blob avatar ("MF") are the only person marker (no real faces).

## 6. Motion language

- Everything is `sine.out` / `sine.inOut` / `power1.*` (profile constraint). No back, elastic, expo, bounce, shake, flash, linear.
- Entrance verb: **rise** (y 28 -> 0, 0.7 s `sine.out`, opacity 0 -> 1 in 0.3 s). Staggers 0.1-0.15 s, hand-set per line, anchored on spoken words with a 0.15 s early lead and a floor of scene start + 0.05.
- Blob-morph transition: the cover path (fill = a tint of the next scene) goes from a 160 px circle to a 1700 px radius blob in 0.4 s (`power1.in`), the scenes swap while fully covered (b - 0.10), then it shrinks back in 0.4 s (`power1.out`) and is hidden at b + 0.31. Total cover time about 0.5 s per cut, five cuts.
- Holds are never frozen: blob breathing, blob morph, tendril, drifting fg pebbles (`y -70`, 3 per scene, in the margins only), camera breathing, background parallax.
- Counter: a single one (60 minutes, 0 -> 60 in 0.7 s `power1.out`, ends on the spoken number). Hero "5" is NOT counted: it rises already final.
- Word times are ESTIMATED by the voice step (no aligner here). Reveal 0.15 s early; show the headline of a scene at scene start + 0.1 whatever the word estimate says.

## 7. Safe handling of facts on screen

- Every number is in the script or derived on screen: "5x4 + 10x4: cộng từ lịch ở trên" under the 60-minute card.
- Footer names the two sources and their dates. English technique names and tier names are labels only (they are not spoken); each is the exact name on the source page.
- A fact with disagreeing sources is left out (the acquisition month differs between two pages; one other programme's month differs between two pages).

## 8. Captions (Vietnamese karaoke)

- Pill `rgba(244,241,234,.93)`, radius `30px 46px 30px 46px`, padding 18 x 34, centred at top 1400, max width 936, SegUIVar 700 44 px `--ink`. Current word `#1f6b4f` (5.69:1 on the pill), set with `tl.set` at the estimated onset and set back at the word end (no tween, so a late estimate never leaves a half colour).
- Chunks: split at `, . : ; ? !`, a segment longer than 6 words is cut evenly (ceil(n/6) chunks) so no orphan word. Fade 0.1 s in and out; the last chunk of the video stays.
- Words are shown as spoken (numbers in words), so spoken and on-screen numbers cannot differ.

## 9. Scene recipes (6 scenes; starts from `voice/timeline.json`; S = scene start)

**R1 Hook, number in a blob (s1, 0-9.5 s).** Blob A (moss to sky) grows 0.82 -> 1.0 in 1.0 s; "5" (Cambria italic 440 px) rises at 0.05, "phút mỗi sáng" (68 px) at 0.3; headline "Chỉ để thở." (128 px) on "chỉ"; three chips on "hướng", "bảy", "hai" (full-width card, then two half chips).

**R2 Title + person (s2).** Headline 3 lines at 122 px on S + 0.1 / 0.22 / 0.34; English gloss on a paper pill; person card (blob avatar + name + role); a deep card and a clay card ("4" at 176 px) on their spoken words; sky blob behind, breathing.

**R3 Schedule as pods (s3).** 8 tracks at S + 0.2; four 5-minute pods grow on "mở đầu ... năm phút", four 10-minute pods on "từ ngày thứ tư", value labels above; deep summary card with the single counter on "sáu mươi".

**R4 Steps on a vine (s4).** Three cards (day pill + technique name), the vine draws across y 1262 with seven seed nodes; two cards for the repeat and the combination; nodes swell on the spoken days.

**R5 Who can use it + merge (s5).** Three tier chips on "ba hạng", clay card "Không tính thêm phí", login card, coach card; Peloton and Breathwrk blobs merge on "mua lại".

**R6 Soft ending, night variant (s6).** `forest.jpg`, deep green; headline `--bg` 136 px on S + 0.1 / 0.3, a breathing blob with the last line, the two source chips; no fade to black, no call to action; the last 1.5 s are the full composition.

## 10. Images (agy)

- 3 images, 768x1376 jpg, 450-630 KB each: a light wash (huge blobs bleeding off the edges, leaf shadows), a dawn leaves gradient, a deep green night wash. Prompt contains the exact hexes, "no text, no letters, no numbers, no logos, no people, no strokes, generous empty centre". All three came back clean. The wash puts strong colour in the corners: keep headlines over the pale diagonal or on a card.
- agy never draws the hero blob, cards or lines: those are SVG/CSS so the morph paths stay equal-point.

## 11. Sound

No music in this showcase; voice only (VieNeu), loudnorm -14 LUFS target applied by the mux step, measured -15.4 LUFS, peak -4.3 dBFS. Profile intent for a real build: ambient or acoustic 70-92 BPM, water-drop and chime SFX at very low density, blobs breathe on downbeats only.

## 12. Must not

- Hard cuts, linear motion, elastic, bounce, shake, flash, neon, pure black, halftone or glitch.
- Live `filter: blur()` (blur is baked in the agy images), more than ~12 blobs, runtime-generated paths, morphs between paths with different point counts.
- `--accent`, `--moss`, `--sky`, `--clay` as text colour; accent-dk text on a moss fill.
- Text below 30 px; text below y 1340 except captions and the footer.
- Calls to like/share/subscribe, prediction, advice, claims the source lacks.

## 13. Traps seen in real builds (this build, 2026-11-13)

1. **Blobs sit in the caption band.** The first draft moved blob groups with `tl.set(y: 560)` on the same group that breathes; blobs landed at y 920-1720, under captions and footer. Fix: static `transform` attribute on the path (`XF(scale, dy)`), group only breathes. Blob scales used: 0.62-0.82.
2. **Long blank run at cuts.** First render: `frame_check.py` BLANK RUNS 9.0 s for 1.0 s and 37.0 s for 1.5 s. Cause: cover grew over 0.55 s and receded over 0.6 s (about 1.2 s of near-empty frames) and the next headline waited for a spoken word (10.3 s, 40.1 s). Fix: grow 0.4 s `power1.in`, recede 0.4 s `power1.out`, swap at b - 0.10, every headline at scene start + 0.1. Result: BLANK frames 9 -> 4 (single samples at 9.5, 19.0, 37.5, 48.0 = the cover itself), runs >= 1 s: none.
3. **Cover flagged by `inspect`.** `text_occluded` and `content_overlap` at t = 9.55 s were the cover over the next section. Mark `#xt`, `#cover` and the scene sections `data-layout-allow-occlusion data-layout-allow-overflow data-layout-allow-overlap`. Result: 0 layout issues across 9 samples.
4. **Orphan line in cards.** "Đăng nhập bằng tài khoản Peloton sẵn có" at 46 px wrapped leaving "có" alone; "Đưa huấn luyện viên..." wrapped too. Fix: 40 px and 38 px.
5. **Night scene text on a mid-green blob.** First version: ink text on `gDeep` at 92% overflowed the blob edge onto deep green (unreadable). Fix: text `--bg` at 88 px, blob opacity 0.5 and scale 0.82 so the text sits inside it.
6. **Footer unreadable over the wave.** 30 px mute text on the clay/pink diagonal. Fix: 90% paper pill behind it; hidden in the night scene (the source chips replace it).
7. **Source headline before the spoken word.** "Không tính thêm phí" as scene 5 headline appeared at 40.1 s, 2.5 s after the cut. Fix: headline "Ba hạng hội viên" at the cut, the fee card on the spoken "không".
8. **Python of our own is blocked in this sandbox** (only `motion_tools.py`, `frame_check.py`, ffmpeg, jq, npx hyperframes run). Contrast came from jq; the word timeline became `timing.js` written by hand from `jq` output.
9. **Lint warning `overlapping_gsap_tweens` on `#cover`** is the grow tween and the previous recede on the shared layer; it renders correctly (explicit `fromTo` values). Harmless.
10. **Estimated word times.** Reveals land within about 0.3 s of the true word; counters and the summary card carry a 0.2-0.25 s lead so the number is on screen when it is spoken.
11. **Pastel blobs are weak "ink" for the frame check** (moss, sky, clay differ from the paper by 70-105 on one channel only); content must carry dark text or deep cards to count as content. A scene with only a blob and a headline reads as blank to the check.

Numbers: video 57.32 s, 1080x1920, 30 fps, 14.7 MB; voice 56.82 s, 6 scenes (9.47 / 9.95 / 8.67 / 9.47 / 10.75 / 8.51 s), 221 spoken words; render 37 s; samples 10.0 s, 4.0 MB and 3.0 MB.
