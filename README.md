# 论文与长文档翻译 · Document Translation

> PDF 论文／官网文档 → 中文版，一条龙：**提取全文 → 分析章节 → 建术语表 → 并行分章 → 质量抽查 → 归档**。
> 面向的是「几十上百页、一个人翻不完、多路并行又怕口径跑偏」的场合。

## 这是什么

一套把长文档翻译拆成可并行工序的流程，核心是**先立口径、再分活**：

1. **提取全文** — PDF 走 `pymupdf`/`fitz`，每页插 `===== PAGE N =====` 标记（页码是后面所有校对的锚点）
2. **分析章节结构** — 按标题行的形态抓边界（短行、大写开头、含空格、不以标点结尾），别靠猜
3. **建术语表** — `zh/术语表.md`，English|中文 对照 ＋ 输出规范。**必须写在派活之前**：多路并行的口径统一，全靠这一份
4. **并行分章** — 每个子代理拿到完整的上下文五件套（模板见 `references/subagent-prompt-template.md`）
5. **质量抽查** — 每章读开头 30–50 行：术语一致？页码标记还在？公式有没有被瞎编？
6. **收尾归档** — 归档前先删掉克隆带的 `.git`（否则 gitlink 坑：文件内容不进版本库）

## 最贵的几条坑

- **数学公式在 PDF 提取后必然乱码**（Unicode 排版错乱）。原则是**能修则修、不能修保留、禁止编造**——乱码处标注「[公式乱码，见原文]」，比编一个像样的公式安全得多。
- **短行数 ≠ 内容少**：某一章 47 行却全是长段落（18KB），抽查时只看行数会漏。
- **文献名保留原文**（Effekt、ZIO、Koishi 这类），参考文献条目不翻译。
- 子代理在大章节上会自然产出 `_part1.md`/`_part2.md` 之类的中间文件再合并——不用干预，但收尾要确认合并完成、中间件已清。

## 怎么用

把它放进你的 skills 目录（目录名用 `document-translation`）：

```bash
git clone https://github.com/feverZHONG/liya-document-translation.git <你的数据根>/skills/document-translation
```

纯文档、无脚本；提取全文那步依赖 `pymupdf`（`python3 -m pip install pymupdf`）。

## 许可

- `scripts/` 下的代码：**MIT**（全文见 `LICENSE`）
- 文档（`SKILL.md`、`references/`、本 README 正文）：**CC BY 4.0**（全文见 `LICENSE-DOCS`）

## 姊妹仓库

**同一族（长文本的搬运与打磨）**

- [liya-subtitle-proofreading](https://github.com/feverZHONG/liya-subtitle-proofreading) —— 字幕校对 / 重建 / 外挂 SRT（5 个纯标准库工具）
- [liya-corpus-line-mining](https://github.com/feverZHONG/liya-corpus-line-mining) —— 从语料 / 会话库挖可复用原句：候选池筛选 + 人审落库（零依赖）
- [liya-prose-quality-metrics](https://github.com/feverZHONG/liya-prose-quality-metrics) —— 稿子读起来「平」怎么办：先量再改（对话占比·句长σ·标点谱）＋ 7 个工具
- [liya-story-revision-plan](https://github.com/feverZHONG/liya-story-revision-plan) —— 小说全稿修订方案：评估 / 缺口清单 / 逐章大纲 / 信息融合 / 优先级

**莉娅名下其他**

- [liya-subtraction-skill](https://github.com/feverZHONG/liya-subtraction-skill) —— 技能库做减法：冗余检测 / 拆薄 / 合并 / 归档判断
- [liya-persona-authoring](https://github.com/feverZHONG/liya-persona-authoring) —— 给 AI agent 写身份文件（SOUL.md 类）：创作流程 / 砍装饰留行为 / 减法与漂移对照
- [liya-sillytavern-cards](https://github.com/feverZHONG/liya-sillytavern-cards) —— 酒馆角色卡写法：V2 格式 / PList+Ali:Chat / 三个 Python 工具
- [liya-sillytavern-worldbook](https://github.com/feverZHONG/liya-sillytavern-worldbook) —— 酒馆世界书（Lorebook）：触发链源码实证 + 体检 / 模拟 / 生成工具
- [liya-vision-recognition-traps](https://github.com/feverZHONG/liya-vision-recognition-traps) —— 视觉模型识图陷阱：22 条实测与对策（附真 OCR 通道、生图物理体检、两图差分）
- [liya-chat-game-referee](https://github.com/feverZHONG/liya-chat-game-referee) —— 群聊小游戏裁判：扫雷 / 五子棋 / 大话骰 / 骗子牌 / 掷骰决斗，一位裁判带六个引擎
- [liya-spy-game](https://github.com/feverZHONG/liya-spy-game) —— 谁是卧底：黑板规则 / 出题方法论 / 词库验证 / 身份分配器
- [liya-sea-turtle-soup](https://github.com/feverZHONG/liya-sea-turtle-soup) —— 海龟汤：推理方法论 + 档案流水线（turtle CLI）
- [liya-delegation-and-verification](https://github.com/feverZHONG/liya-delegation-and-verification) —— 委派与验收：任务书写法 / 并行隔离 / 把「自报」验成事实
- [liya-tavern-card-refinement](https://github.com/feverZHONG/liya-tavern-card-refinement) —— 酒馆角色卡精修：7 字段清单 / 槽位归位 / 6 类断言 / 可用性验收
- [liya-ruozhiba-wordbank](https://github.com/feverZHONG/liya-ruozhiba-wordbank) —— 弱智吧题防御手册：160 道逐题拆解 + 三连防御法（拆前提→指谬误→反杀）
- [liya-dev-workflow](https://github.com/feverZHONG/liya-dev-workflow) —— 开发全流程方法论：环境侦查 / 计划 / spike / TDD / 调试 / 推送排障 / 同步验收
- [liya-news-verification](https://github.com/feverZHONG/liya-news-verification) —— 验证伞：轻量核查 / 交付前多源验证 / 链接危险识别 / 厂商官宣核实 / 链接考古
- [liya-knowledge-persistence](https://github.com/feverZHONG/liya-knowledge-persistence) —— 知识持久化：信息该放记忆层 / 文件 / 技能库的分层规范
- [liya-incident-review](https://github.com/feverZHONG/liya-incident-review) —— 社群事件复盘：素材收集 → 时间线重构 → 交叉验证 → 矛盾管理（输出理解不输出建议）
- [liya-source-code-investigation](https://github.com/feverZHONG/liya-source-code-investigation) —— 外部项目调查：源码审计 / 拆包分层 / 数据实测 / 身份链（结论导向，非取用）
- [liya-character-voice-simulation](https://github.com/feverZHONG/liya-character-voice-simulation) —— 角色声线推演：锚点表双向用——分队推演（隔离上下文）＋ 反查认说话人
- [liya-dialogue-system-builder](https://github.com/feverZHONG/liya-dialogue-system-builder)
---

*莉娅（[@feverZHONG](https://github.com/feverZHONG)）· 宇宙美好记录官*
