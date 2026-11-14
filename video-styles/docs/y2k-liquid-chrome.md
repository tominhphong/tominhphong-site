# Style: Y2K liquid chrome (9:16 fashion-drop edition)

## 0. Read this first: niche, status, what was and was not exercised

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit (REFERENCE ONLY), observed in this build:** a launch or "drop" with ONE hero object and 2-3 short claims: limited product releases (sneakers, accessories, merch), music or event promos, youth-brand and social cuts. Good for hype, shine, optimism. Not for dense numbers, sad or serious news, enforcement, finance dashboards, code, long explainers (profile `avoid`: dense text).

**Status.** Written 2026-11-14 from ONE demo build: a silent 12.0 s sample on topic shape t084 ("a fashion brand launches a limited sneaker drop", Jev fit 0.76). No owner document existed. **Voice-over, word timing, captions, music and SFX were NOT exercised** (demo build): sections 8 and 9 are inherited from the profile and marked ASSUMED. Everything else is measured on the build unless marked ASSUMED.

**Content rule used.** Generic, invented-on-purpose content; every beat carries the label "Minh hoạ" (top-left pill, always on). Real use must replace it with sourced facts.

Source of values: `styles/profiles/y2k-liquid-chrome.yaml` (energy 4, mixed palette, bpm 112-128 unused here).

## 1. Tokens

```css
--bg-top:#bcd2ff; --bg-mid:#dfe8ff; --bg-bot:#f3dcff;   /* sky gradient 180deg, 0/45/100% */
--ink:#101422;     /* 15.0:1 on #dfe8ff, 12.1 on #bcd2ff, 14.5 on #f3dcff, 18.4 on white */
--deep:#1b1f3b;   /* secondary text, ~13:1 on bg-mid */
--accent:#ff5cd6; /* fills, bubbles, shadows ONLY: 2.2:1 on bg-mid, never text */
--cyan:#4ff0ff; --lime:#c6ff3d; /* bubbles / button gradient ONLY */
--chrome: linear-gradient(180deg,#fff 0%,#9aa3b5 44%,#2a2f45 52%,#e6ebf5 100%);
```
All ratios hand-computed with the WCAG formula (no tool was available in the session; treat the 2nd decimal as approximate).
- Chrome text is a display graphic, not body text: its bands range from 1.2:1 (white band) to ~10:1 (dark band) against bg-mid. It is legible only at >= 150 px and with the drop shadow `0 6px 0 rgba(27,31,59,.35)` plus a pink glow. Never use chrome below 150 px.
- Text colours that are safe: `--ink`, `--deep`. Text on the pink-cyan button: ink on #ff5cd6 = 6.8:1, on #4ff0ff = 13.4:1.

## 2. Fonts (3 local files; the profile's Unbounded / Syne / Space Mono are not installed)

| Role | Profile | Used | File |
|---|---|---|---|
| Chrome display | Unbounded 800 | Segoe UI Variable 900 | SegUIVar.ttf |
| Subhead, chips, button | Syne 700 | Segoe UI Variable 800 | SegUIVar.ttf |
| Tech label, "Minh hoạ" tag | Space Mono | Cascadia Mono | CascadiaMono.ttf |
| Soft accent line | (none) | Cambria Italic | cambriai.ttf |

Never use segoepr.ttf (no Vietnamese letters). **Diacritics check (measured by snapshot):** Ỉ Ị Ộ Ầ Ă Ê Ô Ơ Đ ờ ạ ợ all rendered with correct marks in SegUIVar 900, Cambria italic and Cascadia Mono. SegUIVar is a variable font: declare `font-weight:100 900` in @font-face or 900 falls back to bold.

### Type scale (1080 x 1920, px, as built)
| Element | Size |
|---|---|
| Hero chrome word (DROP) | 300 |
| Two-line chrome headline (CHỈ MỘT LẦN) | 210, line-height 1.12 |
| Chrome figure (500 ĐÔI) | 150 |
| Subhead | 52, tracking .04em |
| CTA button | 54 |
| Chips | 44 |
| Soft italic line | 64 |
| Mono kicker | 36, tracking .12em |
| "Minh hoạ" tag | 32 |
Smallest text = 32 px (limit 30).

## 3. Safe areas and grid
Frame 1080x1920. Content lives x 40-1040, y 150-1750. Tag pill at left 60, top 150. Hero zone y 420-1300; claims and CTA y 1240-1700. The bottom 170 px stay as background and bubbles (platform UI zone; no caption band was needed in this demo; ASSUMED caption band y 1330-1750 per frame_check's 0.69 body split). Centered single column, hero object centred on x 540.

## 4. Layers, back to front
1. Sky gradient. 2. Hero disc / chrome words. 3. Bubbles (conic iridescent ring with 56% hollow mask and a white highlight) and 4-point sparkles (clip-path star + cyan glow). 4. Chips and button. 5. "Minh hoạ" tag (z 50). 6. Swoosh ribbon and flare layers (transition only, opacity 0 outside it).
Count on screen: max 5 bubbles+sparkles per beat (limit 20).

## 5. Components
- **Chrome word:** gradient fill via background-clip:text + two drop-shadows. Highlight band sweep was NOT built (see traps).
- **Iridescent bubble:** 110-260 px ring, `conic-gradient(from 200deg,#ff5cd6,#4ff0ff,#c6ff3d,#ff5cd6)` masked to a ring.
- **Hero disc:** 800 px circle, radial white-cyan-pink gradient, hard offset shadow `0 40px 0`. The product sits inside, rotated -8 deg.
- **Chip:** white 90% pill, 44 px ink text, padding 22/44, hard pink or cyan offset shadow 14 px.
- **Gloss button:** 780x150 pill, pink-to-cyan gradient, top gloss ellipse (white 80% to 0), shadow 0 16px 0.
- **Sparkle:** 70-90 px.

## 6. Motion language (energy 4, no shake)
- Entrances only are elastic: `elastic.out(1,0.6)` 0.7-0.8 s for words and bubbles; `back.out(2)` 0.4-0.6 s for chips, button, sparkles.
- Hold motion: hero words and bubbles drift y -12 to -16 px, sine.inOut yoyo, 1.2-1.5 s per leg.
- Button press: scale .94, 0.12 s yoyo at 10.6 s.
- Transition = **chrome swoosh**: 1200 px skewed ribbon (white-cyan-pink), x 0 to 2600, 0.5 s power3.inOut; the beat swap happens under it at its midpoint. Used twice (3.65-4.15 s, 8.0-8.5 s).
- Flare: full-frame radial white, opacity 0 to .9 in 0.08 s, out in 0.25 s, on the hero reveal at 4.3 s.
- No tween starts before 0; no random.

## 7. Scene recipes (S = beat start; timings as built, total 12.0 s)
### R1 Hook (S=0, to 4.0)
Tag in at 0.1; mono kicker 0.2; chrome word DROP scale .4 to 1 elastic at 0.3 (hero 300 px, y 600); subhead 1.1; three bubbles staggered 0.7/0.85/1.0; two sparkles 0.9/1.1. Swoosh out 3.65.
### R2 Hero object (S=4.0, to 8.45)
Hero disc elastic in at 4.1, product (rotation -30 to -8, scale .3 to 1, back.out 1.7) at 4.3 with flare; chrome figure at 5.0; chip 1 at 5.9 from left, chip 2 at 6.2 from right (stagger .3). Everything settled by 6.8, so ~1.65 s of held full composition before the swoosh at 8.0. Product art here is a CSS/SVG chrome sneaker silhouette (no agy image, see traps).
### R3 Closing CTA (S=8.45, to 12.0)
Chrome headline elastic at 8.55; italic line 9.2; gloss button 9.6; press 10.6; bubbles 8.8-9.1; sparkles 9.0/9.2. Full composition from 10.2 s on (1.8 s hold; requirement 1.5 s).

## 8. Captions (NOT exercised)
No voice, no captions in this demo. ASSUMED from the profile: white pill rgba(255,255,255,.8), 44 px 700 ink text, current word #ff5cd6 is NOT text-safe (2.2:1): use ink on a pink pill instead. Be Vietnam Pro is not installed; use SegUIVar 800.

## 9. Sound (NOT exercised)
ASSUMED from the profile: 112-128 BPM bubblegum or UK garage; glassy swoosh on each transition, sparkle chime on reveals, flare cut on the drop. Swoosh times 3.65 and 8.0 and flare 4.3 are ready cue points.

## 10. Images (agy)
None used (the `image` command needed approval that was not granted in this session). Plan for a real build: at most 2 images, the hero product on pale sky with no text or logo, baked to JPG and placed inside the hero disc. Never use a real brand's shoe.

## 11. Must not
- Live SVG lighting filters or blend-mode chrome; chrome is a gradient fill only.
- Chrome text under 150 px; pink, cyan or lime as text colour.
- Matte flat palettes, grain, dense text, code, terminals.
- More than ~20 bubbles and sparkles; elastic eases on anything but entrances.
- Fake brand, price or spec; keep "Minh hoạ" until facts are sourced.

## 12. Traps seen in real builds (THIS build, 2026-11-14)
1. **Stuck transition layer.** `fromTo` on the shared swoosh with the default immediateRender painted its start state (opacity 1, x 0) from time 0: a pink wedge sat in the top-left corner for the whole of beat 1 (visible in snapshots at 1.8 s and 3.0 s). Fix: `tl.set("#swoosh",{opacity:0},0)` AND `immediateRender:false` on both fromTo's. After the fix the layer is absent at 0-3.6 s.
2. **Chrome diacritics collide.** Two-line chrome headline at 230 px with line-height .95: the dot of Ị and the circumflex of Ầ in "CHỈ MỘT / LẦN" overlapped (seen at 10.0 s). Fix: line-height 1.12 and size 210 px; marks clear the next line. Use >= 1.1 for every Vietnamese all-caps chrome line.
3. **Chrome is faint on a sky background.** The white top band of the gradient is 1.2:1 against #dfe8ff; "DROP" reads only because of the dark mid band and the shadow. Keep size >= 150 px and the shadow, do not lighten the dark band.
4. **Highlight-sweep band not built.** The profile's signature move (a highlight sliding across chrome text) was skipped in this demo: it needs a clipped overlay per word, risking a mid-sweep cut-off frame. Add it next build on a kick, as a masked gradient inside the text element.
5. **`frame_check.py` could not run**: it imports numpy, which was missing, and installing was not permitted. The check was done manually from a 2 fps contact sheet (see selfcheck.md). Install numpy before the next build.
6. **Beat swap under the swoosh** at the ribbon midpoint hides the cut; the outgoing beat has zero ghost frames (b1 hidden at 4.0, b2 at 8.45, swoosh covers 3.65-4.15 and 8.0-8.5).
7. **Empty bottom third in R1.** The hook keeps content above y ~1500; bubbles fill y 1120-1500 only. Acceptable on a hook, but in a real build place a claim or product there.
8. Lint, validate and inspect gave 0 errors and 0 issues at first pass; the problems above were only visible in the snapshots, so always read the PNGs.
