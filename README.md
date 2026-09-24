# Awesome AI Game Case

[简体中文](README_CN.md)

A source-first list of playable games and game experiments made with AI. Every entry includes a direct game or original showcase link, a concise description, a genre, the documented AI role, and a real game screenshot or source video poster.

The companion website is maintained in the separate `awesome-ai-game-case-web` repository. English is the default website language; Simplified Chinese is available under `/zh-CN/`.

## What belongs here

- A direct playable game URL, or an original creator post when no public build exists.
- A real screenshot or video poster with its source recorded.
- A clear distinction between AI-assisted development, generated assets, AI characters/gameplay, and an unverified AI role.
- One primary game genre and one or more actual runtime platforms.
- English and Simplified Chinese descriptions backed by the listed source.

Store-only pages, generic platform landing pages, unsupported AI claims, and abstract placeholder covers are excluded.

## Playable games

| Game | Genre | Model / workflow | Play | Source |
| --- | --- | --- | --- | --- |
| [Pelican on a Bike](https://claude-opus-5-5.riba2534.cn/) | Casual | Claude Opus 5.5, one-prompt coding experiment | [Play](https://claude-opus-5-5.riba2534.cn/) | [GitHub](https://github.com/riba2534/claude-opus-5-5-demo) |
| [Transport Ship 3D](https://claude-opus-5-5-cf-transport-ship.pages.dev/) | Shooter | Claude Opus 5.5, one-prompt coding experiment | [Play](https://claude-opus-5-5-cf-transport-ship.pages.dev/) | [GitHub](https://github.com/riba2534/claude-opus-5-5-demo) |
| [QQ Speed 3D Experiment](https://claude-opus-5-5-qqfeiche3d.pages.dev/) | Racing | Claude Opus 5.5, one-prompt coding experiment | [Play](https://claude-opus-5-5-qqfeiche3d.pages.dev/) | [GitHub](https://github.com/riba2534/claude-opus-5-5-demo) |
| [Doodle District](https://doodleshooter.vercel.app/) | Shooter | AI role awaits creator confirmation | [Play](https://doodleshooter.vercel.app/) | [Game site](https://doodleshooter.vercel.app/) |
| [Fish Feast](https://fish-feast-sea-game.yanyuzhumang.chatgpt.site/) | Puzzle | AI role awaits creator confirmation | [Play](https://fish-feast-sea-game.yanyuzhumang.chatgpt.site/) | [Game site](https://fish-feast-sea-game.yanyuzhumang.chatgpt.site/) |
| [Claude of Tanks](https://claudeoftanks.kevinliu.studio/) | Action | Claude and Codex development assistance | [Play](https://claudeoftanks.kevinliu.studio/) | [GitHub](https://github.com/Kevin-Liu-01/Claude-of-Tanks) |
| [Bring Them Home](https://slicknickstudio.itch.io/bringthemhome) | Adventure | Claude + Unity MCP and disclosed asset tools | [Play](https://slicknickstudio.itch.io/bringthemhome) | [X post](https://x.com/slicknickstudio/status/2099606594854260751) |
| [Bubble Bay](https://bubble-bay.tripo.page/) | Action | GPT-6 Astra, Tripo P2, ElevenLabs | [Play](https://bubble-bay.tripo.page/) | [Tripo prompt page](https://www.tripo3d.ai/3d-prompts/bubble-bay) |
| [Opus 5.5 NBA 2K](https://genex.games/opus-2k) | Sports | Claude Opus 5.5 keyword recorded from the published title | [Play](https://genex.games/opus-2k) | [Genex page](https://genex.games/opus-2k) |

## X showcase

| Game | Genre | What is available | Original post |
| --- | --- | --- | --- |
| Cockroach Co-op Prototype | Action | A 69-second co-op gameplay clip; no public build was linked. | [View on X](https://x.com/araskodluyor/status/2094945201727168548) |

## Model discovery

The index tracks search intent including **GPT-6 Astra games**, **GPT-6 Sol games**, and **Claude Opus 5.5 games**. A model name is attached to an individual case only when the public title or creator source supports it. A keyword appearing here does not claim that the catalog already contains a verified project for every model.

## Repository structure

```text
data/cases.json            canonical bilingual case data
media/cases/               editorial screenshots and source posters
docs/CASE_SCHEMA.md        case fields and validation rules
docs/X_COLLECTION_SPEC.md  X collection contract for grot-bot
docs/SEO_PLAN.md           search themes and future page rules
docs/PLAN.md               product and website plan
```

The website repository runs `npm run sync:data` before a build. It validates the records, copies the JSON snapshot, and syncs matching media into its public directory.

## Add a case

Follow [the schema](docs/CASE_SCHEMA.md) and edit `data/cases.json`. Add the matching image under `media/cases/`. Use `other` when the genre is unclear, an empty `models` array when no model is verified, and `unverified` when the public source does not establish the AI role.

For X candidates, use the [grot-bot collection specification](docs/X_COLLECTION_SPEC.md). Bot output remains a draft until a human checks the original post, expanded links, playable state, media, model claims, and creator identity.

## License and media

Repository code, original documentation, and original data structure are released under the [MIT License](LICENSE). Third-party game screenshots, posters, names, trademarks, and linked content remain the property of their respective owners and are not relicensed by this repository. Review media reuse before public release.
