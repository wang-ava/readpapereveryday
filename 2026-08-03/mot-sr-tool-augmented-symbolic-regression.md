# MOT-SR: Multi-Objective Tool-Augmented Scientific Equation Discovery with Large Language Models

Spotlight：MOT-SR 把科学方程发现从“单一拟合误差最小化”升级为多目标优化（准确性/复杂度/泛化），并通过工具增强的策略器推动 LLM 生成更可解释、可泛化的科学模型。

- 论文标题：MOT-SR: Multi-Objective Tool-Augmented Scientific Equation Discovery with Large Language Models
- 作者：Boxiao Wang；Runxiang Wang；Kai Li；Chongming Li；Zhiwei Chen；Yifan Zhang；Jian Cheng
- 机构（如可得）：arXiv 条目未直接给出机构信息
- 发布时间：2026-07-31（v1）
- 主题标签：#AI4S `#SymbolicRegression` `#LLM` `#ScientificDiscovery` `#ToolUse`
- 论文链接：[https://arxiv.org/abs/2607.29561v1](https://arxiv.org/abs/2607.29561v1)
- PDF 链接：[https://arxiv.org/pdf/2607.29561v1](https://arxiv.org/pdf/2607.29561v1)
- 项目/代码/数据链接：[https://github.com/wswbx/MOT-SR](https://github.com/wswbx/MOT-SR)

## 核心问题
经典符号回归常依赖单目标拟合，容易过拟合、忽略可解释复杂度与泛化。能否引入 LLM 的程序生成能力并通过工具化约束与多目标搜索，稳定发现更可用的科学方程？

## 方法概要
MOT-SR 采用双模块闭环：
- Meta Strategy Generator：基于当前 Pareto 解选择分析工具并生成结构优化策略
- Equation Generator：按策略生成候选方程

训练过程以动态 Pareto front 维护准确率、复杂度、泛化目标，并通过外部分析工具提取结构先验来约束搜索空间，避免陷入局部最优。

## 主要贡献
- 将 LLM 生成候选与工具化结构先验结合，形成多目标闭环 discovery 机制。
- 将误差最小化与物理可解释性约束显式并行，贴近 AI4S 可复用需求。
- 在科学领域高风险任务（如 EMRI 轨道建模）给出跨任务验证，强调长期预测稳定性。

## 关键实验或结果
- 在 40 个标准符号回归任务上，MOT-SR 在准确率、泛化和效率上均优于既有方法（摘要层面）。
- 在极端质量比旋比轨道（EMRI）建模案例中，MOT-SR 学到的可解释修正项在 held-out 配置下实现最低轨道级积分误差。
- 提供公开代码，降低复现门槛。

## 适合关注的原因
AI4S 场景需要“看得见、用得住”的公式发现，而不是黑箱拟合。该文将可解释性与性能并列为目标，非常契合科学模拟与工程建模任务。

## 局限性或待验证点
- 部分实验指标缺少标准化对比数值（摘要信息未披露完整表格），需查看正文确认增益幅度。
- 方程搜索依赖工具可用性，工具故障会影响闭环稳定性。
- 对高维、强噪声、多约束科学问题的扩展仍需进一步测试。

## 对后续研究/应用的启发
- 可直接用于引导科学建模 pipeline：让 LLM 提出候选方程，工具模块负责物理约束与复杂度控制。
- 建议与自动实验数据采集闭环结合，形成“假设提出—验证—修正”闭环。
- 对天体物理、化学动力学和材料建模中的可解释建模均有延展空间。

## Obsidian 快速浏览总结
一句话：MOT-SR 的价值在于把科学方程发现从拟合任务变为多目标治理任务，兼顾精度、泛化和可解释度。

## 标准化研究框架
- **Research question：** 如何让 LLM 在符号回归中同时优化拟合精度、模型复杂度和泛化表现？
- **Literature：** 与现有 symbolic regression 基线相比，本工作关注多目标约束与工具增强，但保持科学可解释导向一致。
- **Theory：** 单一误差目标不足，需把复杂度与泛化纳入优化以避免脆弱模型。
- **Hypotheses：** 通过工具注入的结构先验与动态 Pareto 排序，LLM 可生成更稳定且可解释方程。
- **Method：** 采用 meta strategy + equation generator 双模块闭环，在 40 个标准任务和 EMRI 任务上联合评测。
- **Data and Analysis：** 以标准基准与天体物理子任务验证，对比误差、复杂度、泛化表现并分析多目标权衡。
- **Findings：** 多目标工具增强机制比单目标基线更有利于长期模拟场景的方程质量。
- **Conclusion：** 框架提高了科学方程发现的可迁移性，特别适合 AI4S 中对可解释模型的需求。
