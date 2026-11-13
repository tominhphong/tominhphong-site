# Style: glass-keynote (9:16 Vietnamese news edition, detail round 1)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build: product and feature news where the story IS a set of things a person can see on a screen: OS and app updates, feature drops with "who gets it / when", device lists, spec and pricing cards, release calendars. 3 to 6 beats, each beat one glass card, 2 to 8 small facts, no sad or urgent tone. Not for hard-news with a ruling or a victim, one-number economic data, warm human stories, long explainers or hype. Use it when the work is for another purpose, channel or client, so the search does not start from zero. Tier 2 never widens tier 1.

**Reading order.** Sections 1-11 are the design as built. Section 12 lists the traps seen in the build, with measured numbers; where 12 contradicts 1-11, section 12 wins.

**Clips and screenshots are optional.** This build used no clip and no screenshot: one agy image as a backdrop, everything else is CSS cards. Never fake or invent media or a UI that looks like a real product screen: a mock card must carry the chip "Minh hoạ".

**Example videos show the recipe, not the niche.** The build that wrote this document is a Google Pixel Drop story; copy how it is built.

**Status.** Written 2026-11-13 from one full build (`final.mp4`, 55.4 s, 6 scenes) and two 10 s samples. Profile: `styles/profiles/glass-keynote.yaml` (energy 3). The old landscape reference `style-glass-keynote.md` (1920x1080, 124 BPM, music) is the parent; this file adapts it to 1080x1920, voice only, no music.

Look: dark indigo space, a baked glass-bubble image behind everything, three slow colour orbs, a dot grid, frosted glass cards, gradient display words with an italic serif accent. Calm, premium, keynote.

## 1. Tokens

```css
--bg:#070817; --ink:#f5f3ff; --mute:#aeacd6; --dim:#8f8dbb; --lilac:#c4b5fd; --violet:#8b5cf6; --pink:#f0abfc; --sky:#60a5fa;
--stroke:rgba(196,181,253,.26); --grad:linear-gradient(100deg,#f0abfc 0%,#a78bfa 45%,#60a5fa 100%);
card: linear-gradient(180deg, rgba(38,33,92,.94), rgba(22,19,58,.94)), 1.5px --stroke border, radius 24,
      shadow 0 30px 60px rgba(2,2,12,.55) + inset 0 1.5px 0 rgba(255,255,255,.14)
```

Contrast, WCAG formula, measured in this build (card top #26215c, card bottom #16133a, page #070817):

| Token | on page | on card top | on card bottom | Use |
|---|---|---|---|---|
| `--ink` #f5f3ff | 18.13 | 13.16 | 16.11 | headlines, card titles |
| `--mute` #aeacd6 | 9.16 | 6.65 | 8.14 | sub-lines, footer, unread caption word |
| `--dim` #8f8dbb | 6.34 | 4.60 | 5.63 | only on page or card bottom; NOT used as text in this build |
| `--lilac` #c4b5fd | 10.77 | 7.82 | 9.57 | kicker |
| `--pink` #f0abfc | 11.30 | 8.21 | 10.04 | caret, gradient start |
| `--sky` #60a5fa | 7.82 | 5.68 | 6.95 | gradient end |
| `#a78bfa` (gradient middle) | 7.31 | 5.31 | 6.49 | the weakest part of gradient text |
| `--violet` #8b5cf6 | 4.70 | 3.41 | 4.17 | marks and bars only, never text |
| current caption word #e9d5ff | 14.61 | 10.61 | 12.98 | caption |

Other measured pairs: dark ink #0b0b22 on the gradient badge 7.11 / 10.99 / 7.61 (start, middle, end); unread caption #aeacd6 on the pill (#0f0d22 effective) 8.78; chip sky text #dbeafe on #1c3a6e 9.16; chip amber #fde68a on #3b2a06 11.10.

Rules: the gradient only fills display words (`em`, `.slam`) and the badge; state colours (green, amber, sky) only on chips, always with a coloured border and light text; no pure black, the end of the video is a full composition, never a fade to black.

## 2. Fonts (local files; Plus Jakarta, Instrument Serif, JetBrains Mono, Be Vietnam Pro are not installed)

| Role | Profile asks | Used here | Vietnamese check (36 letters ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ, glyph test with PIL against the .notdef glyph) |
|---|---|---|---|
| Headline, titles, captions | Plus Jakarta 800 | `SegUIVar.ttf`, weight 700 (axis 300-700; 800 does not exist) | 36 of 36 |
| Kickers, chips, timeline words | JetBrains Mono | `CascadiaMono.ttf` 600 | 36 of 36 |
| Accent word inside a headline | Instrument Serif Italic | `cambriai.ttf` (Cambria Italic, 400 only), gradient fill | 36 of 36 |
| Never | | `segoepr.ttf` | **1 of 36**: do not use for any text |

Declare each face with `font-display:block`. Headline line-height 1.1 and the `.ln` mask padding (12 px top, 10 px bottom, negative margins) keep tone marks (Ệ, ẫ, ỡ) inside the mask.

### Type scale (1080 x 1920, px; nothing under 30 except the single footer line)

| Token | Font | Size | Notes |
|---|---|---|---|
| `.kicker` | Cascadia 600 uppercase, +0.08em | 30 | `--lilac`, with a 46 px gradient number badge |
| `.h1` | Seg 700, -0.035em | 74 / 1.1 | max 2 lines; second line or key word in `em` (Cambria italic, gradient) |
| `.slam` | Seg 700, -0.05em | 190-210 | one number per scene: "8", "10", "X×" |
| card title | Seg 600-700 | 36-44 | |
| sub-line | Seg 500 | 32 | `--mute` |
| chip | Cascadia 600 | 30 in a 52 px pill | |
| tile text | Seg 600 | 36 | |
| source footer | Seg 500 | 26 | the one allowed line under 30 px; always starts "Nguồn:" |
| caption | Seg 700 | 44 / 1.25 | pill, see section 8 |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  top platform UI: empty
y 170  -216  kicker
y 236  -400  .h1 (2 lines of 74 px)
y 470  -1290 CARD ZONE (820 px)  x 72 - 1008 (936 px)
y 1304 -1330 source footer (26 px, one line)
y 1342 -1480 caption pill (bottom edge 1480; bottom: 440 px)
y 1480 -1920 bottom platform UI: empty
```

The card zone ends at 1288-1298 in every scene (measured: s1 1290, s2 1298, s3 1288, s4 1290, s5 1290, s6 1290), which satisfies "lowest content edge at y >= 1250". Cards are absolute children of the scene; inside a card everything is absolute from the card's own top-left with 36-44 px padding. Cards: 936 wide, gap 18-30. Two-column tiles: 458 x 112, gap 20 and 20 px between the columns (left 72, right 550).

## 4. Layers, back to front

`#bgimg` (agy glass-bubble image 768x1376, scaled to 1200x2040, opacity .55, drifts x 0->50, y 0->-70, scale 1->1.12 over the whole video, linear) -> `#scrim` (vertical gradient 78% / 35% / 55% / 85% bg colour: keeps headline contrast over the bubbles) -> `#o1 #o2 #o3` (three radial orbs 1000 px, violet / pink / blue, 26-40% alpha, `sine.inOut` drift over the whole video) -> `#grid` (baked 1080x1920 dot-grid PNG with a radial mask; no beat pulse, there is no music) -> `#vig` -> `#stage` (perspective 2200) with `.sc` scenes, each with a `.cam` wrapper for the hold motion -> `.foot` -> `#caps` -> `#fade` (bg colour, 1 -> 0 in the first 0.25 s only). No `#flash`, no `#wipe` band: they belong to kick beats and this build has no music.

Heavy-effect budget: 3 radial orbs + 1 image + the vignette; clip-path only in the iris scene (cleared to `none` 0.05 s after it ends). Rendered with no black frames.

## 5. Components

- **Kicker**: gradient badge with the scene number + mono label ("PIXEL DROP · 10/11/2026").
- **Card** (section 1), **tile** (112 px high card with a 18 px coloured dot and a name), **row card** (170 px: 112 px gradient icon square, title 36, sub-line 32).
- **Chip**: sky = illustration/info ("Minh hoạ"), amber = caution ("Một số thị trường"), green = available now, new = outlined. Chips pop `back.out(1.6)`.
- **Slam number**: 190-210 px gradient numeral inside a card, left, with a 40 px text block to its right; lands by scale 1.25 -> 1 in 0.4 s `expo.out` while a counter runs 0 -> N in 0.5 s `power3.out`.
- **Icon tiles**: 168 px squircles with different radii, gradient fills and one white glyph; the grid is 5 x 2 (936 wide, 24 gap).
- **Vertical timeline card**: 6 px gradient line (draws `scaleY` 0 -> 1 in 1.4 s), nodes of 46 px, mono 54 px label + 40 px line.
- **Hero card that shrinks** (see 12.2): 580 px tall, big gradient icon square 288 px + 50 px title; shrinks to a 240 px summary row when the first example arrives.
- **Bars**: 7 gradient columns, radius 16/6, grow `scaleY` 0 -> 1 with `back.out(1.3)`, stagger 0.07 from the end. Bars carry no numbers.

## 6. Motion language (energy 3)

Allowed eases: `power3.out`, `expo.out`, `back.out(1.3-1.6)`, `power3.inOut`, `sine.inOut` (holds), `none` (counters, camera). No bounce, no elastic, no shake, no flash.

| Verb | Recipe (measured values) |
|---|---|
| Card pop | opacity 0 -> 1, scale .9 -> 1, y 30 -> 0, 0.4-0.5 s `back.out(1.4)` |
| Headline | two masked lines rise y 110 -> 0, rotation 2 -> 0, 0.55 s `power3.out`, second line 0.08 s later |
| Kicker | rise y 20, 0.35 s |
| Typed prompt | a counter over the string, 1.5 s `none`, a caret that follows `offsetWidth`; finished 0.6 s before the card ends its entrance; no text is ever cut on a held frame |
| Counter | 0 -> N in 0.5 s `power3.out`, ends on the spoken word (all counts end <= 0.8 s) |
| Hold motion | `.cam` scale 1 -> 1.03 (even scenes, linear) or x 0 -> -14 at scale 1.012 (odd scenes); main cards float y 0 -> -5/-6 px, `sine.inOut`, 1.8 s, finite odd repeat count so they end at 0 |
| Out | opacity 0 + scale .95 in 0.14 s `power2.in`, ending at the next scene's start |
| In | starts 0.1 s BEFORE the voice scene start (overlap = the 0.14 s ghost allowance) |

Transitions, rotated so neighbours never match: s1 none, s2 `up` (y 110 -> 0, 0.25 s), s3 `zoom` (1.3 -> 1, 0.3 s `expo.out`), s4 `flip` (rotationY -70 -> 0, 0.3 s), s5 `iris` (circle 0 -> 80%, 0.55 s), s6 `up`. The profile asks for 0.5 s on `up`/`flip`; 0.25-0.3 s is what removed the empty frames (12.1).

## 7. Scene recipes (S = voice scene start; W() = estimated word onset)

The build is 6 scenes, 7.7 / 9.3 / 8.4 / 11.6 / 11.7 / 6.6 s. Each scene = kicker + 2-line headline + 1-4 glass cards. Any beat that arrives late in the scene is preceded by a hero card that is already on screen (12.2).

### R1 Hook with typed prompt (s1, 0-7.7 s)
Prompt card (250 px) pops at 0.15; typing 0.5-2.0 s; "Tạo" button presses (scale .94, 0.1 s yoyo) at 1.85; result card (520 px, ends y 1290) pops on `W(dựng) - 0.35`; its 7 bars grow on `W(widget) - 0.5`. Float on both cards.

### R2 Feature with examples (s2)
Hero card (580 px) pops at S-0.05, icon sways +-6 deg over 2.4 s; at `W(chi) - 0.7` the hero fades its big content (0.25 s) and shrinks to 240 px (0.55 s `power3.inOut`) while the small summary fades in; example rows (170 px) pop on `W(chi)-0.3`, `W(đấu)-0.45`, `W(đồng)-0.4`.

### R3 Number + device grid (s3)
Card (224 px) pops at S-0.05 with its text; the "8" slam lands on `W(tám)-0.4`; tiles pop per column on the first / second "bốn", 0.16 s apart; the amber chip on `W(số)-0.2`.

### R4 Number + icon grid (s4)
The 10 icon tiles pop at S-0.05 + 0.07 s each; the "10" card lands on `W(mười)-0.35`; the "Pixel 6a trở lên" card on `W(sáu)-0.5`. Tiles float in a wave from S+3.

### R5 Rollout timeline (s5)
820 px card from S-0.05 with the line drawing; node 1 at S+0.35, node 2 on `W(tuần)-0.3`, node 3 on `W(đồng)-0.3`. The card is full height from the start so the lowest edge never drops below 1290.

### R6 Recap (s6, last, soft)
Two cards (380 + 410 px, y 470-850 and 880-1290) pop at S-0.05 and S+0.2; the border of each lights (pink, then sky, 0.3 s yoyo) on the word of its topic. The last 1.5 s is the full composition, no fade.

## 8. Captions (Vietnamese karaoke)

Pill: `rgba(10,8,30,.78)`, 1.5 px border `rgba(196,181,253,.2)`, radius 20, padding 14 x 30, Seg 700 44 px / 1.25, centred, width 888, bottom edge y 1480. Word states: unread `#aeacd6` (solid, 8.78:1), current `#e9d5ff`, read `#ffffff`. Chunks <= 5 words or 26 characters, split at punctuation after >= 3 words, never across a scene end; chunk end = min(last word end + 0.15, next chunk start - 0.04); the first chunk starts at 0.25. 50 chunks for 229 words. One line almost always; two lines would reach y 1342 and still clear the footer (ends 1330). Caption text = spoken text (numbers in words).

## 9. Sound

Voice only in this build (VieNeu "Hải Đăng", 229 words, 55.38 s = 4.13 words/s). Final mix by `motion_tools.py mux`: -15.7 LUFS, peak -4.3 dBFS. Profile asks for music ~124 BPM and soft whooshes; not available here, so beat reactions (orb pulse, wipe band, flash) are dropped, not faked. With music available: music 4-6 dB under speech, whoosh on cuts, pop on chips.

## 10. Images (agy)

One image: "Abstract soft frosted glass sphere cluster floating in dark indigo space, violet pink and blue glows, premium keynote look, no text, no logos, no people" -> 768 x 1376 JPG in 73 s. It works as a full-frame backdrop at 55% opacity under a scrim; the focal bubbles sit around x 300-700, y 700-1400, i.e. behind the lower cards, so it never competes with text. Re-use the same file with a drift; do not ask agy for a UI, a phone screen, a chart or a skyline.

## 11. Must not

- No emoji; no hard stepped motion; no halftone or comic textures; no shake, flash or elastic.
- No gradient on body text; gradient only on display words, numerals and badges.
- No text under 30 px except the one source footer line (26 px).
- No dimmed or semi-transparent state on a held frame (nothing under 90% opacity for more than 0.2 s): unread caption words are a solid colour, not 50% white; there is no "dim the other cards" state.
- No mock of a real product screen without the chip "Minh hoạ"; mock bars carry no numbers.
- No number on screen that no opened page states; derived numbers say how (none were needed here).
- No call to like, share or subscribe; no advice, no prediction.
- No second transition kind shared by two neighbouring scenes.
- Nothing below y 1330 except the caption pill; no card edge under y 1298.

## 12. Traps seen in real builds (this build, 2026-11-13, measured)

1. **Empty gap at every scene boundary.** First version: outgoing fade 0.14 s, then the incoming scene started at S with a 0.4-0.5 s fade and its cards popping at S+0.15-0.2. Measured in `final.mp4` (ink % of the body zone): 15.2 % at 7.60 s, 3.0 % at 7.67, then 0.2-0.3 % from 7.73 to at least 7.77 s; same shape at 17.0 and 37.0. `frame_check.py` flagged BLANK at 7.5, 17.0, 37.0. Fix: the incoming scene starts 0.1 s before S (the overlap is the allowed 0.14 s ghost), transitions shortened to 0.25-0.3 s, kicker at S-0.08, headline at S-0.08, first card at S-0.05 with a 0.4 s pop. After: BLANK frames 0, TOPHEAVY 0, and frames at 7.70 / 17.1 / 37.1 show the new headline and card.
2. **A late first example leaves a scene bare.** In s2 the first example is spoken 3.6 s after the scene starts, so only a 240 px card was on screen (lowest edge y 710). Fix: a 580 px hero card (big icon + title, lowest edge 1050) that shrinks to 240 px at `W(chi) - 0.7`. Do the same whenever the first spoken fact comes later than 1.5 s into the scene.
3. **Numeral overflow.** `inspect` reported `text_box_overflow #n8` : a 210 px numeral (line box 285 px) in a 200 px card, overflow 43 px. Fix: card 224 px, numeral `line-height 1.05`, top 6 px. 0 layout issues after.
4. **50% white unread words break the opacity rule.** The reference uses unread = 50% white; on a held frame that is under 90% opacity. Replaced by solid `#aeacd6` (8.78:1).
5. **No CDN.** The skill template loads GSAP from jsdelivr; the render must not depend on the network. A local `gsap.min.js` (3.15.0) in `assets/js/` rendered the same.
6. **Lint warning `overlapping_gsap_tweens` on "dwell/hold" (n between 0 and 0.5 s)**: two counters share the property name `n` on different objects (the "8" and the "10"). Harmless, accepted; every other lint result was clean (0 errors).
7. **Fonts.** Segoe Print has 1 of the 36 test letters: never use. The profile's 800 weight does not exist in `SegUIVar` (axis max 700); the serif accent is Cambria Italic at 400, so keep it >= 74 px or it looks thin against the 700 sans.
8. **Voice length.** 229 words gave 55.38 s (4.13 words/s), inside 45-58 s on the first run; the video is 55.4 s. Unknown English words listed for a native listener: Custom, Drop, Google, Hai, Icon, Pixel, Watch, Widget (no respelling was applied; "Hai" is Vietnamese, a false listing).
9. **Size.** Silent render 21.9 MB; after `mux` the file is 17.1 MB (under the 25 MB limit). Render time 34-35 s for 55.4 s at default quality.
10. **Frame-check heuristic.** `frame_check.py` measures "ink" against the median colour of the frame; a scene full of big opaque cards lowers it. Open every flagged frame and look, and measure the boundary frame by frame (30 fps) as in trap 1.
11. **Estimated word times.** Visuals anchored to `W()` can drift; every anchor was placed 0.2-0.7 s early for that reason and the held state, not the entrance, carries the reading.

## 13. Samples (10 s, silent, generic content, label "Minh hoạ")

`samples/t032` (spec card: "X×" slam, 4 spec bars that fill one by one at 1.6 + 1.1 s steps) and `samples/t025` (release calendar: 4 week tiles, a gradient sweep, 3 feature rows with chips "Có ngay" / "Tuần 2" / "Tuần 3"). Both: 0 lint errors, 0 layout issues, BLANK frame only at 0.0 s (the entrance), final composition from 6.9 s.
