# 论文与长文档翻译

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

- [liya-subtraction-skill](https://github.com/feverZHONG/liya-subtraction-skill)
- [liya-persona-authoring](https://github.com/feverZHONG/liya-persona-authoring)
- [liya-sillytavern-cards](https://github.com/feverZHONG/liya-sillytavern-cards)
- [liya-sillytavern-worldbook](https://github.com/feverZHONG/liya-sillytavern-worldbook)
- [liya-vision-recognition-traps](https://github.com/feverZHONG/liya-vision-recognition-traps)
- [liya-chat-game-referee](https://github.com/feverZHONG/liya-chat-game-referee)
- [liya-spy-game](https://github.com/feverZHONG/liya-spy-game)
- [liya-sea-turtle-soup](https://github.com/feverZHONG/liya-sea-turtle-soup)
- [liya-delegation-and-verification](https://github.com/feverZHONG/liya-delegation-and-verification)
- [liya-tavern-card-refinement](https://github.com/feverZHONG/liya-tavern-card-refinement)
- [liya-prose-quality-metrics](https://github.com/feverZHONG/liya-prose-quality-metrics)
- [liya-ruozhiba-wordbank](https://github.com/feverZHONG/liya-ruozhiba-wordbank)
- [liya-subtitle-proofreading](https://github.com/feverZHONG/liya-subtitle-proofreading)
- [liya-corpus-line-mining](https://github.com/feverZHONG/liya-corpus-line-mining)
- [liya-story-revision-plan](https://github.com/feverZHONG/liya-story-revision-plan)
- [liya-dev-workflow](https://github.com/feverZHONG/liya-dev-workflow)
- [liya-news-verification](https://github.com/feverZHONG/liya-news-verification)
- [liya-knowledge-persistence](https://github.com/feverZHONG/liya-knowledge-persistence)
- [liya-incident-review](https://github.com/feverZHONG/liya-incident-review)

---

*莉娅 · 宇宙美好记录官*
