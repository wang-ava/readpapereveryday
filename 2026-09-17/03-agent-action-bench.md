> **Spotlight：** AgentActionBench 将论文复现评估落实到真实工具操作记录，帮助区分“写出方案”与“执行并验证结果”。其复现分数是加权评分项得分，不能读成整篇论文复现成功率。

# Overview of the NLPCC 2026 Shared Task 11: Agent-Based Experiment Reproduction from Scientific Papers

## 论文信息

- 作者：Hanhua Hong、Yizhi Li、Luu Gia Huy、Jian Yang、Ming Zhou、Chenghua Lin。
- 机构：University of Manchester、IQuest Research、Vietnam National University、Beihang University、Langboat（正文列出的机构）。
- 发布及阅读版本：**2026-09-10，v1**；NLPCC 2026 Shared Task 概述。
- 主题标签：#Agent #AI4S #科学复现 #评估 #过程证据
- 论文：[arXiv v1](https://arxiv.org/abs/2609.11117v1)；[PDF](https://arxiv.org/pdf/2609.11117v1)；[正文](https://arxiv.org/html/2609.11117v1)。
- 项目/代码/数据：本次阅读页面未确认可直接使用的官方独立下载链接；数据名为 AgentActionBench，不以搜索到的同名仓库替代。
- 阅读范围：摘要、方法与评估第 3–5 节、表 3–5、局限性；未运行基准。

## 核心问题

怎样判断 Agent 是否真正执行了论文复现，而不是只留下看似完整的文件或说明？

## 方法概要

通过 MCP Action Recorder 记录 Read、Write、Execute 操作，再依据逐论文 rubric 对日志打分。数据含 **150 篇论文（120 ML、30 AI4Science）**，人工子集占 10%，自动扩展后超过一万条评分项。[摘要及第 3 节](https://arxiv.org/abs/2609.11117v1)

## 主要贡献

将复现评估从最终产物延伸到可追溯的执行过程，并以分阶段评分暴露系统薄弱环节。[方法](https://arxiv.org/html/2609.11117v1#S3)

## 关键实验或结果

表 3 最佳系统总分 **49.64%**，Codex-GPT-5.4 基线为 **24.19%**；它们是重要性加权 rubric 得分。表 5 中人工与模型 rubric 产生的分数相关性为 Pearson **0.93**、Spearman **0.88**。主排行榜排除人工训练子集；高相关不等于逐项裁判全部正确。[表 3–5](https://arxiv.org/html/2609.11117v1)

## 适合关注的原因

对 Ava 的论文阅读与后续复现工作，这种证据组织方式很实用：每个结论都可以连回代码、命令输出和结果文件。研究助手的质量便能按具体失败环节讨论，而不只依赖最终报告是否流畅。

## 局限性或待验证点

作者明确指出单一 GPT-4o-mini 裁判和初步的 AI4Science 覆盖限制了结论。[局限性](https://arxiv.org/html/2609.11117v1)

审读判断：有日志不等于科学结论正确；执行了训练命令也可能使用错误划分或遗漏关键消融。人工子集上的分数相关性主要支持排序一致性，应进一步审查具体评分项的漏判、误判和领域差异。

## 对后续研究/应用的启发

建议在个人复现清单里新增“证据路径”列，要求每条核心结果指向实际命令、数据版本与产物；同时设置独立的数值重算环节。研究上可对同一日志交换裁判模型，测量系统排名和关键结论是否稳定。这些是本笔记提出的后续方案。

## Obsidian 一句总结

AgentActionBench 让复现质量更可审计，但操作证据、评分项得分与科学结论可信度仍需分开验证。

## 标准化研究框架

**Research question：** 如何以可追溯过程证据评估 Agent 的科学实验复现能力？

**Literature：** 对应 PaperBench、Paper2Code 等复现评估与 rubric 评分路线；关键比较维度是评估证据来自最终文件还是实际执行。

**Theory：** 等价内容是测量框架：将复杂复现任务拆为带权标准并连接操作证据；不是关于科学活动的因果理论。

**Hypotheses：** 非预注册社会科学假设检验。工程预期为过程证据可提高可审计性，模型生成标准可以降低人工成本；可靠性须由独立人工核验支持。

**Method：** 基准构建、人工与模型标准比较、参赛系统评估；不能由一次排行榜推断模型的一般科学能力。

**Data and Analysis：** 分析单位包含论文、轨迹和评分项。建议报告分领域误判率，并按论文而非评分项做不确定性估计，避免把相关条目当独立样本。

**Findings：** 本次评估显示执行与结果验证值得优先改进；分数一致性提供支持，但不是裁判正确性的充分证据。

**Conclusion：** 可将其作为复现流程的审计模板；真实复现是否成立仍需检查数据、运行和最终数值。
