# Agon: Competitive Cross-Model RL with Implicit Rival Grading of Reasoning

Agon 把传统 GRPO 的单模型自评训练拆开成两模型竞赛结构，让模型不仅“写答案”，更要在阅读对手草稿后“赢得推理对抗”。它对应了目前 reasoning LLM 的核心困境：结果可验证但思路难度量化，训练信号过于稀疏。

- **论文标题：** Agon: Competitive Cross-Model RL with Implicit Rival Grading of Reasoning
- **作者/机构：** Vladislav Beliaev；论文页未在公开元数据中给出完整机构列表
- **发布日期（版本日期）：** 2026-07-08（v1）
- **主题标签：** #LLM #Reasoning #RLHF #GRPO #Self-Improvement
- **论文链接：** https://arxiv.org/abs/2607.07690v1
- **PDF 链接：** https://arxiv.org/pdf/2607.07690v1
- **项目/代码/数据链接：** 当前 arXiv 记录未给出公开代码/数据仓库；如有更新，建议优先关注作者主页或后续仓库公告

## 核心问题

如何在没有额外过程标签（process labels）和 reward model 的条件下，构造更强的过程级学习信号，避免模型只学会“写更多字数”而非“推理更深”。

## 方法概要

- 在每个问题上运行两个同等级模型；模型轮流扮演 proposer（提交草稿）和 grader（读取草稿后再解题）。
- 用“谁更能超越对手”作为奖励信号，形成隐式竞争关系。
- 训练期两模型持续共同进化，不断提高对手难度；推理期以两阶段级联方式部署。
- 避免显式过程标注，借由对抗互动间接学习 reasoning quality。

## 主要贡献

1. 提出隐式竞争式的跨模型 RL 框架，直接把 process evaluation 纳入训练反馈。
2. 同规模设置下大幅提升硬推理数据集上的 pass@1，而非依赖更大模型。
3. 验证方法跨模型家族可复用（Qwen3.5、Gemma 4 等）并保持稳定增益趋势。

## 关键实验或结果

- 在 DeepMath 的 hard split 上，采用 Qwen3 基座时，Agon 约将 GRPO 的 pass@1 提升到约 2 倍。
- 与 untrained mixture-of-agents baseline 相比，增益接近其 8 倍以上的级别。
- 在 competitive-programming code 与不同模型家族上重复出现顺序一致的提升。

## 适合关注的原因

它将“评测瓶颈=结果可验证但推理过程难评分”转化为可训练机制，特别适合当前 Reasoning Agent 和数学推理工作流，用较少监督成本拿到更稳健的推理深度。

## 局限性或待验证点

1. 论文摘要未披露复杂任务上的成本—收益（训练成本、训练稳定性）细节。
2. 两模型是否始终保持“行为风格差异”可能影响最终收益，仍缺少更多控制实验。
3. 当前仍为文本交互机制，模型间可否在 latent space 协作尚未展开。

## 对后续研究/应用的启发

- 对 Agent Reasoning 而言，Agon 提供了可落地的“自对抗式微调”方向。
- 这类机制可与 verifier、tool use policy 联动，形成更少噪声的长链思考训练范式。

一句中文总结：Agon 用对手式竞争把推理过程作为训练目标之一，使硬问题上的 reasoning 能力更接近真实可用。 

## 标准化研究框架

- **Research question：** 如何在无过程标签条件下，用 RL 训练提升模型的推理深度，而非仅提升答案长度。
- **Literature：** 继承 GRPO/可验证奖励（verifiable reward）范式，问题聚焦在“过程信息缺失”导致的学习信号退化。
- **Theory：** 假设“跨模型竞争”可放大困难样本难度，使模型在同样监督预算下学到更有区分力的推理策略。
- **Hypotheses：** 竞争机制应提升 hard-split 推理任务的 pass@1；同模型家族间可复现增益。
- **Method：** 两模型交替角色，基于互评结果更新策略；在 DeepMath、竞赛编程等任务做多模型对比实验。
- **Data and Analysis：** 使用公开数学推理类基准与多模型族群对照，分析 pass@1 与方法对比基线（GRPO、untrained mixture）差异。
- **Findings：** 实验表明 Agon 在多任务上持续改善 hard-case 性能，且对模型家族有一定迁移性。
- **Conclusion：** 该研究并非社会科学因果检验；字段可等价理解为“通过对抗机制验证学习机制是否能替代过程标签”这一技术假设。
