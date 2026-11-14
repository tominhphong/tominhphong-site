# Style: developer workflow (9:16 Vietnamese "what a repo does" edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** A story about a code project told as a short arc: "something got big" (a number), "what it does" (a diff), "why it can be trusted" (checks go green, branch merges). Good for: open-source repository news, release or changelog notes, CI/CD explainers, "how a pull request works" lessons, dev-tool onboarding. Not for: finance dashboards with 4+ equal numbers (use saas-bento), enforcement or sad stories, anything where green/red would be misread as good/bad outside code, hype with no mechanism to show. Tier 2 never widens tier 1.

**Reading order.** Sections 1-12 are the design as built on 2026-11-14. Section 13 is the trap list from that build (newer fixes would go in later sections and win on conflict).

**Status / what was NOT exercised.** This document comes from a DEMO-ONLY build: one silent 12.0 s sample (`samples/sample-t028.mp4`, topic shape t028: "GitHub repository gains ten thousand stars in a week: what it does"), 1080x1920, 30 fps, no voice-over, no word timing, no music, no captions. **Voice, pronunciation, karaoke caption and sound rules were therefore not exercised;** sections 8 and 9 are carried from the profile and marked ASSUMED. All content on screen is generic and labelled "Minh hoạ"; no real repository, company, number or logo.

Source of values: `styles/profiles/developer-workflow.yaml`. Anything the profile does not give is **ASSUMED**.

Character: dark editor stage, warm but quiet. A number lands, a diff adds and removes lines, a branch forks and merges with one purple pulse. Energy 3: no shake, no flash, no glitch.

## 1. Tokens (contrast measured with the WCAG formula)

```css
--bg:#10131a;       /* page                                   ink 15.64:1 */
--surface:#171b24;  /* panels, pills                           ink 14.50:1 */
--border:#2f3540;   /* 1 px panel border */
--ink:#e8ecef;      /* headline, code, numerals */
--mute:#808891;     /* labels, line numbers, footer: 5.18 on bg, 4.80 on surface  (NOT on a diff-add band: 3.45) */
--accent:#4a74f0;   /* marks only (dot in the badge): 4.47 on bg, 4.14 on surface = FAILS as text */
--accent-ink:#8aa5f6; /* ASSUMED text-safe accent: 7.78 on bg, 7.22 on surface; key word in the headline */
--add:#3ab86e;      /* diff +, check fill, branch line: 7.31 on bg, 6.78 on surface */
--del:#ec6040;      /* diff - only: 5.59 on bg */
--merge:#b46ee8;    /* merge moment only: 5.61 on bg; headline word "hợp nhất" */
--warn:#c98126;     /* the star glyph: 5.89 on bg (decoration, never text) */
--empty:#1d222c;    /* empty activity cell */
```
Derived: diff-add band `rgba(58,184,110,.15)` (about #1d3a2d): ink on it 10.43:1; dark tick `#10131a` on add 7.31:1; white on the merge pill fill `#7a37b6` 6.89:1 (the profile merge `#b46ee8` is too light for white text: 2.9, so the pill uses the darker fill). Activity-grid ramp (5 steps): `#1d222c #173a28 #1f6b45 #2d9a5c #3ab86e`.

Colour rules (profile, confirmed): green/red only for diff lines and checks; purple only for the merge moment; blue for focus and the key word. The star is the single warm accent. No gradient text, no glow except the merge panel.

## 2. Fonts (local files in `assets/fonts`; the profile's Inter / JetBrains Mono / Be Vietnam Pro are not installed)

| Role | Used | Vietnamese check |
|---|---|---|
| Headline, labels, pills, footer | `SegUIVar.ttf`, weight axis 300-700; headline 700, `letter-spacing:-.02em` | all 36 test letters present (ắằẳẵặấầẩẫậếềểễệốồổỗộớờởỡợứừửữựơưỵỷỹ + đ), rendered "Một kho mã nguồn mở", "hợp nhất", "Đã hợp nhất" correctly in frames |
| Numerals, code, line numbers | `CascadiaMono.ttf`, weight axis 200-700 | all present (tested via the comment line "# ví dụ minh hoạ") |
| Editorial line | `cambriai.ttf` | not used in this build |
| Never | `segoepr.ttf` | lacks Vietnamese letters |

Declare faces with `font-display: block` and `font-weight: 300 700` / `200 700`. Keep identifiers in code lines ASCII (`doc_ma_nguon()`), as real code would be; Vietnamese only in comments and UI text.

### Type scale (1080 x 1920, px; measured in this build)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| badge "MINH HOẠ" | Seg 700, +.06em | 30 / 54 in a 56 px pill | always on screen, top left |
| `.h1` | Seg 700 | 72 / 1.12, max 3 lines | profile 72; key word in `--accent-ink` (merge scene: `--merge`) |
| counter numeral | Casc 600, -.04em | 170 (line box 170, needs 218 px to the unit line below) | tabular-nums |
| unit / grid caption | Seg 600 | 32 / 30 | `--mute` |
| code | Casc 400 | 34 / 72 row | profile says 22 px; acceptance floor here is 30 px, so 34 (about 39 chars fit a 960 px panel after the 150 px gutter) |
| file name | Casc 600 | 32 | |
| pills, check labels | Seg 600 | 32-34 | |
| merged pill / bar | Seg 700 | 38 pill, 54 text | |
| footer | Seg 400 | 26 | the one allowed line under 30 px: "Minh hoạ: nội dung giả định, không phải số liệu thật." |

## 3. Safe areas and grid (1080 x 1920)

```
y 0    -170  platform UI: empty
y 176  -232  badge "MINH HOẠ" (x 96)
y 270  -520  .h1 (x 96, 888 wide)
y 560  -1460 stage: counter + activity grid | diff panel | graph + checks
y 1290 -1440 merge bar (scene C)
y 1486 -1516 grid caption (scene A)
y 1560 -1590 footer
y 1600 -1920 empty (bottom UI)
x 96 - 984   content column (888 px); the diff panel is 960 wide (x 60-1020) to fit code
```
Scene A: counter panel x 96, y 630, 888 x 290; activity grid x 102, y 980, 13 columns x 7 rows of 60 px cells, 8 px gap (876 x 476). Scene B: diff panel y 560, 960 x 520, rows 72 px starting y 96 inside; pills y 1150 (height 64). Scene C: graph svg x 96, y 580, 380 x 640; checks panel x 520, y 580, 464 x 420 (rows 146 px apart, 128 tall).

## 4. Layers, back to front

`#dots` (CSS radial dot grid, 2 px dots `#2a303c` on 54 px pitch; 91 cells + the dots stayed far under the renderer's 40-gradient-element limit because the dot grid is ONE element) -> `#badge` -> scene A / B / C (`.scene`, one visible at a time) -> `#foot` -> `#fade` (bg colour, 1 -> 0 in 0.3 s at the start). No flash layer, no shake layer.

## 5. Components

- **Panel**: `--surface`, 1 px `--border`, radius 6, no shadow (profile).
- **Counter panel**: numeral left, star glyph right (SVG path, `--warn`), unit line under the numeral.
- **Activity cell**: 60 px, radius 6; level = seeded `rng(28)` plus a column ramp so later days are brighter (data reads as "rising").
- **Diff row** (72 px): line number (`--mute`, right-aligned in 84 px), sign column, code. `.add` band 15% green, `.del` band 15% red; the deleted text gets `line-through` and `--mute` at the strike moment.
- **Pill**: 64 px high, radius 32, surface + border, green `+` before the label.
- **Check row**: 56 px icon (spinner arc `--mute`, then a filled `--add` circle with a dark tick), 34 px label.
- **Graph**: main line `--mute` 6 px, branch line `--add` 6 px, commit dots 14 px radius with 5 px stroke, merge commit 20 px `--merge`.
- **Merge bar**: `--surface`, 1 px `--merge` border, pill "Đã hợp nhất" (fill #7a37b6) plus the sentence "vào nhánh chính"; a `box-shadow: 0 0 70px 14px rgba(180,110,232,.55)` on a separate element behind it (the only glow in the style).

## 6. Motion language

Allowed eases: `power3.out` (headline, panel), `power2.out` (rows, cells, checks), `power2.inOut` (graph draw, collapse), `back.out(1.4)` (star, pills, commit dots, check fill), `sine.inOut` (hold drift), `none` (counter, spinner, fades).

| Verb | Recipe (measured) |
|---|---|
| Headline | rise 30 px + fade, `power3.out` 0.5 s, 0.05-0.15 s after scene start |
| Counter | `{v}` 0 -> 10000, `ease:"none"`, 1.1 s from 0.35 s (done at 1.45 s), text via `onUpdate`, thousands separator "." |
| Activity grid | cell scale .6 -> 1 and colour to its level, 0.3 s, start `0.7 + col*0.05 + row*0.012` s: a left-to-right wave finishing about 1.8 s |
| Diff add | slide x -60 -> 0 + fade 0.4 s, one per 0.3 s (6.1, 6.4, 6.7 s) |
| Diff delete | strike (hard set at 5.7 s), then height 72 -> 0 and fade over 0.4 s (6.0 s) so the rows below collapse up |
| Pill | y 24 -> 0, scale .85 -> 1, `back.out(1.4)` 0.4 s, 0.2 s stagger |
| Branch / merge | main line draws 0.5 s; branch curve draws 1.3 s with `stroke-dashoffset`; commit dots pop 0.28 s apart |
| Checks | spinner turns 0.45 s, then fill + tick (0.25 s), one per 0.35 s from 9.2 s (profile: one per beat) |
| Merge pulse | purple ring scale 1 -> 3.2, opacity 1 -> 0, 0.7 s at 10.05 s; glow in 0.4 s; bar rises 40 px |
| Micro-motion | counter panel y 0 -> -6 yoyo (1.2 s), code panel -8 (0.5 s), merge bar -6 (0.7 s); nothing frozen > 1.5 s |
| Camera | locked off (profile's scroll and push not needed in 12 s) |

Transitions (profile set, measured): fade 0.15 s out then the next scene's headline rises in 0.05 s later (no ghost > 0.15 s). The profile's branch-off and merge-join are used INSIDE scene C (the branch is the content), not as a scene transition. The persistent badge, dots and footer keep the frame from going empty during the 0.15-0.3 s between scenes.

## 7. Scene recipes (12.0 s sample; for a full video lengthen holds, keep the order)

Timeline: A 0.0-4.2, B 4.2-8.4, C 8.4-12.0. The last 1.5 s (10.5-12.0) is the finished merge composition.

### A "Something got big" (stats; 0-4.2 s)
Headline "Một kho mã nguồn mở vừa nhận **10.000 sao** trong bảy ngày" (3 lines at 72 px). Counter panel at 0.3 s, counter done at 1.45 s, star pops at 0.5 s, activity grid wave 0.7-1.8 s, grid caption at 0.9 s. Hold 1.8-4.05 s with the panel drift. Exit: 0.15 s fade.

### B "What it does" (code / diff; 4.2-8.4 s)
Headline "Nó làm gì? Gom việc thủ công thành **một lệnh**". Panel at 4.35 s; context line 1 and comment line 5 at 4.7-4.8 s; the deleted line `lam_thu_cong()` at 5.0 s, struck at 5.7 s, collapsed 6.0-6.4 s; three added lines 6.1-7.1 s; three "+" pills 7.0-7.8 s naming the benefits. Hold with the panel drift to 8.25 s.

### C "Why trust it" (diagram + checks + merge; 8.4-12.0 s)
Headline "Xanh hết thì **hợp nhất**" (merge colour on the key word). Graph draws 8.5-10.1 s, three checks go green 9.2-10.25 s, the merge commit appears at 10.0 s with the purple ring pulse, the merge bar rises at 10.1 s. Hold to 12.0 s.

## 8. Captions (NOT exercised; profile only, ASSUMED)
Profile: surface pill, 1 px border, radius 8, 40 px Be Vietnam Pro 600 ink, current word accent. In 9:16 the contract's caption band is y 1370-1480 (bottom edge 1480): keep scene C's merge bar (y 1290-1440) and the footer (1560) out of that band when captions are added; move the merge bar up to y 1180 in a captioned build.

## 9. Sound (NOT exercised; profile only, ASSUMED)
Lo-fi or synthwave-lite 100-120 BPM; key taps, a soft tick per check, a warm swell on merge. No music or SFX were made in this build.

## 10. Images
None used (0 of the allowed 2). The style needs no photographs: every picture is built from panels, SVG and the dot grid. If one is added it is decoration only (dark, abstract, no text, no logo, no real person).

## 11. Must not

- No brand mascot, logo, wordmark, real repository name, real star count or real code from a real project; the star count in this style is an illustration and the screen says "Minh hoạ".
- Green/red only for diff lines, checks and branch lines; never as "good/bad" colour elsewhere.
- No light pastel theme, no heavy textures, no hype stutter cuts, no shake or flash.
- No text under 30 px except ONE footer line (26 px); no code under 30 px in 9:16.
- `--accent #4a74f0` and `--mute` on a coloured diff band are not text colours (4.47 / 3.45).
- Never `segoepr.ttf`.

## 12. Acceptance results of the sample (see `selfcheck.md`)
1080x1920, 12.0 s, 30 fps, 1.5 MB, silent; hyperframes lint 0/0, validate "10 text elements pass WCAG AA", inspect 0 layout issues; no empty panel > 0.3 s (the 0.15 s scene gap keeps badge, dots and footer); counter finished at 1.45 s and held 10.000 for 2.6 s; last 1.5 s = full composition.

## 13. Traps seen in real builds (written from THIS build, 2026-11-14)

1. **The preview was right and the render was wrong.** `hyperframes snapshot` showed scene A at 2.5 s and 3.2 s, but the rendered MP4 was a blank stage from 2.4 s to 4.2 s (1.8 s). Cause (measured: the same project rendered with `--workers 1` was correct, with the default workers it was not): the render splits the timeline across parallel workers (12 s / 5 = a chunk starting at 2.4 s) and each worker seeks straight to its chunk. Scene visibility that was set by `gsap.set(..., {autoAlpha:0})` outside the timeline plus `tl.set('#sA',{autoAlpha:1}, 0)` inside it lost the "at time 0" set. Rule: the first scene is visible by CSS; every later scene appears with `tl.fromTo(sel,{autoAlpha:0},{autoAlpha:1,duration:0.01},t)`; never rely on a `tl.set` at time 0; always check the rendered MP4 (tile sheet), never only the snapshot.
2. **`immediateRender:false` on single-use tweens shows the end state early.** After I copied the contract's flag onto every `fromTo`, scene B showed all diff rows, pills and the finished code at 5.0 s (planned 7.8 s). The flag is only for a shared layer reused by several tweens (flash, wipe). Rule: single-use element = plain `fromTo`; if two tweens on one element chain, only the later one gets `immediateRender:false` (the purple pulse ring needed exactly that: otherwise the ring sat visible before the merge).
3. **Lazy `.to()` is unsafe with parallel seeking.** Scene exits, the delete collapse and the spinner rotation were `tl.to` (start value read at first render). Rewritten as `fromTo` with explicit start values (`{opacity:1}`, `{height:72}`, `{rotation:0}`). Hold drifts (`y:-6`, yoyo) may stay `.to`.
4. **Text boxes overlap before the eye sees it.** `inspect` flagged `#num` (170 px line box) over `#unit` at 196 px: moved the unit to y 218 and grew the panel 250 -> 290. The deleted and added diff row share one row position on purpose: mark both `data-layout-allow-overlap`.
5. **Contrast of the profile's accent.** `#4a74f0` is 4.47:1 on bg and 4.14:1 on surface: fine for the badge dot, fails as text. Key words use `#8aa5f6` (7.78:1). White on the profile's merge purple fails (2.9), so the merge pill uses a darker `#7a37b6` (6.89:1). Mute text on the green diff band is 3.45:1: keep the comment line on the plain surface.
6. **Profile code size is too small for 9:16.** 22 px (profile) is below the 30 px floor and unreadable on a phone; 34 px mono gives about 39 characters per line in a 960 px panel, so code lines must be short (the longest here is 20 characters).
7. **Collapsing a deleted line leaves a gap at the bottom of the panel.** After `height 72 -> 0` the panel still had a 72 px hole above the last comment row and a tall empty bottom; the panel was shortened 640 -> 520 px and the pills moved up (y 1290 -> 1150). Scene B still ends at y 1214 with about 350 px of dark space above the footer: acceptable for a demo, but a full video should add a second element (for example a one-line result card) there.
8. **Small label collisions.** The grid caption sat 8 px under the last cell row (moved to y 1486); the "nhánh mới" label touched the main line and then the curve (moved left of the branch dots, right-anchored at x 226, y 346); the merge headline wrapped "hợp / nhất" on two lines at 72 px, so the copy was shortened to "Xanh hết thì hợp nhất".
9. **Counter on frame 0 and while counting.** The counter is mid-count from 0.35 s to 1.45 s (1.1 s), after that 10.000 holds; the headline is already readable at 0.3 s. Do not make a counter longer than about 1.1 s in a 12 s piece.
10. **Tooling gaps in this environment.** `frame_check.py` needs numpy, which was not installed (and not installable here), so the frame check was done with an ffmpeg tile sheet (`fps=4,scale=180:-1,tile=8x6`) read by eye, plus a fine sheet around each scene cut. GSAP loaded from the jsdelivr CDN at render time (works with network; for an offline machine vendor `gsap.min.js` into `assets/`).
