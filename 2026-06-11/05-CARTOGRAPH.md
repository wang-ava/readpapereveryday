# When Should an AI Scientist Stop? Verifiable Experiment Steering and Refusal for Autonomous Discovery

CARTOGRAPH 为 AI Scientist 问题提供“可验证终止/回撤”能力：在实验设计循环里加入 unresolved-subspace、ambiguity closure 和 refuse 机制，减少模型在模型库结构错配时误报创新成果的风险。

## 基本信息

- 论文标题：When Should an AI Scientist Stop? Verifiable Experiment Steering and Refusal for Autonomous Discovery
- 作者/机构（如可得）：Neel Tushar Shah、Manglam Kartik（机构信息未在页面直接展开）
- 发布日期或版本日期：2026-05-30
- 主题标签：#AI4Science #AutonomousScientist #BayesianExperimentalDesign #ModelDiscrepancy #ResponsibleAI
- 论文链接：https://openreview.net/forum?id=DdDTacsJnr
- PDF 链接：https://openreview.net/pdf?id=DdDTacsJnr
- 项目/代码/数据链接（如可得）：代码仓库 https://github.com/ai4science-boed/cartograph.git

## 核心问题

AI 科学系统常倾向于持续给出“看似确定”的建议，但若内部模型库结构错误，持续输出会放大误报。关键问题是：系统什么时候应当继续试验、什么时候应当拒绝并等待更可信证据？

## 方法概要

文中提出 CARTOGRAPH：
1. 选择 unresolved-subspace 实验用于辨别不充分信息区域；
2. resolve 阶段降低歧义；
3. refuse 机制检测 residual 型库不充分并触发撤回。

作者还给出数学形式：在局部线性高斯情形下 residual-based 不充分度给出解析规则，CARTOGRAPH-A 对应 exact unresolved A-optimal 规则；并与 EIG、Box–Hill 指标作为 comparator。

## 主要贡献

- 在 AI Scientist loop 中引入 first-class 的不确定性拒绝（refuse）接口。
- 提供实验选择与拒绝并行的闭环框架，而非单次输出后验评估。
- 用 residual 统计检测 library inadequacy，避免“模型错误但高置信”驱动假阳性发现。
- 给出可复核的代码仓库，适合直接验证。

## 关键实验或结果

文中报告在五个测试床中，CARTOGRAPH-A 在 d=8 下以显著优势优于 raw projection（129W/0T/15L）；并在 A-Lab autonomous materials 案例复核中，refuse guard 命中 4/4 被后续判定为不确定 claim，同时通过 32/36 的 confirmed claims。

## 适合关注的原因

AI4Science 场景中“召回更多假创新”与“错报风险”一直是核心治理问题。该框架把治理信号前置到实验策略层，能直接提升自治科研系统的可验证性和可信度。

## 局限性或待验证点

- 结果里部分指标记号/设置需查原文才能完全复核（如 W/T/L 在不同测试床的定义）。
- 仍偏向实验驱动设置，跨任务复杂真实实验的鲁棒性有待验证。
- 当前尚处于 workshop/论文草稿阶段，工程细节与参数范围需关注后续版本。

## 对后续研究/应用的启发

为科研型 agent pipeline 提供了一个可复用范式：不仅“能不能继续”，更要判断“是否该暂停/回退”。可用于材料、药物、工程建模等闭环自动化系统。

## Obsidian 快速浏览总结

CARTOGRAPH 的价值在于把 AI 科学家从“永远说继续”转成“知道什么时候该拒绝”，这是 AI4S 落地到高风险领域的必要安全机制。

## 标准化研究框架

**Research question：** 在闭环科学发现系统中，如何通过实验设计与残差检测判断“继续探索”与“主动拒绝/停止”的最佳边界？

**Literature：** 现有 autonomous scientist 工作强调生成与搜索，较少把 refutation 与 uncertainty refusal 写入主循环；本工作把治理层与实验选择统一。

**Theory：** 这里的理论含义是“实验信息增益与残差驱动不充分检测如何界定可继续搜索的可验证区域”，对应可验证决策边界的推导，而非社会学/心理学假设检验。

**Hypotheses：** 假设 refuse 机制可在不显著牺牲已确认真命题命中率的前提下降低误发现率；这是一个模型与决策边界假设。

**Method：** 以 unresolved-subspace 实验选择 + resolve + residual 检测三段构建闭环，比较 CARTOGRAPH 与基线策略的准确率/误判表现。

**Data and Analysis：** 在五个测试床和 A-Lab retrospective audit 上评估，通过 W/T/L 等指标统计是否改进模型继续实验的决策质量。

**Findings：** 报告显示 CARTOGRAPH-A 提升了决策收益，并能把后续被判定为不确定的 claim 更有效拦截。

**Conclusion：** 该框架为 AI4S 的安全、可验证自治决策提供了实用起点；后续应重点验证跨领域稳定性与阈值标定策略。
