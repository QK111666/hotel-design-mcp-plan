# 酒店 / 商家作图设计 Skills — 给 GPT 的安装意见与清单

> 整理：海鸥（Muse），2026-11-09 实查 GitHub 后写成。
> 用途：做酒店封面、酒店头图、酒店海报、酒店长图（详情长图）、酒店宣传图，以及餐饮等各种商家的宣传作图。
> 重要前提：GitHub 上**没有专门为酒店写的 skill**。下面 7 个是实查后最接近的通用/商家/电商设计 skill，已分别 fork 到用户账号 `QK111666` 下，**每个仓单独一个，不要合并、不要互相覆盖**。请从 fork 地址安装，不要直接用上游（fork 地址才是用户自己的存档）。

---

## 一、总意见（先看结论）

**不要 7 个全装全用，会互相抢触发、风格打架。按这个优先级装：**

| 优先级 | 仓（fork 地址） | 只装其中这些 skill | 干什么用 |
|---|---|---|---|
| P0 必装 | `QK111666/luobo-design` | 整仓（就 1 个 skill） | 商家作图主流程：海报、价目表、开业/活动宣传、小红书封面；带广告法自检、可编辑交付、品牌记忆 |
| P0 必装 | `QK111666/baoyu-skills` | `baoyu-cover-image`、`baoyu-infographic`、`baoyu-xhs-images`、`baoyu-image-gen` | 封面图引擎 + 长图/信息图引擎 + 成套图文卡 |
| P0 必装 | `QK111666/ecommerce-image-skills` | `xiaohongshu-cover`、`taobao-detail-long-image`、`sale-banner`、`selling-point-infographic`、`ecommerce-listing-suite` | 主图/卖点图/大促 Banner/详情长图整套出图；有“产品身份锁定”，能锁住酒店房间照不被 AI 改样 |
| P1 装 1 个子集 | `QK111666/ui-ux-pro-max-skill` | **只装 `banner-design`**（路径 `.claude/skills/banner-design/`），其余 12 个 skill 不要装 | 横版封面/头图/Header/网站 Hero，HTML/CSS 出精确尺寸 PNG，内置尺寸与安全区 |
| P2 按需 | `QK111666/poster-generator-skill` | 整仓（就 1 个 skill） | 纯文本 → 设计师级海报，20 种风格，适合活动海报快速起稿 |
| P2 按需（只借流程） | `QK111666/qiaomu-poster` | 整仓（就 1 个 skill） | 只借它的“商业海报 + 可验证二维码 + 可编辑排字”流程，案例图很多、仓很重（58MB 无 .git），不要把案例素材当模板照抄 |
| P3 只当参考库 | `QK111666/designskills` | 不要全装；只挑 `poster-design`、`banner-design`、`thumbnail-design`、`social-media-graphic`、`ad-creative-design` 读其规则 | 品类最全的规则合集，靠 Gemini 生图；星数低（19），当参考不当主力 |

**酒店专用化改造（装完必须做，不要原样用）：**
1. 新建酒店版预设，不要改坏原 skill：封面（抖音团购商品图比例 + 底部标题安全区，卖点/价格不得压到底部平台信息区）、头图（横版，酒店名+核心卖点+实景图）、海报（竖版 1080×1920，标题 > 卖点 > 价格 > 二维码层级）、长图（按模块分屏：头图卖点 → 房型 → 设施 → 餐食 → 位置/交通 → 须知，每屏单独出图再用拼接脚本合成，切片导出）。
2. 房间/大堂/外景照片执行“身份锁定”：形状、颜色、Logo、文字原样带入每条提示词，禁止 AI 重绘房间结构；没有真实照片时宁可出提示词，也不要编造酒店实景。
3. 价格、房型名、早餐/取消政策等事实只能用商家提供的数据，禁止编造；出图后自检：文字溢出、对比度、广告法违禁用语（“最/第一/顶级”等）、二维码可扫性、手机小图预览可读性。
4. 同一家酒店的品牌色、字体、Logo、电话存成品牌配置复用（借 luobo-design 的品牌记忆做法），换酒店时先换品牌配置再出图。

---

## 二、每个仓的实查档案（2026-11-09 核过）

### 1. luobo-design（萝卜设计）— P0
- Fork：https://github.com/QK111666/luobo-design
- 上游：https://github.com/zhouwei713/luobo-design
- 星/许可/更新：89 星 · MIT · 2026-11-04 更新 · 本地核验 commit `5710c083`
- 内容：1 个 SKILL.md。开业海报、活动海报、通知、菜单、价目表、名片、logo、小红书封面（8 种结构）。流程：最多问 3 个问题 → 出 3 个视觉方向（稳妥/概念/大胆）→ 规格文件一条命令出图 → 自检文字溢出/对比度/广告法 → 交付带 `editor.html` 可点改。
- 依赖：Node.js；`pip install playwright pillow fonttools brotli` + `python -m playwright install chromium`。不接生图模型也能用（程序排字+插画）；接了可走 OpenAI/Gemini/即梦等（配置见仓内 `references/imagegen.md`，Key 放环境变量，不要写进文件）。
- 安装：`npx skills add QK111666/luobo-design`

### 2. baoyu-skills（宝玉）— P0，只装 4 个子 skill
- Fork：https://github.com/QK111666/baoyu-skills
- 上游：https://github.com/JimLiu/baoyu-skills
- 星/许可/更新：27,415 星 · MIT · 2026-11-06 更新 · 本地核验 commit `ca703c2d`，仓内共 22 个 SKILL.md
- 只装：`skills/baoyu-cover-image/`（封面，类型×配色×渲染×文字×情绪，11 配色×7 渲染）、`skills/baoyu-infographic/`（长图/信息图，21 版式×多风格）、`skills/baoyu-xhs-images/`（成套图文卡，封面钩子+内容卡+收尾 CTA，第一张做锚图保证全套风格一致）、`skills/baoyu-image-gen/`（多供应商生图引擎）。
- 注意：其余 18 个（漫画、幻灯、翻译、发帖等）与酒店作图无关，不要装，避免触发混乱。它的封面默认偏手绘风，酒店要实景商业风时必须在参数里明确写死风格。
- 安装（只装子集时手动复制对应文件夹到 skills 目录）：`npx skills add QK111666/baoyu-skills` 后删除不需要的子 skill，或逐个复制上述 4 个文件夹。

### 3. ecommerce-image-skills（电商出图）— P0，只装 5 个子 skill
- Fork：https://github.com/QK111666/ecommerce-image-skills
- 上游：https://github.com/xianyu110/ecommerce-image-skills
- 星/许可/更新：162 星 · MIT · 2026-10-08 更新 · 本地核验 commit `f4566fdc`，仓内共 12 个 SKILL.md，体积最小（344KB 无 .git）
- 只装：`skills/xiaohongshu-cover/`（3:4，6 种爆款版式）、`skills/taobao-detail-long-image/`（750 宽详情长图，分屏规划+拼接切片脚本 — 改成酒店详情长图就靠它）、`skills/sale-banner/`（大促 Banner 多平台尺寸）、`skills/selling-point-infographic/`（一图一卖点）、`skills/ecommerce-listing-suite/`（总入口，规划整套图并质检）。
- 依赖：优先用宿主自带生图工具；否则需 `GPTIMAGE_API_KEY`（任意 OpenAI 兼容接口，`GPTIMAGE_BASE_URL` 可配）。没有 Key 时它只输出最终提示词。仓 README 里推荐的第三方镜像/API 站是作者的推广，**不要照单全收、不要把 Key 填进不明站点**，用官方或自己已有的网关。
- 安装：`npx skills add QK111666/ecommerce-image-skills`

### 4. ui-ux-pro-max-skill 里的 banner-design — P1，只装这 1 个
- Fork：https://github.com/QK111666/ui-ux-pro-max-skill
- 上游：https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- 星/许可/更新：整仓 147,190 星 · MIT · 2026-11-07 更新 · 本地核验 commit `4f2dbb67`
- 只装：`.claude/skills/banner-design/`。做社交封面、广告图、网站 Hero、印刷横幅；一次给多个艺术方向（22 种风格），HTML/CSS → 浏览器截图导出精确尺寸 PNG，内置各平台尺寸表与安全区。
- 注意：整仓有 13 个 SKILL.md（UI/设计系统/幻灯等），全装会污染触发。只复制 banner-design 一个文件夹。
- 安装：手动复制 `.claude/skills/banner-design/` 到目标 Agent 的 skills 目录。

### 5. poster-generator-skill — P2
- Fork：https://github.com/QK111666/poster-generator-skill
- 上游：https://github.com/howardz27/poster-generator-skill
- 星/许可/更新：37 星 · MIT · 2026-09-24 更新 · 本地核验 commit `fa2a40bf`
- 内容：1 个 SKILL.md。任意文本 → 生产级海报：自动分析内容、组织信息、荐风格、写精细生图 prompt，再调用宿主已有的生图工具渲染。20 种视觉风格。
- 依赖：宿主必须有可用的生图 skill/工具，否则只能出 prompt。仓体积 24MB（无 .git）多为示例图。
- 安装：`git clone https://github.com/QK111666/poster-generator-skill.git ~/.claude/skills/poster-generator`（Codex 用 `~/.agents/skills/`）

### 6. qiaomu-poster — P2，只借流程
- Fork：https://github.com/QK111666/qiaomu-poster
- 上游：https://github.com/joeseesun/qiaomu-poster
- 星/许可/更新：7 星 · MIT（仓内声明）· 2026-10-27 更新 · 本地核验 commit `32c377fb`
- 内容：1 个 SKILL.md。给网址/活动信息/Logo → 商业活动海报：品牌主视觉 + 可编辑 HTML 排字 + 确定性二维码生成 + 逐张看图质检，18 个真实案例。
- 注意：星数低、仓最重（58MB 无 .git，全是案例图）。价值只在“二维码可扫验证 + 排字与生图分离”这套做法，酒店订房二维码海报可借鉴。不要全量复制案例素材。
- 安装：`git clone https://github.com/QK111666/qiaomu-poster.git` 后读其 SKILL.md 执行。

### 7. designskills — P3，参考库
- Fork：https://github.com/QK111666/designskills
- 上游：https://github.com/ArnavPuri/designskills
- 星/许可/更新：19 星 · MIT · 2026-09-28 更新 · 本地核验 commit `c7873015`，仓内共 28 个 SKILL.md
- 有用子集：`skills/poster-design/`、`skills/banner-design/`、`skills/thumbnail-design/`（视频封面/文章头图）、`skills/social-media-graphic/`、`skills/ad-creative-design/`、`skills/infographic/`。
- 依赖：生图走 Gemini 3.1 Flash Image，需 `GEMINI_API_KEY`，`pip install google-genai Pillow`。
- 意见：规则写得全，但社区验证少。只读它的尺寸/构图/品牌上下文（design-context）规则，不要作为唯一出图主力。
- 安装（仅参考时）：`npx skills add QK111666/designskills --skill poster-design banner-design thumbnail-design`

---

## 三、给 GPT 的原话（用户可整段复制）

```
请安装并使用以下 GitHub 仓库里的 Agent Skills，为我做酒店和商家的宣传作图（酒店封面、头图、海报、详情长图、宣传图、团购主图/Banner）：

P0 必装：
1. https://github.com/QK111666/luobo-design —— 整仓安装（商家海报/价目表/小红书封面主流程）
2. https://github.com/QK111666/baoyu-skills —— 只装 baoyu-cover-image、baoyu-infographic、baoyu-xhs-images、baoyu-image-gen 四个子 skill，其余不要装
3. https://github.com/QK111666/ecommerce-image-skills —— 只装 xiaohongshu-cover、taobao-detail-long-image、sale-banner、selling-point-infographic、ecommerce-listing-suite 五个子 skill

P1：
4. https://github.com/QK111666/ui-ux-pro-max-skill —— 只装 .claude/skills/banner-design 一个，不要装整仓其他 skill

P2 按需再装：QK111666/poster-generator-skill、QK111666/qiaomu-poster；QK111666/designskills 只作参考、不要全装。

安装后请先逐个读它们的 SKILL.md，向我汇报：每个 skill 的触发方式、依赖（需要哪个生图 API Key）、输入输出格式。然后按文档里的“酒店专用化改造”四条，为我新建一套酒店预设（封面/头图/海报/长图），不要改坏原 skill。所有价格和酒店事实必须用我给的数据，禁止编造；房间照片必须锁定原样，禁止重绘房间结构。先拿我接下来给的一家酒店资料试做一套（封面+头图+海报+长图）给我看，确认后再批量。
```

---

## 四、本地存档说明

- 7 个仓已由海鸥在本机完整下载并逐个核验 SKILL.md 数量与许可证（见上），原始下载存 `workspace/design-skills-github-2026-11-09/raw/`（每仓独立文件夹、独立 .git）。
- GitHub 侧采用 **fork** 方式存到 `QK111666`：每个仓单独一个 fork、与上游同名、保留完整历史与许可证，GPT 用 `npx skills add QK111666/<仓名>` 或 git clone 即可安装，与从上游安装等价。fork 前已查：这 7 个名字在 QK111666 下均无同名仓（API 返回 404），不会覆盖已有仓。
- **完成状态（2026-11-09 22:37 CST 复核）：7 个 fork 已全部创建成功，并经 GitHub API 二次核验——7/7 均为 `fork=true`、parent 与上游一一对应、均为公开仓。**
