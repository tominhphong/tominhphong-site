# Style: ambient-intelligence (detail, round 1, DEMO build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in the one build (topic shape t030, "how a large language model uses a context window", Jev fit 0.72):** calm explainers of how an AI system works, assistant demos, research or model announcements told as a mechanism rather than a number. Works when the story is a flow of "things enter, a limit is hit, a result is produced". Not for several equal numbers (use saas-bento), enforcement or urgent news, warm local stories, or anything needing a hard, fast rhythm. Tier 2 never widens tier 1.

**Status.** Written 2026-11-13 from ONE demo build: one silent 13.0 s sample, 1080x1920. **Voice-over, word timing, captions and music were NOT exercised** (demo build): sections 7 and 9 are copied from the profile and marked ASSUMED. Everything else below is measured on this build. The profile is `references/styles/profiles/ambient-intelligence.yaml`.

**Example video shows the recipe, not the niche.** Copy how it is built, not what it says. All content on screen is generic and labelled "Minh hoạ".

## 1. Tokens

```css
:root{
  --bg:#ffffff;
  --ink:#0d0d0d;          /* 19.4:1 on white, 12.7:1 on peach */
  --mute:#5b5b68;         /* DARKENED from profile #8a8a96 (3.4:1 on white fails); 6.7:1 on white. WHITE SURFACES ONLY: on peach it is 4.4 */
  --accent:#1f9e98;       /* 3.3:1 on white: FILL, line, dot, ring only, never text */
  --accent-dk:#0e6e69;    /* ASSUMED token: accent text, 6.1:1 on white, ~5.2 on --accent-soft */
  --accent-soft:#d9f0ee;  /* chip fill */
  --peach:#f7c8a8; --lilac:#c9c2f0; --sky:#a8d8f0;   /* fields and token cells only */
  --line:#e5e5e5;
  --sh:0 20px 60px rgba(0,0,0,.06);                  /* the one shadow, profile value */
}
```
Contrast: relative luminance by hand with the WCAG formula (no script runner was available in this build; numbers are hand-computed, ~0.1 accuracy). Rules: type is `--ink` on fields, `--mute` or `--ink` only on white panels; colour on type never (profile rule); the accent is one cursor, one line, one ring. Two pastels per beat: beat 1 peach + lilac, beats 2-3 sky + lilac.

## 2. Fonts

| File | Missing Vietnamese glyphs | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 (TÀI LIỆU NÓI: fluent-productivity doc, same file, glyph test of all capitals and lower case); confirmed by eye on "Mỗi", "chiếm", "Cửa sổ ngữ cảnh", "Tóm tắt" in the snapshots | EVERYTHING read. Substitute for the profile's Inter. Weight 500 headlines (-0.02em), 400 body |
| `CascadiaMono.ttf` | 0 (same source; seen rendering "CỬA SỔ NGỮ CẢNH", "TRẢ LỜI", "Tóm tắt tài liệu giúp tôi") | Substitute for IBM Plex Mono: panel label, counter, typed prompt |
| `cambriai.ttf` | 0 | not used (no quote in the sample) |
| `segoepr.ttf` | 92 (same source) | never used |

Be Vietnam Pro (profile caption face) is not in `assets/fonts`; unused because no captions. Mono caps get +0.04em tracking.

## 3. Type scale, safe areas and grid (1080 x 1920)

Measured px: headline beat 1 **84** (-0.02em, line-height 1.08, 3 lines); headline beat 2 **64**; sub **38** (beat 1) / **34** (beat 2); mono labels and counter **30**; chips **30**; typed prompt **38**; response text **40** (line-height 1.3); footer **26** (the one allowed line under 30). Nothing else under 30.
- Left column x 100, content width 880 (right margin 100). Text left aligned. Radius 24 on panels and bars, 16 on token cells, 999 on chips.
- y 0-120 empty; "Minh hoạ" chip y 130-186 (always on screen).
- Beat 1: headline top 560, sub top 1010, rest is colour field (whitespace is the design).
- Beats 2-3: headline y 240, sub y 330, window panel y 440-1122 (880 x 682), response card y 1190-1422 (232 high), input bar y 1470-1590 (120 high), footer y 1700. Nothing below y 1730; the 1730-1920 band stays empty.

## 4. Layers, back to front

1. `#root` white.
2. `#washA` / `#washB` (z 1): baked 1188 x 2112 pastel-blob images (1.1x of frame), left -54, top -96. Baked with ffmpeg `geq` (two gaussian blobs on white, no blur filter at runtime); 220-230 KB PNG each. Breathing: scale 1.0 -> 1.08 and 30 px drift over 4.6 s (A) / 8.6 s (B), `sine.inOut`, one pass.
3. Scene sections `#s1`, `#s2` (visibility toggled with `tl.set`).
4. Panels and bar (flat white, 1 px `--line`, `--sh`).
5. `#path` SVG overlay (accent line) and ring, above panels.
6. `#tag` "Minh hoạ" chip (z 30). No fade layer: the video starts on the colour field and ends on the full composition.

## 5. Components

- **Window panel**: white, radius 24, header 52 px with mono label left, counter right, optional chip between. Token grid inside: 4 columns, cell 185 x 72, gap 20 (column pitch 205, row pitch 92), 6 rows visible + 1 spare below, inside an `overflow:hidden` box (rows carry `data-layout-allow-overflow`).
- **Token cell**: pastel fill, radius 16, no text (colour legend is in the sub line). Legend by colour word, never by coloured type.
- **State chip** ("Cũ nhất rơi ra"): `--accent-soft` fill, `--accent-dk` 30 px text, height 46.
- **Input bar**: white, radius 24, mono text 38 px, 3 px accent cursor.
- **Response card**: white, mono label, 40 px streamed text, thinking dot 26 px accent.
- **Attention line**: 4 px accent path with `pathLength=1` dash draw from the card edge, around the left margin (x 28-100), to a token cell; end dot 20 px and a 4 px accent ring around the target cell.

## 6. Motion language

- Entrances: panel `power3.out` y 40 -> 0, 0.6 s; bar 0.5 s; cells opacity + scale 0.88 -> 1, 0.35 s `power2.out`, stagger 0.075 (24 cells = 1.8 s).
- Streaming: words are `inline-block` spans, opacity 0 -> 1 with a 0.01 s tween at stagger 0.06 (sub) to 0.1 s (headline); no movement.
- Typing: proxy tween `ease:none`, 0.04 s per char (25 chars = 1.0 s), cursor x = n * 22.9 px at 38 px Cascadia; cursor hidden when done (a held frame never shows a half word).
- Counter: proxy tween `ease:none` synced to the cell stagger, 0 -> 24 in 1.8 s, finished 0.55 s before the next move (no counter held mid-count).
- Window slide ("oldest falls out"): all rows y -92 over 0.8 s `power3.inOut`, row 0 fades 0.5 s `power2.in`, new row fades in at 7.9 s.
- Thinking dot: fade-in 0.28 s, one pulse 1 -> 1.3 -> 1 (0.4 s up, yoyo, repeat 1), fade-out 0.25 s. Finite; never `repeat:-1`.
- Text dissolve out: per word 0.3 s `power2.in`, stagger 0.025 (3.4-4.2 s). Field bloom: crossfade of two washes 1.0 s `sine.inOut`.
- Holds are never frozen: wash drift, panel scale 1.0 -> 1.012 over 8.5 s.
- No bounce, flash, shake, speed lines.

## 7. Captions

NOT EXERCISED (demo build, silent). ASSUMED from the profile: 42 px Be Vietnam Pro 500, no pill, bottom band, current word ink and unread mute. Note the profile's "unread mute" needs the darkened `--mute` (#5b5b68) and works only over white; over a pastel field use ink for both.

## 8. Scene recipes (as built: 13.0 s, 3 beats)

**R1 Title with streaming text (0-3.9 s), peach + lilac field.** "Minh hoạ" chip fades 0.2-0.8; headline "Mô hình đọc qua một cửa sổ có giới hạn" streams from 0.4 (0.1 s/word); sub streams from 1.6 (0.06 s/word); read hold 2.7-3.4; dissolve out 3.4-4.2 while the field blooms into sky + lilac (3.6-4.6).
**R2 Window fills (3.95-8.4 s), the signature recipe.** Headline "Mỗi token chiếm một chỗ" 4.0, sub 4.5; panel rises 4.6; bar 4.75; prompt typed 5.0-6.0; 24 cells fill 5.0-6.8 with the counter; hold 6.8-7.4; the first (lilac) row falls out and the grid slides up 7.4-8.2 with the chip "Cũ nhất rơi ra" (7.5) and a new row in (7.9).
**R3 Answer and attention (8.4-13.0 s).** Response card rises 8.4; thinking dot 8.8-9.5; answer streams 9.45-10.7 (14 words, 0.09 s/word); accent line draws 10.5-11.5 to a "Tài liệu" cell; ring and end dot 11.3-11.6. Full composition holds 11.6-13.0 (1.4 s of still image plus drift).

## 9. Transitions

Used: text dissolve + field bloom (R1 to R2), same-surface continuation (R2 to R3: nothing leaves, a new card enters). From the profile, not exercised: slow cross-fade 0.8 s, cut to white on section turns. Outgoing section gets `visibility:hidden` after its words are at 0.

## 10. Image guidance (agy)

No agy image was used. The soft fields were baked with ffmpeg `geq` (two gaussian blobs, hex-exact pastels). If agy is used: prompt "soft blurred pastel colour field, peach and lilac, painterly gradient, no text, no objects, large empty areas", expect a plain gradient, re-encode `-q:v 4`, oversize 1.1x. Never ask agy for cells, grids, lines or text.

## 11. Safe handling of facts

Generic illustrative content only: no number is a real spec ("24" cells is a drawing). Every beat carries the "Minh hoạ" chip and the footer "Hình minh hoạ chung, không đại diện cho mô hình hay sản phẩm cụ thể." A real-fact version needs a source chip per number.

## 12. Must not

- Colour on type, `--accent` on text (3.3:1), `--mute` on a pastel field (4.4:1).
- Neon, brains, circuits, robots, any AI lab logo or product name; dense dashboards; hard fast cuts.
- Bounce or elastic eases, flashes, shake; `repeat:-1`; live CSS blur.
- segoepr for Vietnamese.
- Sound: ambient pads and a faint key tick are in the profile; not tested here.

## 13. Traps seen in real builds (this build, 2026-11-13)

1. **Profile mute fails contrast.** `#8a8a96` is 3.4:1 on white. Darkened to `#5b5b68` (6.7:1). That token is still only 4.4:1 on peach, so on a field use ink.
2. **Accent is not a text colour.** `#1f9e98` is 3.3:1 on white; the chip text needed `#0e6e69` (6.1:1).
3. **Empty panel at entrance.** First cut had the panel rise at 4.1 and the cells start at 5.2: an empty white panel for 1.1 s (limit 0.5). Fixed by panel at 4.6 and cells at 5.0 (empty 0.4 s measured on a 5 fps strip).
4. **Offscreen spare row triggers `container_overflow`** (92 px, three samples) in `inspect`. Fixed with `data-layout-allow-overflow` on each row; inspect then 0 issues.
5. **Same-property tween warning.** Dot fade-in ended at 9.10 s exactly where the pulse started: `overlapping_gsap_tweens`. Shortened the fade to 0.28 s; lint 0/0.
6. **Typed cursor position** uses a fixed 22.9 px per char at 38 px Cascadia; a different mono font or size breaks it.
7. **Attention line crossing content.** A straight line from the answer card to a cell crosses 3 rows of cells; routing it through the left margin (x 28-100, cubic curve) keeps the panel clean. The ring is positioned in frame pixels and the panel drifts by scale 1.012 (about 3 px at the edge): keep the drift under 1.015 or put the ring inside the panel.
8. **Tool gaps in this environment.** `frame_check.py` needs numpy, which was not installed, so the frame check was done with ffmpeg strips read by eye (see selfcheck.md). Contrast and glyph numbers are hand-computed or cited.
9. **Render.** `hyperframes render` 13.0 s, 1080x1920, 30 fps, 2.0 MB, 12.5 s render time; GSAP loaded from the CDN at render time (needs network).

## 14. Weak spots / still ASSUMED

Captions, voice, music and SFX untested; a long-form (45-60 s) pacing of this style is unknown; the lower 190 px is empty by design; Inter and Plex Mono are substituted; beat 1 is text only (no focal object) and relies on the field.
