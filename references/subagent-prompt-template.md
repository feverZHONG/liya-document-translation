# 子代理 context 模板（delegate_task 5 件套）

> 每个翻译子代理的 context 必须给全以下 5 项，缺一项就容易翻车（术语乱、覆盖不清、编公式）。

## 模板

```text
这是一篇由<机构>作者写的 <N> 页形式化论文（<背景一句话，如 Cordis 框架理论基础>）。
原文全文已提取为纯文本：<路径>/paper-fulltext.txt（<总行数> 行）。

你的翻译范围：第 <X> 章从行 <start> 开始（'<英文标题>'），到行 <end> 之前结束（下一节是行 <end> 的 '<下一节标题>'）。
<该章内容简介，如：这一章是全文最重的形式化章节，数学证明密集>

请先用 read_file 读术语表 <路径>/zh/术语表.md 统一术语，再分段 read_file 读原文（每次读 300-500 行），然后写翻译文件。

输出规范（重要）：
- 中文 Markdown，标题保留英文原名如 '# 4. 动态组合演算 (A Calculus of Dynamic Composition)'
- 定义/定理/引理（Definition/Lemma/Theorem/Corollary/Proof）标题翻译、陈述尽量完整翻译、证明概括要点或节译（讲清思路即可，不逐行硬翻）
- 公式/数学记号（𝔈∗、𝛿、𝜃、Definition 编号、转换规则名）保留原样；PDF 提取乱码的能修则修、不能修保留、禁止编造；无法理解的标注『[公式乱码，见原文]』
- 页码标记保留为 <!-- p.XX -->
- 学术语气；术语必须用术语表
- 文献名（如 Effekt、ZIO、Kitsune、COP、AOP 等）保留原文；参考文献条目不翻译
- 原文是英文，输出必须是中文
```

## 分工边界要点

- **行号范围精确**：`L100-1390` 这种，别含糊。子代理 read_file 有 2000 行/次上限，让它自己分段读
- **大章拆 part**：单章原文 >1000 行时提示子代理「可以分多个 _partN.md 写，最后合并」——task 自己会涌现这策略，给了提示更稳
- **第二批等第一批**：max_concurrent_children=3，第 7+8 章等前 3 个完成再派；第一批完成一个槽位就空出（delegate 会自动等全部返回，所以显式分两批派更可控）
- **单任务用 goal 字段**：delegate_task 单任务调用必须传 `goal`（可加 `context`/`role`），传 `tasks: [单个]` 会报错「Provide either 'goal' (single task) or 'tasks' (batch)」——只有多任务并行才用 tasks 数组（2026-08-14 实测踩过）
