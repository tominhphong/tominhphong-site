# Style: monochrome-developer (9:16 Vietnamese edition, first document, written from the t029 demo build)

## 0. Read this first: niche, reading order, status

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY, observed in this build).** A command-line or developer-platform tool that turns an input into a running result: a README into a deployment, a build log into a "ready" state, a deploy or install flow, an infrastructure or launch-week announcement. It is built for log-driven, step-by-step "one command in, one result out" stories with 3 to 6 short mono lines. Not for warm human stories, many-number dashboards, mood pieces or anything that needs a colour palette. Tier 2 never widens tier 1.

**Status.** DEMO-ONLY build, 2026-11-14: one silent 12.0 s sample (`samples/sample-t029.mp4`), topic shape t029 "command line tool that turns a README into a deployment" (Jev fit 0.77). Voice-over, word timing, captions, music and SFX were NOT exercised: sections on captions and sound are inherited from the profile and untested. Content on screen is generic and labelled "Minh hoạ".

Profile: `skill/references/styles/profiles/monochrome-developer.yaml` (energy 3, dark, family brand-inspired). Black canvas, 1 px grid with plus marks, a terminal with a log burst that ends in "Ready", a soft spotlight beam. Marks: **SUBST** = a local font replaces the profile's font. **DEVIATION** = knowingly differs from the profile.

SUBST 1: Inter Tight -> `SegUIVar.ttf` (headline weight 700). SUBST 2: JetBrains Mono -> `CascadiaMono.ttf`. SUBST 3: the profile's Be Vietnam Pro captions are not installed; captions would use SegUIVar (untested).
DEVIATION 1: the profile gives mono logs 20 px and kicker 16 px (scaled 24). For 1080 x 1920 and the 30 px floor, logs are 32 px and kicker 30 px.
DEVIATION 2: the profile bakes the beam as a PNG at 20%. This build used one CSS element (clip-path polygon plus a linear-gradient with alpha inside the colour, element opacity 1) because no image tooling was available. One element, no renderer problem seen.
DEVIATION 3: cell borders use #383838, not the profile's line colour, see section 1.

## 1. Tokens

```css
:root{
  --bg:#000000;      /* profile bg */
  --ink:#ededed;     /* 17.9:1 on bg, 16.9:1 on surface */
  --mute:#a1a1a1;    /* 8.1:1 on bg, 7.7:1 on surface: allowed for text */
  --white:#ffffff;   /* headlines, solid pill, 21:1 */
  --line:#1f1f1f;    /* grid rules = rgba(255,255,255,.12) flattened on black; 1.27:1, non-text */
  --edge:#383838;    /* cell borders, DEVIATION 3, 1.7:1, non-text */
  --surface:#0a0a0a; /* cells */
  --ok:#4bd69a;      /* 11.4:1 on bg, 10.8:1 on surface: status dot, check, "ok", the Ready line only */
}
```
Contrast was computed by hand with the WCAG formula (python was not usable in this build); `hyperframes validate` independently reported "10 text elements pass WCAG AA". `--err #ff6a4d` (7.4:1) is in the profile and was not used. Rules: text only from `--ink --mute --white --ok`; flatten every alpha colour to a solid hex so no element sits below 90% opacity; the only alpha is the beam gradient (a texture, not text). Headline sits over the beam (white at 20% over black = about #333): white text still above 12:1. Never put a colour other than `--ok` on screen.

## 2. Fonts

| File | Role | Vietnamese |
|---|---|---|
| `SegUIVar.ttf` | headlines (700, -0.05em), UI text (600), body (400), pill text | rendered correctly in the build for: ư ơ ă â ê ô đ and tone marks including ở ẩ ể ử ạ ụ ỉ |
| `CascadiaMono.ttf` | kicker, logs, timestamps, README lines, address field, footer | rendered correctly in the build for: ứ ụ ư đ ẩ ặ ư ẽ and all log lines |
| `cambriai.ttf` | unused | not needed |
| `segoepr.ttf` | NEVER (92 missing Vietnamese letters, per the fluent-productivity document) | - |

The fontTools glyph test (all Vietnamese capitals and lower case) could NOT be run in this build because running a python script was refused by the sandbox; it must be run before any full video. What was checked: every character on screen was looked at in snapshots and in the rendered contact sheet, no fallback glyph or tofu seen. Both fonts are variable: declare `font-weight: 100 900` in `@font-face`, otherwise bold is synthesised.

## 3. Grid and safe areas (1080 x 1920)

- Vertical rules x=72 and x=1008 over the whole height; horizontal rules y=200, 560, 1640. Plus marks (28 px, 2 px stroke) at the 6 intersections.
- y 0-200 status zone: only the kicker "MINH HOẠ" (mono 30 px, tracking 0.12em, mute) at y 128. y 200-560 headline block (two lines). y 580-960 zone A (380 px, one cell, swaps per beat). y 1000-1600 terminal cell (600 px, persistent). y 1634 footer line (26 px, the one allowed text under 30 px). y 1650-1920 empty.
- Cells: x 72, width 936, 1 px `--edge` border, radius 6, fill `--surface`.
- Measured: 4 lines of content fit zone A only at 32 px / 50 px line height (5 README lines at 54 px overflowed the cell by 11 px, see Traps).

## 4. Layers, back to front

1. `#root` black. 2. `#world` camera wrapper, scale 1.00 -> 1.02 linear over 12 s (profile: locked-off, a slight settle). Inside it: beam (z lowest), grid rules, plus marks, kicker, headline stack, zone A cells (3 stacked, one visible), terminal, footer. No caption layer (not exercised). No flash layer, no fade at the end.

## 5. Components

- **Cell**: surface fill, 1 px edge, radius 6, header strip 76 px (mono 30 px mute, bottom border).
- **Status pill**: 48 px high, 1 px edge, radius 999, dot 16 px. "Đang dựng": white dot pulsing 1.0 -> 1.5 every 0.5 s. "Sẵn sàng": dot hidden, `--ok` check drawn in 0.3 s.
- **Log line**: 56 px row, timestamp in mute then text in ink, `ok` right-aligned in `--ok`; the final "sẵn sàng" line is fully `--ok`.
- **Plan row**: 82 px row, 36 px circle outline in mute; on completion the border turns `--ok` and a check is drawn (`stroke-dashoffset` 1 -> 0, 0.3 s).
- **README cell**: markdown lines in mono 32 px, heading white bold, sub-heading mute.
- **Browser cell (generic)**: three 16 px dots, address field, title 64 px, subtitle 32 px mute, solid white pill button with black 32 px text. No real site, no logo.

## 6. Motion language

Easing: entrances `expo.out`, cell swap out `power3.in` 0.14 s then in `expo.out` 0.3 s, no bounce, no `back`. Grid rules draw with `scaleY`/`scaleX` 0 -> 1 over 0.6 s `power3.out`, stagger 0.07-0.08. Plus marks pop 0.4 -> 1 at 0.45 s. Headline lines rise out of a mask (`yPercent` 115 -> 0, 0.55 s `expo.out`, stagger 0.09) and leave upward in 0.14 s. Typing is a seeded-free proxy tween (`ease: "none"`, `onUpdate` slices the string): 20 characters in 1.0 s for the command and the address. Log burst: three lines 0.12 s apart, then a hold, then a second burst, then completion ticks 0.5 s apart. Micro-motion through every hold: camera 1.02, beam drifts +-5 degrees over 3-3.5 s, plus marks flash white for 0.2 s every second beat (2 s... every 1.0 s at 120 BPM), caret blinks with a 0.15 s off phase, status dot pulses.

## 7. Captions

NOT EXERCISED (demo build, silent). Profile value to try first: black box, 1 px border, radius 6, 40 px SegUIVar 600, unread words mute. In 9:16 keep the box between the terminal bottom and y 1650 or in the lower safe band; this build left the footer line there, so a caption would collide with it.

## 8. Scene recipes (3 beats in 12.0 s, BPM 120 so 0.5 s per beat)

1. **Beat 1, 0.0-4.0 "README in"**: grid draws 0.05-0.7, plus marks 0.45, beam fades in 0.3-1.2, kicker 0.4, headline "README vào, / bản triển khai ra." 0.55, README cell and terminal 0.9-1.0, README lines 1.25 (0.16 s apart), command typed 1.7-2.7, "Enter" flash 3.0 (command and steps go white).
2. **Beat 2, 4.0-8.0 "Log burst"**: headline swaps (4.0), README cell flips to the plan cell (3.88-4.33, 3 rows), logs 1-3 at 4.3, logs 4-6 at 5.5, ok tags and drawn checks at 6.2, 6.7, 7.2. Hold 7.2-8.0 with everything complete.
3. **Beat 3, 8.0-12.0 "Ready"**: beam sweep (rotation -24 -> 0, 0.7 s), headline "Một lệnh, / một địa chỉ xem thử.", pill to "Sẵn sàng" with check at 8.05, last log line 8.1, plan cell flips to browser cell (7.88-8.55, rises 50 px), URL typed 8.6-9.6, title 8.9, subtitle 9.1, button 9.4. Full composition from 9.8; the last 2.2 s are held with micro-motion only.

## 9. Transitions

Used: grid-draw (opening), cell-swap (zone A flips through scaleY 1 -> 0 -> 1 in about 0.45 s), beam-sweep (beat 3 reveal), headline mask swap. Never a fade to black. Each swap starts 0.12 s before the beat so the outgoing content is gone by the beat: no ghost above 0.15 s.

## 10. Image guidance for agy

None used (optional, not needed). If used: black-and-white abstract globe or beam, no text, no logos, no colour beyond a faint grey; place it behind the grid, never behind logs.

## 11. Safe handling of facts on screen

Generic only: "Ứng dụng mẫu", `ung-dung-mau.example`, "3 bước". No real product, price, spec or company. Every frame carries "MINH HOẠ" (kicker) and the footer "Minh hoạ: ví dụ giả định, không phải sản phẩm thật". The log timestamps are invented and only illustrate the pattern. For a real video, every command, URL and time must come from the source.

## 12. Must not

No colour except `--ok` on status dots, checks and log words. No gradients except the single beam. Grid lines 1 px. No triangle logo shapes, no brand wordmarks, no real site in the browser cell. No bounce, no shake. No fade-in of text below 90% opacity as a resting state. No mascot. No segoepr.

## 13. Traps seen in real builds (from THIS build, measured)

1. **Python is not available to the builder.** `frame_check.py` failed with `ModuleNotFoundError: numpy`, and ad-hoc python (fontTools, PIL) was refused. Consequence here: no automatic frame check, no fontTools glyph test, no baked PNG beam. Substitutes used: `ffmpeg` contact sheet at 2 fps (24 tiles), single-frame extraction at 3.95 s, 4.1 s and 11.9 s, hand-computed contrast, `hyperframes validate` for contrast. Install numpy for the lane before the next build.
2. **Cell overflow by 11 px.** Five README lines at 54 px line height and 22 px padding overflowed the 380 px cell by 11.04 px (inspect flagged t=2 and t=3.33). Fix: 50 px line height, 16 px padding. Rule: content height = header 76 + padding 32 + lines x 50 must be at most 378.
3. **Two beam tweens overlapped** (intro rotation 0.3-1.2 s and drift from 1.0 s): lint warned `overlapping_gsap_tweens`. Start each drift when the intro ends.
4. **Descendant selector missed the green Ready line**: `.ln .g` never matched `class="ln g"`, so the last log line rendered in ink, not `--ok` (seen in the 8.6 s snapshot). Use `.ln.g`.
5. **Caret blink loop ran past the beat**: the loop re-showed the caret at 4.3 s, after beat 2 had hidden it. Cap the loop at the end of the beat (t < 3.4).
6. **Mask padding for Vietnamese stacked diacritics.** Line masks are 120 px plus 14 px top padding at 80 px type and 1.2 line height; with `overflow: hidden` and no padding the tone marks on Ế, Ở would clip. No clipping seen on held frames. Masks carry `data-layout-allow-overflow`.
7. **Beat 3 browser cell is empty for about 0.35 s** (8.55-8.9: header and dots only, address typing) before the title lands; a longer typing delay would break the "no empty panel > 0.5 s" rule. Keep the first content within 0.4 s of the cell appearing.
8. **Terminal is 600 px but 8 rows use about 450**: the lower 100 px of the terminal stays dark in every beat. Either shrink the cell to about 540 px and move the footer up, or add a 9th row. Left as is in the demo.
9. **Grid rules are weak after H.264**: `#1f1f1f` on black is 1.27:1; they are visible but faint in a 1.9 MB file. Plus marks (mute grey) carry the grid read, so keep them.
10. **Final held frame is full**: at 11.9 s headline, browser cell, button, terminal with the green last line, footer and plus marks all show; nothing moves except the camera, beam and marks.

## 14. Measured numbers of the sample

12.0 s, 1080 x 1920, 30 fps, h264, 1.9 MB, silent. Headline 80 px / -0.05em, logs 32 px, kicker 30 px, footer 26 px (the one line under 30 px), button text 32 px. Typing speed 20 characters per second. Longest hold without a new element: about 0.8 s (7.2-8.0) with pulses and camera motion running.
