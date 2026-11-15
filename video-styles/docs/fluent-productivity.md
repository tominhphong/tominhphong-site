# Style: fluent-productivity (detail, from the demo build of 2026-11-14)

Written from ONE real build: a 12.0 s silent 1080 x 1920 sample on topic shape t034 ("Pricing change: an AI assistant adds a cheaper plan", Jev fit 0.72). All numbers below were measured or taken from that build. Voice, word timing, captions and music were NOT exercised (demo build): sections 7 and 11 say what is untested.

## 0. Read this first: niche, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), as observed in this build.** Calm, dependable, product-UI stories where one app window can carry the whole explanation: an AI assistant or workplace tool gains a plan, a feature or a setting, and the story is "what changed, how it compares, which to pick". Worked well on t034 (two plans, one price delta, one feature list). Not for urgent, entertainment or sad stories (the style has no shake, flash or bounce to carry them). Tier 2 never widens tier 1.

**Status.** Demo only: one sample, no voice-over, no captions, no music, no full video. Everything about voice sync, caption pills, anchors on spoken words and sound is carried over from the profile (`fluent-productivity.yaml`) and was not tested here. Content on screen is generic and labelled "Minh hoạ" (no real company, product, price or spec).

**Deviations from the profile (all deliberate).**
1. Profile lays out "headline left, window right" for 16:9. In 1080 x 1920 everything stacks: kicker, headline, window, footer.
2. Profile says `avoid: hook`. This sample opens on the assistant answering a question inside the window, entering with the calmest verb (decelerated word stream), no slam.
3. Profile fonts (Noto Sans, Be Vietnam Pro) replaced by the local `SegUIVar.ttf` (Segoe UI Variable, itself a Fluent face) and `CascadiaMono.ttf`.
4. Wash backdrop: the profile says "baked PNG". The agy image tool needed a permission approval that was not available, so the wash is a baked JPG made with ffmpeg (four `drawbox` blocks, `gblur` sigma 140, 3% noise). No live blur in the page.

## 1. Tokens

```css
:root{
  --bg:#eef1f6; --ink:#242424; --mute:#616161; --surface:rgba(255,255,255,.96);
  --accent:#2a5fc4; --accent-dk:#1d4aa0; --accent-soft:#d6e0fa; --teal:#13856f;
  --stroke:rgba(0,0,0,.06); --sh-win:0 32px 64px rgba(0,0,0,.18); --sh-fly:0 8px 16px rgba(0,0,0,.14);
}
```

Contrast (WCAG formula, computed by hand with awk-equivalent arithmetic, +/-0.1; `hyperframes validate` independently reported "35 text elements pass WCAG AA"):

| Pair | Ratio | Use |
|---|---|---|
| ink on white | 15.5 | all body and headline text |
| ink on --bg | 13.7 | headline over the wash |
| ink on --accent-soft | 11.8 | bubble text, note panel text |
| mute on white | 6.2 | sub-lines, placeholder, footer, units |
| mute on --bg | 5.5 | kicker over the wash, footer |
| mute on --accent-soft | 4.7 | not used on soft in this build (below 5) |
| accent-dk on white | 8.3 | "Minh hoạ" label, selected tab on white |
| accent-dk on --accent-soft | 6.3 | selected tab on the pill, delta chip text |
| white on accent-dk | 8.3 | "MỚI" chip |
| accent on --accent-soft | 4.5 | borderline: accent is a fill or border only, never text |

Rules: text colours only from `--ink --mute --accent-dk` (and white on `--accent-dk`). `--accent` and `--teal` are fills, borders and icons. Surface alpha was raised from the profile's .82 to .96 so text contrast does not depend on the wash behind the window (the wash is lighter than the page but varies). One accent per beat.

## 2. Fonts (Vietnamese diacritics check)

| File | Role | Result |
|---|---|---|
| `SegUIVar.ttf` | headlines (650), UI text (500-650), numbers (700) | declared `font-weight:100 900`; rendered every string below with correct marks |
| `CascadiaMono.ttf` | kicker, window title, footer, "MỚI" chip, "GIÁ" label (30 px, +0.03em) | rendered "TRỢ LÝ AI · GÓI DỊCH VỤ" and "MỚI" with Ợ Ý Ị Ớ intact |
| `cambriai.ttf` | copied, unused (no quoted sentence in this story) | not exercised |
| `segoepr.ttf` | never used (lacks Vietnamese letters) | not copied |

Check method: the glyph table (fontTools) could not be run because Python needed an approval in this environment; instead every on-screen string was rendered in the real fonts and read on the snapshots (see `selfcheck.md`). No tofu or fallback glyph was seen. Fonts are copied into the project and `render` embeds them as data URIs (Segoe 1808 KB, Cascadia 363 KB). Without the copy, `validate` printed 404 on both fonts: copy `assets/fonts` first.

## 3. Type scale, grid and safe areas (1080 x 1920)

- Margins 72 px, content width 936. Window x 72, y 470, 936 x 1080 (ends y 1550). Inner content x 40 to 896 (856 wide), coordinates measured from the window's top-left.
- y 0-130 empty; kicker y 132 (30 px mono); headline y 196-396 (two lines, 88 px / 100 px line height, SegUIVar 650, tracking -0.01em); window y 470-1550; footer line y 1586 (30 px mono). y 1650-1920 empty; right rail x 960-1080 empty below y 1100.
- Scale: headline 88; plan name 56; price hero 150 (one third of frame height is the upper limit for a hero; 150 px is 7.8 %); price in recap row 72; chat text 40; bubble and rows 38; delta chip 38; unit and sub-lines 32-34; all mono labels 30. Smallest authored text: 30 px (kicker, footer, window title, chip). The one footer line is also 30 px, so no text is under 30 px.
- Radius: window 12, card 12, flyout 12, chip 999. Depth stack: window (back), card or panel (middle), flyout and chip (front), 3 layers at most.

## 4. Layers, back to front

1. `#root` `--bg`.
2. `#wash` (img, 1188 x 2112, offset -54/-96, i.e. 1.1x): drifts x +18, y -40 over 12 s, 0.3x of nothing else (the world scales 1.00 to 1.02 in the same time).
3. `#world`: kicker, three headlines, window, footer; `scale 1 -> 1.02` linear over 12 s (the micro-motion that keeps every hold alive).
4. `#win`: header strip 64 px with three 14 px `--accent-soft` dots (no traffic lights) and a mono title; scale 0.98 -> 1 in 0.7 s `power3.out` from t 0.
5. Beat groups `#g1 #g2 #g3` (each 936 x 1080, absolute, children animate), plus `#bridge` (the connected chip) as a direct child of the window so it can cross between groups.
No caption layer, no fade layer (frame 0 already shows a built composition).

## 5. Components (as built)

- **Chat bubble**: right aligned, `--accent-soft`, radius 12, 22 x 30 padding, 38 px 500.
- **Assistant row**: 64 px accent circle with a 4-point star (inline SVG, white), text 40 px / 56 px, 768 wide, streamed word by word (see motion).
- **Shimmer lead**: 180 x 6 px bar, gradient `--accent` to transparent, sweeps x 0 -> 588 in 1.2 s `power2.inOut` while the text streams, then fades 0.2 s.
- **Flyout preview card** `#pv`: 856 x 320, white, radius 12, `--sh-fly`, two 120 px rows (name 44 px 650, sub 32 px mute).
- **Chip** "MỚI": 120 x 56, `--accent-dk`, white mono 30 px bold, radius 999. The signature connected element.
- **Plan card**: 856 x 370, white, radius 12, 1 px stroke (the new plan gets a 3 px `--accent` border); name 56 px, sub 32 px mute, price block right (150 px 700 tabular figures + 34 px unit).
- **Delta chip**: `--accent-soft` pill 72 px high, `--accent-dk` 38 px 700 text, plus a 34 px mute sub-line.
- **Segmented tabs + selection pill**: track 856 x 88 (`--bg` fill, stroke), pill `--accent-soft` 422 x 74 slides x 0 -> 428 in 0.45 s `power3.out`; selected label `--accent-dk`, unselected `--mute`, colours switched by `tl.set` at the slide start.
- **Feature row**: 110 px, 44 px icon (teal filled check for included; 3 px mute ring with a dash for not included), 38 px 500 text, 1 px bottom stroke.
- **Price row**: 856 x 120, mono "GIÁ" label 30 px left, value 72 px + unit right.
- **Note panel**: 856 x 220 `--accent-soft`, `--sh-fly`, 42 px 600 ink, two lines.
- **Composer**: 856 x 88 input with placeholder "Hỏi trợ lý…" and an accent send button (fills the lower window in beat 1).
- Icons are inline SVG circles and strokes only.

## 6. Motion language (measured in the build)

- Entrances decelerate: cards `power3.out` y 40 -> 0 + fade 0.4 s (second card 0.12 s later); rows y 20 -> 0, 0.35 s, 0.06 s stagger; headline y 24 -> 0, 0.3 s; flyouts `power2.out` y -12 -> 0, 0.3 s. No `back`, `elastic`, bounce, shake, flash, whip.
- Exits accelerate: `power2.in`, 0.15 s (about 40 % of the entrance; the acceptance rule of 0.15 s for a ghost forced this, the profile's 0.25 s would ghost).
- **Connected animation**: the "MỚI" chip rides on the preview card in beat 1 (appears with it at 1.6 s), then, while the chat fades out (3.8-3.95 s), flies to the title of the new plan card: x `power3.inOut` and y `power2.inOut`, 0.7 s, dx -442, dy -324. It lands at 4.5 s while the card counts.
- **Counters**: proxy tween, `power3.out`, text written in `onUpdate`. 0 -> 8 over 0.8 s (4.4 s), 0 -> 20 over 0.9 s (4.5 s); final from 5.4 s, held 2.4 s.
- **Streaming text**: 14 words, `tl.set` opacity at 0.3 s + i x 0.09 s, complete at 1.5 s.
- **Selection pill**: slides at 9.9 s, row group swap 9.9-10.4 s, so the last 1.6 s is a held, finished frame.
- Holds are never frozen: world scale drift, wash drift, a 5 px float (finite yoyo, `sine.inOut`) on the preview card, the delta chip and the note panel.

## 7. Captions

Not exercised (silent demo). The profile's acrylic pill (40 px, current word accent) is untested here. If captions are added, they live below y 1400 and the window must end above them (this sample ends at y 1550 and has none).

## 8. Scene recipes (3 beats in 12.0 s)

**R1 Assistant answers (0.0-4.0 s).** Headline "Trợ lý AI vừa thêm / một gói rẻ hơn". Window with a user bubble already in place at frame 0, composer at the bottom. 0.3-1.5 s: assistant text streams behind a shimmer lead. 1.6 s: preview card drops 12 px with the chip. Hold with float and world drift. Exit 3.8-3.95 s.

**R2 Compare (4.0-8.0 s).** Headline "Gói Nhẹ có giá / thấp hơn gói Pro". Two plan cards enter 0.12 s apart; the chip lands on the first; counters 8 and 20; delta chip "Rẻ hơn 60%" slides x 30 -> 0 at 5.6 s (derived: (20-8)/20 = 60 %, labelled "so với gói Pro"). Hold 6.0-7.8 s. Exit 7.83-7.98 s.

**R3 Choose (8.0-12.0 s).** Headline "Chọn gói theo / mức độ sử dụng". Tabs enter 8.0 s, three feature rows 8.15-8.27 s, price row 8.4 s, note panel 8.8 s. At 9.9 s the pill slides to "Gói Pro" and the row group and price swap (20). Final composition 10.5-12.0 s: tabs, three checks, price row, note.

## 9. Transitions (as built)

Beat 1 -> 2: connected chip plus entrance-slide. Beat 2 -> 3: entrance-slide (outgoing 0.15 s `power2.in`, incoming from the boundary). Beat 3 internal swap: crossfade of row groups, 0.15 s out and 0.35 s in. Outgoing groups get `autoAlpha:0` (visibility hidden) after fading so `inspect` does not report hidden text under cards. Never a hard cut, never a flash.

## 10. Image guidance

Only a baked wash was used (no agy image: not run, see section 0). A wash must be baked (ffmpeg or an agy still) and used at 1.1x so its drift never shows an edge; keep it lighter than white-ish `--bg` tints (measured: ink 13.7 on --bg). agy would only supply mood, never windows, text or icons.

## 11. Safe handling of facts

Not exercised with real sources. In this sample every number is a labelled illustration: "Minh hoạ" in the kicker (accent-dk, mono) AND in the footer line "Minh hoạ · số liệu giả định, không phải giá thật" on every frame, so the label is on screen the whole 12 s. Prices (8 and 20 $/tháng) and the 60 % derived from them are invented; a real build must replace them with sourced numbers and a source chip.

## 12. Must not

- Live `backdrop-filter`, more than 3 depth layers, bounce / elastic / back eases, shake, flash, speed lines, whip pans.
- Neon or dark looks, traffic-light dots, any real vendor logo or replica of a real interface, emoji.
- `--accent` or `--teal` as text colour; mute text on `--accent-soft` below 5:1 (4.7 measured).
- `segoepr` for Vietnamese; serif except a single quote.
- Counters caught mid-count at a hold; text under 30 px.
- Putting beat content in a container whose own children are the only thing faded (the container keeps reporting its hidden text; hide the container too).

## 13. Traps seen in real builds (this build, measured)

1. **Fonts 404.** `cp -R assets/fonts` was refused by the shell and silently skipped; `validate` then failed with 4 errors (404 on SegUIVar and CascadiaMono). Copy the files one by one into `samples/t034/assets/fonts/` and re-run: result 0 errors, "35 text elements pass WCAG AA".
2. **Static `.rows` containers flowed.** The two row groups had no `position:absolute`, so the second stacked 1000 px below the first; `inspect` printed `canvas_overflow` up to 254 px on "20" at 11.33 s. Fix: `position:absolute`. Lint and validate were both clean while this was wrong: only `inspect` found it.
3. **Hidden text under a card.** Fading the children of `#g1` left the group itself visible; `inspect` reported 2 `text_occluded` errors and 12 `content_overlap` warnings against it. Fix: `tl.set("#g1",{autoAlpha:0},3.97)` after the 0.15 s out. Final: 0 layout issues in 9 samples.
4. **Empty lower window.** First layout (window 1000 px, content to y 1470) left y 1560-1920 bare and a 180 px hole under the preview card at 2.6 s. Window grown to 1080 px (ends 1550), card tops moved (+30 on preview, +20 on plan 1, +30 on plan 2), footer to y 1586. Lowest content edge at holds: y 1550 (window), 1626 (footer).
5. **Preview card too late.** At 3 fps the contact sheet showed the lower half of the window empty from 0.3 to 2.0 s (1.7 s of white). Card and chip moved from 2.0 s to 1.6 s (text finishes streaming at 1.5 s). The remaining empty stretch is the composer-only area, below 0.5 s of an empty panel.
6. **Shimmer visible at frame 0.** A `fromTo` with `autoAlpha:1` rendered at time 0 because `immediateRender` defaults to true; frame 0 showed a stray bar. Fixed with `immediateRender:false` (and `gsap.set(autoAlpha:0)` at build).
7. **Chip flight crosses text.** Mid-flight at 4.2 s the chip passes over the price area of card 1 (counter showing 0); it lands right of the title ("Gói Nhẹ" ends x 246, chip starts x 270 in card coordinates). Accepted: the flight is 0.7 s and the overlap is under 0.3 s.
8. **Counter starts after the card.** Cards arrive at 4.0 s, counters start at 4.4 s, so "0" shows for about 0.4 s. Not a held frame; start counters with the card if a calmer read is wanted.
9. **Frame-check tool not runnable.** `frame_check.py` needs numpy (missing) and the other pythons needed approval, so it was replaced by ffmpeg contact sheets (3 fps over 12 s, plus 0.7 s windows around both cuts). This is weaker: BLANK and TOPHEAVY numbers were not produced.
10. **agy image not available.** `motion_tools.py image` needed an approval; no agy image is in this build.

## 14. Weak spots, still assumed

- Frame 0 shows the chat half built (user bubble and composer, assistant text not yet): the style's "no hook, calm entrance" collides with "frame 0 finished composition". Accepted for a demo.
- Hand-computed contrast (+/-0.1), not a tool report, except the `validate` pass.
- Only one topic shape (t034) tried; list, ring and search recipes of other builds were not rebuilt.
- Silent: sound, captions, word anchors, karaoke highlight untested.
- Render: `render -q standard`, 2.5 MB for 12.0 s, 10.9 s render time, 360 frames, h264.
