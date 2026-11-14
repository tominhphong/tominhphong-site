# Video Style Gallery

**English** | [Tiếng Việt](README.vi.md)

![License](https://img.shields.io/badge/license-Apache--2.0-blue) ![Styles built](https://img.shields.io/badge/styles%20built-52%2F70-0b6e5c) ![HyperFrames](https://img.shields.io/badge/built%20with-HyperFrames-black) ![AgentKit](https://img.shields.io/badge/styles%20from-AgentKit%20motion--video-orange)

<p align="center"><img src="assets/banner.jpg" alt="Samples from 52 built styles" width="100%"></p>
<p align="center"><img src="assets/gif-art-deco.gif" width="170"> <img src="assets/gif-pixel.gif" width="170"> <img src="assets/gif-manga.gif" width="170"></p>

▶ **[Browse all 70 styles in the Gallery](https://tominhphong.github.io/video-style-gallery/)** · 🌐 **[tominhphong.com/video-styles](https://tominhphong.com/video-styles)**

## What this is

A browsable library of the 70 [AgentKit motion-video](https://agentkit.best/?ref=JGRILPGH) styles. Each style has a one-line look, the topics it fits best (scored by Jev), and, for the styles built so far, two 10-second 1080x1920 samples plus a **recipe document** you can copy into your own agent (Claude Code, Codex or similar) so it builds the same look.

It is not a video generator. Every sample is drawn by code (HTML + GSAP, rendered with HyperFrames); the recipes describe layout, palette, type, scene types, pacing, caption rules and the traps hit while building.

## How it works

```
topic list (176)  ->  Jev scores each style x topic  ->  top 3 topics per style
        ->  one full build + two 10 s samples per style  ->  recipe document  ->  gallery
```

1. 176 candidate news and explainer topics were written across real estate, government, AI, culture, games, finance, science, lifestyle and community.
2. Jev (TypeSafe) scored every style against every topic: "is this a strong fit for a 45-60 s explainer on this topic?"
3. Each style's best topic became one full 1080x1920 build; the next two became 10-second samples.
4. The build is written up as the style's recipe document.

## What's new

- **2026-11-13** 52 of 70 styles built (waves 1-6, waves 3-6 demo-only, silent 12 s). Samples and recipe documents for all 52.
- **2026-11-11** Gallery page, topic list and Jev scores published.

## Use

| Say to your agent | What happens |
|---|---|
| "Build a 55 s vertical explainer in the `retro-crt-broadcast` style about this story." | The agent reads the recipe from `docs/retro-crt-broadcast.md` and follows its layout, palette and scene rules |
| "Pick a style for a product-launch story." | Use the fit scores in the Gallery: each card lists its top 3 topics |
| "Copy the recipe for `soft-clay-3d`." | The Gallery's **Copy recipe** button copies the document |

## Built styles (52 of 70)

| Preview | Style | Family | Best-fit topic | Jev |
|---|---|---|---|---|
| <a href="https://tominhphong.github.io/video-style-gallery/#accelerated-compute"><img src="p/accelerated-compute-sample-t027.jpg" width="90" alt="accelerated-compute"></a> | [`accelerated-compute`](docs/accelerated-compute.md) | Brand-inspired | Chip maker unveils a GPU with benchmark charts against last year's model | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#ambient-intelligence"><img src="p/ambient-intelligence-sample-t030.jpg" width="90" alt="ambient-intelligence"></a> | [`ambient-intelligence`](docs/ambient-intelligence.md) | Brand-inspired | How a large language model uses a context window | 0.72 |
| <a href="https://tominhphong.github.io/video-style-gallery/#art-deco-luxury"><img src="p/art-deco-luxury-sample-t103.jpg" width="90" alt="art-deco-luxury"></a> | [`art-deco-luxury`](docs/art-deco-luxury.md) | Aesthetic | Perfume house relaunches a 1920s classic fragrance | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#blueprint-engineering"><img src="p/blueprint-engineering-sample-t132.jpg" width="90" alt="blueprint-engineering"></a> | [`blueprint-engineering`](docs/blueprint-engineering.md) | Aesthetic | Smartphone maker shows an exploded view of its new camera module | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#character-comedy"><img src="p/character-comedy-sample-t108.jpg" width="90" alt="character-comedy"></a> | [`character-comedy`](docs/character-comedy.md) | Brand-inspired | Habit-tracking app adds streaks and a mascot to help people save money | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#cinematic-product-launch"><img src="p/cinematic-product-launch-sample-t111.jpg" width="90" alt="cinematic-product-launch"></a> | [`cinematic-product-launch`](docs/cinematic-product-launch.md) | Brand-inspired | Camera maker launches a cinema lens with anamorphic look | 0.75 |
| <a href="https://tominhphong.github.io/video-style-gallery/#cinematic-technology"><img src="p/cinematic-technology-sample-t111.jpg" width="90" alt="cinematic-technology"></a> | [`cinematic-technology`](docs/cinematic-technology.md) | Brand-inspired | Camera maker launches a cinema lens with anamorphic look | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#comic-multiverse"><img src="p/comic-multiverse-sample-t164.jpg" width="90" alt="comic-multiverse"></a> | [`comic-multiverse`](docs/comic-multiverse.md) | House | Youth sneaker and streetwear brand announces an anime collaboration | 0.79 |
| <a href="https://tominhphong.github.io/video-style-gallery/#creative-canvas"><img src="p/creative-canvas-sample-t142.jpg" width="90" alt="creative-canvas"></a> | [`creative-canvas`](docs/creative-canvas.md) | Brand-inspired | Architects and clients review a floor plan together on a shared online board | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#creative-suite"><img src="p/creative-suite-sample-t088.jpg" width="90" alt="creative-suite"></a> | [`creative-suite`](docs/creative-suite.md) | Brand-inspired | Photo editing app releases AI masking and before-and-after tools | 0.86 |
| <a href="https://tominhphong.github.io/video-style-gallery/#data-editorial"><img src="p/data-editorial-sample-t059.jpg" width="90" alt="data-editorial"></a> | [`data-editorial`](docs/data-editorial.md) | Aesthetic | Monthly housing report: inventory, median price, days on market in Austin | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#developer-workflow"><img src="p/developer-workflow-sample-t028.jpg" width="90" alt="developer-workflow"></a> | [`developer-workflow`](docs/developer-workflow.md) | Brand-inspired | GitHub repository gains ten thousand stars in a week: what it does | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#documentary-purpose"><img src="p/documentary-purpose-sample-t149.jpg" width="90" alt="documentary-purpose"></a> | [`documentary-purpose`](docs/documentary-purpose.md) | Brand-inspired | Nature reserve outside Austin restores prairie and tells the founder's story | 0.87 |
| <a href="https://tominhphong.github.io/video-style-gallery/#editorial-collage-explainer"><img src="p/editorial-collage-explainer-sample-t175.jpg" width="90" alt="editorial-collage-explainer"></a> | [`editorial-collage-explainer`](docs/editorial-collage-explainer.md) | Brand-inspired | Tenant union zine explains your rights in plain language | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#editorial-intelligence"><img src="p/editorial-intelligence-sample-t079.jpg" width="90" alt="editorial-intelligence"></a> | [`editorial-intelligence`](docs/editorial-intelligence.md) | Brand-inspired | Sleep and screens: what the research actually says | 0.76 |
| <a href="https://tominhphong.github.io/video-style-gallery/#expressive-material"><img src="p/expressive-material-sample-t118.jpg" width="90" alt="expressive-material"></a> | [`expressive-material`](docs/expressive-material.md) | Brand-inspired | Phone operating system update personalises colours and widgets | 0.84 |
| <a href="https://tominhphong.github.io/video-style-gallery/#friendly-system-motion"><img src="p/friendly-system-motion-sample-t108.jpg" width="90" alt="friendly-system-motion"></a> | [`friendly-system-motion`](docs/friendly-system-motion.md) | Brand-inspired | Habit-tracking app adds streaks and a mascot to help people save money | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#functional-playful"><img src="p/functional-playful-sample-t169.jpg" width="90" alt="functional-playful"></a> | [`functional-playful`](docs/functional-playful.md) | Brand-inspired | How to assemble a flat-pack bookshelf in four steps | 0.88 |
| <a href="https://tominhphong.github.io/video-style-gallery/#glass-keynote"><img src="p/glass-keynote-sample-t025.jpg" width="90" alt="glass-keynote"></a> | [`glass-keynote`](docs/glass-keynote.md) | House | Phone operating system update personalises colours and widgets | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#groovy-seventies"><img src="p/groovy-seventies-sample-t134.jpg" width="90" alt="groovy-seventies"></a> | [`groovy-seventies`](docs/groovy-seventies.md) | Aesthetic | Retro seventies diner reopens in Fort Worth with a nostalgic menu | 0.86 |
| <a href="https://tominhphong.github.io/video-style-gallery/#holographic-hud"><img src="p/holographic-hud-sample-t032.jpg" width="90" alt="holographic-hud"></a> | [`holographic-hud`](docs/holographic-hud.md) | Aesthetic | Chip maker unveils a new accelerator with specs and price | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#human-storytelling"><img src="p/human-storytelling-sample-t040.jpg" width="90" alt="human-storytelling"></a> | [`human-storytelling`](docs/human-storytelling.md) | Brand-inspired | Small business spotlight: a family taqueria in San Antonio | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#immersive-console"><img src="p/immersive-console-sample-t121.jpg" width="90" alt="immersive-console"></a> | [`immersive-console`](docs/immersive-console.md) | Brand-inspired | New game console reveal: price, launch lineup and storage | 0.75 |
| <a href="https://tominhphong.github.io/video-style-gallery/#ink-woodblock"><img src="p/ink-woodblock-sample-t122.jpg" width="90" alt="ink-woodblock"></a> | [`ink-woodblock`](docs/ink-woodblock.md) | Aesthetic | History of the Mekong delta rice trade told with ink illustrations | 0.74 |
| <a href="https://tominhphong.github.io/video-style-gallery/#isometric-systems"><img src="p/isometric-systems-sample-t169.jpg" width="90" alt="isometric-systems"></a> | [`isometric-systems`](docs/isometric-systems.md) | Aesthetic | Low-code platform lets teams snap together apps from reusable blocks | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#joyful-pop"><img src="p/joyful-pop-sample-t090.jpg" width="90" alt="joyful-pop"></a> | [`joyful-pop`](docs/joyful-pop.md) | Brand-inspired | A bold ad campaign for a sparkling water brand | 0.80 |
| <a href="https://tominhphong.github.io/video-style-gallery/#manga-ink"><img src="p/manga-ink-sample-t123.jpg" width="90" alt="manga-ink"></a> | [`manga-ink`](docs/manga-ink.md) | Aesthetic | Youth sneaker and streetwear brand announces an anime collaboration | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#mid-century-retro"><img src="p/mid-century-retro-sample-t125.jpg" width="90" alt="mid-century-retro"></a> | [`mid-century-retro`](docs/mid-century-retro.md) | Aesthetic | Toy company releases a build-it-yourself robot kit for kids | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#mission-control"><img src="p/mission-control-sample-t072.jpg" width="90" alt="mission-control"></a> | [`mission-control`](docs/mission-control.md) | Brand-inspired | Space telescope releases a new deep-field image | 0.76 |
| <a href="https://tominhphong.github.io/video-style-gallery/#modular-build"><img src="p/modular-build-sample-t125.jpg" width="90" alt="modular-build"></a> | [`modular-build`](docs/modular-build.md) | Brand-inspired | Toy company releases a build-it-yourself robot kit for kids | 0.83 |
| <a href="https://tominhphong.github.io/video-style-gallery/#monochrome-developer"><img src="p/monochrome-developer-sample-t029.jpg" width="90" alt="monochrome-developer"></a> | [`monochrome-developer`](docs/monochrome-developer.md) | Brand-inspired | Command line tool that turns a README into a deployment | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#music-editorial"><img src="p/music-editorial-sample-t127.jpg" width="90" alt="music-editorial"></a> | [`music-editorial`](docs/music-editorial.md) | Brand-inspired | Year in review: most streamed songs and artists in Texas | 0.81 |
| <a href="https://tominhphong.github.io/video-style-gallery/#neon-cyberpunk"><img src="p/neon-cyberpunk-sample-t136.jpg" width="90" alt="neon-cyberpunk"></a> | [`neon-cyberpunk`](docs/neon-cyberpunk.md) | Aesthetic | Synthwave album release with a neon visual concept | 0.81 |
| <a href="https://tominhphong.github.io/video-style-gallery/#organic-biomorphic"><img src="p/organic-biomorphic-sample-t117.jpg" width="90" alt="organic-biomorphic"></a> | [`organic-biomorphic`](docs/organic-biomorphic.md) | Aesthetic | Wellness app launches a guided breathing programme | 0.88 |
| <a href="https://tominhphong.github.io/video-style-gallery/#paper-cut-collage"><img src="p/paper-cut-collage-sample-t133.jpg" width="90" alt="paper-cut-collage"></a> | [`paper-cut-collage`](docs/paper-cut-collage.md) | Aesthetic | Underground zine fair in Austin: bands, printers and tickets | 0.79 |
| <a href="https://tominhphong.github.io/video-style-gallery/#pixel-arcade"><img src="p/pixel-arcade-sample-t129.jpg" width="90" alt="pixel-arcade"></a> | [`pixel-arcade`](docs/pixel-arcade.md) | Aesthetic | Retro console returns as a mini edition with fifty games | 0.76 |
| <a href="https://tominhphong.github.io/video-style-gallery/#playful-game-system"><img src="p/playful-game-system-sample-t130.jpg" width="90" alt="playful-game-system"></a> | [`playful-game-system`](docs/playful-game-system.md) | Brand-inspired | Family board game night: new releases for the holidays | 0.74 |
| <a href="https://tominhphong.github.io/video-style-gallery/#playful-productivity"><img src="p/playful-productivity-sample-t115.jpg" width="90" alt="playful-productivity"></a> | [`playful-productivity`](docs/playful-productivity.md) | Brand-inspired | Team chat app adds threads, emoji reactions and integrations | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#precision-dark-product"><img src="p/precision-dark-product-sample-t029.jpg" width="90" alt="precision-dark-product"></a> | [`precision-dark-product`](docs/precision-dark-product.md) | Brand-inspired | Command line tool that turns a README into a deployment | 0.78 |
| <a href="https://tominhphong.github.io/video-style-gallery/#precision-hardware"><img src="p/precision-hardware-sample-t032.jpg" width="90" alt="precision-hardware"></a> | [`precision-hardware`](docs/precision-hardware.md) | Brand-inspired | Smartphone maker shows an exploded view of its new camera module | 0.89 |
| <a href="https://tominhphong.github.io/video-style-gallery/#premium-ui-demo"><img src="p/premium-ui-demo-sample-t128.jpg" width="90" alt="premium-ui-demo"></a> | [`premium-ui-demo`](docs/premium-ui-demo.md) | Brand-inspired | Wellness app launches a guided breathing programme | 0.76 |
| <a href="https://tominhphong.github.io/video-style-gallery/#product-spec-film"><img src="p/product-spec-film-sample-t132.jpg" width="90" alt="product-spec-film"></a> | [`product-spec-film`](docs/product-spec-film.md) | Brand-inspired | Smartphone maker shows an exploded view of its new camera module | 0.91 |
| <a href="https://tominhphong.github.io/video-style-gallery/#punk-zine"><img src="p/punk-zine-sample-t172.jpg" width="90" alt="punk-zine"></a> | [`punk-zine`](docs/punk-zine.md) | Aesthetic | Underground zine fair in Austin: bands, printers and tickets | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#retro-crt-broadcast"><img src="p/retro-crt-broadcast-sample-t057.jpg" width="90" alt="retro-crt-broadcast"></a> | [`retro-crt-broadcast`](docs/retro-crt-broadcast.md) | Aesthetic | Retro TV network marks fifty years with a special broadcast | 0.90 |
| <a href="https://tominhphong.github.io/video-style-gallery/#saas-bento"><img src="p/saas-bento-sample-t131.jpg" width="90" alt="saas-bento"></a> | [`saas-bento`](docs/saas-bento.md) | Aesthetic | Team chat app adds threads, emoji reactions and integrations | 0.75 |
| <a href="https://tominhphong.github.io/video-style-gallery/#sensory-tech"><img src="p/sensory-tech-sample-t118.jpg" width="90" alt="sensory-tech"></a> | [`sensory-tech`](docs/sensory-tech.md) | Brand-inspired | Phone operating system update personalises colours and widgets | 0.77 |
| <a href="https://tominhphong.github.io/video-style-gallery/#soft-clay-3d"><img src="p/soft-clay-3d-sample-t108.jpg" width="90" alt="soft-clay-3d"></a> | [`soft-clay-3d`](docs/soft-clay-3d.md) | Aesthetic | Toy company releases a build-it-yourself robot kit for kids | 0.85 |
| <a href="https://tominhphong.github.io/video-style-gallery/#sport-editorial"><img src="p/sport-editorial-sample-t084.jpg" width="90" alt="sport-editorial"></a> | [`sport-editorial`](docs/sport-editorial.md) | Brand-inspired | A fashion brand launches a limited sneaker drop | 0.82 |
| <a href="https://tominhphong.github.io/video-style-gallery/#swiss-kinetic-editorial"><img src="p/swiss-kinetic-editorial-sample-t141.jpg" width="90" alt="swiss-kinetic-editorial"></a> | [`swiss-kinetic-editorial`](docs/swiss-kinetic-editorial.md) | Aesthetic | Industrial policy announcement: new factory subsidies explained | 0.73 |
| <a href="https://tominhphong.github.io/video-style-gallery/#systematic-enterprise"><img src="p/systematic-enterprise-sample-t026.jpg" width="90" alt="systematic-enterprise"></a> | [`systematic-enterprise`](docs/systematic-enterprise.md) | Brand-inspired | AI company reports quarterly revenue, margin and backlog | 0.80 |
| <a href="https://tominhphong.github.io/video-style-gallery/#terminal-ops"><img src="p/terminal-ops-sample-t027.jpg" width="90" alt="terminal-ops"></a> | [`terminal-ops`](docs/terminal-ops.md) | Aesthetic | Command line tool that turns a README into a deployment | 0.81 |
| <a href="https://tominhphong.github.io/video-style-gallery/#y2k-liquid-chrome"><img src="p/y2k-liquid-chrome-sample-t084.jpg" width="90" alt="y2k-liquid-chrome"></a> | [`y2k-liquid-chrome`](docs/y2k-liquid-chrome.md) | Aesthetic | A fashion brand launches a limited sneaker drop | 0.76 |

**Not built yet (18):** `athletic-impact`, `bauhaus-geometry`, `calm-workspace`, `cinematic-streaming`, `community-chaos`, `constructivist-poster`, `extreme-energy`, `fluent-productivity`, `gradient-fintech`, `keynote-stage`, `kinetic-typography`, `minimal-future-product`, `monochrome-luxury`, `neo-brutalist-web`, `newsprint-editorial`, `quirky-editorial`, `vaporwave-memphis`, `wpa-screenprint`.

## Get AgentKit

The styles come from the AgentKit motion-video skill. **Affiliate disclosure:** the link below is the author's referral link; buying through it gives you 20% off your first purchase (per the AgentKit referral programme) and the author earns a commission. The gallery itself is free and Apache-2.0.

https://agentkit.best/?ref=JGRILPGH

## Notes

- Samples are generic "illustration" content, silent, and labelled as such; they show the look and motion of a style, not a real news story.
- The recipe documents are written from trial builds. Tool names inside them (the `agy` image helper, `motion_tools.py`, VieNeu voice) are private helpers of the author's setup and are not included.
- Fit scores are a guide, not a rule.

## Credits and licence

Created by **Phong To**. Apache-2.0 (see `LICENSE`). Style profiles come from [AgentKit motion-video](https://agentkit.best/?ref=JGRILPGH) (MIT); see `NOTICE` for the upstream source. Page layout inspired by video-shotcraft (Apache-2.0); no code or assets were copied.
