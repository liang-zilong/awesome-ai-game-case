# Case data schema v0.3

`data/cases.json` is the content source of truth. The website's `npm run sync:data` validates and copies it with matching media from `media/cases/`. Required fields:

| Field | Meaning |
| --- | --- |
| `id` | Stable lowercase slug, unique across the catalog. |
| `title`, `summary`, `description`, `gameplay`, `ai_use`, `cover_alt` | Objects with nonempty `en` and `zh-CN` values. Visible detail copy should be original and factual. |
| `creator` | Creator or team; use an honest unknown/team label when the public page is unclear. |
| `platforms` | Nonempty list of `mobile`, `web`, `pc`. These are game platforms, not source websites. |
| `genre` | One primary genre: `action`, `casual`, `puzzle`, `racing`, `shooter`, `sports`, `strategy`, `simulation`, `adventure`, `survival`, `role_playing`, `other`. Unclear cases use `other`. |
| `ai_roles` | Evidence-backed roles such as `ai_built`, `art_audio`, `gameplay`, `npc`, `world_generation`; `unverified` when the creator's public material does not establish the AI role. |
| `models` | Evidence-backed model/tool names for discovery and SEO, such as `GPT-6 Astra` or `Claude Opus 5.5`. Use `[]` when the source does not establish a model. |
| `status` | `playable` or `showcase` for current cases; `demo` and `unavailable` reserved for later use. |
| `play_url` | Direct public game page, or `null` for X-only showcases. Store listing and generic platform landing pages are excluded. |
| `source_url` | Primary project repository, creator page or post. |
| `x_post_url` | Canonical original X status URL when known, else `null`. A showcase requires this. |
| `cover_url` | Local `/cases/filename.jpg`/`.png`/`.webp`, always backed by a real game screenshot or source video poster. No generated glyph placeholder. |
| `cover_source_url` | Public page/asset used to obtain the image or screenshot. Visible attribution in the case page. |
| `preview_mode` | `iframe` for a web game preview candidate, `none` otherwise. Never assume all targets permit embedding. |
| `added_at`, `verified_at` | `YYYY-MM-DD`; update `verified_at` after checking links and key claims. |

All link fields except local `cover_url` use HTTPS. The sync script rejects missing bilingual fields, invalid genre/platform, missing images, store-only URLs, and cases with neither playable URL nor X post. A release check should also inspect image dimensions, link reachability and factual evidence; syntactic validation cannot establish truth.
