# SEO 主题与内页规划 v1

本地审核稿，2026-09-23。参考了用户给的 [Web Cafe 教程](https://new.web.cafe/tutorial/detail/if8ls06pcd) 对关键词、内容、技术 SEO、监测的分工，并按 [Google Search Central SEO 入门指南](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)和[多语言网站指南](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)落实。**没有真实搜索量数据**，以下是按搜索意图提出的待验证主题，不能当作流量承诺。

## 搜索意图与当前页面

| 意图 | 英文长尾词示例 | 中文长尾词示例 | 页面 |
| --- | --- | --- | --- |
| 找可玩的目录 | play AI-made browser games, AI-built games you can play online | AI 制作的网页游戏在线玩、可玩的 AI 游戏合集 | 首页 `/` 与 `/zh-CN/` |
| 按玩法找游戏 | AI browser shooter games, AI-made racing browser game, AI puzzle game online | AI 网页射击游戏、AI 制作的赛车网页游戏、AI 益智游戏 | `/genres/[genre]/` |
| 找具体作品 | Claude of Tanks browser game, Pelican on a Bike play online, Bring Them Home game jam | Claude of Tanks 在线玩、鹈鹕骑单车网页游戏、Bring Them Home 雪地救援 | `/games/[slug]/` |
| 了解 AI 用途/可玩性 | how was AI used to make [game], is [game] playable | [游戏名] 如何使用 AI、[游戏名] 能玩吗 | 案例详情正文与 FAQ |
| 采集/提交 | submit AI game to directory, AI game X showcase | 提交 AI 游戏、X AI 游戏推文收录 | `/faq/`，未来独立提交说明页 |
| 按模型找案例 | GPT-6 Astra games, GPT-6 Sol games, Claude Opus 5.5 games | GPT-6 Astra 游戏、GPT-6 Sol 游戏、Claude Opus 5.5 游戏 | 首页可见模型区、已核实案例详情；有足够案例后再生成模型页 |

标题和正文应回答相应问题，自然使用词语。Web Cafe 教程提到的固定关键词密度、固定字数之类经验值不作为门槛；Google 明确建议为人写有用内容，并避免堆砌关键词。先在 Search Console 看真实查询词，再调整标题与内容。

模型名称同时进入页面可见正文、案例搜索与适用案例的 metadata keywords。metadata keywords 对 Google 排名没有直接保证，因此主要依靠真实案例正文和内部链接。有模型证据的案例写入 `models`；没有证据的模型只作为目录关注方向，不强行绑定到项目。等某个模型积累至少两到三条独立案例后，再考虑生成 `/models/[model]/`，避免单条或空白薄页。

## 已落地

- 每条案例有英中静态 HTML、独立 title/description、可见玩法与 AI 用途、真实图片 alt、来源与直达链接。
- 首页、案例、类型、FAQ 有可爬取的普通链接；客户端筛选是增强，默认完整列表已在 HTML 中。
- 英文默认、中文独立 URL，canonical 和 `hreflang`（en、zh-CN、x-default）；Open Graph 图片与推文卡片；`robots.txt` 和包含当前内容页的 `sitemap.xml`。
- 首页 `CollectionPage`/`ItemList`，案例按实际可玩性使用 `VideoGame` 或 `CreativeWork`，案例/类型/FAQ 有 `BreadcrumbList`。结构化数据与可见内容一致。
- FAQ 是真实可见内容。Google 目前大幅限制 FAQ 富结果展示，因此**不把 FAQPage rich result 当成目标**，也不为排名机械添加问答标记。
- `sitemap.xml` 只包含已生成且有内容的类型；不伪造更新频率或优先级。正式域名确定后重建，绝不发布 localhost canonical。

## 未来新增内页的预留规则

1. 新游戏进入 `data/cases.json` 后自动生成双语 `/games/[slug]/`，加入首页列表和 sitemap。标题、简介、真实媒体、玩法、AI 证据、来源均须独特。
2. 新玩法类型进入枚举、翻译与 `genreText` 后，**至少有一条案例**才生成双语 `/genres/[genre]/`；避免空页。只有足够内容与明确搜索需求时再做更细的子类型页。
3. 可增加 `/guides/[slug]/`（如“如何判断 AI 参与制作”）、`/collections/[slug]/`（如 Game Jam 专题）、`/creators/[slug]/`。发布条件：原创正文、明确作者/案例关系、双语内容、独立搜索意图、真实内部链接；不能批量造只有标题和卡片的薄页。
4. 新闻/时间敏感页要有真实发布日期和实质更新；不用把“核对链接日期”当成内容更新时间。若未来提供视频播放，先满足 Google 视频页面与 VideoObject 的可见性要求，再添加标记。

## 发布与持续检查

- 正式 `SITE_URL`、双语 canonical/hreflang、sitemap URLs、404、移动端和分享图；提交 sitemap 到 Search Console 后看索引覆盖与查询数据。
- 用 PageSpeed Insights/Core Web Vitals 检查图片尺寸和首屏加载；图片压缩且不阻塞文本。动态 iframe 由用户点击后才加载。
- 定期检查游戏、X、封面链接；停服时更新状态或撤下。`lastmod` 只在正文真实更改时记录。
- 观察搜索词后补充能回答实际问题的正文与 FAQ；不堆砌词，不承诺特定排名或 FAQ 富结果。

主要依据：[Google SEO 入门](https://developers.google.com/search/docs/fundamentals/seo-starter-guide)、[Google 搜索基本要求](https://developers.google.com/search/docs/essentials)、[站点地图指南](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap)、[多语言 URL](https://developers.google.com/search/docs/specialty/international/managing-multi-regional-sites)、[FAQ 富结果政策](https://developers.google.com/search/blog/2023/08/howto-faq-changes)。
