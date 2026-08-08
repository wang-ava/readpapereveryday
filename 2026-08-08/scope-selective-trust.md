> **Spotlight：** SCOPE 把“抗误导”改写成“选择性信任”：不是一味拒绝外部信号，而是学习在 clean / misleading / correct / irrelevant 四种上下文条件下做条件化决策。
> 这份工作最值得借鉴的是 MIST 的四匹配场景和 SC2W 指标，把“本来答对却被误导翻转为错误”的风险明确可量化，可直接迁移到 Agent 和 RAG 评测。

# Learning When to Trust via Selective Context Preference Optimization

- **论文标题：** Learning When to Trust via Selective Context Preference Optimization
- **作者/机构：** Xian Sun（Duke University）、Wei Chow（National University of Singapore）、Yingshuo Wang（UC Berkeley）、Junhao Liu（UC Irvine）、Wei Gao（Northeastern University）、Qing Wu（Nanyang Technological University, Singapore）、Lingdong Kong（National University of Singapore）。
- **发布日期/版本：** 2026-08-06（v1）
- **主题标签：** #LLM #可信AI #偏好优化 #ContextReliability #RAG
- **论文链接：** [https://arxiv.org/abs/2608.06377](https://arxiv.org/abs/2608.06377)
- **PDF：** [https://arxiv.org/pdf/2608.06377](https://arxiv.org/pdf/2608.06377)
- **项目/代码/数据：** [项目页](https://worldbench.github.io/scope/)、[GitHub](https://github.com/worldbench/SCOPE)、[MIST Data](https://huggingface.co/datasets/worldbench/MIST-Bench)

## 核心问题

当上下文包含误导信息时，LLM 往往会把原本答对的推理题翻错；但把模型训练成“拒绝一切上下文”虽然看似稳健，却会失去正确上下文带来的收益。作者要解决的是：如何让模型既能抗误导，又能在有用上下文到来时继续正确受益。

## 方法概要

构建四条件 benchmark（MIST）：对同一问题配对四种上下文——clean、misleading、correct-context、irrelevant。核心指标 SC2W 统计“在 clean 条件答对样本中，因误导而翻到错误答案的比例”。训练策略 SCOPE 不改损失函数（仍是标准 DPO），而是重构偏好对：显式挖掘 clean-correct / misleading-wrong 的脆弱样本，并在四条件之间做均衡配对，以减弱模型对错误信号的依赖偏置。

## 主要贡献

1. 将上下文鲁棒性从“抗干扰绝对值”改成“选择性信任”问题，强调兼顾拒绝误导与吸收有用信号。
2. 提供了可复用的 MIST 评测范式，让上下文质量变化下的翻转风险可追踪。
3. 用 SCOPE 证明仅通过数据构造的重平衡，就能显著压低 SC2W 同时不明显牺牲 clean、correct、irrelevant 条件上的表现。

## 关键实验或结果

- 多种模型普遍出现“误导上下文导致正确答案翻错”；SCOPE 针对该脆弱点优化。
- 摘要报告与项目页显示，在主流开源模型上可显著降低 SC2W（约 53%、35% 等量级下降示例在项目文档公开）。
- 项目页中的 leaderboard 表明该方法在 clean / correct / irrelevant 条件上保持竞争力，同时减少误导带来的风险翻转。

## 适合关注的原因

这是当前 RAG 与 Agent 安全性方向直接可落地的一类工作：工程上常见“工具输出错误但系统仍采用”的隐性风险，需要有机制量化“应该采信/不采信”而不是二元鲁棒化。SCOPE 的四条件设定很适合替代传统单一准确率评测。

## 局限性或待验证点

- MIST 的误导来源主要是人工构造，离真实检索噪声、对抗提示和多跳证据冲突仍有差距。
- SC2W聚焦 clean-correct 样本，难以直接度量“正确上下文下新增收益”与更复杂任务链的系统收益。
- 实验细节（规模、模型家族、计算成本）需结合正文和项目代码复核。

## 对后续研究/应用的启发

可以把“selective trust”直接扩展为 Agent 的 tool-use policy：在同一 query 下注入多版本工具证据（正确、错误、过时、无关）并比较行为翻转率；配合 source scoring 做显式采信决策树，而不是只有最终输出判断。

## Obsidian 快速浏览总结

**一句话：SCOPE 用四条件偏好构造，让模型学会“该信时信、该拒时拒”，从而把上下文可靠性问题变成可审计的选择性决策问题。**

## 标准化研究框架

**Research question：** 在上下文质量不确定场景下，模型如何在抗拒错误提示和利用有用信息之间做结构化权衡？

**Literature：** 相关于 LLM 可信性、RAG 证据质量评估、偏好学习（DPO）与任务上下文鲁棒性研究；以往工作多数偏重整体防误导，而少有兼顾正确上下文收益的成对评估。

**Theory：** 采用 selective trust 视角：稳健性不是“越不变越好”，而是对上下文可靠性做条件化响应。

**Hypotheses：** 等价框架：使用四条件匹配偏好对平衡训练，可以降低 clean→misleading 的翻转率且不明显损害对有用上下文的利用。

**Method：** 构造 MIST 四场景数据、定义 SC2W 指标、采用 DPO 在四类偏好对上优化。

**Data and Analysis：** 在多模型上统计 clean、misleading、correct、irrelevant 四条件下答案准确率与翻转比例，比较训练前后差异。

**Findings：** 脆弱性是普遍存在的；SCOPE 能在多个模型上显著降 SC2W，并保留对正确上下文的可用性。

**Conclusion：** 评估与训练都应以“选择性信任”作为目标，否则“拒绝所有上下文”会被误判为鲁棒性。 
