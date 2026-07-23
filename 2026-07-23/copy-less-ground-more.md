# Copy Less, Ground More: Overcoming Repetitive Copying in Long-Context Reasoning via Evidence-Aware Reinforcement Learning

Spotlight：这篇工作指出了 LLM 长上下文推理中的“复写幻觉”问题，并通过 Evidence-Aware Reward 明确把“引用证据”与“复写抑制”绑定起来，兼顾正确率与可解释性。

- 论文标题：Copy Less, Ground More: Overcoming Repetitive Copying in Long-Context Reasoning via Evidence-Aware Reinforcement Learning
- 作者：Lizhe Fang, Weizhou Shen, Tianyi Tang, Yisen Wang
- 机构（如可得）：论文页面未显式展示机构归属。
- 发布日期或版本日期：2026-07-21（v1）
- 主题标签：#LLM #长上下文 #Reasoning #ReinforcementLearning #Robustness
- 论文链接：https://arxiv.org/abs/2607.19345v1
- PDF 链接：https://arxiv.org/pdf/2607.19345v1
- 项目/代码/数据链接：未在论文与 arXiv 页面直接给出；目前未检索到公开可验证仓库/站点。

## 核心问题
当上下文变长时，模型在逐步推理时容易大量复制输入片段，导致推理链看似合理但证据引用不足、决策可靠性下降。论文关注这个失效模式是否在高质量 benchmark 上仍普遍存在，以及如何系统抑制。

## 方法概要
作者将输入按“任务关键证据”和“无关干扰上下文”区分，提出 GEAR（Grounding Evidence-Aware Reward）强化学习奖励：
- 引入关键证据重叠奖励，鼓励模型输出与有效证据对齐；
- 引入干扰上下文惩罚，抑制复写与误引用；
- 构建自动证据标注数据流水线（基于输入文本自动生成），避免额外大量人工标注。

## 主要贡献
- 首次系统性刻画并量化了 long-context 推理中的 repetitive copying。
- 给出奖励函数替代方案，使 grounding 成为可优化目标，而不只优化最终答案正确率。
- 设计可复用的数据构造流程，便于不同任务上迁移。
- 在多个基准上验证了“grounding-aware RL”比纯准确率奖励更能改善长上下文推理质量。

## 关键实验或结果
论文报告在多个基准上平均提升最高约 +4.6（v1 实验口径）。主要观察是：
- 复写率显著下降；
- 推理轨迹更集中于任务证据；
- 长上下文下相对增益更明显。

## 适合关注的原因
它将长上下文可靠性问题具体化为可训练目标，适合需要将 LLM 推理从“看起来会想”升级到“证据可检验”的团队直接参考。

## 局限性或待验证点
- 该方法强调 reward shaping，对奖励权重是否在不同任务/领域稳定尚未给出全面敏感性分析。
- 依赖于证据标注流程质量，若证据抽取偏差大可能放大偏差。
- 目前公开结果偏重 benchmark，离线真实业务链路中的泛化还需持续验证。

## 对后续研究/应用的启发
可在企业知识问答、合约审核、长文档法务分析中加入“证据一致性 reward”，并与规则抽检器联动，在高风险任务里优先拦截高复写样本进行人工复核。

## 一句 Obsidian 快速浏览总结
一句话：把长上下文推理的核心风险从“答案正确性”扩展为“证据依赖质量”，并用 GEAR 把模型拉回到“先证据后推理”。

## 标准化研究框架
- **Research question：** 长上下文下，能否通过 evidence-aware 奖励显式抑制 repetitive copying，并提升可追溯推理质量？
- **Literature：** 研究基于 RLHF/RL 方向的奖励函数设计与长上下文鲁棒性，接续了 chain-of-thought 可控性与 grounded reasoning 的讨论。
- **Theory：** 在奖励建模中显式加入证据对齐项，理论上会引导策略优先选择支持性证据，降低无证据抄写行为；该方向属于可塑性较高的“目标函数工程”。
- **Hypotheses：** 若证据-干扰对比可被建模，那么 GEAR 应同时减少复写行为、提升高上下文任务的最终正确率，且效果随上下文长度增大更明显。
- **Method：** 1) 构建证据/干扰划分；2) 定义综合 reward；3) 用自动化管线构建训练样本；4) 在多模型和基准上做对照实验。
- **Data and Analysis：** 利用抽取到的标注样本与多个 benchmark 比较基线；分析指标包括答案正确性、复写比例、推理长度分布与稳定性。
- **Findings：** 论文给出平均 +4.6 的改善、复写率下降与更长上下文鲁棒性增强的证据，支持该奖励设计。
- **Conclusion：** 对于本类工作，social-science 的“假设检验”可映射为“目标函数设定 → 行为约束 → 任务表现”这三段链路；结论是 grounding 约束是可复用的方向，不建议简单回退到答案准确率单目标。
