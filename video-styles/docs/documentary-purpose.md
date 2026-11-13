# Style: documentary-purpose (9:16 Vietnamese news edition, field-note documentary)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in the first build).** Calm, evidence-led "restoration and purpose" stories with a person or an organisation behind them and 3 to 6 sourced numbers that each take one line on a paper note: conservation and land restoration, reforestation, a founder or legacy story, a community or housing project, a nonprofit's results. Not for breaking news with one hard headline number, enforcement, crashes, product specs or hype. Tier 2 never widens tier 1.

**Reading order.** One document, written from one real build (section 13 holds the traps with measured numbers). Where section 13 and an earlier section disagree, section 13 wins.

**Clips are optional.** This build used four AI stills (agy) with slow push and seeded drift; no footage. If real footage exists, the profile prefers it; never fake it.

**Example videos show the recipe, not the niche.** The tested video is about a Texas ranch restoration (`selah-bamberger-rung-bach-xu`, 54.2 s); copy how it is built, not what it is about.

**Status.** Written 2026-11-13 from one full build plus two 10 s samples. No owner has reviewed it. Marks: **MEASURED** = a command or the renderer showed it. **HAND** = computed by hand with the WCAG formula (no script runner was available). **ASSUMED** = invented here. **SUBST** = a profile font is not installed. **DEVIATION** = knowingly differs from the profile.

Profile: `skill/references/styles/profiles/documentary-purpose.yaml` (energy 2, mixed mode). Format 1080 x 1920, 30 fps, VieNeu voice, no music, estimated-word karaoke captions.
DEVIATION 1: the profile says handheld drift "3-6 px"; built as seeded offsets of up to +-4.5 px and +-0.3 deg (measured by the code, not by eye).
DEVIATION 2: profile cross-dissolve is 1.0-1.2 s; photos dissolve in 0.6 s and all text swaps in 0.15 s, because the acceptance rule "no ghost of the outgoing scene longer than 0.15 s" beats the profile.
DEVIATION 3: profile counters take 2 s; here 0.5-0.8 s ("counts finish within 0.8 s").
DEVIATION 4: the profile asks for a topographic contour PNG on map scenes; no scene had map data, so none was built (never decorate with a fake map).

## 1. Tokens

```css
:root{
  --bg:#1f1d1a;        /* profile bg; page and letterbox colour */
  --ink:#f3ede2;       /* profile ink: 14.4:1 on --bg (HAND) */
  --accent:#d9632b;    /* profile accent: 4.6:1 on --bg, 3.0:1 on paper => FILL ONLY on paper */
  --accent-dk:#a8461a; /* ASSUMED: rust TEXT on paper, 4.85:1 (HAND) */
  --moss:#5a6b3c;      /* profile moss: 4.8:1 on paper (HAND): bar fill and text ok */
  --slate:#43505a;     /* profile slate: 6.8:1 on paper (HAND): labels */
  --sand:#c9b38c;      /* profile sand: 8.25:1 on --bg (HAND): footer line */
  --paper:#efe8da;     /* profile paper: dark ink #1f1d1a on it 13.8:1 (HAND) */
  --unread:#b5ae9f;    /* ASSUMED: caption unread word, SOLID colour (not opacity) */
}
```
Other pairs (HAND): bar fill `#b9501d` on paper 4.07:1 (graphics need 3:1); `#f3ede2` on moss 5.3.
Rules: text on paper only from `#1f1d1a`, `--accent-dk`, `--moss`, `--slate`. `--accent` is never text on paper (3.0 fails). Text on photo only `--ink` or `--sand`, always over a baked scrim. Rust marks the key number and the hand-drawn circle, nothing else. No pure white, no neon, no gradient on text.
Renderer check (MEASURED, `hyperframes validate`): first pass 10 contrast warnings (sand kicker 1.01:1 on bright sky, headline 1.33:1 at t=5.4 s); after a stronger top scrim and an `--ink` kicker: "35 text elements pass WCAG AA".

## 2. Fonts (SUBST: the profile's Fraunces, Space Mono and Be Vietnam Pro are not installed)

| File | Role | Replaces |
|---|---|---|
| `cambriai.ttf` (italic only) | headlines 96 px, big numerals 112-250 px | Fraunces 600 |
| `CascadiaMono.ttf` | field-note text 31-42 px, labels 30 px, footer 26 px | Space Mono |
| `SegUIVar.ttf` | captions, 600 weight, 46 px | Be Vietnam Pro 500 |
| `segoepr.ttf` | NOT used: lacks Vietnamese letters (92 missing in the sibling owner doc) | none |

Diacritics check (MEASURED by eye on snapshots, because no font-table script could be run): every headline and note in the build rendered with correct marks in all three fonts: "Mảnh đất tệ nhất vùng đồi Texas", "Không một giọt nước", "Mạch nước", "Chim muông trở về", "Bảo vệ khu đất", "Mảnh đất của ông vẫn còn đó", "chặt bớt", "phần lớn phủ cây bách xù", "không tìm thấy một giọt nước", "những năm đầu", and the caption line "Ba nghìn mẫu Anh". No fallback glyph appeared. Italic Cambria sets the headline slightly wider than Fraunces would: 96 px fits 24 characters per 936 px line.

### Type scale (px, 1080 x 1920)
| Role | Font | Size |
|---|---|---|
| Kicker (top-left, whole video) | Cascadia | 30 |
| Headline (max 2 lines) | CambriaI | 96 / line 1.04 |
| Hero numeral on a note | CambriaI | 250 (single fact) / 112-150 (rows) / 200 (two columns) |
| Note body | Cascadia 500 | 36-42 |
| Note label | Cascadia 500 | 30, +0.05em |
| Note sub line | Cascadia | 31 |
| Caption | SegUI 600 | 46 / 1.3 |
| Footer (the one small line) | Cascadia | 26 |
Nothing else is below 30 px.

## 3. Safe areas and grid (1080 x 1920)

- Side margin 72, content width 936.
- y 0-110 empty (status zone). Kicker at y 124. Headline block y 196-400 (1-2 lines).
- Photo window y 400-740 stays clear: the picture carries colour.
- Note zone: top 620-860, always **bottom-aligned to y 1340** (heights 480, 520, 600, 720). Lowest content edge at every hold is therefore 1340 (>= 1250).
- Caption block: centred, bottom edge y 1580 (CSS `bottom: 340px`), at most 2 lines (y ~1450-1580).
- Footer line y 1664. Below 1690 empty. Right rail x 960-1080 below y 1100: no text.

## 4. Layers, back to front

1. `#root` `--bg`.
2. `#cam` (z1): the photo stack; seeded handheld drift lives on this wrapper. Each `.ph` is 1140 x 1980 (inset -30) so drift never shows an edge.
3. `#scrim` (z2): baked RGBA PNG: top 74% black fading to 0 by y 620, bottom 92% from y 1000 to 1650 (ffmpeg `geq`).
4. `#grain` (z3): 540 x 540 baked noise tile, `mix-blend-mode: overlay`, opacity .16, background-position jumped every 0.2 s from a seeded rng.
5. `.kick`, scene sections `.sc` (z4-12): headline + one paper note each.
6. `#foot`, `#caps` (z50), `#fade` (z60, black; used only for the cut to black).

## 5. Components

- **Field-note card** `.card`: baked RGBA PNG (936 x 480/600/720, paper `#efe8da`, fibre noise 9, torn edge made by a sine-wobbled threshold plus per-pixel jitter, blurred 0.9), `drop-shadow(0 14px 20px rgba(0,0,0,.45))`, rotated -0.5 or +0.5 deg alternately, padding 46/58/40. Stretched with `background-size: 936px 100%`; a 520 px card on the 600 px PNG showed no visible distortion.
- **Label strip**: "GHI CHÚ HIỆN TRƯỜNG · 0n", mono 30 px, slate.
- **Hero numeral**: CambriaI in `--accent-dk`; counters use a GSAP proxy object and `onUpdate` writing `textContent` (see trap 4: never `tl.set({textContent})`).
- **Typed line**: `typeIn` clip reveal at 0.04 s per character; the clip is removed 0.01 s after the end.
- **Hand-drawn circle / underline**: rough SVG path with `pathLength=1`, stroke 7 px `--accent-dk`, drawn in 0.7-0.9 s. Always sits at least 30 px clear of other text (trap 7).
- **Bar** (chart): 56 px high, `transform-origin: 0 50%`, `scaleX` 0 to 1, starts at zero, one shared scale (221 -> 760 px, "dưới 50" -> 172 px), label above and a mono line "thang chung, bắt đầu từ 0".
- **Footer**: "Nguồn: <domain> · ảnh minh hoạ" for stills made by AI.
- **Badge** (samples only): "Minh hoạ" in a 3 px rust frame, rotated -3 deg, top-right of the note.

## 6. Motion language

- Energy 2: no bounce, no overshoot, no flash, no shake, no whoosh.
- Photo push 1.00 -> 1.07 over the scene (or 1.06 -> 1.00 as a pull-back on one scene); close-crop scenes start at 1.22-1.25. Alternate push and pull, and different `transform-origin`, between neighbours.
- Handheld drift (seeded, `sine.inOut`, 1.4-2.2 s per leg): +-4.5 px x and y, +-0.3 deg.
- Entrances: note rises 30 px in 0.4 s `power2.out`; rows 14 px in 0.3-0.4 s; headline rises 14 px in 0.4 s. Exits: 0.15 s `power1.in` fade.
- Counters: `power3.out`, 0.5-0.8 s, started 0.5 s before the spoken number; last value is exact.
- Cut to black before the hardest fact (here the death date): `#fade` 0 -> 1 in 0.12 s at S-0.2, 1 -> 0 in 0.45 s at S+0.08. Measured: the only BLANK frame of the build (46.5 s), 0.2 s.
- Word times are ESTIMATED (character share of each scene's speech); anchors use `W(sid, fragment)` and reveal 0.3-0.6 s early.

## 7. Scene recipes (S = scene start from `voice/timeline.json`)

All scenes: one headline (2 lines max) + one note, aligned to y 1340. A scene shows content within 0.5 s: the note's first row is on screen at S+0.05-0.3.

**R1 Hook (S 0, 5.3 s)** - photo "before" push; headline fully visible at frame 0; note 520 px with the year 1969 at 250 px, a rust circle drawn at 1.0 s, two typed lines.
**R2 Three facts, one note (5.3-12.1 s)** - note 600 px: three rows (3.000 mẫu Anh / 0 con suối còn chảy / 7 giếng khoan sâu). Row A at S, row B on "suối", row C on "bảy". Counts 0.5-0.6 s.
**R3 Person and verbs (12.1-18.0 s)** - name as headline; note 480 px with two italic verbs and mono objects typed; rust underline drawn on "cỏ bản địa".
**R4 Paired numbers (18.0-25.4 s)** - first typed line repeats the spoken opening so the note is never empty; then two columns, 7 and 11, counted on their words.
**R5 Bars (25.4-31.5 s)** - note 600 px; top bar 221 counted and grown in 0.75 s; second bar "dưới 50" on its word; shared scale line.
**R6 Date and why (31.5-38.7 s)** - 2002 at 190 px visible at S; two typed lines on "lập"; a sub block for who and why.
**R7 Ledger (38.7-46.5 s)** - note 720 px: 5.500 counted from 3.000 (0.8 s), then two rows on their words.
**R8 Close (46.5-54.2 s)** - cut to black, then sky photo; date, age counted; last 1.5 s is a full composition, no fade out.
Samples (10 s, silent): the same note recipe over a generic still: counter, typed lines, rust circle, second row at 3.6 s, "Minh hoạ" badge.

## 8. Captions (Vietnamese karaoke)

- No pill. SegUI 600 46 px, `text-shadow: 0 2px 12px rgba(0,0,0,.8), 0 0 3px rgba(0,0,0,.6)`, centred, bottom edge y 1580, 936 px wide.
- Unread word `--unread` `#b5ae9f` (solid, so nothing is below 90% opacity), current and read words `--ink`. Highlight by `tl.set` at the estimated word onset.
- Chunks: split after `, .` once 3 words are in, hard cap 6 words, a 1-word orphan joins the previous chunk. The first chunk of a scene starts at S+0.1. Fade 0.1 s in, 0.08 s out.
- The caption is the spoken text (numbers in words); numerals live on the notes only.

## 9. Sound

Voice only in this build (VieNeu "Hải Đăng", 51.0 s of speech in 54.2 s). The profile calls for acoustic ambience and natural SFX; none was available, so none is faked. Final loudness MEASURED: -15.4 LUFS, peak -4.3 dBFS.

## 10. Images (agy)

- Four stills in the film grade of the profile, 768 x 1376: a dry juniper hillside, a golden restored grassland, a spring over limestone, a golden-hour grass horizon. All four read as photographs and none contained text or people.
- Prompt recipe that worked: "Documentary photograph, <subject>, <light>, muted warm earthy film grade, 35mm grain, no people, no buildings". "Before" and "after" were two prompts of one place: they work as a pair for restoration stories.
- One image used twice (different crop and push) is fine; an image is atmosphere, never proof. The footer says "ảnh minh hoạ" for every AI still.
- Never let agy draw maps, charts, signs or text.

## 11. Must not

- No emoji, no gloss or glass, no neon, no whoosh, no flash, no shake, no fast cut.
- No number that no opened page states; a derived number says its derivation on screen.
- No hype copy, no prediction, no call to like or share.
- No `--accent` text on paper; no text under 30 px except the footer.
- No empty note: a note's first row is on screen within 0.5 s of its scene.
- No hand-drawn circle across other text.
- No fake map, fake footage, real person or logo.
- Do not name a US organisation by acronym in the voice (`org-names-vi.json`); this story named none.

## 12. Fixes after the build (these override sections above)

1. Kicker colour `--ink`, not `--sand` (validate: 1.01:1 on bright sky).
2. Top scrim 0.45 -> 0.74 strength and 330 -> 620 px reach.
3. Note rise 0.55 -> 0.4 s so the translucent entrance is short.
4. Notes sized to content: 520 px for one big numeral plus two lines, not 480.

## 13. Traps seen in real builds (this build, measured)

1. **`textContent` in a GSAP tween eats the thousands dot.** `tl.set(el, {textContent: "3.000"})` made GSAP parse the string and show "3", "5.5", "2" (snapshot at 8.0 s). Fix: set text only from `onUpdate` of a proxy tween, never through GSAP's `textContent` plugin path.
2. **Monospace line wider than its column.** "Texas (Hill Country)" at 36 px needs about 432 px; the right column had 390, so the text ran past the card edge. Fix: restack the note (numeral above, text below at 40 px) and drop the parenthesis.
3. **Notes empty at the start of a scene.** At S+0.2 s in scenes 3 and 4 the note held only its label until the spoken word arrived (1.7 and 3.0 s later). Fix: first typed row at S+0.05-0.3 (a verb row; the opening spoken words typed), later rows on their words.
4. **Silent render is huge.** The grain overlay changes every 0.2 s: `hyperframes render` gave 102.6 MB for 54.2 s; the first mux (crf 20) 56.1 MB, over the 25 MB limit. Fix: re-encode with `-crf 28 -preset slow -maxrate 3500k -bufsize 7000k`: final.mp4 8.6 MB, no visible loss.
5. **Hand-drawn circle struck through text.** In the first sample render the 190 px high circle bottom (y 286 in the card) crossed the typed lines (y 290). Fix: circle 170 px high, text `margin-top: 44px`. Same trap in t151 where the circle covered the unit; width cut to 330 px so it holds the numeral only.
6. **Dissolve vs ghost.** A 1.0-1.2 s profile dissolve would leave the outgoing note visible for 1 s. Photos dissolve in 0.6 s; each scene's text layer fades in 0.15 s and the next one rises 0.1 s after: a frame at exactly S (5.3 s) still showed the outgoing headline "đồi Texas" at about 10% opacity under the new headline, so the headline exit should start 0.05 s earlier than the 0.15 s used here. Residual ghost: one frame.
7. **Estimated word times.** Anchors drift; every reveal runs 0.3-0.6 s early and rows are laid out so an early reveal is harmless (checked on the s2 frames: row C visible before "bảy" ends).
8. **Contrast tool vs scrim.** The validator reads the photo under the text, not the scrim's effect only on average: a bright sky behind a 74% top scrim still scored 2.6:1 for a sand kicker. Ink colour and a 2-layer shadow got it to pass.
9. **Counter mid-count.** The first sheet at S+0.1 caught "2.534" and "114" mid-count. They finish within 0.6-0.8 s (rule 6) and were never held; the check is that frames at +1.0 s show the final value.
10. **Frame-check BLANK flag at 46.5 s** is the intended cut to black (0.2 s, one sample), not a defect. Judge it, do not "fix" it.
11. **Word budget.** 233 spoken words fit 51.0 s of speech (4.6 words/s with this voice); total 53.84 s with gaps. Brief range was 190-225; the video length was the real constraint, so the words stayed.
