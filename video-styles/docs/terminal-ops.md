# Style: terminal-ops (9:16 Vietnamese news edition)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY).** This fit was observed in this build. The style suits stories whose subject is a command, a tool or a technical process with steps and states, such as CLI and developer-tool launches, release notes and changelogs, "how X works" explainers for APIs, rate limits, deploys and builds, and benchmark leaderboards for code tools. It is good when the story has 3-6 steps, statuses or flags that can each become one terminal line. It is weak for stories about people, money dashboards with many large numbers, emotional or human stories, and anything without a process. Tier 2 never widens tier 1.

**Reading order.** Sections 1 to 11 are the design as built and measured in the first real build (2026-11-11). Section 12 lists the traps seen in that build with the fixes. Where two sections disagree, section 12 wins.

**Clips and screenshots are optional.** This build used none. The style works without media: the terminal itself is the picture. Never fake terminal output that claims to be real: any illustrative output is labelled "minh hoạ" in the pane title.

**Example videos show the visual recipe, not the niche.** Copy how it is built, not what it is about.

**Status.** Written 2026-11-11 from one full build (51.1 s, story "DeployHQ `dhq launch`", 6 scenes) and two 10 s silent samples (API rate limit; benchmark leaderboard). The owner keeps it; it is not yet merged into the skill folder.

Profile: `skill/references/styles/profiles/terminal-ops.yaml` (energy 3, dark). The whole frame is one terminal session. Commands type in character by character, output lines snap in, spinners turn into check glyphs on the spoken word, and ASCII boxes and tables are drawn row by row. A clear screen is the cut, and the cursor survives it. Format: 1080 x 1920, 30 fps, VieNeu voice (about 3.9 words/s), no music, karaoke captions with estimated word times.
Marks: **ASSUMED** means the profile gives no value and this document invented one. **SUBST** means a named font is missing and a local one replaces it. **DEVIATION** means the build knowingly differs from the profile.

## 1. Tokens (contrast measured with the WCAG 2.x formula against #0c0f0a)

```css
:root{
  --bg:#0c0f0a;        /* profile                                                     */
  --ink:#d7e0d0;       /* profile; body text, commands          14.2:1                */
  --accent:#39ff88;    /* profile; prompt, success, current caption word  14.6:1      */
  --mute:#6b7a66;      /* profile; RULES AND FRAMES ONLY        4.2:1, fails as text  */
  --mute-ink:#8a9a84;  /* ASSUMED; pending lines, labels, footer 6.5:1                */
  --warn:#ffcc4d;      /* profile; warnings, "minh hoạ" tags    12.8:1                */
  --error:#ff5f56;     /* profile; 429, excluded, failures      6.4:1                 */
  --info:#5ccfe6;      /* profile; version lines, questions, headers 10.6:1           */
  --glow:0 0 8px rgba(57,255,136,.35);   /* profile text-shadow, on accent text only  */
}
```
- On the black caption bar (#000), ink measures 15.5:1, mute-ink 7.0:1 and accent 15.8:1.
- The agy phosphor backdrop (section 10) is lighter than #0c0f0a in the centre, about #17241a by eye. `hyperframes validate` measured against the real pixels: "80 text elements pass WCAG AA".
- Colour rule (profile): colour carries status only. Accent means done or prompt, warn means caution, error means rejected or excluded, info means metadata. A headline takes accent, warn or error only on the word that states the status: accent "LINK ĐANG CHẠY", warn "MỌI TỆP", error "VÌ SAO BỊ CHẶN".

## 2. Fonts (SUBST: JetBrains Mono and Be Vietnam Pro are not installed)

| Role | Profile asks | Used | Vietnamese |
|---|---|---|---|
| Everything on screen except captions | JetBrains Mono 500/700/800 | `CascadiaMono.ttf` (variable 200-700). Text 500, headline 700, no 800 (ASSUMED) | Owner doc check with fontTools (saas-bento, 2026-11-03): all 36 test letters present. This build: every held frame inspected by eye. Ệ Ồ Ẫ Ở Ữ Ỹ đ, with stacked marks in uppercase 72 px, rendered whole |
| Captions | Be Vietnam Pro 600 | `SegUIVar.ttf` 600 | Same check, all present |
| Box drawing, Braille spinner, arrows, check | | ┌─┐│└┘ ╔═╗║╚╝ ├┤┬┴┼ ⠋⠙⠹⠸⠼⠴⠦⠧⠇⠏ → ▼ ↑ ✓ ✗ █ ░ all rendered in snapshots | Not checked whether ✓/✗ come from Cascadia or a system fallback (fontTools could not run in this environment, see 12.11) |
| Never | | `segoepr.ttf` (it lacks Vietnamese letters); `cambriai.ttf` (a serif, against the profile's "avoid serif") | |

Declare each face with `font-display:block` and a weight range (`200 700`, `300 700`).
Cascadia Mono advance = 1200/2048 em = **0.5859 em**. The typing helper uses this value to size the reveal width. At 36 px a character is 21.1 px, so the 880 px pane text width holds **41 characters**. At 40 px it holds 37, and at 72 px (headline) 22 per line in 960 px.

### Type scale as built (px)

| Token | Font | Size / line | Notes |
|---|---|---|---|
| status line | Cascadia 500 | 30 / 52 | `● dhq · deployhq-cli` left, `bước n/6` right in mute-ink |
| `.hd` headline | Cascadia 700 uppercase | 72 / 86 | 2 lines, each 22 characters or fewer, explicit `<br>`, status word coloured |
| pane title | Cascadia 500 | 30 / 36 | sits on the top frame line: `┤ minh hoạ · theo tài liệu DeployHQ ├` |
| command line | Cascadia 500 | 40-48 / 52-60 | `$` or `~/du-an $` in accent |
| output / step lines | Cascadia 500 | 36-40 / 50-92 | step lists use line-height 92 (5 steps fill 460 px) |
| ASCII box / table | Cascadia 500 | 36-42 / 46-52 | boxes 28-36 characters inner width |
| footer comment | Cascadia 500 | 30 / 40 | `# nguồn: ...`, the single footer line, at y 1226 |
| caption | Segoe 600 | 44 / 58 | see section 8 |

No text is below 30 px. Line-height is at least 1.2 for anything uppercase with stacked marks.

## 3. Safe areas and grid (1080 x 1920)

```
y   92 - 156   status line (1 px mute rule at the bottom)
y  196 - 368   headline, 2 lines x 86
y  452 - 488   pane title on the frame line
y  470 - 1300  PANE: 960 x 830 at x 60, 1 px mute frame, text column x 100 - 980
y 1226 - 1266  footer comment inside the pane (always present; the lowest content edge is therefore 1262-1266 on every frame)
y 1372 - 1528  caption bar (black, 1 px mute top rule), text box y 1388 - 1512
y 1528 - 1920  empty (platform UI)
```
- Split panes (tmux feel): a 1 px mute line across the pane at y 950-1000. Below it sits a sub-pane with a solid `--bg` fill, so the sliding pane never shows what is behind it.
- Samples have no captions. There the pane is 900 px high (470-1370), the footer comment sits at y 1300 and a 34 px warn "Minh hoạ: ..." tag sits at y 1420.

## 4. Layers, back to front

`#bgimg` (agy phosphor still, opaque, full frame) -> `#scan` (one repeating-linear-gradient, 1 px line every 4 px at 4 % ink: the profile's "baked scanlines" without a PNG) -> `#status` -> `#pane` frame + `#ptitle` (persistent across scenes) -> one `<section class="sc">` per scene (headline + pane content, `display:none` unless active) -> `#capbar` -> `#caps`. The layers do not include flash, shake, fade or beat pulse.

## 5. Components

- **Prompt + typed command**: `<span class="ac">$ </span><span class="ty">dhq launch</span><span class="cur"></span>`. `.ty` is an inline-block with `overflow:hidden; white-space:pre; padding:.2em 0; margin:-.2em 0`. The padding keeps tone marks inside the clip box.
- **Cursor** `.cur`: an accent block 0.56 em x 1.0 em with glow. Blink = 0.4 s on and 0.2 s off by visibility sets, finite, and only on the scene's last prompt.
- **Spinner line**: `<span class="sp" data-f="⠋">` with `::before{content:attr(data-f)}`. The frames are set through GSAP `attr` at 12 fps. On the spoken word the attr becomes `✓` (`data-s="ok"`, accent + glow), `✗` (error) or `!` (warn). The line's text turns from mute-ink to ink, or to error or warn, in the same frame.
- **ASCII box**: `box(lines, inner, "s"|"d", cls)` builds rows from real box characters, padded to the inner width with spaces (pad by code points). Single line for neutral content, double line for the hero (accent) or a warning (warn). Each row is one `<span class="row">` revealed row by row, 0.04-0.08 s apart.
- **ASCII table**: columns 14 + 24 characters (full video) or 4 + 18 + 14 (sample). `├─┼─┤` separators sit between groups. Rows reveal on the spoken word of the row.
- **Tree view**: `├──` / `└──` rows with a status glyph column at character 22 (`↑ tải lên`, spinner then `✗ loại ra`).
- **Selection bar**: a `rgba(57,255,136,.14)` fill with a 6 px accent left border behind the selected option box. It moves 168 px in 0.2 s `power2.inOut` on the spoken word. This is the only eased move inside a pane.
- **Block bar** (sample t035): `[█░░░░]` as attr text, one block per completed request. It turns error colour when the quota is used up.
- **Footer comment**: `# nguồn: ...`, mute-ink 30 px, static for the whole scene.
- **Decorative still** (`#rackbox`, scene 6): a framed 880 x 230 crop of the agy rack picture with a 40 px linear drift. It is atmosphere only and is never placed near a number.

## 6. Motion language (energy 3, stepped)

The profile constraint "text reveals stepped per character or line, never faded" binds. No text element ever has an opacity tween.

| Verb | Recipe as built |
|---|---|
| typeIn | `fromTo(el,{width:0},{width:n*0.5859*fs+2, ease:"steps(n)", duration:n/cps})`, then `set(width:"auto")`. Commands 40-60 cps, version lines 70 cps, headlines 120 cps (the profile says 22 cps; DEVIATION, because a 30-character headline at 22 cps holds a half-typed title for 1.4 s and breaks acceptance item 3) |
| line snap | `tl.set(row,{visibility:"visible"},t)`, stagger 0.04-0.12 s |
| spinner -> glyph | 12 fps attr frames from the line's arrival to the spoken word, glyph on `W(word)` |
| clear-screen cut | at the scene start: previous section `display:none`, next `display:block`, status `bước n/6` updates; headline types over; first pane line from S+0.05 |
| pane-split | sub-pane `fromTo x 980 -> 0`, 0.4 s `power2.inOut`, starting 0.45 s before its spoken word |
| key-line zoom | warning box `scale 1 -> 1.06` (0.35 s `power2.inOut`) on the spoken word, back to 1 when the next pane splits in. The profile asks for 1.6; DEVIATION, because at 1.6 a 36-column box exceeds 960 px and the text would be cut by the frame edge |
| scroll-push (sample t027) | the old table is hidden and the new order shown at once, y 50 -> 0 in `steps(2)` over 0.2 s |
| micro-motion in holds | spinners turning, the cursor blinking, the rack drift. Camera locked-off (profile) |

There are no counters. Numbers are static text that appears with its line (no "held mid-count" risk). Timing anchors: `W(sid, fragment)` = the estimated onset of the first word containing the fragment. Spinners resolve exactly on it; lines and boxes arrive 0.1-0.15 s before it.

## 7. Scene recipes (S = scene start; times as built)

- **R1 Hook, before -> after diagram (7.5 s).** Frame 0 is final: the headline, `~/du-an $ dhq launch█`, box A "THƯ MỤC MÃ NGUỒN" and the footer. The arrow rows reveal on `W("ra")`, double-line accent box B "LINK ĐANG CHẠY THẬT" on `W("đường")` with a spinner that resolves on `W("thật")`, and the two-line tool label on `W("công")`.
- **R2 Step list (8 s).** The command types at S+0.05. Five spinner lines (pending, mute-ink) snap in from S+0.1 at 0.05 s. Each resolves to `✓` on its own spoken verb ("xem", "nhận", "dựng", "triển", "trả"). This is the signature scene: the voice walks the list and the checks follow it.
- **R3 Choice + dry run (7.7 s).** Command, the `? chọn chỗ chứa` question in info, two option boxes with their flags (`--static`, `--vps`), and the selection bar on `W("hosting")` that moves on `W("máy")`. The sub-pane splits in before `W("muốn")` and types `dhq launch --dry-run --json` at 30 cps, then `→ xem trước chi phí và các bước`.
- **R4 Warning quote + tree (11.7 s; internal cut-in by the split).** A version line in info, then a double-line warn box. It holds the English sentence verbatim, the Vietnamese gloss in warn, and "(trích nguyên văn ghi chú v0.25.0)" in mute-ink. The box zooms to 1.06 on `W("mọi")`. At `W("vì")` the tree pane splits in, and its `✗ loại ra` marks land on `W("script")` and `W("cấu")`.
- **R5 Spec table + install (9.6 s).** Table frame and first group at S+0.05, `số lệnh | hơn 60` on `W("sáu")`, `hệ điều hành` on `W("macos")`. `$ dhq skills install` types 0.6 s before `W("claude")`, and the three agent names resolve to checks on their own names.
- **R6 Soft ending (6.6 s, including a 1.0 s silent tail).** A version line, a status block with two spinners (accent `✓ miễn phí: giai đoạn thử nghiệm` on `W("miễn")`, warn `! sau đó: có thể tính phí` on `W("tính")`), the framed rack still at S+0.3, the recap line `kho mã ──▶ dhq launch ──▶ link` on `W("sau")`, and a blinking `~/du-an $█` to the last frame. There is no fade: the last 1.5 s are the full composition.
- **Sample recipes.** t035: a quota box, a block bar, request log lines whose spinners resolve to `200 OK`, a sixth that resolves to `✗ 429 Too Many Requests`, a warn `Retry-After` box, and a new window with one more `200 OK`. t027: a leaderboard table drawn row by row, `bench run` with two spinners, the score resolving, and the table re-ordered with the new row highlighted.

## 8. Captions

- The bar is black, full width, y 1372-1528, with a 1 px mute top rule (profile). Text is Segoe 600 44 px / 58, centred in 960 px, with at most 2 lines.
- Chunks: split after `, . : ?` once 3 words are in, or at 7 words. A tail under 3 words merges into the previous chunk (at most 9). Chunks never cross a scene end. The first chunk of a scene starts at S, and each chunk stays until the next one starts, so the bar is never empty.
- Word states use `tl.set` only, with no fades: unread mute-ink, current accent, read ink.
- The caption DOM is `.cap` (flex centring) containing ONE inner `<div>` with the word spans (see trap 12.2).
- Captions carry the spoken words: numbers appear in words ("không chấm hai mươi lăm"), while the pane shows the digits (`v0.25.0`, `06/11/2026`, `hơn 60`).

## 9. Sound

This build has voice only (VieNeu "Hải Đăng"), with no music or SFX: those media tools were unavailable. The full profile calls for dark synth or minimal techno at 100-120 BPM, quiet key-tap clicks (vol 0.15) while typing and a soft blip on each check, with no whooshes. Without music the "cursor blink locked to beats" rule became a fixed 0.6 s cycle.

## 10. Images (agy)

Images are atmosphere only. The terminal is drawn in HTML, never in an image.
- `phosphor` worked as the backdrop. The prompt asked for an almost black #0c0f0a background with an extremely faint dark-green phosphor glow, like an old monochrome monitor glass, with fine scanlines, a vignette, no objects and no text. The output is 768 x 1376 with a centre lighter than #0c0f0a (about #17241a), used full frame with `object-fit:cover`.
- `rack` worked as a decorative strip. The prompt asked for a macro of server rack status LEDs in green and amber, with bokeh, near black, no text, labels, people or screens. It was used as an 880 x 230 crop (`object-fit:cover`, margin-top -130).
- Do not ask agy for a screen, code or a terminal: it would draw fake text. Do not ask for "matrix" visuals (profile avoid).

## 11. Must not

- Do not fade text in or out (profile constraint). Do not use glossy window chrome, glass, gradients on text, matrix rain, serif or display fonts, or emoji.
- Do not use decorative colour: every coloured word states a status.
- Do not use `--mute` (#6b7a66) for text (4.2:1).
- Do not show terminal output that pretends to be a real log. Illustrative output carries "minh hoạ" in the pane title; quoted release text says "trích nguyên văn".
- Do not show a number or name that no opened page states, and do not use a fake URL (the hook says "LINK ĐANG CHẠY THẬT" instead of inventing a domain).
- No element may be visible in a section that is not active (trap 12.1). Do not use a zoom that pushes text past the frame.
- Do not speak an acronym of a US organisation. "MIT" (the licence name) was cut from both the voice and the screen for this reason.

## 12. Traps seen in real builds (2026-11-11, video "deployhq-dhq-launch", 51.1 s; samples t035 and t027)

1. **Visibility inheritance.** Sections were hidden with `visibility:hidden` while their rows were revealed with `visibility:visible`. A child set to visible shows even inside a hidden parent, so the first snapshot set showed every earlier scene stacked under the current one (scenes 1-3 all visible at 23.8 s). Fix: toggle sections with `display:none/block` sets. The same bug came back in sample t027, where the old leaderboard stayed under the new one at 9.8 s, and got the same fix. **Rule: hide containers with `display`, reveal leaves with `visibility`.**
2. **Captions lost their spaces.** Word spans joined with `" "` directly inside the flex `.cap` rendered "Mộtdònglệnh". Flex drops whitespace text nodes between items. Fix: one inner `<div>` holds the spans.
3. **Lint error `template_literal_selector`.** `querySelectorAll(\`#${id} .hd .ty\`)` fails the HyperFrames bundler. Use `getElementById(id).querySelectorAll(".hd .ty")`.
4. **Table ran into the command line.** In scene 5 the 9-row table at line-height 50 ended at y 966, but the command sat at 900, and the two overlapped in the 43.9 s snapshot. Fix: line-height 46 (ends 926), command at 956, output at 1022 with line-height 62 (ends 1208), above the footer at 1226. **Rule: compute every block's bottom (rows x line-height) before placing the next one.**
5. **Clear-screen cut = near-empty frames.** `frame_check.py` flagged BLANK at 23.0 s (the s3 -> s4 cut). The frame shows the status line, the frame, a half-typed headline "MỌI" and an empty pane, because the first content started at S+0.3. After moving every scene's first content to S+0.05-0.12 the flag stayed (that 2 fps sample lands 1-2 frames after the cut), so it was accepted as well under the 0.5 s limit. Next time, show the first pane line at S exactly, with no typing.
6. **Half-typed headline at 80 cps.** The 7.6 s snapshot showed "TỪ KHO MÃ / Đ" and 15.7 s showed "XEM". At 120 cps a 2-line headline finishes in 0.2-0.3 s.
7. **Sample t035 overlap.** The 7th log line (line-height 54, reaching y 1134) overlapped the retry box at 1104. Fix: log line-height 50 (ends 1102), box at 1118 with 34 px / 42 (ends 1286).
8. **Mute fails as text.** The profile's mute #6b7a66 measures 4.2:1 on the bg. The ASSUMED token `--mute-ink` #8a9a84 (6.5:1) carries all grey text, and #6b7a66 is used only for rules and frames.
9. **Voice length.** The first script had about 230 words and ran 61.06 s, over the 58 s limit. Trimmed to 195 words: 50.10 s of voice (3.9 words/s with 0.35 s gaps). Video = voice + 1.0 s tail = 51.1 s. Scenes ran 7.47 / 8.03 / 7.71 / 11.71 / 9.55 / 6.63 s. For this voice, aim at 190-200 words for 50-55 s.
10. **Story shape vs real story.** No story from the last 48 h matched "CLI turns a README into a deployment". The nearest real one was DeployHQ's `dhq launch`, released in v0.25.0 on 06 Nov 2026 (5 days old). It inspects the repository, not the README. The script says only what the pages say ("xem kho mã"), and the mismatch is recorded in the manifest. Do not bend the facts to fit the shape.
11. **Environment limits.** Arbitrary `python3 <script>` and `node -e` calls needed approval here, so the fontTools glyph check could not run. The diacritics check is visual (snapshots at 72 px uppercase), plus the earlier fontTools result in the saas-bento owner doc for the same two font files. The word timing is computed inside the page from the scene text, start and speech length, the same character-share formula `motion_tools.py` uses, so no build script is needed.
12. **Tool facts (hyperframes 0.7.26).** Lint: 0 errors, 2 warnings (an `overlapping_gsap_tweens` false positive on the zoom box and `composition_file_too_large` at 314 lines). Validate: no console errors, 80 text elements pass AA. Inspect: 1 warning about the rack image overflowing its crop box, removed with `data-layout-allow-overflow`, plus info notes about off-canvas sub-panes before they slide in, which are intended. Render took 79 s for 51.1 s. Silent file 4.9 MB, final 5.0 MB, -15.4 LUFS, peak -4.0 dBFS. Samples took 30 s each and came to 1.0 MB.
