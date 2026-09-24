# grot-bot X 游戏推文采集规范 v1

目的：让 grot-bot **给出可人工核对的候选事实**，而不是直接写网站宣传文案。每条推文输出一个 JSON 对象。找不到的信息写 `null`，不要猜测游戏名、平台、发布时间、工具版本或可玩链接。截图或视频海报必须来自原帖/作者页面；保留原始 URL 和来源。不可把 X 视频或商店页当作可玩游戏。

## 输入

给机器人一条完整状态页 URL，例如：

- `https://x.com/slicknickstudio/status/2099606594854260751`
- `https://x.com/araskodluyor/status/2094945201727168548`

## 必填输出结构

```json
{
  "x_post_url": "https://x.com/handle/status/123",
  "post_id": "123",
  "author_handle": "handle",
  "author_display_name": null,
  "posted_at_utc": null,
  "post_text_exact": "原帖完整原文，保留换行与表情",
  "media": [
    {
      "kind": "video",
      "poster_url": "https://pbs.twimg.com/...",
      "duration_seconds": null,
      "width": null,
      "height": null,
      "source_post_url": "https://x.com/handle/status/123"
    }
  ],
  "expanded_external_links": [
    { "url": "https://creator.example/game", "label_in_post": "Play it here", "purpose": "play_candidate" }
  ],
  "game_title_as_stated": null,
  "play_url_candidate": null,
  "playability": "playable | showcase | unknown",
  "platforms_evidenced": [],
  "genre_candidate": "other",
  "gameplay_observed": null,
  "ai_claims": [
    { "exact_quote": "原文相关片段", "role_candidate": "ai_built", "tool_names_as_stated": [], "evidence_url": "https://x.com/handle/status/123" }
  ],
  "creator_project_url": null,
  "facts_needing_verification": [],
  "checked_at_utc": null
}
```

字段要求：`post_id` 保持字符串，避免大整数精度丢失；`posted_at_utc` 必须带 `Z` 和核实来源，界面本地时间不能直接当 UTC；`checked_at_utc` 在真实采集时填写当前 UTC 时间；`post_text_exact` 不得翻译或改写；短链要展开；`media` 写海报/图片源和时长，**不要提交登录后才可访问或短期失效的 blob 视频 URL**。`gameplay_observed` 只描述视频可见内容，不能推断完整玩法。`platforms_evidenced` 只写有证据的平台。`ai_claims` 每条要有原文片段和 URL。将工具名、型号按原帖拼写保留，网页简介可另由编辑翻译。封面本地化与转载权限由编辑核对。

## 判定规则

1. `playable`：原帖或作者项目页给出能实际运行的公开版本；`play_url_candidate` 指向游戏本身。进入页面并看到 Run/Play 或真实游戏界面后才能在主库定为 `playable`。
2. `showcase`：有演示视频/图片，但没有核实可玩的公开版本；主按钮指向 X 原帖。
3. `unknown`：推文或链接无法读取，不能下结论。不要用 Steam、App Store、Google Play、公司首页或预告片 URL 填 `play_url_candidate`。
4. 类型从可见玩法判定。动作、休闲、益智、赛车、射击、体育、策略、模拟、冒险、生存、角色扮演；不明确用 `other`。
5. 输出不包含虚构的搜索量、玩家数、AI 用途或授权结论。事实与推测分开放到 `facts_needing_verification`。

## 两条样例的已核对要点

### Slicknick Studio

[原帖](https://x.com/slicknickstudio/status/2099606594854260751)写明游戏名 **Bring Them Home**、72 小时 Game Jam、单人周末制作、Claude + Unity MCP 工作流，带约 15 秒视频并附 [itch.io 游戏页](https://slicknickstudio.itch.io/bringthemhome)。游戏页有 **Run game**，因此可作为 `playable` 候选。itch.io 页还披露 Tripo、Mixamo、ElevenLabs 等资产/配音工具。机器人仍要返回原文、展开链接、海报、UTC 时间和证据，而非只给一句摘要。

### araskodluyor

[原帖](https://x.com/araskodluyor/status/2094945201727168548)介绍三天制作的蟑螂合作游戏片段，提及 Gemini 3.7 Flash + Blender MCP 和 Unity MCP，视频约 69 秒。帖子未见公开游戏地址，因此是 `showcase` 候选，`play_url_candidate` 为 `null`。游戏正式名称和目标平台如果无法确认，分别返回 `null` 和空数组。网站目前用 **Cockroach Co-op Prototype** 作编辑标题，并在详情页说明没有核实可玩版本。

## 编辑接收流程

机器人输出 → 人工打开原帖与展开链接 → 核对 AI 原话/可玩状态/玩法分类 → 选用真实图片或视频海报并记来源 → 写简短英中介绍 → 加入 `data/cases.json` → 网站同步、构建与链接检查。若 X 删除或媒体失效，保留可验证的作者来源或撤下案例。
