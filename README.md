# hotel-design-mcp-plan — 酒店/商家作图软件（MCP 化）方案仓

> 本仓是**方案与决策仓**，不是代码仓。用途：把酒店封面、头图、海报、详情长图、宣传图及各类商家作图的计划集中放一处，供 GPT（或其他智能体）读完后决定并实施「做成服务器软件 + 接入 GPT 生图 + 自带 Bot 经 MCP 调用」。
> 整理：海鸥（Muse），2026-11-09。

## 文件导读（按顺序读）

| 文件 | 内容 | 谁该读 |
|---|---|---|
| `01-skill-suggestions-and-install.md` | 7 个设计 skill 仓的实查档案、优先级（P0–P3）、只装哪些子集、依赖与坑、酒店专用化改造 4 条 | GPT 装 skill 前必读 |
| `02-mcp-software-plan.md` | 软件总体方案：架构、11 个 MCP 工具规格、渲染分工铁律、自带 Bot 设计、鉴权与成本、v0→v1→v2 路线图、未定事项 | 做软件决策时必读 |
| `03-gpt-decision-task.md` | 给 GPT 的任务单原话（可整段复制）+ 用户验收口径 | 用户直接复制使用 |

## 关联的 7 个 skill 仓（已 fork 到 QK111666，单独分开，不要合并）

| 仓 | 上游 | 用途定位 |
|---|---|---|
| https://github.com/QK111666/luobo-design | zhouwei713/luobo-design | P0 商家作图主流程（海报/价目表/小红书封面） |
| https://github.com/QK111666/baoyu-skills | JimLiu/baoyu-skills | P0 封面/长图/成套图文引擎（只用 4 个子 skill） |
| https://github.com/QK111666/ecommerce-image-skills | xianyu110/ecommerce-image-skills | P0 主图/卖点图/Banner/详情长图（只用 5 个子 skill） |
| https://github.com/QK111666/ui-ux-pro-max-skill | nextlevelbuilder/ui-ux-pro-max-skill | P1 只用 banner-design（头图/横版封面） |
| https://github.com/QK111666/poster-generator-skill | howardz27/poster-generator-skill | P2 文本直出海报 |
| https://github.com/QK111666/qiaomu-poster | joeseesun/qiaomu-poster | P2 只借二维码验证流程 |
| https://github.com/QK111666/designskills | ArnavPuri/designskills | P3 规则参考库 |

> 7 个 fork 保持上游原样、不往里加文件，是为了 GPT 用 `npx skills add QK111666/<仓名>` 安装时与上游等价、不被额外文件干扰。所有计划性文档集中放本仓。

## 决策状态

- 方向已定（用户，2026-11-09）：做成服务器软件，接入 GPT 生图，软件自带 Bot，Bot 与外部智能体统一走 MCP。
- 未定（见 `02` 第 9 节与 `03` 决策题）：Bot 通道、对话/生图模型细节、部署规格、人工闸门、费用上限、平台尺寸实测数值。
- 下一步：用户把本仓给 GPT → GPT 按 `03` 回报三步 → 用户拍板 → 开工。
