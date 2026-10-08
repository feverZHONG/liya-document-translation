# 实战复盘：88 页 Cordis 论文翻译（2026-08-14）

## 任务

《A Programming Paradigm for Spatiotemporal Composability》——北大×DeepSeek-AI 作者，Cordis 框架理论基础（DeepSeek Harness 底层范式）。88 页、4755 行提取文本、27 万字符。

## 执行时间线

| 阶段 | 耗时 |
|:---|:---|
| clone 论文仓库 + pymupdf 提取全文 + 章节分析 | ~2 分钟 |
| 术语表 + README 框架 | ~1 分钟 |
| 第一批 3 子代理（1+2+3 章 / 4 章 / 5+6 章） | ~6 分钟（task0 360s 完成） |
| 第二批 1 子代理（7+8 章，第一批完成后派） | ~4 分钟 |
| 质量抽查 + git 归档 | ~5 分钟 |

**总量：约 4 个并行子代理 × 300s ≈ 并行 10 分钟完成全译。**

## 产出规模

| 章节 | 译文规模 |
|:---|:---|
| 01-引言 | 54 行 / 8.9KB |
| 02-预备知识 | 52 行 / 5.6KB |
| 03-可逆效应与反应式共效应 | 698 行 / 57.8KB |
| 04-动态组合演算 | 725 行 / 92.9KB（最重，子代理自己拆 4 个 _part 写再合并） |
| 05-实现与案例研究 | 425 行 / 36.6KB |
| 06-讨论 | 103 行 / 21.7KB |
| 07-相关工作 | 47 行 / 18.4KB（行少但全，长段落） |
| 08-结论 | 9 行 / 1.9KB |
| 合计 | 260KB 译文 + 术语表 |

## 质量抽查点（实战验证有效）

1. **01-引言开头**：术语统一（时间组合性/空间组合性/可逆效应/反应式共效应）、页码 `<!-- p.4 -->` 在、脚注保留
2. **03 章定义区**：`定义 1（扭曲复合）` 公式代码块包裹、逆元概念完整
3. **04 章组件定义**：`定义 43` 三元组 (𝑑, 𝑝, 𝑒) 数学符号保留
4. **07 章**：47 行但 18.4KB——每个子节（效应系统/编程范式/时间组合性/空间组合性）都覆盖，文献名全保留
5. **08 章**：结论完整 + 子代理自己加了「参考文献保留原文」的处理说明

## 踩坑记录

1. **gitlink 坑**：clone 的论文仓库带 .git，`git add <素材目录>/` 警告 "adding embedded git repository" → 文件内容不进版本库。修复：`git rm --cached -rf` + `rm -rf .git` + 重新 add。**教训：归档第三方仓库前先删 .git。**
2. **delegate_task 单任务格式**：`tasks` 参数只用于 batch，单任务用 `goal`+`context`——第一次派第二批时传错格式报 "Provide either 'goal' (single task) or 'tasks' (batch)"
3. **PDF 不入 git**：.gitignore 用 `**/*.pdf` 拦 paper.pdf；提取的 paper-fulltext.txt + 译文入库
4. **环境事实**：pymupdf (fitz) 可用；无 pdftotext/pypdf——用 fitz 提取

## 术语表节选（可复用）

| English | 中文 |
|:---|:---|
| spatiotemporal composability | 时空组合性 |
| temporal composability | 时间组合性 |
| spatial composability | 空间组合性 |
| revertible effect | 可逆效应 |
| reactive coeffect | 反应式共效应 |
| context type | 上下文类型 |
| calculus | 演算 |
| observational equivalence | 观察等价 |
| hot module replacement | 热模块替换 |
| configuration reconciliation | 配置调和 |
