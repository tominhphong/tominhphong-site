# Style: playful-productivity (detail, first build, 2026-11-13)

## 0. Read this first: niche, status, reading order

**Niche (two tiers; do not mix them).**
- **Tier 2 - general fit of the style (REFERENCE ONLY), observed in this build.** Warm, human, busy team-app stories about what people do inside a chat or collaboration tool: threads, reactions and emoji, integrations and connected apps, shared boards, live cursors and comments, workplace-culture features. Strong when the story is a list of small, friendly, user-visible changes (each can be a card, a tile or a pill). Weak for numbers-heavy stories (the style has no data scene; counters need real counts), bad news, enforcement, or anything formal. Tier 2 never widens tier 1.

**Status.** Written 2026-11-13 from one full build (Discord Patch Notes of 2026-11-09, 52.94 s, 3.8 MB) and two 10 s samples (generic "Minh hoạ" brainstorm board and design-comment scenes). No owner has reviewed it. The profile is `skill/references/styles/profiles/playful-productivity.yaml` (energy 4, mixed palette); this document fills what the profile leaves open and records where this build changed it.

**Marks.** SUBST = installed font replaces a named one. ASSUMED = the profile gives no value and this document chose one. DEVIATION = knowingly differs from the profile.

**Reading order.** 1 to 12 are the design as built. 13 lists traps from this build with numbers. 14 holds the sample recipes. Format: 1080 x 1920, 30 fps, VieNeu voice (about 4.1 words/s including 0.35 s gaps), no music, estimated-word karaoke captions.

DEVIATION 1: profile asks for music at 110 to 128 BPM and beat-synced pops. No music tool in this run: cuts follow the voice, beat response is dropped.
DEVIATION 2: profile asks for reaction counters. A counter needs a real count; the news page gave none, so the final has no counter and the samples have illustrative ones labelled "Minh hoạ".
DEVIATION 3: profile type sizes 26 to 30 px are raised to a 30 px floor for a phone.

## 1. Tokens (contrast measured with the WCAG formula, python)

```css
:root{
  --bg:#f4ede4;      /* profile plum_light; page background (cream)       ink 14.42, mute 5.19, plum 11.58 on it */
  --card:#ffffff;    /* profile bg; window and cards                       ink 16.75, mute 6.02 on it */
  --ink:#1e1d22;     /* profile ink */
  --mute:#63626a;    /* profile mute: 6.02:1 on white, 5.19:1 on cream: allowed for text */
  --plum:#3a2358;    /* profile plum: sidebar, caption pill, key words; 11.58:1 on cream; white on plum 13.45:1 */
  --blue:#2458b0;    /* profile accent: avatars, cursor tag; white on blue 6.78:1; blue on cream 5.84:1 */
  --teal:#26a69a;    /* FILL ONLY: 3.0:1 on white. Ink on teal 5.58:1 is the only text on it */
  --orange:#f29544;  /* profile "yellow" (it is orange): fill; ink on it 7.30:1; as the live caption word on plum 5.87:1 */
  --red:#e2445a;     /* FILL / ICON ONLY: white on red 4.03:1 and ink on red 4.15:1 both fail 4.5 */
  --sky:#5aa9ec;     /* fill; ink on sky 6.64:1 */
  --sk:#d8d0c6;      /* skeleton bars (ASSUMED) */
  --sh:0 12px 32px rgba(30,29,34,.12);  /* profile */
}
```
Extra tokens used for cursor tags (ASSUMED): `#17756b` (white on it 5.54:1) and `#d1364b` (white on it 4.84:1). Rules: text colours only from ink, mute, plum, blue and white-on-plum / white-on-blue; text on a bright tile is ink, never white; red, teal and sky never carry text smaller than a headline; one tile colour per card, four brights in total on screen, rotating by position (teal, orange, sky left to right). Never lighten a text token. No dark mode.

## 2. Fonts (glyph test: PIL render of 134 Vietnamese letters against the notdef glyph)

| File | Missing | Role |
|---|---|---|
| `SegUIVar.ttf` | 0 | everything read: headlines (800), message and card text (700, 600 for sub), captions (700). SUBST for Nunito (headlines) and Lato (messages) and Be Vietnam Pro (captions) |
| `CascadiaMono.ttf` | 0 | kicker, labels, chips of the source line, "Minh hoạ" tags (30 px) |
| `cambriai.ttf` | 0 | unused in this build (no quote scene); keep for a single quoted sentence |
| `segoepr.ttf` | 92 of 134 (every ơ ư and dotted or hooked vowel) | never used |

SegUIVar variable weight 800 renders (checked in the snapshots); a "wobble per letter" headline entry was replaced by a per-word rotate (rotation -5 -> 0 with back.out(1.8), stagger 0.04 s) because per-letter spans break Vietnamese diacritics' line wrap and slowed the build.

## 3. Type scale (px, 1080 x 1920)

| Role | Size / line | Weight |
|---|---|---|
| Headline, 2 lines max | 78 / 86 | 800, second line in plum |
| Card title | 36 / 44 | 800 |
| Message, tile label, toast | 32 / 40 (tiles 32 / 38) | 700 to 800 |
| Sub line | 30 / 38 | 600, `--mute` |
| Mono label / kicker / chip text | 30 / 36 | 400 mono, or 700 for chips |
| Caption | 44 / 56 | 700 |
| Sidebar item | 30 / 68 | 700 |
| Footer (the only footer line) | 30 / 36 mono | 400 |

Nothing below 30 px (profile asked 26). A mono label of 30 px is about 18 px per character: a card 640 px wide holds 34 characters at most; keep labels to 31 (see trap 5).

## 4. Grid and safe areas

- Side margin 72, content width 936. Platform top zone y 0 to 120 empty; kicker (mono 30) at y 122; headline y 184 to 356 (two lines of 86).
- **Window** x 72, y 430, 936 x 900, radius 16. Sidebar x 0 to 220 (plum). Column x 220 to 936 (716 wide). Column header 92 px (channel name 36 px, "Minh hoạ" tag right when the content is a mock). Body x +24, y +112, 668 x 770: it ends at y 430 + 112 + 770 = 1312. Cards fill the body down to 1294 to 1312.
- Captions: pill centred, top y 1420, max width 936, one or two lines (56 px per line + 32 padding): y 1420 to 1508 (one line) or 1564 (two). Footer line y 1700. y 1564 to 1920 otherwise empty (platform UI zone); this reads bare, see compare.md.
- Radius: window and cards 16, tiles 20, chips 28 (full), note 12, bubble 20 with 6 on the tail corner.
- Right rail x 960 to 1080 below y 1100: no text.

## 5. Layers, back to front

1. `#root` bg `--bg`. 2. `#world` (z 1): holds everything; scale never animated (a 1.04 zoom would cut the 72 px margin). 3. Kicker and headlines `#h1..#h6` (six stacked, one visible). 4. `#win` window with `#side`, `#pill`, six `.col` columns (one visible). 5. `#foot`. 6. `#caps` (above window). 7. `#fx`: confetti and emoji sprites (DOM built first, seeded). No fade layer: frame 0 is a finished composition.

Depth: background cream (static), window and cards (mid), confetti/sprites/cursors (front, fastest). Parallax is not used: the style's depth comes from shadows and the overlapping pop-ins.

## 6. Components

- **Window** (white, radius 16, shadow `--sh`) with plum sidebar: three 20 px dots (orange, teal, sky), six channel items `# chung`, `# luồng`, `# emoji`, `# ứng dụng`, `# tiện ích`, `# nguồn` (30 px, 196 x 68, radius 14). The **selection pill** (white, 196 x 68) slides to the item of the current scene on the scene start (y step 84, 0.45 s `power3.out`); the item colour flips plum/white with `tl.set` at S+0.1.
- **Card**: `--bg` fill on white window, radius 16, no shadow.
- **Tile** (profile "tile-snap"): 212 x 290, radius 20, one bright fill, a 72 px SVG icon and a 32 px two-line label in ink.
- **Message bubble**: `--bg`, radius 6/20/20/20, padding 16 x 22, 32 px; avatar 64 px plum circle with a 34 px letter.
- **Typing dots**: bubble 120 x 44, three 8 px radius `--mute` circles, yoyo y -8 for 0.22 s x 4, stagger 0.1 s; then the dots bubble hides and the message pops at S+0.85.
- **Skeleton bar**: 18 px, radius 9, `--sk`: stands for mock text so the mock UI never invents words.
- **Reaction pill / vote pill**: height 54, radius 27, white, 36 px SVG heart or smile, 32 px bold count. Count tween 0.6 s `power3.out`.
- **Emoji sprites**: inline SVG `<symbol>`s (smile orange, heart red, star teal, bolt sky). Never an emoji character, never an image.
- **Cursor**: 40 x 48 SVG arrow with white stroke 3 plus a name tag (30 px bold white on a dark tag colour, radius 22). Move on stepped waypoints, x `power2.inOut` and y `sine.inOut` (an arc).
- **Integration hub** (scene 4): 200 px plum circle, two satellites 240 x 110 (orange, teal), lines stroke 14 round caps, drawn 0.5 s `power2.out` from the hub.
- **Chip**: height 56, radius 28, 30 px 700. Source chip `discord.com/blog` plum with white text.
- **Selection ring** (rows): 6 px plum border, radius 24, slides row to row 0.45 s `power3.out`.
- **Caption pill**: see section 9.

## 7. Motion language

- Entrances bounce: `back.out(1.7 to 1.8)`, 0.45 to 0.5 s (cards y 100 -> 0 with a 0.15 s opacity ramp, tiles and pills scale .5 -> 1, tile fly-ins x/y plus rotation +-14 -> 0). Overshoot never leaves the screen margin.
- Scene change = channel-switch: outgoing column x -> -120 and opacity 0 in 0.15 s `power2.in` ending on the boundary; incoming column from x +140 with `back.out(1.4)` 0.5 s and a 0.12 s opacity ramp; headline words rise y 50 -> 0 with rotation -5 -> 0 (`back.out(1.8)`, stagger 0.04 s). The window body is empty for about 0.15 s at each cut (measured: 8.1, 19.4, 47.2 s).
- Anchors: reveals on the spoken word with `A(sid, word, nth, lo) = max(S + lo, W(...) - 0.15)`. Word times are estimated: floors keep a drifted word from leaving a block late. Cards that must not wait for a word are timed from the scene start (S+0.05, S+0.2 ...), not from the word.
- Bursts: one per scene at most (seeded mulberry32): 14 to 18 confetti pieces, angle from the rng, distance 220 to 520 px, x `expo.out` 0.9 s, y `power2.out` with a 80 to 200 px fall, fade at +0.75 s. Emoji sprites: 8, rise 120 to 280 px, scale .4 -> 1.1 back.out(2), fade at +0.9 s.
- Holds are not frozen: notes sway y -5 (1.2 s yoyo), cursors drift on waypoints, a pin bobs 6 px, the selection ring moves with the speaker.
- Energy 4 budget used: pops, tile-snap, confetti, bump (scale 1.08 -> 1, 0.12 + 0.3 s) on the spoken keyword. Not used: shake, flash, whip.

## 8. Scene recipes (6 scenes of the final; starts from `voice/timeline.json`: 0.0 / 8.03 / 19.34 / 31.21 / 39.24 / 47.19 s)

**R1 Hook (s1, 8.0 s).** Kicker "DISCORD · GHI CHÚ CẬP NHẬT · 9.11.2026", headline "Discord cập nhật ngày 9 tháng 11" (present at frame 0). Window `# chung`: typing dots at 0 to 0.85 s, message "Bản ghi chú cập nhật ngày 9.11.2026" pops at 0.85. Three tiles (teal "Luồng thảo luận", orange "Biểu tượng cảm xúc", sky "Ứng dụng") fly in at 0.5, 0.68, 0.86 s; burst at 1.0; source card (white text on cream: "NGUỒN", "Discord Patch Notes: November 9, 2026", chip discord.com/blog) rises at 1.5. Each tile bumps on its spoken keyword (5.2, 6.0, 6.9 s).
**R2 Two-card fix scene (s2, 11.3 s).** Headline "Luồng thảo luận (thread) trên máy tính". Card A "Máy tính · tạo luồng mới": skeleton message, thread card unfolds (scaleY 0 -> 1) on "tạo", ring moves from `# kênh này` to `# kênh khác` on "sang", teal chip "Không bị kéo quay lại" on "kéo". Card B "Thông báo của luồng": three rows, the ring flips down and back (0.18 s each) on "quá", orange toast "Chậm lại một chút, rồi thử lại" on "lời".
**R3 Three-card emoji scene (s3, 11.9 s).** Cards A (picker with a plum 6 px border that snaps from offset (-20, 10) to 0 on "căn"), B (Android row: defaults then custom tiles; guide line scales 0 -> 1 on "thẳng"), C (placeholder thumbnail becomes the loaded thumbnail and a "Đã tải" chip on "tải"). Sprite burst at S+0.25 from y 900.
**R4 Integration hub (s4, 8.0 s).** Hub pops, two lines draw, two satellites pop ("Letterboxd", "@game"), two cards "Thêm Letterboxd làm tài khoản có thể kết nối" and "Lệnh game: thêm nhiều trò chơi di động, gồm trò chơi nhiều nền tảng". Satellites bump on their spoken word.
**R5 List of three (s5, 7.95 s).** Three cards 222 px high (star "Mục yêu thích", bookmark "Dấu trang và lời nhắc", clock "Hẹn giờ gửi"), 6 px ring slides 548 px down on "dấu" and "hẹn".
**R6 Source and close (s6, 5.15 s).** Desk banner (agy image, crop 700 x 520, shown 668 x 300), source card, three chips (Âm thanh teal, Hình ảnh orange, Hỗ trợ tiếp cận sky), burst at S+0.2. No fade out; the last frame is the full composition.

For a number-led story add **R7 Reaction counter** (see section 14: pill pops, count 0.6 s, winner ring, burst), which this build could not use in the final.

## 9. Captions (karaoke)

Plum pill (#3a2358), radius 16, padding 16 x 30, SegUIVar 700 44 px / 56 line, white; the current word `#f29544` (5.87:1). Top y 1420, width 936, centred, up to two lines. Chunking: split at `, . : ;` after at least 3 words, max 7 words, merge chunks under 3 words into the previous one: 36 chunks for 214 words. Visibility and word colour by `tl.set` only (no tween, so no ghost or half state). Text equals the spoken text word for word (not digits): "chín tháng mười một". Estimated word onsets: the highlight can lag or lead by up to about 0.3 s.

## 10. Sound

No music (the production tool is absent here). The profile's bouncy 110 to 128 BPM indie pop with pings, reaction pops and confetti swish was not built: add it when a music tool exists and re-anchor pops to beats. Voice only: VieNeu "Hải Đăng", -15.6 LUFS, peak -4.3 dBFS after mux.

## 11. Images (agy)

2 images, about 1 and 2 minutes each, in parallel: `desk` (flat top-down desk, laptop, plant, cup, sticky notes in the five palette colours) and `confetti` (rounded tiles and bubbles; generated, NOT used). The desk crop (`crop=700:520:40:420`, 34 KB) fills the banner of scene 6. Prompts state: flat vector, exact hexes, no text/letters/logos/people, empty centre. agy never draws geometry or UI: windows, tiles, hub, cursors, emoji, icons are CSS/SVG. A full-bleed desk image behind everything fights the headline (plant at the top right): use it as a card, not a background.

## 12. Must not

- Any brand mark: Slack hash pinwheel, Discord logo, product screenshots, real usernames. Mock UI is generic and tagged "Minh hoạ".
- Emoji characters; use SVG sprites.
- Counters, votes or reaction numbers that the source does not give (samples excepted, tagged).
- Text below 30 px; text on red; white text on teal, orange or sky tiles; teal or red as text.
- More than 2 bursts in a scene; unseeded randomness; CSS animations; `repeat: -1`.
- A scene with only a headline and an empty window for more than 0.5 s.
- A card or label for something the voice no longer says (trap 3).
- Calls to like/share, predictions, advice, "new feature" wording for a bug fix.

## 13. Traps seen in real builds (this build, 2026-11-13)

1. **Typing dots on top of the message text.** At 0.3 s the dots (a child of the bubble) overlapped the bubble text. Fix: dots in their own bubble (80, 30, 120 x 44), the message bubble starts at S+0.85. Check frame 0.3 s.
2. **Spoken text cut but its card stayed.** The first script had a sentence about bot-embed thumbnails; it was trimmed for length (240 words = about 62 s -> 214 words = 52.3 s) while the hub still showed "Khung nhúng bot" and a card sub line used a derived count "hai mục". Fix: removed both; compare the list of on-screen nouns to the final script. Count words with `len(text.split())` first: 240 words first draft.
3. **Mono labels overrun cards.** A 30 px mono label is about 18 px per character; "Android · emoji mặc định và tùy chỉnh" (37) and "Ứng dụng · ảnh nhỏ emoji tùy chỉnh" (34) touched the card edge (640 px). Fix: labels of at most 31 characters.
4. **Selection ring clipped its chip.** A fixed 188 px ring over a 220 px chip cut "# kênh khác". Fix: tween `width` 188 -> 220 with the move.
5. **Chips touching.** Two chips at left 30 and 200 touched in the source card; second chip to 222.
6. **Burst over the headline.** Sprites spawned at y 700 and rose 260 to 520 px, crossing the headline at 20 s. Fix: origin y 900, rise 120 to 280.
7. **Empty hub gap.** After deleting the third satellite, hub and the lower cards left a 130 px hole; nodes moved to y 80, hub to y 190, lines re-pathed (334, 290) -> (120, 135) / (548, 135).
8. **Window body empty at each cut.** The column leaves in 0.15 s and the next arrives 0.5 s with a 0.12 s ramp: about 0.15 s with an empty white window (8.1, 19.4, 47.2 s) and the headline already new. Inside the 0.5 s limit, accepted; to avoid it start the incoming column 0.05 s before the boundary.
9. **Lint/validate surprises.** `<svg>` defs placed before `#root` -> "root_missing_composition_id" and "root_missing_dimensions": put the defs inside `#root`. Selectors like `.w`, `.td` in tweens -> "unscoped_gsap_selector": use `getElementsByTagName` or `[data-composition-id="main"] .x`. Validate printed 5 contrast warnings on the sidebar item under the moving white pill (1:1): false positive (the pill is a transformed sibling); the snapshots are right.
10. **Inspect errors on moving cursors (samples).** Cursor tags crossing note text gave `text_occluded` and `content_overlap` at 1.67, 2.78, 3.89 s (4 errors). Fix: `data-layout-allow-overlap data-layout-allow-occlusion` on both the cursors and the notes. Resting positions were also moved (cursor on a vote count at 9 s).
11. **Lowest-edge probe is noisy for white on cream.** A probe that counts pixels differing from the cream background by more than 25 levels sees white (255) as 27 away: the white window edge (1330) and card bodies dominate it. Measure the layout (body bottom 1312) and look at the frame, do not trust the number alone. One reading of 1055 at S+0.3 of s5 was the sliding column.
12. **Story age.** No story of the rank-1 shape was inside 48 h; Discord's patch notes were 4 days old. Search results are weak for recency; opening the vendor feeds (Slack changelog, Workspace Updates, Teams blog, Discord blog) found the newest dated pages. The Discord post is a bug-fix list: write "giờ đã ..." and never "tính năng mới". Say the age in manifest notes.
13. **Fetch tool summary wrong.** The first fetch of the 70 k character page returned verbatim text for 40 k and a model summary for the rest that claimed "details absent". A re-open at offset 39931 returned everything. Re-open with the offset before concluding a section is missing. Quotes are capped at 125 characters: paraphrase and say so.
14. **No second image used.** `confetti.jpg` arrived about 50 s after `desk.jpg` and was never used; decide on the use of each agy image before asking (cost 2 x about 1 min).
15. **Still not checked.** Pronunciation of Discord, Letterboxd, Android, emoji, game (default VieNeu readings, unheard); caption highlight drift; whether native speakers accept "luồng thảo luận" for thread.

## 14. Sample recipes (10 s, silent, generic "Minh hoạ" content; each its own HyperFrames project in `samples/t143` and `samples/t115`)

Shared: headline 78 px, window 936 x 900 with sidebar and "Minh hoạ" tag, a footer line "Minh hoạ · nội dung mẫu, không phải sản phẩm thật" (30 px), seeded confetti (18 pieces, one burst), counters 0.6 s `power3.out`. No captions, no audio. Render 10.6 and 11.9 s, 1.3 MB and 0.7 MB. Frame check 20 frames, 0 BLANK; inspect 0 issues.

**S1 Brainstorm board (t143).** Six sticky notes (320 x 220, radius 12, orange / teal / sky / red / cream / teal, 36 px "Ý tưởng A-F") fly in from the edges with +-16 degrees spin, 0.6 s `back.out(1.5)`, stagger 0.16 s (0.15 to 1.0 s). Three cursors pop in at 1.4 s and move on three waypoints each (0.9 to 1.2 s steps) to rest in empty note areas. Vote pills pop at 3.6 s + 0.22 s per note with counts 3 5 2 7 1 4, each 0.6 s. Winner (D, 7 votes) bumps 1.07, gets a plum 8 px ring and a confetti burst at 5.5 s. Typing dots at 6.2 s, message "Cả nhóm chọn Ý tưởng D" pops at 7.0 s; hold to 10 s with notes swaying and a cursor drifting. Lowest content edge y 1322 (message bar).
**S2 Design comment (t115).** An artboard (616 x 470 with a plum bar, a sky image block, two skeleton lines, an orange button) rises at 0.1 s; three cursors enter at 1.0 s and rest on the image block and beside the button; a red pin "1" pops at 3.2 s; a comment card (668 x 258) rises at 3.5 s with the dots, message "Đổi màu nút này nhé" at 4.8 s, pills heart 3 and smile 2 (5.6 and 5.9 s), then the button turns teal at 6.9 s, a teal chip "Đã giải quyết" pops and a burst at 7.2 s. Lowest content edge y 1322 (card bottom).

Both end with a full composition and no fade. In both, cursor tags leave the window edge only mid-move, never on a held frame (checked at 9.5 s).
