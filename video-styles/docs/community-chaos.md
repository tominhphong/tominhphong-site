# Style: community-chaos (9:16 Vietnamese demo edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** Observed in this build (topic shape t050, "Esports final: bracket, teams and prize pool", Jev fit 0.64): loud, youthful, memetic stories that are about a crowd and a few events: gaming and esports finals, community launches, youth promos, live-event hype, fan reactions, bracket/winner reveals, a headline prize number with 2-4 supporting lines. Not for serious, sad or enforcement stories, dense numeric dashboards, specs, or anything needing premium restraint. Use it when the work is for another purpose, channel or client; it never widens tier 1.

**Status.** Written 2026-11-15 from ONE demo build: a 12.0 s silent 1080x1920 sample (`samples/sample-t050.mp4`). Voice-over, captions, word timing, music and SFX were NOT exercised (demo build): sections 9 and 10 repeat the profile and are untested. Every number below was measured or computed in this build; anything the profile does not give and the build did not test is marked **ASSUMED**.

**Reading order.** Sections 1-8 are the recipe. Section 12 is the must-not list. Section 13 holds the traps found in this build; where it disagrees with an earlier section, section 13 wins.

**Example video shows the visual recipe, not the niche.** All content in the sample is generic and labelled "Minh hoạ" (team names, scores and the 1.000.000 USD prize pool are invented).

Source of values: `styles/profiles/community-chaos.yaml` (energy 5, family brand-inspired). Character: a group call at 2 a.m. in a dark chat app: chat floods, tilted stickers with thick white outlines, speaking rings, meme-caption slabs, zoom punches.

## 1. Tokens

```css
--bg:#1c1d24;        /* page                                          */
--ink:#f1f1ee;       /* text                14.8:1 on bg              */
--mute:#9a9aa6;      /* labels, footer      6.0:1 on bg, 5.1:1 on surface */
--surface:#2a2b33;   /* tiles, HUD pill, prize rows                   */
--surface-hi:#32333d;/* tile border, score chip                       */
--accent:#7358ee;    /* headline card, lines, ring borders  3.5:1 on bg (graphics only) */
--voice:#2bb38a;     /* speaking rings and live dot ONLY              */
--pink:#f0508a;      /* stickers, avatars                             */
--yellow:#e8ec5a;    /* key word, champion card, prize number  13.3:1 on bg, 11.1:1 on surface */
--red:#e8533a;       /* one avatar only                               */
```

Ratios are computed with the WCAG relative-luminance formula by hand (EM TÍNH); `hyperframes validate` reported "10 text elements pass WCAG AA".

Pairings that work (measured): ink on bg 14.8; yellow on bg 13.3; mute on bg 6.0; dark `--bg` text on yellow 13.3, on voice green 6.3, on pink 5.0, on red avatar 4.6. Pairings that fail small text: `--ink` on `--accent` is only **4.25:1** (white `#fff` is 4.8). It is safe in this build only because every ink-on-accent string is >= 36 px bold (large text, 3:1). Never put body-size text on accent. Accent on bg (3.5) is for lines and borders only.

Colour rules: blurple leads; green only for speaking rings and the live dot; pink and yellow for stickers and chaos; red once. Sticker text is dark `--bg`, never white (white on pink is 3.4:1).

Texture: noise 4% opacity as an inline SVG `feTurbulence` data-URI (deterministic, no baked PNG needed). Material: radius 16 everywhere (profile 8-16); stickers and cards carry a 6 px `#fff` border and a hard `0 8px 0 rgba(0,0,0,.45)` shadow.

## 2. Fonts

None of the profile's fonts (Unbounded, Rubik, Anton, Be Vietnam Pro) is installed. Substitutes, all local files with `font-display: block`:

| Role | Profile asks | Used here | Vietnamese check |
|---|---|---|---|
| Headlines, stickers, names, meme caption | Unbounded 800 / Anton | `SegUIVar.ttf`, weight 700 (axis 300-700; 800 does not exist) | Vietnamese letters rendered correctly in every snapshot (TỔNG GIẢI THƯỞNG, SƠ ĐỒ ĐẤU, VÀO TRẬN, CẦM CÚP, Rồng Lửa, Hổ Xanh, Bão Tím). `owner-docs` (same file) records all 36 test letters present. The fontTools check could not be re-run in this session (python scripts were blocked), so the glyph list is TÀI LIỆU NÓI plus visual proof |
| Chat messages, numerals, scores, HUD | Rubik 500 | `CascadiaMono.ttf`, 200-700, `tabular-nums` | all present per owner-docs; chat lines with đ ă ơ ư ỗ rendered correctly |
| Never | | `segoepr.ttf` (35 of 36 letters missing), not used |

The meme caption (Anton uppercase, 6 px stroke) is imitated with SegUI 700 uppercase, `-webkit-text-stroke: 12px #000; paint-order: stroke fill` (12 px stroke = 6 px visible outside the glyph). White fill on black stroke reads on any background.

## 3. Type scale (1080 x 1920, px; all measured in this build)

| Token | Font | Size | Notes |
|---|---|---|---|
| Hook headline `#hcard .h` | SegUI 700, -0.02em | 136 / 1.14 | 2 lines "CHUNG KẾT" / "ESPORTS", fits 888 px in one line each (about 700 px wide); 1.02 line-height caused tone-mark overlap in `inspect` |
| Hook kicker | SegUI 700 +0.04em | 36 | on accent card |
| Scene headline `#h2` / `#h3` | SegUI 700 | 112 (one line) / 120 (two lines, 1.14) | key word in `--yellow` |
| Sticker | SegUI 700 | 56 (hook), 48 (reaction pile), 150 (slap transition) | dark text on pink / yellow / green |
| HUD pill | Cascadia 600 | 30 | `#chung-kết-live` with 18 px green dot |
| "Minh hoạ" sticker | SegUI 700 | 44 | yellow, 6 px white border, rotate 4 deg, on screen the whole 12 s |
| Column label | Cascadia 600 +0.06em | 30 | `--mute` |
| Team name | SegUI 700 | 36 (round 1), 30 (finalists) | no text below 30 px |
| Score | Cascadia 700 | 44 | chip radius 12 |
| Prize number | Cascadia 700 | 150, -0.04em | "1.000.000" = about 810 px wide, fits a 984 px card |
| Prize row | SegUI 700 label 38, Cascadia 700 value 48 | | |
| Meme caption | SegUI 700 uppercase | 92 | stroke 12 |
| Footer (the one allowed small line) | SegUI 500 | 26 | `--mute`, "Minh hoạ: nội dung giả định, không phải giải đấu thật." |
| Chat | username SegUI 700 30, message Cascadia 500 30 | | rows 76 px high |

## 4. Safe areas and grid (1080 x 1920)

```
y 0    -170  platform UI: empty
y 176  -252  HUD pill (x 48) and "Minh hoạ" sticker (x 716)
y 290  -420  scene headline
y 330  -1430 chat flood zone (scene 1 only, clipped box)
y 446        column labels (scene 2)
y 520  -1120 bracket (scene 2)
y 600  -890  prize number card (scene 3)
y 930  -1290 three prize rows (104 px high, 128 px pitch)
y 1330 -1430 meme caption
y 1438       footer line
y 1480 -1920 bottom platform UI: empty
x 48   -1032 content column (984 px)
```

Bracket columns (x): round 1 tiles 48-368 (w 320); finalists 400-706 (w 306); champion card 728-1032 (w 304). Gaps 32 and 22 px hold the 6 px neon connector lines. Rows: round 1 tiles y 520, 660, 860, 1000 (h 120); finalists y 590 and 930; champion y 660-980. Body ends y 1120 (58% of the frame), so the frame-check "TOPHEAVY" threshold (55%) is cleared, and the reaction stickers (y 1200-1400) fill the lower third.

## 5. Layers, back to front

`#noise` -> `.scene` x3 (`#s1` chat + card + stickers, `#s2` bracket, `#s3` prize; one visible at a time via `visibility`) -> persistent HUD (`#hud`, `#mh`, `#foot`) -> `#slap` (sticker-slap transition) -> `#punch` (yellow circle for the zoom-punch transition). No black fade layer: a hard dark bg start is fine (HUD fades in 0.3 s); the last frame is a full composition.

## 6. Components

- **Chat row** (76 px): 56 px coloured dot, username in its colour, message in mono. 40 rows built once from a seeded rng (seed 20261115); only the first 20 pop in (0.03 s stagger, 0.2 s `power2.out`, 60 px slide).
- **Headline card**: accent fill, 6 px white border, hard shadow, rotate -4, with the kicker above two lines.
- **Sticker**: pink / yellow / green / accent, 6 px white border, radius 16, hard shadow, rotated -6 to +7, dark text.
- **Team tile** (120 px high): surface fill, 3 px `surface-hi` border, avatar circle with the team initial, name, score chip, and an invisible voice ring (inset -10, 5 px `--voice`, radius 24) that fades in for the winner.
- **Connector lines**: SVG paths with `pathLength=1`, 6 px accent, round caps, drawn with `strokeDashoffset 1 -> 0`.
- **Champion card**: yellow, 6 px white border, "VÔ ĐỊCH", pink avatar, team name 52, final score in mono.
- **Prize row**: surface, label left, mono value right, 12 px bar on the bottom edge scaling from the left to its share (1, .5, .25 of the row width).
- **Meme caption**: see fonts.

## 7. Motion language

Energy 5. Eases used: `power4.out` (slams, punches), `power3.out`, `power2.out`, `back.out(1.6-2)` (pops), `sine.inOut` (wobbles), `none` (counter, scroll, shake). Randomness only from the seeded `rng`. The timeline is one paused GSAP timeline, 360 frames at 30 fps.

| Verb | Recipe (measured values) |
|---|---|
| chat-flood | rows pop at 0.03 s stagger; the list scrolls -1500 px in 3.4 s with `ease:"none"` (441 px/s, about 5.8 rows per second: too fast to read) |
| slam | from scale 2.2-2.8 and rotate -14 to -22 to its tilt, 0.2-0.3 s `power4.out`; followed by a 6-cycle x/y shake of 10-14 px at 0.05 s per half-cycle |
| sticker-slap transition | the "VÀO TRẬN!" sticker slams at 3.4 s (0.2 s), root shake at 3.6, scene swap at 3.75 behind it, sticker scales to 1.7 and fades 3.9-4.08, hidden at 4.1. Total hold about 0.5 s |
| zoom-punch (element) | champion card 0.3 -> 1.35 in 0.14 s `power4.out`, back to 1.0 in 0.4 s `back.out(1.8)`; headline card 1 -> 1.14 -> 1 in 0.32 s |
| zoom-punch transition | yellow full-frame circle clip-path grows from the champion (870, 820) to 2200 px in 0.32 s `power3.in` (7.5-7.82), scenes swap at 7.84, the circle shrinks into the prize card (540, 700) in 0.4 s `power3.out` (7.9-8.3) |
| pop | tiles from scale .6 with a seeded rotation +-8 deg, 0.35 s `back.out(1.6)`, 0.12 s stagger |
| line draw | `strokeDashoffset` 0.4 s `power2.out`, 0.05 s stagger |
| voice ring | fades in 0.15 s then pulses scale 1.05 every 0.22 s (yoyo) |
| counter | 0 -> 1.000.000 in 1.3 s `ease:"none"` (8.4-9.7), text formatted with "." thousands separators, then forced to the exact final string at 9.7 |
| micro-motion | live dot pulse every 0.5 s all video; stickers and cards rotate +-3 deg on `sine.inOut` through every hold; nothing static longer than 0.5 s |

## 8. Scene recipes (the 12 s sample: 3 beats)

| Beat | Time | Recipe |
|---|---|---|
| 1 Hook | 0 - 3.75 | Chat flood fills the frame from t=0; headline card slams at 0.3 s (shake 0.85-1.15); "GG!" sticker 1.45 s, "AI THẮNG?" sticker 1.95 s; zoom punch 3.0 s; sticker-slap out at 3.4 s |
| 2 Bracket | 3.75 - 7.84 | Headline "SƠ ĐỒ ĐẤU" rises 3.95 s (ĐẤU slams in yellow 4.1 s); column labels 4.2; 4 round-1 tiles pop 4.25-4.6; scores appear 4.9; connectors draw 4.95; winner rings 5.2; finalists pop 5.55 and 5.67; reaction stickers pile up 5.1 s at 0.18 s stagger; final connectors 5.95; champion zoom punch 6.55 (+ tile shake); hold with micro-motion to 7.5; zoom-punch transition out |
| 3 Prize pool | 7.84 - 12.0 | Headline 8.0 / 8.15 s; number card 8.15 s; counter 8.4-9.7 s with a 1.08 punch and shake at 9.7; three prize rows 8.9, 9.06, 9.22 s with bars growing 0.6 s; meme caption slap 10.1 s then wobble; everything complete and moving gently from 10.3 s to the end (last 1.5 s = full composition) |

Recipe for other shapes: hook = chat flood + one slammed headline card; reveal = tiles/stickers popping with seeded rotation; one number = counter inside a card with a punch on landing; every beat change = sticker-slap or zoom-punch, never a plain cut.

## 9. Captions

NOT exercised (demo build: no voice-over, no word timing). Profile (untested): surface pill radius 12 with a 2 px accent border, 42 px bold, current word yellow; captions layer sits on top of the chaos with a clear band. This build used on-screen text only; if captions are added, keep the 1370-1480 band clear (the meme caption at y 1330-1430 would have to move).

## 10. Sound

NOT exercised (silent demo). Profile (untested): hyperpop / phonk / chiptune-EDM 120-150 BPM; pings, slaps and boom hits on the sticker and punch moments. The slap times above (0.3, 3.4, 6.55, 7.5, 10.1 s) are the natural SFX anchors.

## 11. Images

None used (0 of the allowed 2). Stickers, cards, avatars and connectors are CSS and SVG. If one agy image is added: a flat sticker-style illustration with a thick white outline on a transparent or dark background, no text, no logos, no real people; place it inside a sticker frame rotated -6 to 6 deg.

## 12. Must not

- No real team, league, company, price or logo; invented names and numbers carry "Minh hoạ" on screen for the whole video.
- No white text on pink or yellow; no body-size text on accent.
- No `segoepr.ttf`; no text under 30 px except one footer line.
- No unseeded randomness, no CSS animation, no `Date`.
- No long static holds, no corporate greys, no premium restraint (profile avoid list).
- Do not let the chat flood run behind a held headline: the flood moves, the card holds.
- No plain cuts between beats.

## 13. Traps seen in real builds (this build, 2026-11-15)

1. **Round-2 tile too narrow.** At 250 px wide the finalist tile (avatar 60 + name 32 px + score chip) needed about 316 px; the score "3" hit the tile edge and the connector. Fix: tile 306 px, avatar 52, name 30 px (the first fix to 28 px broke the 30 px minimum). A Vietnamese team name such as "Rồng Lửa" is about 150 px at 32 px bold.
2. **Hand-measured widths lie.** Measure the longest string in the render (snapshot at the end of the tile's reveal), not in the editor.
3. **Line-height 1.02 on 120-136 px uppercase Vietnamese** made `inspect` report `content_overlap` between the two headline lines (tone marks of Ế, Ổ, Ở). 1.12-1.14 clears it.
4. **Stacked heading and card touched.** The two-line scene-3 headline ended at y 557 and the prize card began at 560; the snapshot showed them glued. Card moved to y 600 and the rows and caption down by 40 px.
5. **First 0.5 s was nearly empty.** With rows starting at 0.1 s and a 0.06 s stagger, the t=0.4 s frame held 5 chat rows and no headline. Fixed by starting rows at 0 (0.03 s stagger) and the card at 0.3 s. A flood style must show the flood from frame 0.
6. **Chat list too short.** 26 rows (1976 px) scrolled -1500 px left the bottom of the zone empty after about 1.9 s; 40 rows fixes it. Rule: rows >= (scroll distance + visible height) / 76.
7. **`inspect` errors on the flood are by design.** 24 `text_occluded` / `clipped_text` errors remained, all from chat rows passing under the headline card, stickers, HUD and the clipped chat box (`data-layout-allow-overflow` and `-overlap` do not silence `text_occluded`). Every non-chat check was clean (lint 0 errors 0 warnings, validate no console errors, WCAG pass). Confirm by listing the errors and checking that each names `#chat` rows or a descendant `.un` / `.ms`.
8. **GSAP overlap warning.** Two wobble tweens on `#stk2` overlapped 0.01 s (2.20 vs 2.21); start the wobble 0.05 s after the entrance ends.
9. **Transition cover must hide the swap.** The slap sticker is fully opaque from 3.6 s and the scene swap is at 3.75 s, so no ghost of the outgoing beat exists; the yellow circle covers the frame at 7.82 s and the swap is at 7.84 s. Do not swap before the cover is opaque.
10. **Counter landing.** Setting the exact string at 9.7 s after the tween avoids a rounding frame such as "999.999"; the number is held (1.000.000) from 9.7 to 12 s, 2.3 s, never mid-count.
11. **Tooling.** `frame_check.py` needs numpy, which was missing in this environment (`ModuleNotFoundError`), so the frame check was done with an ffmpeg 2 fps contact sheet read by eye. If numpy is missing, say so; do not claim the script ran.
12. **Font gap.** The profile's fonts are not installed; SegUI 700 and Cascadia stand in. The look is cleaner and less rounded than Unbounded; the stickers, tilt and stroke carry the chaos, not the typeface.
13. **Size.** 12 s, 1080x1920, 30 fps, h264, 3.7-3.9 MB, rendered in about 12 s.
