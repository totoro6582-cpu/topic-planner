# 选题过三关 · Topic Planner

内容选题策划与判断 Agent（Claude Code / Cowork Skill）。
A content-topic planning & judgment skill for Claude Code / Cowork.

---

## 这是什么 / What it does

**中文**：这个技能覆盖图书出版、公众号图文、短视频（抖音/视频号/B站）、小红书笔记、播客音频五类媒介，帮你做两件事：①从一批材料（访谈、笔记、行业观察）里提炼可发布的选题；②判断一个已有选题、标题或方向值不值得做、有没有市场。判断的核心是一套跨媒介通用的框架——**选题过三关**：需求关 → 竞争关 → 回报关，前两关是硬门槛，第三关是加速器。

**English**: This skill covers five media types — book publishing, WeChat articles, short video (Douyin/Video Channels/Bilibili), Xiaohongshu notes, and podcasts. It does two things: (1) extracts publishable topics from raw materials (interviews, notes, industry observations), and (2) judges whether an existing topic/title/direction is worth pursuing. Judgment runs on a medium-agnostic framework called **Clear the Three Gates**: Demand Gate → Competition Gate → Return Gate. The first two are hard pass/fail gates; the third is an accelerator, not a bar.

---

## 支持的媒介 / Supported media

| 媒介 / Medium | 参考文件 / Reference file |
|---|---|
| 图书出版 / Book publishing | `references/media-criteria/图书.md` |
| 公众号图文 / WeChat articles | `references/media-criteria/公众号图文.md` |
| 短视频（抖音/视频号/B站）/ Short video | `references/media-criteria/短视频.md` |
| 小红书笔记 / Xiaohongshu notes | `references/media-criteria/小红书笔记.md` |
| 播客音频 / Podcasts | `references/media-criteria/播客音频.md` |
| 其他媒介 / Anything else | 类推最接近的一类 / Reason by analogy to the closest of the five above |

---

## 两种模式 / Two modes

**中文**
- **模式一 · 选题提炼**：你有一批原始材料，还没确定选题。技能会梳理主题、判断受众、提炼 1-3 个选题、给出标题/结构建议，并用「选题过三关」逐项评估。
- **模式二 · 选题判断**：你已经有明确选题/标题/方向，只想知道值不值得做。技能会先联网检索该媒介的市场数据，再逐关判断，跳过标题和目录（除非你明确要求）。

**English**
- **Mode 1 — Topic extraction**: you have raw material but no fixed topic yet. The skill surfaces the core theme, identifies the audience, extracts 1–3 candidate topics, suggests titles/structure, and evaluates each via Clear the Three Gates.
- **Mode 2 — Topic judgment**: you already have a topic/title/direction and just want a verdict. The skill searches the web for medium-specific market data first, then judges gate by gate — skipping title/structure generation unless you ask for it.

---

## 核心框架：选题过三关 / Core framework: Clear the Three Gates

| # | 关卡 / Gate | 性质 / Type | 判断项 / Items |
|---|---|---|---|
| 01 | 需求关 / Demand Gate | 硬门槛 / Hard | 话题势能 Topic momentum · 刚需强度 Need intensity · 即时驱动力 Immediate drive（因媒介而变 / label & action vary by medium） |
| 02 | 竞争关 / Competition Gate | 硬门槛 / Hard | 竞争位势 Competitive position · 载体适配度 Format fit |
| 03 | 回报关 / Return Gate | 加速器 / Accelerator | 触达潜力 Reach potential · 复利潜力 Compounding potential |

判断阈值：需求关、竞争关任一项「不成立」都要降级；两关合计 2 项及以上不成立，或「刚需强度」「即时驱动力」单独一项不成立，直接建议暂不推进。回报关不影响是否推进，只影响要不要加码。

Threshold: any hard-gate failure downgrades the recommendation; 2+ failures across the two hard gates, or a lone failure on "need intensity" / "immediate drive," means recommending to hold off. The Return Gate never blocks a go/no-go call — it only tells you whether to invest more.

**数据支撑要求 / Data-support requirement**：所有判断必须先联网检索对应媒介的市场数据，检索不到的项目标注「存疑——缺乏数据」，不得编造数字或来源。All verdicts must be backed by web-searched market data for the identified medium; items with no data found are marked "unverified — no data," never fabricated.

---

## 文件结构 / File structure

| 文件 / File | 用途 / Purpose | 何时读取 / When to read |
|---|---|---|
| `SKILL.md` | 主入口：触发时机、核心工作流、标准输出格式 / Main entry: triggers, workflow, output template | 每次调用 / Every invocation |
| `references/gotchas.md` | 16 条常见陷阱与处理规则 / 16 known failure modes & rules | 判断/提炼过程中按需 / As-needed during judgment |
| `references/media-criteria/*.md` | 五类媒介各自的数据源、三关具体指标、产出物格式 / Per-medium data sources, gate criteria, output format | 步骤 0 识别媒介后 / After Step 0 (medium ID) |
| `assets/topic-report-template.md` | 完整选题报告模板 / Full topic-report template | 需要交付正式报告时 / When delivering a formal report |
| `agents/openai.yaml` | 非 Claude agent 的英文版配置（逻辑与 SKILL.md 保持一致）/ English config for non-Claude agents (kept logically in sync with SKILL.md) | 在非 Claude 平台运行时 / When running on non-Claude platforms |
| `选题判断看板示例/` | 一份「选题过三关」判断结果的可视化看板示例（虚构选题"AI霸总短剧"，PDF+PNG，全部数据均为虚构占位）/ Example visual dashboard rendering a judgment result (fictional topic "AI CEO Short Drama", PDF+PNG, all data is fabricated placeholder content) | 需要参考可视化交付格式时 / When you need a visual-deliverable reference |

---

## 安装 / Installation

**Claude Code**：把整个文件夹放进项目的 `.claude/skills/` 目录（或建立符号链接），触发词命中时会自动加载。
Drop the whole folder into your project's `.claude/skills/` directory (or symlink it) — it auto-loads on trigger words.

**Cowork**：打包成 `.skill` 文件后通过「Save skill」按钮安装。
Package it into a `.skill` file and install via the "Save skill" button.

**其他 Agent 平台（豆包 / Kimi / 通义千问 / 文心一言等，没有原生 Skill 机制的平台）**：
这些平台不认 `.skill` 格式，但本技能天生就是纯文本（Markdown + YAML），可以直接当"自定义指令/知识库"用：
1. 把 `agents/openai.yaml` 里 `system:` 字段下的全部内容（英文版，逻辑与 SKILL.md 完全一致）粘贴进平台的"人设/自定义指令/System Prompt"设置里；中文场景也可以直接用 `SKILL.md` 正文（去掉最上面的 YAML frontmatter 三行）作为指令文本。
2. 把 `references/media-criteria/` 下对应媒介的文件、`references/gotchas.md`、`assets/topic-report-template.md` 作为"知识库文件"上传（如果平台支持文件上传/长期记忆），或需要时手动粘贴对应内容。
3. 这些平台一般没有自动联网检索工具，判断前提醒 AI（或自己动手）先去当当/京东/抖音/小红书等对应平台查数据，检索不到的项目必须标注"存疑/未核实"，不能编造——这条规则在 `references/gotchas.md` 陷阱 14/15 里有详细说明。
4. `离线工具/选题过三关-离线清单.html` 和使用哪个 AI 平台无关，双击直接在浏览器打开，可以当团队通用的人工核对清单来用。

For platforms without a native skill mechanism (Doubao, Kimi, Qwen, ERNIE Bot, etc.): the skill is plain Markdown/YAML, so paste the `system:` block from `agents/openai.yaml` (or `SKILL.md`'s body, minus the frontmatter) into the platform's custom-instructions/system-prompt field, upload the `references/` files as a knowledge base if supported, and remember most of these platforms lack built-in web search — manually gather medium-specific market data first, or explicitly mark ungathered items "unverified" per `gotchas.md` #14/#15. The offline HTML checklist in `离线工具/` works identically regardless of which AI platform your team uses.

---

## 局限与免责声明 / Limitations & disclaimer

- 判断结论依赖联网检索的真实数据，检索工具不可用或检索不到数据的项目会明确标注，不会静默编造。
  Verdicts depend on real web-searched data; when search is unavailable or turns up nothing, that's explicitly flagged rather than silently fabricated.
- 审读/合规层面的风险标注仅供参考，不替代人工复核。
  Compliance/editorial-review flags are advisory only and do not substitute for human review.
- `选题判断看板示例/` 里的 PDF/PNG 是纯格式演示：选题（"AI霸总短剧"）和全部数据来源都是虚构的，不引用任何真实机构、真实报道或真实平台统计，不能直接当作真实市场判断依据。
  The PDF/PNG in `选题判断看板示例/` are pure format demos — the topic ("AI CEO Short Drama") and every data source are fictional; nothing in it references a real organization, real report, or real platform statistic. Do not treat it as real market evidence.
- 各媒介参考文件里的数据源（当当/京东、抖音/视频号、小红书、小宇宙等）是针对中国内容市场调优的，这是当前的主要使用场景；「选题过三关」框架本身与市场无关，判断海外选题时替换成对应地区平台（如 Amazon/Goodreads、TikTok/YouTube）即可，三关结构和判断阈值不变。
  The data sources listed in each media-criteria file (Dangdang/JD, Douyin/Video Channels, Xiaohongshu, Xiaoyuzhou, etc.) are tuned for the Chinese content market, which is the primary use case today. The Clear-the-Three-Gates framework itself is market-agnostic — for non-Chinese markets, swap in the equivalent local platforms (e.g. Amazon/Goodreads, TikTok/YouTube) while keeping the same gate structure and thresholds.
