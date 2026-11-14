# Thư viện phong cách video

[English](README.md) | **Tiếng Việt**

![License](https://img.shields.io/badge/license-Apache--2.0-blue) ![Styles built](https://img.shields.io/badge/styles%20built-42%2F70-0b6e5c) ![HyperFrames](https://img.shields.io/badge/built%20with-HyperFrames-black) ![AgentKit](https://img.shields.io/badge/styles%20from-AgentKit%20motion--video-orange)

<p align="center"><img src="assets/banner.jpg" alt="Samples from 42 built styles" width="100%"></p>
<p align="center"><img src="assets/gif-art-deco.gif" width="170"> <img src="assets/gif-pixel.gif" width="170"> <img src="assets/gif-manga.gif" width="170"></p>

▶ **[Xem cả 70 phong cách trong Thư viện](https://tominhphong.github.io/video-style-gallery/)** · 🌐 **[tominhphong.com/video-styles](https://tominhphong.com/video-styles)**

## Đây là gì

Thư viện 70 phong cách video của [AgentKit motion-video](https://agentkit.best/?ref=JGRILPGH). Mỗi phong cách có mô tả kiểu hình ảnh, các chủ đề hợp nhất (điểm Jev) và, với các phong cách đã dựng, hai đoạn mẫu 10 giây 1080x1920 cùng một **tài liệu công thức** để chép vào agent của bạn (Claude Code, Codex...) dựng lại đúng kiểu đó.

Đây không phải công cụ tạo video. Mọi đoạn mẫu đều vẽ bằng mã (HTML + GSAP, dựng bằng HyperFrames); công thức mô tả bố cục, bảng màu, chữ, các loại cảnh, nhịp, quy tắc phụ đề và các bẫy gặp khi dựng.

## Cách hoạt động

```
danh sách chủ đề (176)  ->  Jev chấm từng phong cách x chủ đề  ->  3 chủ đề tốt nhất mỗi phong cách
        ->  1 video đầy đủ + 2 đoạn mẫu 10 giây mỗi phong cách  ->  tài liệu công thức  ->  thư viện
```

1. Viết 176 chủ đề tin tức và giải thích: bất động sản, chính phủ, AI, văn hóa, game, tài chính, khoa học, đời sống, cộng đồng.
2. Jev (TypeSafe) chấm từng phong cách với từng chủ đề: "phong cách này có hợp mạnh với một video giải thích 45-60 giây về chủ đề này không?"
3. Chủ đề tốt nhất của mỗi phong cách thành một bản dựng đầy đủ 1080x1920; hai chủ đề kế thành đoạn mẫu 10 giây.
4. Bản dựng được viết lại thành tài liệu công thức của phong cách đó.

## Có gì mới

- **13/11/2026** 42 trên 70 phong cách đã dựng (đợt 1-5; đợt 3-5 chỉ video demo 12 giây, không voiceover), có đoạn mẫu và tài liệu công thức.
- **11/11/2026** Đăng trang thư viện, danh sách chủ đề và điểm Jev.

## Cách dùng

| Nói với agent | Điều gì xảy ra |
|---|---|
| "Dựng video dọc 55 giây phong cách `retro-crt-broadcast` về tin này." | Agent đọc công thức ở `docs/retro-crt-broadcast.md` và làm theo bố cục, màu, quy tắc cảnh |
| "Chọn phong cách cho tin ra mắt sản phẩm." | Xem điểm hợp trong Thư viện: mỗi thẻ ghi 3 chủ đề hợp nhất |
| "Chép công thức của `soft-clay-3d`." | Nút **Chép công thức** trong Thư viện chép tài liệu |

## Các phong cách đã dựng (42 trên 70)

| Xem trước | Phong cách | Nhóm | Chủ đề hợp nhất | Jev |
|---|---|---|---|---|
| <a href="https://tominhphong.github.io/video-style-gallery/#accelerated-compute"><img src="p/accelerated-compute-sample-t027.jpg" width="90" alt="accelerated-compute"></a> | [`accelerated-compute`](docs/accelerated-compute.md) | Lấy cảm hứng thương hiệu | Chip maker unveils a GPU with benchmark charts against last year's model | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#ambient-intelligence"><img src="p/ambient-intelligence-sample-t030.jpg" width="90" alt="ambient-intelligence"></a> | [`ambient-intelligence`](docs/ambient-intelligence.md) | Lấy cảm hứng thương hiệu | How a large language model uses a context window | 0.72 |
| <a href="https://tominhphong.github.io/video-style-gallery/#art-deco-luxury"><img src="p/art-deco-luxury-sample-t103.jpg" width="90" alt="art-deco-luxury"></a> | [`art-deco-luxury`](docs/art-deco-luxury.md) | Thẩm mỹ | Perfume house relaunches a 1920s classic fragrance | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#blueprint-engineering"><img src="p/blueprint-engineering-sample-t132.jpg" width="90" alt="blueprint-engineering"></a> | [`blueprint-engineering`](docs/blueprint-engineering.md) | Thẩm mỹ | Smartphone maker shows an exploded view of its new camera module | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#character-comedy"><img src="p/character-comedy-sample-t108.jpg" width="90" alt="character-comedy"></a> | [`character-comedy`](docs/character-comedy.md) | Lấy cảm hứng thương hiệu | Habit-tracking app adds streaks and a mascot to help people save money | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#cinematic-technology"><img src="p/cinematic-technology-sample-t111.jpg" width="90" alt="cinematic-technology"></a> | [`cinematic-technology`](docs/cinematic-technology.md) | Lấy cảm hứng thương hiệu | Camera maker launches a cinema lens with anamorphic look | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#comic-multiverse"><img src="p/comic-multiverse-sample-t164.jpg" width="90" alt="comic-multiverse"></a> | [`comic-multiverse`](docs/comic-multiverse.md) | Của nhà | Youth sneaker and streetwear brand announces an anime collaboration | 0.79 |
| <a href="https://tominhphong.github.io/video-style-gallery/#creative-canvas"><img src="p/creative-canvas-sample-t142.jpg" width="90" alt="creative-canvas"></a> | [`creative-canvas`](docs/creative-canvas.md) | Lấy cảm hứng thương hiệu | Architects and clients review a floor plan together on a shared online board | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#creative-suite"><img src="p/creative-suite-sample-t088.jpg" width="90" alt="creative-suite"></a> | [`creative-suite`](docs/creative-suite.md) | Lấy cảm hứng thương hiệu | Photo editing app releases AI masking and before-and-after tools | 0.86 |
| <a href="https://tominhphong.github.io/video-style-gallery/#data-editorial"><img src="p/data-editorial-sample-t059.jpg" width="90" alt="data-editorial"></a> | [`data-editorial`](docs/data-editorial.md) | Thẩm mỹ | Monthly housing report: inventory, median price, days on market in Austin | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#developer-workflow"><img src="p/developer-workflow-sample-t028.jpg" width="90" alt="developer-workflow"></a> | [`developer-workflow`](docs/developer-workflow.md) | Lấy cảm hứng thương hiệu | GitHub repository gains ten thousand stars in a week: what it does | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#documentary-purpose"><img src="p/documentary-purpose-sample-t149.jpg" width="90" alt="documentary-purpose"></a> | [`documentary-purpose`](docs/documentary-purpose.md) | Lấy cảm hứng thương hiệu | Nature reserve outside Austin restores prairie and tells the founder's story | 0.87 |
| <a href="https://tominhphong.github.io/video-style-gallery/#editorial-collage-explainer"><img src="p/editorial-collage-explainer-sample-t175.jpg" width="90" alt="editorial-collage-explainer"></a> | [`editorial-collage-explainer`](docs/editorial-collage-explainer.md) | Lấy cảm hứng thương hiệu | Tenant union zine explains your rights in plain language | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#expressive-material"><img src="p/expressive-material-sample-t118.jpg" width="90" alt="expressive-material"></a> | [`expressive-material`](docs/expressive-material.md) | Lấy cảm hứng thương hiệu | Phone operating system update personalises colours and widgets | 0.84 |
| <a href="https://tominhphong.github.io/video-style-gallery/#friendly-system-motion"><img src="p/friendly-system-motion-sample-t108.jpg" width="90" alt="friendly-system-motion"></a> | [`friendly-system-motion`](docs/friendly-system-motion.md) | Lấy cảm hứng thương hiệu | Habit-tracking app adds streaks and a mascot to help people save money | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#functional-playful"><img src="p/functional-playful-sample-t169.jpg" width="90" alt="functional-playful"></a> | [`functional-playful`](docs/functional-playful.md) | Lấy cảm hứng thương hiệu | How to assemble a flat-pack bookshelf in four steps | 0.88 |
| <a href="https://tominhphong.github.io/video-style-gallery/#glass-keynote"><img src="p/glass-keynote-sample-t025.jpg" width="90" alt="glass-keynote"></a> | [`glass-keynote`](docs/glass-keynote.md) | Của nhà | Phone operating system update personalises colours and widgets | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#groovy-seventies"><img src="p/groovy-seventies-sample-t134.jpg" width="90" alt="groovy-seventies"></a> | [`groovy-seventies`](docs/groovy-seventies.md) | Thẩm mỹ | Retro seventies diner reopens in Fort Worth with a nostalgic menu | 0.86 |
| <a href="https://tominhphong.github.io/video-style-gallery/#holographic-hud"><img src="p/holographic-hud-sample-t032.jpg" width="90" alt="holographic-hud"></a> | [`holographic-hud`](docs/holographic-hud.md) | Thẩm mỹ | Chip maker unveils a new accelerator with specs and price | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#human-storytelling"><img src="p/human-storytelling-sample-t040.jpg" width="90" alt="human-storytelling"></a> | [`human-storytelling`](docs/human-storytelling.md) | Lấy cảm hứng thương hiệu | Small business spotlight: a family taqueria in San Antonio | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#isometric-systems"><img src="p/isometric-systems-sample-t169.jpg" width="90" alt="isometric-systems"></a> | [`isometric-systems`](docs/isometric-systems.md) | Thẩm mỹ | Low-code platform lets teams snap together apps from reusable blocks | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#joyful-pop"><img src="p/joyful-pop-sample-t090.jpg" width="90" alt="joyful-pop"></a> | [`joyful-pop`](docs/joyful-pop.md) | Lấy cảm hứng thương hiệu | A bold ad campaign for a sparkling water brand | 0.80 |
| <a href="https://tominhphong.github.io/video-style-gallery/#manga-ink"><img src="p/manga-ink-sample-t123.jpg" width="90" alt="manga-ink"></a> | [`manga-ink`](docs/manga-ink.md) | Thẩm mỹ | Youth sneaker and streetwear brand announces an anime collaboration | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#mid-century-retro"><img src="p/mid-century-retro-sample-t125.jpg" width="90" alt="mid-century-retro"></a> | [`mid-century-retro`](docs/mid-century-retro.md) | Thẩm mỹ | Toy company releases a build-it-yourself robot kit for kids | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#modular-build"><img src="p/modular-build-sample-t125.jpg" width="90" alt="modular-build"></a> | [`modular-build`](docs/modular-build.md) | Lấy cảm hứng thương hiệu | Toy company releases a build-it-yourself robot kit for kids | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#monochrome-developer"><img src="p/monochrome-developer-sample-t029.jpg" width="90" alt="monochrome-developer"></a> | [`monochrome-developer`](docs/monochrome-developer.md) | Lấy cảm hứng thương hiệu | Command line tool that turns a README into a deployment | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#music-editorial"><img src="p/music-editorial-sample-t127.jpg" width="90" alt="music-editorial"></a> | [`music-editorial`](docs/music-editorial.md) | Lấy cảm hứng thương hiệu | Year in review: most streamed songs and artists in Texas | 0.81 |
| <a href="https://tominhphong.github.io/video-style-gallery/#neon-cyberpunk"><img src="p/neon-cyberpunk-sample-t136.jpg" width="90" alt="neon-cyberpunk"></a> | [`neon-cyberpunk`](docs/neon-cyberpunk.md) | Thẩm mỹ | Synthwave album release with a neon visual concept | 0.81 |
| <a href="https://tominhphong.github.io/video-style-gallery/#organic-biomorphic"><img src="p/organic-biomorphic-sample-t117.jpg" width="90" alt="organic-biomorphic"></a> | [`organic-biomorphic`](docs/organic-biomorphic.md) | Thẩm mỹ | Wellness app launches a guided breathing programme | 0.88 |
| <a href="https://tominhphong.github.io/video-style-gallery/#paper-cut-collage"><img src="p/paper-cut-collage-sample-t133.jpg" width="90" alt="paper-cut-collage"></a> | [`paper-cut-collage`](docs/paper-cut-collage.md) | Thẩm mỹ | Underground zine fair in Austin: bands, printers and tickets | 0.79 |
| <a href="https://tominhphong.github.io/video-style-gallery/#pixel-arcade"><img src="p/pixel-arcade-sample-t129.jpg" width="90" alt="pixel-arcade"></a> | [`pixel-arcade`](docs/pixel-arcade.md) | Thẩm mỹ | Retro console returns as a mini edition with fifty games | 0.76 |
| <a href="https://tominhphong.github.io/video-style-gallery/#playful-productivity"><img src="p/playful-productivity-sample-t115.jpg" width="90" alt="playful-productivity"></a> | [`playful-productivity`](docs/playful-productivity.md) | Lấy cảm hứng thương hiệu | Team chat app adds threads, emoji reactions and integrations | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#precision-dark-product"><img src="p/precision-dark-product-sample-t029.jpg" width="90" alt="precision-dark-product"></a> | [`precision-dark-product`](docs/precision-dark-product.md) | Lấy cảm hứng thương hiệu | Command line tool that turns a README into a deployment | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#precision-hardware"><img src="p/precision-hardware-sample-t032.jpg" width="90" alt="precision-hardware"></a> | [`precision-hardware`](docs/precision-hardware.md) | Lấy cảm hứng thương hiệu | Smartphone maker shows an exploded view of its new camera module | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#product-spec-film"><img src="p/product-spec-film-sample-t132.jpg" width="90" alt="product-spec-film"></a> | [`product-spec-film`](docs/product-spec-film.md) | Lấy cảm hứng thương hiệu | Smartphone maker shows an exploded view of its new camera module | 0.91 |
| <a href="https://tominhphong.github.io/video-style-gallery/#punk-zine"><img src="p/punk-zine-sample-t172.jpg" width="90" alt="punk-zine"></a> | [`punk-zine`](docs/punk-zine.md) | Thẩm mỹ | Underground zine fair in Austin: bands, printers and tickets | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#retro-crt-broadcast"><img src="p/retro-crt-broadcast-sample-t057.jpg" width="90" alt="retro-crt-broadcast"></a> | [`retro-crt-broadcast`](docs/retro-crt-broadcast.md) | Thẩm mỹ | Retro TV network marks fifty years with a special broadcast | 0.90 |
| <a href="https://tominhphong.github.io/video-style-gallery/#sensory-tech"><img src="p/sensory-tech-sample-t118.jpg" width="90" alt="sensory-tech"></a> | [`sensory-tech`](docs/sensory-tech.md) | Lấy cảm hứng thương hiệu | Phone operating system update personalises colours and widgets | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#soft-clay-3d"><img src="p/soft-clay-3d-sample-t108.jpg" width="90" alt="soft-clay-3d"></a> | [`soft-clay-3d`](docs/soft-clay-3d.md) | Thẩm mỹ | Toy company releases a build-it-yourself robot kit for kids | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#sport-editorial"><img src="p/sport-editorial-sample-t084.jpg" width="90" alt="sport-editorial"></a> | [`sport-editorial`](docs/sport-editorial.md) | Lấy cảm hứng thương hiệu | A fashion brand launches a limited sneaker drop | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#systematic-enterprise"><img src="p/systematic-enterprise-sample-t026.jpg" width="90" alt="systematic-enterprise"></a> | [`systematic-enterprise`](docs/systematic-enterprise.md) | Lấy cảm hứng thương hiệu | AI company reports quarterly revenue, margin and backlog | 0.80 |
| <a href="https://tominhphong.github.io/video-style-gallery/#terminal-ops"><img src="p/terminal-ops-sample-t027.jpg" width="90" alt="terminal-ops"></a> | [`terminal-ops`](docs/terminal-ops.md) | Thẩm mỹ | Command line tool that turns a README into a deployment | 0.81 |

**Chưa dựng (28):** `athletic-impact`, `bauhaus-geometry`, `calm-workspace`, `cinematic-product-launch`, `cinematic-streaming`, `community-chaos`, `constructivist-poster`, `editorial-intelligence`, `extreme-energy`, `fluent-productivity`, `gradient-fintech`, `immersive-console`, `ink-woodblock`, `keynote-stage`, `kinetic-typography`, `minimal-future-product`, `mission-control`, `monochrome-luxury`, `neo-brutalist-web`, `newsprint-editorial`, `playful-game-system`, `premium-ui-demo`, `quirky-editorial`, `saas-bento`, `swiss-kinetic-editorial`, `vaporwave-memphis`, `wpa-screenprint`, `y2k-liquid-chrome`.

## Lấy AgentKit

Các phong cách lấy từ bộ AgentKit motion-video. **Tiết lộ liên kết tiếp thị:** link dưới đây là link giới thiệu của tác giả; mua qua link được giảm 20% lần mua đầu (theo chương trình giới thiệu của AgentKit) và tác giả nhận hoa hồng. Thư viện này miễn phí, giấy phép Apache-2.0.

https://agentkit.best/?ref=JGRILPGH

## Ghi chú

- Đoạn mẫu là nội dung "minh hoạ" chung, không tiếng, có ghi rõ; chỉ để xem kiểu hình ảnh và chuyển động, không phải tin thật.
- Tài liệu công thức viết từ các bản dựng thử, bằng tiếng Anh. Tên công cụ trong đó (`agy`, `motion_tools.py`, giọng VieNeu) là công cụ riêng của tác giả, không kèm theo.
- Điểm hợp chỉ là gợi ý, không phải luật.

## Ghi công và giấy phép

Tạo bởi **Phong To**. Apache-2.0 (xem `LICENSE`). Phong cách lấy từ [AgentKit motion-video](https://agentkit.best/?ref=JGRILPGH) (MIT); xem `NOTICE` để biết nguồn gốc. Bố cục trang lấy cảm hứng từ video-shotcraft (Apache-2.0); không chép mã hay tài nguyên.
