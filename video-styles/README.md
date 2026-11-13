# Video Style Gallery

**EN** A browsable gallery of the 70 [AgentKit motion-video](https://github.com/bestagentkits/motion-video-skill) styles, built with HyperFrames. Each style card shows its summary, the three topics that fit it best (scored by Jev, 100-176 candidate topics), and, for the styles built so far, two 10-second 1080x1920 samples plus a recipe document you can copy into your own agent.

**VI** Thư viện 70 phong cách video của AgentKit motion-video, dựng bằng HyperFrames. Mỗi thẻ có mô tả, ba chủ đề hợp nhất (điểm Jev), và với các phong cách đã dựng thì có hai đoạn mẫu 10 giây 1080x1920 cùng tài liệu công thức để chép vào agent của bạn.

Created by **Phong To**.

## What is here

| Path | What |
|---|---|
| `index.html` | The gallery (static page, no build step): search, family filter, status filter, VI/EN, light/dark, "Copy recipe" |
| `data.json` | 70 styles: family, summary, energy, palette mode, best-for, top-3 topics with fit score |
| `v/`, `p/` | 10-second sample clips (silent, H.264 540x960) and poster frames |
| `docs/` | One English recipe document per built style: layout, palette, type, scene types, pacing, caption rules, traps seen in the build |

17 of the 70 styles are built so far; the rest show their summary and planned topics. The page is updated as more are built.

## Run it

```bash
python -m http.server 8000   # then open http://localhost:8000
```

Or use the live page (GitHub Pages) linked in the repository sidebar.

## Notes

- Samples are generic "illustration" content, silent, and labelled as such; they show the look and motion of a style, not a real news story.
- The recipe documents are written from trial builds. Tool names inside them (`agy` image helper, `motion_tools.py`, VieNeu voice) are private helpers of the author's setup and are not included; treat those sections as a description of what was done.
- Fit scores are Jev (TypeSafe) probabilities for "this style is a strong fit for a 45-60 s explainer on this topic". They are a guide, not a rule.

## Get AgentKit

The styles come from the AgentKit motion-video skill. **Affiliate disclosure:** the link below is the author's referral link; buying through it gives you 20% off your first purchase (per the AgentKit referral programme) and the author earns a commission. The gallery itself is free and Apache-2.0.

https://agentkit.best/?ref=JGRILPGH

## Credits and licence

Apache-2.0 (see `LICENSE`). Style profiles come from AgentKit motion-video (MIT); see `NOTICE`. Page layout inspired by video-shotcraft (Apache-2.0).
